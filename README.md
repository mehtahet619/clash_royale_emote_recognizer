# Clash Royale Emote Detector

A machine learning-based pose detection system that identifies and classifies different emotes/expressions using computer vision and pose recognition.

## Overview

This project detects and classifies four distinct emote poses from video input:
- **Laughing** 😂
- **Yawning** 😴
- **Crying** 😢
- **Taunting** 😏

The system uses MediaPipe for pose detection and scikit-learn's Random Forest classifier for classification.

## Features

- Real-time pose detection using MediaPipe Holistic
- Machine learning-based pose classification
- Audio feedback for detected emotes
- Interactive data collection interface
- Training and inference capabilities
- Reference images for each emote

## Project Structure

```
.
├── main.py                    # Main application entry point
├── data_collector.py          # Data collection and training utilities
├── pose_classifier.py         # ML classifier for poses
├── holistic_detector.py       # MediaPipe pose detection wrapper
├── requirements.txt           # Python dependencies
├── pose_data/                 # Collected pose data and trained models
├── images/                    # Reference images for emotes
├── sounds/                    # Audio files for emotes
└── README.md                  # This file
```

## Requirements

- Python 3.10 or 3.11 (Python 3.13 not supported due to mediapipe compatibility)
- pip package manager
- Webcam for real-time detection

### Dependencies

```
opencv-python==4.8.1.78
mediapipe==0.10.7
numpy==1.24.3
scikit-learn==1.3.2
pygame==2.5.2
```

## Installation

### 1. Create Virtual Environment

Using Python 3.11 (recommended):
```bash
py -3.11 -m venv .venv
```

If you only have Python 3.10:
```bash
py -3.10 -m venv .venv
```

### 2. Activate Virtual Environment

**Windows (PowerShell):**
```bash
.\.venv\Scripts\Activate.ps1
```

**Windows (Command Prompt):**
```bash
.venv\Scripts\activate.bat
```

**macOS/Linux:**
```bash
source .venv/bin/activate
```

### 3. Upgrade pip

```bash
python -m pip install --upgrade pip
```

### 4. Install Dependencies

```bash
pip install -r requirements.txt
```

## Usage

### 1. Collect Training Data

Run the data collector to gather pose samples:

```bash
python data_collector.py
```

**Controls:**
- `0` - Set pose to Laughing
- `1` - Set pose to Yawning
- `2` - Set pose to Crying
- `3` - Set pose to Taunting
- `a` - Toggle auto collection (start/stop)
- `s` - Save collected data to files
- `t` - Train model with collected data
- `l` - Load previously saved data
- `q` - Quit

### 2. Run Main Application

Once the model is trained, run the detector:

```bash
python main.py
```

The application will:
- Display webcam feed with pose landmarks
- Show detected emote on screen
- Play audio feedback when emotes are detected
- Display reference images for each emote

## How It Works

### 1. Pose Detection (MediaPipe)
- Detects 33 key points across the body using MediaPipe Holistic
- Tracks head, shoulders, torso, and limb positions in real-time

### 2. Feature Extraction
- Computes features like:
  - Shoulder width and angles
  - Arm positions and angles
  - Head position relative to body
  - Hand positions
  - Posture characteristics

### 3. Classification (Random Forest)
- Trained Random Forest classifier distinguishes between emotes
- Uses extracted pose features for prediction
- Returns confidence scores for each emote class

### 4. Post-Processing
- Applies temporal smoothing to reduce noise
- Triggers audio and visual feedback only for high-confidence detections
- Displays bounding boxes and pose landmarks on video

## File Descriptions

### `main.py`
- Real-time emote detection from webcam
- Displays video feed with pose landmarks
- Shows reference images and detection results
- Handles audio playback with pygame

### `data_collector.py`
- Interactive interface for collecting pose samples
- Auto-collection mode for efficient data gathering
- Trains the Random Forest model
- Saves/loads training data and models

### `pose_classifier.py`
- `PoseClassifier` class for ML classification
- Feature extraction from pose landmarks
- Model training and inference methods
- Loads/saves trained models

### `holistic_detector.py`
- `HolisticDetector` class wrapping MediaPipe
- Pose detection from video frames
- Landmark visualization utilities
- Handles frame preprocessing

## Configuration

### Pose Labels

Modify emote labels in `data_collector.py` or `pose_classifier.py`:
```python
self.pose_labels = {
    0: "Laughing",
    1: "Yawning", 
    2: "Crying",
    3: "Taunting"
}
```

### Data Collection Parameters

In `data_collector.py`:
- `samples_per_pose`: Number of samples to collect per emote (default: 100)
- `collection_delay`: Frame skip for auto-collection (default: 10)

### Model Parameters

In `pose_classifier.py`, modify Random Forest parameters:
```python
n_estimators=100  # Number of trees
max_depth=20      # Tree depth
```

## Troubleshooting

### Import Error: `No module named 'mediapipe'`
Ensure you're using Python 3.10 or 3.11. Mediapipe doesn't support Python 3.13+ on Windows.

### Webcam not detected
- Check that no other application is using the webcam
- Try changing the camera index in `main.py` or `data_collector.py`

### Low accuracy
- Collect more training data (at least 100 samples per pose)
- Ensure good lighting and clear pose visibility
- Try training with more samples for better model generalization

### Audio not playing
- Install pygame: `pip install pygame`
- Check that audio files exist in the `sounds/` directory
- Verify speaker/audio output is working

## Model Training

The first time you run the system:

1. Run `data_collector.py`
2. Perform the desired emote for each class
3. Press `a` to start auto-collection
4. Collect ~100 samples per emote
5. Press `s` to save the data
6. Press `t` to train the model
7. Model will be saved as `pose_classifier_model.pkl`

## Performance Notes

- **Real-time speed**: ~25-30 FPS on modern laptops
- **Accuracy**: Typically 85-95% depending on training data quality
- **Latency**: ~100-150ms from pose detection to classification

## Future Improvements

- [ ] Add more emote classes
- [ ] Implement confidence thresholding
- [ ] Add gesture recognition for hand poses
- [ ] Support for multiple people detection
- [ ] Web interface for easier interaction
- [ ] GPU acceleration for faster processing

## License

See [LICENSE](LICENSE) file for details.
