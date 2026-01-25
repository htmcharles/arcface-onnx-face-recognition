
# ArcFace ONNX Face Recognition

## Requirements

* **Python 3.11** (Highly Recommended)
    * *Note: Python 3.13 is currently incompatible with the legacy MediaPipe solutions used in this project.*
* OpenCV (`opencv-python`)
* NumPy (`numpy`)
* ONNX Runtime (`onnxruntime`)
* MediaPipe (`mediapipe==0.10.11`)

### Installation (Standard Python / No Anaconda)

This is the recommended way if you don't use Anaconda. It works with any standard Python 3.11 installation.

```bash
# 1. Install Python 3.11 from python.org if you haven't
# 2. Create a virtual environment
python -m venv venv

# 3. Activate the environment
# On Windows:
.\venv\Scripts\activate
# On Linux/macOS:
source venv/bin/activate

# 4. Install dependencies
pip install -r requirements.txt
```

### Installation (Anaconda)

```bash
conda create -n face-rec python=3.11 -y
conda activate face-rec
pip install -r requirements.txt
```

## How to Run the Project

Ensure you have activated your environment first (`.\venv\Scripts\activate` or `conda activate face-rec`).

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
* At least 15 captures per person are recommended for reliable recognition.

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
