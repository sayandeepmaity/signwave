# SignWave

**SIGNWAVE** — Smart Interpretation of Gestures using Neural Waveform Analysis and Visual Engine

**SignWave** is a deep learning-based system designed to detect and classify sign language gestures using only hand keypoints. Built using LSTM models and real-time webcam input, it enables efficient recognition of alphabet signs without relying on facial detection or wearable devices.

---

##  The Problem We Saw

Communication barriers for individuals with speech or hearing impairments make interaction in daily life challenging. Existing systems are often expensive, require wearables, or need complex setups.

Key challenges include:

- Limited accessibility to sign language translators
- Lack of real-time, camera-only gesture detection tools
- High hardware requirements for gesture systems
- Insufficient open-source, lightweight alternatives

---

##  Innovation

SignWave addresses these issues by providing:

- Real-time **sign language alphabet recognition**
- No need for facial tracking or wearable tech
- Works using **only webcam and hand landmarks**
- Lightweight, portable solution with GUI feedback

---

##  Research Questions

- Can hand keypoints alone enable accurate gesture detection?
- How well can temporal patterns be learned by deep networks?
- What is the ideal sequence length for gesture accuracy?
- How can real-time predictions be made resource-efficient?

---

##  Features

- Hand tracking via **MediaPipe**
- Custom-trained **LSTM** neural network
- Real-time webcam-based predictions
- Alphabet prediction with confidence score
- Easy-to-use UI using **OpenCV**

---

##  Data Collection

**Script:** `datacollection.py`

- Uses **OpenCV** to record **hand sign gestures** for each alphabet letter (A–Z).
- Captures images via **webcam** and stores them in the `RawData/` folder under corresponding alphabet subdirectories (e.g., A, B, C...).
- Focuses only on the **Region of Interest (ROI)** from **(0, 40)** to **(300, 400)** to isolate and enhance accuracy of hand gesture capture.

---

##  Data Preprocessing

**Script:** `predata.py`

- Loads raw hand sign images and applies **MediaPipe** to extract **21 hand landmarks** (keypoints) for each detected hand.
- Each 30-frame sequence is transformed into a `.npy` file storing extracted keypoints.
- Each sequence represents a complete hand gesture corresponding to a specific alphabet sign.
- The processed data is saved in the `DataPreProcessed/` directory, preserving the same folder structure.

---

##  Model Architecture & Training

**Script:** `trainingmodel.py`

- Implements a deep **LSTM (Long Short-Term Memory)** neural network for classifying temporal gesture sequences.
- Model architecture:
  - **3 LSTM layers** with ReLU activation and `return_sequences=True`
  - **2 Dense layers** with ReLU
  - **1 Output Dense layer** with **Softmax** activation for multi-class classification (A–Z)
- Training setup:
  - Uses `model.fit()` for **200 epochs**
  - Logs metrics via **TensorBoard**
- Post-training:
  - Saves model weights to `model.h5`
  - Saves model architecture to `model.json`

---

##  Real-Time Prediction

**Script:** `application.py`

- Loads trained model using `model.json` and `model.h5`
- Initiates real-time webcam feed using **OpenCV**
- Extracts live hand landmarks with **MediaPipe**
- Maintains a **rolling window of the last 30 frames** for consistent sequence prediction
- UI Overlay includes:
  - Current recognized gesture/class
  - Prediction confidence
  - Real-time feedback display using OpenCV

---

##  Visualization

- Live **probability bar** visualizations show model confidence across all classes (A–Z).
- **Predicted sentence history** is shown at the top of the webcam feed for contextual tracking.
- Confidence values update dynamically for real-time clarity.

---

##  Libraries Used

- **TensorFlow / Keras** – Deep learning model design and training
- **MediaPipe** – Hand tracking and landmark extraction
- **OpenCV** – Video capture, display, and GUI overlays
- **NumPy** – Efficient numerical array operations
- **scikit-learn** – Dataset splitting and utility preprocessing

---

##  Folder Structure

```bash
SignWave/
├── DataPreProcessed/
│   ├── A/
│   ├── B/
│   └── C/
├── RawData/
│   ├── A/
│   ├── B/
│   ├── C/
│   ├── Q/
│   └── t/
├── TrainandValidation/
│   ├── train/
│   ├── validation/
│   └── __pycache__/
├── application.py
├── datacollection.py
├── function.py
├── model.h5
├── model.json
├── predata.py
├── tempCodeRunnerFile.py
├── trainingmodel.py
├── LICENSE
└── README.md
```
