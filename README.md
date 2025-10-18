# MediaPipe Holistic Detector with Pose Classification

A complete MediaPipe Holistic detector implementation with machine learning pose classification using OpenCV and scikit-learn.

## Features

- **Pose Detection**: Full body pose with 33 landmarks
- **Face Detection**: 468 facial landmarks
- **Hand Detection**: Left and right hand with 21 landmarks each
- **Pose Classification**: ML model to classify poses (Standing, Sitting, Arms Raised, Waving)
- **Real-time Processing**: Live webcam feed processing with pose prediction
- **Data Collection**: Tool to collect training data for custom poses
- **Visualization**: Colored landmarks and connections with pose labels
- **Screenshot Capture**: Save detection results

## Installation

1. Install dependencies:
```bash
pip install -r requirements.txt
```

## Usage

### Quick Start

1. **Train the model** (uses sample data):
```bash
python -c "from data_collector import PoseDataCollector; PoseDataCollector().load_sample_data()"
```

2. **Run the detector with pose classification**:
```bash
python main.py
```

### Controls

- **'q'**: Quit the application
- **'s'**: Save a screenshot of the current detection
- **'t'**: Retrain the model with sample data

### Data Collection

To collect your own training data:
```bash
python data_collector.py
```

## Files

- `holistic_detector.py`: Core detector class with MediaPipe integration
- `pose_classifier.py`: ML model for pose classification using Random Forest
- `data_collector.py`: Tool for collecting training data and model training
- `main.py`: Main application script with pose classification
- `requirements.txt`: Python dependencies

## Pose Classes

The model can classify the following poses:
- **Laughing**: Open mouth, hands on stomach, joyful expression
- **Yawning**: Mouth wide open, arms stretched up or to sides
- **Crying**: Hands near eyes, wiping tears, sad expression
- **Taunting**: Provocative gesture, pointing, or mocking expression

## Requirements

- Python 3.7+
- OpenCV 4.8+
- MediaPipe 0.10+
- NumPy 1.24+
- scikit-learn 1.3+

## Notes

- The detector uses your default webcam (camera index 0)
- Frame is horizontally flipped for mirror effect
- Detection confidence can be adjusted in the `HolisticDetector` class
