# aws-ai-image-recognition
AI Image Recognition app using aws Rekognition and Python
# 🤖 AI Image Recognition App — AWS Rekognition & Python

![AWS](https://img.shields.io/badge/AWS-Rekognition-orange?logo=amazon-aws)
![Python](https://img.shields.io/badge/Python-3.13-blue?logo=python)
![Boto3](https://img.shields.io/badge/Boto3-SDK-yellow)
![S3](https://img.shields.io/badge/Amazon-S3-green?logo=amazon-aws)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

A Python application that uses **Amazon Rekognition** to automatically detect objects, scenes, faces and emotions in images — built as part of the **AWS Certified AI Practitioner** learning journey.

---

## 📸 What It Does
- 🏷️ **Label Detection** — Identifies objects, scenes and concepts in any image with confidence scores
- 😊 **Facial Analysis** — Detects age range, dominant emotion, smile, and eyeglasses
- ☁️ **Cloud Storage** — Images stored securely in Amazon S3
- 🐍 **Python Automation** — Fully automated via Boto3 SDK

---

## 🛠️ Tech Stack
| Technology | Purpose |
|---|---|
| Python 3.13 | Core programming language |
| Amazon Rekognition | AI image analysis service |
| Amazon S3 | Cloud image storage |
| Boto3 SDK | AWS Python SDK |
| AWS CLI | Credential configuration |

---

## 🚀 Getting Started

### 1. Clone the repository
git clone https://github.com/Poonam-star10/aws-ai-image-recognition.git

### 2. Install dependencies
pip install boto3
pip install awscli

### 3. Configure AWS credentials
aws configure

### 4. Add your image
Place any .jpg or .png image in the project folder and rename it test.jpg

### 5. Run the app
python rekognition_app.py

---

## 🧠 The Code

import boto3

def analyze_image(image_path):
    with open(image_path, 'rb') as image_file:
        image_bytes = image_file.read()

    rekognition = boto3.client('rekognition', region_name='eu-west-1')

    print("\nLABEL DETECTION")
    print("-" * 40)
    labels = rekognition.detect_labels(
        Image={'Bytes': image_bytes},
        MaxLabels=10,
        MinConfidence=75
    )
    for label in labels['Labels']:
        print(f"  {label['Name']} - {label['Confidence']:.1f}%")

    print("\nFACIAL ANALYSIS")
    print("-" * 40)
    faces = rekognition.detect_faces(
        Image={'Bytes': image_bytes},
        Attributes=['ALL']
    )
    for face in faces['FaceDetails']:
        age = face['AgeRange']
        emotion = max(face['Emotions'], key=lambda x: x['Confidence'])
        print(f"  Age Range: {age['Low']} - {age['High']} years")
        print(f"  Emotion: {emotion['Type']} ({emotion['Confidence']:.1f}%)")
        print(f"  Smile: {face['Smile']['Value']}")

analyze_image('test.jpg')

---

## 📊 Sample Output
LABEL DETECTION
  Person — 99.2%
  Face — 98.5%
  Architecture — 100%
  Building — 100%
  City — 100%

FACIAL ANALYSIS
  Age Range: 20 - 30 years
  Emotion: CALM (94.2%)
  Smile: False

---

## ☁️ AWS Services Used
- Amazon S3 — Bucket: my-ai-image-app-demo, Region: eu-west-1
- Amazon Rekognition — Label Detection and Facial Analysis, Region: eu-west-1

---

## 🔐 Security Notes
- Never commit your AWS Access Keys to GitHub
- Use IAM roles with least privilege in production
- Rotate access keys regularly

---

## 📚 What I Learned
- Creating and managing Amazon S3 buckets
- Using Amazon Rekognition for AI image analysis
- Writing Python scripts with Boto3 SDK
- Configuring AWS CLI and managing credentials
- Applying AWS AI Practitioner knowledge in a real project

---

## 🏆 Certification
AWS Certified AI Practitioner — March 2026

---

## 👩‍💻 Author
Poonam
📧 Poonammanna10@gmail.com
📞 +44 7810794876

---

## 📄 License
This project is open source and available under the MIT License.
