# ArcFace ONNX Face Recognition

## Requirements

* Python 3.12+
* OpenCV (`opencv-python`)
* NumPy (`numpy`)
* ONNX Runtime (`onnxruntime`)
* MediaPipe (`mediapipe`)

### Installation

```bash
pip install opencv-python numpy onnxruntime mediapipe
```

## How to Run the Project

### 1. Enrollment (add new users)
```bash
python -m src.enroll
```

* Enter the name of the person to enroll (e.g., Alice).
* Follow the instructions:
    * **SPACE** = capture current frame
    * **a** = auto-capture multiple frames
    * **s** = save captured embeddings (requires sufficient samples)
    * **r** = reset current session
    * **q** = quit
* At least a few captures per person are recommended to ensure reliable recognition.

The script aligns the face to 112x112 using 5-point landmarks and generates an ArcFace embedding, which is stored in `data/db/face_db.npz`.

### 2. Recognition (identify faces in real-time)
```bash
python -m src.recognize
```

* Opens webcam and detects multiple faces.
* Draws bounding boxes, landmarks, and recognition labels.
* Keys for live control:
    * **q** = quit
    * **r** = reload database from disk
    * **+/-** = adjust distance threshold
    * **d** = toggle debug overlay

Each detected face is aligned, embedded, and compared to the database using cosine similarity.


