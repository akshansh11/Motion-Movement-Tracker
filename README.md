# Motion Movement Tracker

AI powered motion movement analysis using computer vision and pose estimation. Track single or multiple people, analyze their movements, and generate detailed performance metrics.

## Features

### Single Person Tracking
- Real time pose detection with MediaPipe
- Movement velocity calculation
- Joint angle analysis (elbows, knees)
- Frame by frame movement data export

### Multi Person Tracking
- Track multiple people simultaneously
- Color coded skeleton overlay for each person
- Individual movement metrics per person
- Comparative analysis and rankings

### Advanced YOLO Tracking
- YOLO object detection for robust person identification
- Persistent ID tracking across frames
- Energy level calculation combining velocity and pose
- Handles crowded scenes with 10+ people
- Automatic validation and error detection

## Requirements

```bash
Python 3.8+
opencv-python
mediapipe
numpy
ultralytics
```

## Installation

Clone the repository

```bash
git clone https://github.com/yourusername/motion-movement-tracker.git
cd motion-movement-tracker
```

Install dependencies

```bash
pip install opencv-python mediapipe numpy ultralytics
```

## Usage

### Basic Single Person Tracking

```python
from dance_tracker import DanceTracker

tracker = DanceTracker('dance.mp4')
tracker.process_video(output_path='tracked_dance.mp4', save_data=True)
```

### Multi Person Tracking

```python
from dance_tracker import MultiPersonDanceTracker

tracker = MultiPersonDanceTracker('dance.mp4')
tracker.process_video(output_path='multiperson_dance.mp4', save_data=True)
```

### Advanced YOLO Tracking

```python
from dance_tracker import YOLODanceTracker

tracker = YOLODanceTracker('dance.mp4')
tracker.process_video(
    output_path='yolo_tracked_dance.mp4',
    save_data=True,
    min_detection_confidence=0.7,
    max_people=50
)
```

## Output

### Video Output
- Annotated video with skeleton overlays
- Bounding boxes for each detected person
- Real time metrics displayed on frame
- Color coded visualization for multiple people

### Data Output
- JSON file with frame by frame movement data
- Velocity measurements
- Joint angle calculations
- Energy level metrics
- Timestamp information

### Analysis Reports
- Individual person statistics
- Movement velocity averages
- Peak energy moments
- Screen time tracking
- Comparative rankings

## Configuration Options

### YOLO Tracker Parameters

```python
min_detection_confidence  # Detection threshold (default: 0.7)
max_people               # Maximum people to track (default: 50)
frame_skip              # Process every Nth frame for speed
```

### MediaPipe Parameters

```python
model_complexity        # 0, 1, or 2 (higher = more accurate, slower)
min_detection_confidence # Detection threshold (default: 0.5)
min_tracking_confidence  # Tracking threshold (default: 0.5)
```

## Project Structure

```
motion-movement-tracker/
├── dance_tracker.py          # Main tracking implementations
├── requirements.txt          # Python dependencies
├── README.md                # Documentation
├── examples/                # Example scripts
│   ├── single_person.py
│   ├── multi_person.py
│   └── yolo_advanced.py
└── output/                  # Generated outputs
    ├── videos/
    └── data/
```

## Technical Details

### Architecture

The system uses a three tier approach for maximum accuracy

**Tier 1: Single Person Tracking**
- MediaPipe Pose for skeleton detection
- Landmark tracking for 33 body points
- Velocity calculation between frames

**Tier 2: Multi Person Tracking**
- Spatial position based person matching
- Individual color assignment
- Parallel pose estimation

**Tier 3: YOLO Advanced Tracking**
- YOLOv8 for person detection
- Persistent tracking IDs
- MediaPipe pose on cropped regions
- Energy level computation

### Performance

- Single person: 15-20 FPS on CPU
- Multi person (3-5): 8-12 FPS on CPU
- YOLO tracking: 10-15 FPS on CPU
- GPU acceleration available for all models

## Troubleshooting

### Video file issues

```bash
# Validate video
ffprobe dance.mp4

# Re-encode if corrupted
ffmpeg -i input.mp4 -c:v libx264 -c:a aac output.mp4
```

### Too many false detections

Increase confidence threshold

```python
tracker.process_video(min_detection_confidence=0.8)
```

### Memory issues with large videos

Process with frame skipping

```python
tracker.process_video(frame_skip=2)  # Process every 3rd frame
```

## Metrics Explained

**Velocity**: Total movement distance of all body landmarks between frames

**Energy Level**: Combined metric of velocity and joint angles, indicating movement intensity

**Joint Angles**: Angles at major joints (elbows, knees) for pose analysis

**Screen Time**: Total duration a person is visible and tracked

## Contributing

Contributions are welcome. Please follow these guidelines

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

MIT License

Copyright (c) 2025

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## Acknowledgments

- MediaPipe by Google for pose estimation
- Ultralytics YOLO for object detection
- OpenCV for video processing

## Contact

For questions or support, please open an issue on GitHub.

## Citation

If you use this project in your research, please cite

```bibtex
@software{motion_movement_tracker,
  author = {Your Name},
  title = {Motion Movement Tracker},
  year = {2025},
  url = {https://github.com/yourusername/motion-movement-tracker}
}
```
