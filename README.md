# web-app-ysl
ysl connect

This is a fantastic, well-structured technical plan. The separation of concerns between the React frontend (for lightweight capture/rendering) and the FastAPI backend (for heavy inference) is the industry standard for this type of application.

Here is a professional, GitHub-ready **README.md** tailored to your specific architecture and project description.

-----

# 🤟 YSL Connect: Real-Time Sign Language to Text

> **Bridging the communication gap between the Deaf community and the hearing world through AI.**

## 📖 Project Overview

**YSL Connect** is an accessibility-focused web application designed to break down language barriers. By leveraging advanced computer vision and machine learning, the application serves as a real-time interpreter.

It captures sign language gestures via a standard webcam and instantly translates them into coherent, readable English sentences. This tool aims to foster inclusivity, allowing for seamless, two-way interaction without the need for a human interpreter.

### How It Converts Signs to Sentences

The system moves beyond simple static gesture recognition. It employs a three-step pipeline to generate natural language:

1.  **Detection (The "Eyes"):** Utilizing **MediaPipe/CV**, the system extracts 3D hand and body skeletal landmarks in real-time from the webcam feed.
2.  **Classification (The "Brain"):** These landmarks are streamed to a **FastAPI** backend where an ML model classifies the gesture sequences.
3.  **Translation (The "Voice"):** Raw token outputs are processed through an NLP layer to apply grammar, syntax, and smoothing, converting disjointed signs (e.g., "ME GO STORE") into fluent English (e.g., "I am going to the store").

-----

## 🏗 System Architecture

This project is built as a decoupled system using a **React + TypeScript** frontend and a **FastAPI** backend, communicating over **WebSockets** for low-latency performance.

### 1️⃣ Frontend (React + TypeScript)

  * **Webcam Capture:** Manages camera access and captures frames at \~15-30 FPS.
  * **Landmark Extraction:** (Optional) Extracts lightweight keypoints client-side to reduce network bandwidth.
  * **Communication:** Establishes a persistent WebSocket connection to stream data and receive predictions.
  * **UI/UX:** Displays the live video feed, real-time translated text, and confidence scores with an accessible, high-contrast design.

### 2️⃣ Backend (FastAPI)

  * **Inference Engine:** Receives frames/keypoints and runs them through the classification model (CNN/LSTM/Transformer).
  * **Session Management:** Maintains context for sentence construction and smoothing.
  * **API Layer:** Handles WebSocket events and standard REST endpoints for application logic.

-----

## 🚀 Tech Stack

| Component | Technology | Description |
| :--- | :--- | :--- |
| **Frontend** | React, TypeScript | UI Library and Type Safety |
| **Styling** | Tailwind CSS | Rapid, responsive styling |
| **State** | React Hooks / Context | Managing video stream states |
| **Backend** | Python, FastAPI | High-performance async API |
| **ML/CV** | TensorFlow / PyTorch, MediaPipe | Model inference and landmark detection |
| **Protocol** | WebSockets | Real-time, bidirectional communication |

-----

## 🔄 Data Flow Pipeline

1.  **Input:** User signs in front of the webcam.
2.  **Capture:** Frontend captures video frames/keypoints.
3.  **Transport:** Data is streamed via WebSocket to the Backend.
4.  **Preprocessing:** FastAPI resizes frames or normalizes keypoints.
5.  **Inference:** The ML model predicts the sign/gloss.
6.  **Post-processing:** The backend constructs the sentence (smoothing & de-duplication).
7.  **Output:** Prediction is sent back to the Frontend and displayed instantly.

-----

## 🛠 Installation & Setup

### Prerequisites

  * Node.js & npm
  * Python 3.9+
  * Git

### 1\. Clone the Repository

```bash
git clone https://github.com/yourusername/ysl-connect.git
cd ysl-connect
```

### 2\. Backend Setup (FastAPI)

```bash
cd backend
# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Start the server
uvicorn main:app --reload
```

### 3\. Frontend Setup (React)

```bash
cd frontend
# Install dependencies
npm install

# Start the development server
npm start
