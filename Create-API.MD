## Steps to Deploy Your YOLO Model as a REST API
## Install Dependencies
* Ensure you have Flask and required libraries installed:

```
pip install flask pillow torch torchvision numpy opencv-python
```

## Step 2: Create app.py File
```
from flask import Flask, request, jsonify
import torch
from PIL import Image
import yolov5

app = Flask(__name__)

# Load YOLOv5 model
model = torch.hub.load('ultralytics/yolov5', 'custom', path='runs/train/exp8/weights/best.pt', force_reload=True)

@app.route('/', methods=['GET'])
def home():
    return "Ambulance Detection API is Running"

@app.route('/predict', methods=['POST'])
def predict():
    if 'image' not in request.files:
        return jsonify({"error": "No image uploaded"}), 400

    image = request.files['image']
    img = Image.open(image)

    # Perform inference
    results = model(img)
    detections = results.pandas().xyxy[0].to_dict(orient="records")

    # Check if an ambulance is detected
    ambulance_detected = any(d['name'] == 'ambulance' for d in detections)

    return jsonify({
        "ambulance_detected": ambulance_detected,
        "detections": detections
    })

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=True)
```

## Step 2: Run the Correct Command in the Correct Directory
```
cd C:\Users\parth\yolov5
```
```
python app.py
```

##Step 3: Restart Flask & Test API
```
curl -X POST -F "image=@path/to/your/image.jpg" http://127.0.0.1:5000/predict
```
