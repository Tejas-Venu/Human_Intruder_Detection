# Human_Intruder_Detection

This project combines **YOLOv8-based object detection** with **FaceNet-based face recognition** to detect human intrusions and identify known individuals (students or faculty). Unknown faces are labeled as **"Intruder"**.  

---

## 🚀 Features
- **YOLOv8 Object Detection**
  - Detects humans in images or video streams.
  - Includes saliency visualization using EigenCAM.
- **Face Recognition with FaceNet**
  - Detects and extracts embeddings using `MTCNN` and `InceptionResnetV1`.
  - Compares embeddings against stored datasets:
    - `faces_embeddings_students.npz`
    - `faces_embeddings_teachers.npz`
- **Intruder Detection**
  - Identifies known students/faculty.
  - Marks unknown persons as `"Intruder"`.
- **Dataset Preparation**
  - Automatic splitting into `train/val/test` sets.
  - YOLO-compatible `data.yaml` generation.

---

## 🛠️ Installation & Setup

### 1. Clone the repository
```bash
git clone https://github.com/your-username/human-intrusion-detection.git
cd human-intrusion-detection
```

### 2. Create and activate a virtual environment
```bash
python -m venv venv
source venv/bin/activate   # On macOS/Linux
venv\Scripts\activate      # On Windows
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Ensure model weights and embeddings are present
`updated_best.pt` → trained YOLOv8 model weights

`faces_embeddings_students.npz` → student embeddings

`faces_embeddings_teachers.npz` → faculty embeddings

---

## ▶️ Usage

### 1. YOLO Object Detection

Run on a folder of images:
```bash
python object_detector.py
```

Run with webcam (inside script):
```bash
video()
```

### 2. Face Recognition

Run face recognition with webcam:
```bash
python face_recog.py
```

Run face recognition on a folder:
```bash
predict_for_folder("path_to_images/")
```

### 3. Dataset Preparation (YOLO Training)

Split dataset and generate data.yaml:
```bash
python splitter.py
```
Default classes:
```yaml
nc: 3
names: ["intruder", "student", "faculty"]
```

---

## 🔑 How It Works

1. Object Detection: YOLOv8 detects humans.

2. Face Detection: MTCNN extracts detected faces.

3. Embedding Generation: InceptionResnetV1 creates embeddings.

4. Comparison: Embeddings compared against stored .npz files.

5. Classification:
    
    Student → labeled with name from student embeddings.
    
    Faculty → labeled with name from teacher embeddings.
    
    No match → "Intruder".

---
