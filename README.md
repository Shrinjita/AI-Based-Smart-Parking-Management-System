# AI-Based Smart Parking Management System
## Overview
This project implements a novel AI-based smart parking management system that integrates computer vision for parking slot detection with gesture recognition for user interaction. The system provides a cost-effective alternative to sensor-based parking solutions while offering intuitive human-computer interaction.

### Key Features
- **Parking Space Detection**: Real-time monitoring of parking lot occupancy using YOLOv8
- **Gesture-Based Interaction**: Natural user interface through pose estimation with MediaPipe
- **Web Dashboard**: Admin interface for monitoring and management
- **User Displays**: Interactive display for users to select and reserve parking spots
- **API Integration**: RESTful API for potential integration with mobile applications

## System Architecture
The system follows a layered architecture:

1. **Data Acquisition Layer**: Camera input processing
2. **Processing Layer**: AI models for object detection and pose estimation
3. **Application Layer**: Core business logic
4. **Presentation Layer**: User interfaces and feedback mechanisms

![image](https://github.com/user-attachments/assets/b2d685af-c9ee-4b8e-9634-a561c55899f2)

## Installation

### Prerequisites

- Python 3.8+
- CUDA-compatible GPU (recommended)
- Webcam or IP camera

### Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/smart-parking-system.git
   cd smart-parking-system
   ```

2. Create and activate a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Download pre-trained models:
   ```bash
   python scripts/download_models.py
   ```

5. Configure your camera settings:
   ```bash
   cp config/camera_config.sample.json config/camera_config.json
   # Edit camera_config.json with your camera details
   ```

## Usage

### Parking Space Definition

1. Capture a reference frame from your parking lot camera:
   ```bash
   python tools/capture_reference_frame.py --camera_id 0 --output reference_frame.jpg
   ```

2. Define parking spaces using the annotation tool:
   ```bash
   python tools/parking_space_annotator.py --image reference_frame.jpg --output parking_regions.json
   ```

### Starting the System

1. Start the main system:
   ```bash
   python main.py --config config/system_config.json
   ```

2. Access the admin dashboard:
   ```
   http://localhost:5000/admin
   ```

3. For testing with sample videos instead of live cameras:
   ```bash
   python main.py --config config/system_config.json --parking_video samples/parking_lot.mp4 --user_video samples/user_gestures.mp4
   ```

## Gesture Interaction

The system recognizes the following gestures:

- **Pointing**: Select a parking space
- **Wave**: Cancel selection
- **Hands joined above head**: Confirm selection

![Gesture Guide](https://github.com/yourusername/smart-parking-system/raw/main/docs/images/gesture_guide.png)

## Demo Dataset

The repository includes a small demo dataset in the `samples` directory:

- `parking_lot.mp4`: Sample parking lot footage
- `user_gestures.mp4`: Sample user gesture footage
- `demo_images/`: Sample images for testing the detection algorithm

For larger datasets, check the [PKLot dataset](https://web.inf.ufpr.br/vri/databases/parking-lot-database/) which contains thousands of annotated parking lot images.

## System Components

### Parking Detection Module

The parking detection module utilizes YOLOv8 for recognizing vehicles and parking space occupancy. The system can handle varying lighting conditions and camera angles through adaptive perspective transformation.

### Gesture Recognition Module

Built on MediaPipe's pose estimation framework, this module enables natural interaction with the system through intuitive gestures.

### Integration Server

A Flask-based server handles communication between modules, manages the business logic, and serves the web interfaces.

### Admin Dashboard

The admin dashboard provides monitoring capabilities and manual override options for parking management staff.

## Development

### Project Structure

```
smart-parking-system/
├── config/                  # Configuration files
├── data/                    # Data storage
├── docs/                    # Documentation and images
├── models/                  # Pre-trained AI models
├── samples/                 # Sample videos and images
├── scripts/                 # Utility scripts
├── src/                     # Source code
│   ├── detection/           # Parking detection module
│   ├── gesture/             # Gesture recognition module
│   ├── integration/         # System integration logic
│   ├── ui/                  # User interfaces
│   └── utils/               # Utility functions
├── static/                  # Static web assets
├── templates/               # HTML templates
├── tests/                   # Test suite
├── tools/                   # Development tools
├── main.py                  # Main entry point
├── requirements.txt         # Dependencies
└── README.md                # This file
```

### Adding Custom Gestures

To add custom gesture definitions:

1. Create a new gesture file:
   ```bash
   cp src/gesture/definitions/default_gestures.json src/gesture/definitions/custom_gestures.json
   ```

2. Edit the gesture definition file with your custom gestures
3. Update your configuration to use the custom gestures:
   ```json
   {
     "gesture_recognition": {
       "definitions_file": "src/gesture/definitions/custom_gestures.json"
     }
   }
   ```

## Performance

The system achieves:
- 95% accuracy in parking space detection
- 92% accuracy in gesture recognition
- 200ms average end-to-end latency

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Citation

If you use this project in your research, please cite:

```
@article{paul2023ai,
  title={An AI-Based Approach for Smart Parking Management Using Computer Vision and Gesture Recognition},
  author={Paul, Shrinjita and Ghosh, Sumedha and Khan, Ali},
  journal={Artificial Intelligence and Transportation Systems},
  year={2023}
}
```

## Acknowledgments

- [Ultralytics YOLOv8](https://github.com/ultralytics/yolov8)
- [MediaPipe](https://github.com/google/mediapipe)
- [PKLot Dataset](https://web.inf.ufpr.br/vri/databases/parking-lot-database/)
