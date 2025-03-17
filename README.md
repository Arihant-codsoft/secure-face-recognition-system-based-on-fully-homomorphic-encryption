# secure-face-recognition-system-based-on-fully-homomorphic-encryption

Below is a **detailed `README.md` file** for your project. This README provides a comprehensive overview, including installation steps, usage instructions, and an explanation of the project's architecture.  

---

# Secure Face Recognition with Fully Homomorphic Encryption  

### **A secure face recognition authentication system using Flask, face_recognition, and TenSEAL for encrypted biometric authentication.**

## 📌 Table of Contents  
1. [Project Overview](#project-overview)  
2. [Features](#features)  
3. [Technology Stack](#technology-stack)  
4. [Project Architecture](#project-architecture)  
5. [Installation](#installation)  
6. [Usage](#usage)  
7. [Security Considerations](#security-considerations)  
8. [Future Improvements](#future-improvements)  
9. [License](#license)  

---

## 🔹 Project Overview  
This project provides a **secure face recognition authentication system** that integrates **fully homomorphic encryption (FHE)** to protect sensitive biometric data. Instead of storing face embeddings in plaintext, **TenSEAL's CKKS encryption** is used to store encrypted embeddings, ensuring data privacy even if the database is compromised.  

Originally using **DeepFace**, the project was optimized with **face_recognition** to reduce processing time from **~10 seconds to under 2 seconds** for a smoother user experience.  

**Key Highlights:**  
- Uses **Flask** for the backend.  
- **Homomorphic encryption (CKKS)** ensures biometric privacy.  
- **face_recognition** for real-time face embedding extraction.  
- Stores encrypted embeddings in an **SQLite database** using **SQLAlchemy**.  
- Supports **real-time authentication** through a web-based camera capture system.  

---

## 🔥 Features  
✔ **Real-Time Face Authentication** – Secure face recognition for user login and signup.  
✔ **Homomorphic Encryption** – Encrypts biometric data before storage for enhanced privacy.  
✔ **Fast Processing** – Optimized image preprocessing and face recognition ensure authentication within **2 seconds**.  
✔ **Modular Architecture** – Clean separation between the main app, encryption, and decryption logic.  
✔ **Scalable & Secure** – Designed to integrate with Django if Flask scalability becomes a concern.  

---

## 🛠 Technology Stack  

| Component                | Technology Used |
|--------------------------|----------------|
| **Backend Framework**    | Flask          |
| **Database**            | SQLite (via SQLAlchemy) |
| **Face Recognition**    | face_recognition (previously DeepFace) |
| **Encryption**          | TenSEAL (CKKS scheme) |
| **Image Processing**    | OpenCV         |
| **Frontend**            | HTML, JavaScript (Webcam API) |

---

## 🏗 Project Architecture  
```
├── app.py                  # Main Flask application
├── encryption_method.py     # Handles encryption using TenSEAL
├── decryption_method.py     # Handles decryption and comparison
├── templates/               # HTML templates (signup, login, home)
├── static/                  # Static files (CSS, JavaScript)
├── user_images/             # Stores preprocessed user images
└── README.md                # Project documentation
```

### **🔄 Data Flow**
1. **User captures an image** via webcam (JavaScript).  
2. **Image is preprocessed** (Base64 decoding, resizing).  
3. **Face embedding is extracted** using `face_recognition`.  
4. **Embedding is encrypted** via `TenSEAL` and stored in the database.  
5. During login, a **new image is captured** → **Embedding is extracted** → **Decryption & Comparison**.  
6. If embeddings match (based on Euclidean distance), authentication is successful.  

---

## 🚀 Installation  

### **1️⃣ Clone the Repository**
```bash
git clone https://github.com/yourusername/secure-face-auth.git
cd secure-face-auth
```

### **2️⃣ Create a Virtual Environment**
```bash
python -m venv venv
source venv/bin/activate   # On Mac/Linux
venv\Scripts\activate      # On Windows
```

### **3️⃣ Install Dependencies**
```bash
pip install -r requirements.txt
```

> **Dependencies:**  
> Flask, SQLAlchemy, OpenCV, face_recognition, TenSEAL, NumPy  

### **4️⃣ Run the Flask App**
```bash
python app.py
```
Visit **http://127.0.0.1:5000** in your browser.

---

## 🎯 Usage  

### **Sign Up**
1. Open the app and go to `/signup`.  
2. Enter your **name and email**, then **capture a photo** using the webcam.  
3. The system extracts **face embeddings**, encrypts them, and stores them securely.  
4. After successful signup, you can proceed to login.  

### **Login**
1. Visit `/login`.  
2. Enter your **username and email**, then **capture a new image**.  
3. The system decrypts the stored embedding and compares it with the new one.  
4. If authentication is successful, you are redirected to the homepage.  

---

## 🔐 Security Considerations  
- **Data Protection:** All face embeddings are stored **only in encrypted form** using TenSEAL’s CKKS encryption.  
- **Secure Key Handling:** Encryption keys are securely managed, preventing unauthorized access.  
- **Flask Secret Key:** Dynamically generated with `os.urandom(24)`.  
- **Sanitized File Handling:** Prevents path traversal attacks via `secure_filename`.  
- **CSRF Protection:** Consider implementing Flask-WTF for additional security in production.  

---

## 🔮 Future Improvements  

### **🚀 Framework Migration**
- If Flask's scalability becomes a limitation, the project may be migrated to **Django** for better session handling and authentication management.

### **⚡ Performance Enhancements**
- Explore **GPU acceleration** for faster encryption and decryption.  
- Optimize face matching with **lower-latency image preprocessing techniques**.  

### **🔑 Advanced Security**
- Implement **multi-factor authentication (MFA)** for additional login security.  
- Integrate **hardware security modules (HSMs)** for key management.  

### **📊 Dashboard & Admin Panel**
- Develop an **admin dashboard** to monitor authentication logs and user activity.  
