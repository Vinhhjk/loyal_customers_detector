# 🛠️ Loyal Customer Detection & Analysis System

## 📚 Project Description
Real-time face recognition and demographic analysis system. It uses a combination of **YOLOv4 for face detection**, **OpenCV deep learning models for age and gender prediction**, and **face_recognition for facial identification**.

The system detects customers, recognizes if they are returning visitors, estimates their age and gender, and logs their visits in an **SQLite database** for customer tracking and analytics.

---

## 📂 Folder Structure

```
loyal_customers_detector/
│-- models/                # Pre-trained models (YOLO, AgeNet, GenderNet, Face Detector)
│-- config.py               # Config file (camera URL, model paths, etc.)
│-- customer_data.db        # SQLite database for customer info (auto-created if missing)
│-- main.py                  # Main script to run the project
│-- README.md                # This guide
│-- .gitignore               
```

---

## ⚙️ Features

✅ Real-time face detection using **YOLOv4**  
✅ Age & Gender prediction using OpenCV models  
✅ Customer identification via **face_recognition**  
✅ Automatic new customer registration with age & gender logging  
✅ Visit count tracking & customer logs in **SQLite database**  
✅ Multi-threaded design for performance  

---

## 📊 Requirements

Install required dependencies:

```bash
pip install -r requirements.txt
```

**`requirements.txt`:**
```
opencv-python
face-recognition
numpy
sqlite3
```

---

## ⚙️ Configuration (config.py)

Create `config.py` with the following content:

```python
CAMERA_URL = 0  # or your RTSP/Camera URL
CACHE_UPDATE_INTERVAL = 30  # seconds
ABSENCE_THRESHOLD = 10 # seconds

MODEL_PATHS = {
    "face_detector": ("models/deploy.prototxt", "models/res10_300x300_ssd_iter_140000_fp16.caffemodel"),
    "age_net": ("models/age_deploy.prototxt", "models/age_net.caffemodel"),
    "gender_net": ("models/gender_deploy.prototxt", "models/gender_net.caffemodel"),
    "yolo": ("models/yolov4-tiny.weights", "models/yolov4-tiny.cfg")
}

age_list = ['(0-2)', '(4-6)', '(8-12)', '(15-20)', '(21-22)','(23-24)','(25-32)', '(38-43)', '(48-53)', '(60-100)']
gender_list = ['Male', 'Female']

```

---

## 🚀 How to Run

1. Clone the repository:
    ```bash
    git clone https://github.com/Vinhhjk/loyal_customers_detector.git
    cd loyal_customers_detector
    ```

2. Install dependencies:
    ```bash
    pip install -r requirements.txt
    ```

3. Prepare models:  
   Place the following files in `models/` folder:
    - yolov4-tiny.cfg
    - yolov4-tiny.weights
    - age_deploy.prototxt
    - age_net.caffemodel
    - gender_deploy.prototxt
    - gender_net.caffemodel
    - deploy.prototxt (Face detector)
    - res10_300x300_ssd_iter_140000_fp16.caffemodel

4. Edit`config.py` (see above).

5. Run the system:
    ```bash
    python main.py
    ```

---

## 📄 Database Schema (customer_data.db)
```
### customers table
| Column       | Type      | Description                       |
|--------------|-----------|-----------------------------------|
| id           | INTEGER   | Unique customer ID (auto-increment) |
| face_encoding| TEXT      | Face encoding array as string    |
| visit_count  | INTEGER   | Total visits                     |
| last_seen    | TEXT      | Last visit timestamp             |
| last_location| TEXT      | Last seen camera/location        |
| age          | TEXT      | Estimated age                    |
| gender       | TEXT      | Estimated gender                 |
```
```
### customer_logs table
| Column       | Type      | Description                       |
|--------------|-----------|-----------------------------------|
| id           | INTEGER   | Log ID (auto-increment)          |
| customer_id  | INTEGER   | Linked to `customers.id`         |
| timestamp    | TEXT      | Event time                       |
| event        | TEXT      | Description of event (e.g., "Entered Frame") |
```
---

## 🛠️ Recommended .gitignore

```
__pycache__/
*.pyc
*.pyo
```

---

## 📑 Example Output

On running, you will see:

✅ Live feed with bounding boxes  
✅ Detected age & gender shown on screen  
✅ VIP customers recognized with ID & demographics  
✅ New customers added to database automatically  
✅ Logs printed in terminal and saved to `customer_data.db`

---

## 🏅 Future Enhancements

- Add face mask detection
- Sync logs to cloud (Firebase/AWS)
- Add real-time web dashboard
- Face re-training for better accuracy

---


