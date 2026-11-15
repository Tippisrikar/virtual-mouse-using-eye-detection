# 👁️ Virtual Mouse Using Eye Detection

<p align="center">
  <b>Control Your Computer with Your Eyes!</b>
  <br>
  A Computer Vision-Based Virtual Mouse Using Eye Tracking Technology.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.9%20%7C%203.10%20%7C%203.11%20%7C%203.12-blue?logo=python" alt="Python">
  <img src="https://img.shields.io/badge/OpenCV-Computer%20Vision-green?logo=opencv" alt="OpenCV">
  <img src="https://img.shields.io/badge/MediaPipe-Face%20Mesh-orange" alt="MediaPipe">
  <img src="https://img.shields.io/badge/Status-Active-success" alt="Project">
  <img src="https://img.shields.io/badge/License-Not%20Specified-lightgrey" alt="License">
</p>

---

## 📌 Project Overview

**Virtual Mouse Using Eye Detection** is a computer vision-based application that allows users to control their computer mouse cursor using eye movements instead of a traditional physical mouse.

The project uses a webcam to capture real-time video, detects facial and eye landmarks using Google's MediaPipe Face Mesh, and processes the detected eye movements using OpenCV.

The detected iris position is translated into screen coordinates to control the mouse cursor. Additionally, the system detects a left-eye closure gesture to perform a mouse click.

This project demonstrates how Artificial Intelligence, Computer Vision, and Python can be combined to develop an alternative human-computer interaction system.

## ✨ Key Features

- 👁️ **Real-Time Eye Tracking:** Tracks eye movements using a webcam.
- 🖱️ **Virtual Mouse Control:** Moves the computer cursor according to iris position.
- 👀 **Eye-Closure Click Detection:** Detects a left-eye closure gesture to perform a mouse click.
- 🎥 **Live Camera Feed:** Displays the real-time video feed with detected eye landmarks.
- ⚡ **Real-Time Processing:** Processes facial landmarks continuously.
- 💻 **Hands-Free Interaction:** Reduces the need for a physical mouse during basic pointer operations.

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| Python | Main programming language |
| OpenCV | Webcam access and image processing |
| MediaPipe | Facial and eye landmark detection |
| PyAutoGUI | Mouse cursor movement and click simulation |
| NumPy | Numerical operations used by the computer vision ecosystem |

## 📋 System Requirements

### Hardware Requirements

- Desktop computer or laptop.
- Working webcam (built-in or external).
- Minimum 4 GB RAM recommended.
- Stable lighting conditions.
- Display screen.
- Keyboard for application interruption.

### Software Requirements

- Windows 10/11 recommended, or a compatible desktop operating system.
- Python 3.9–3.12 recommended for the specified MediaPipe version.
- pip (Python package manager).
- PyCharm, Visual Studio Code, or any Python-supported IDE (optional).

### Required Python Libraries

| Library | Version / Package | Description |
|---|---|---|
| OpenCV | opencv-contrib-python | Image and video processing |
| MediaPipe | 0.10.21 | Face Mesh and eye landmark detection |
| PyAutoGUI | pyautogui | Mouse automation |

**Note:** MediaPipe installs an OpenCV dependency. The application imports it using `cv2`.

## 🚀 Installation and Setup

Follow these instructions to download, configure, and run the project on your computer.

### Step 1: Clone the Repository

Open your terminal or command prompt and execute:

```bash
git clone https://github.com/Tippisrikar/virtual-mouse-using-eye-detection.git
```

Navigate to the project directory:

```bash
cd virtual-mouse-using-eye-detection
```

### Step 2: Create a Virtual Environment

Creating a virtual environment is recommended to keep project dependencies separate.

```bash
python -m venv venv
```

Activate the environment on Windows:

```bash
venv\Scripts\activate
```

For macOS/Linux:

```bash
source venv/bin/activate
```

### Step 3: Upgrade pip

```bash
python -m pip install --upgrade pip
```

### Step 4: Install Required Libraries

Install the required dependencies:

```bash
pip install mediapipe==0.10.21 pyautogui
```

This installs MediaPipe, its OpenCV dependency, and PyAutoGUI.

### Step 5: Verify Installation

Run the following command to check whether the required libraries are installed correctly:

```bash
python -c "import cv2, mediapipe as mp, pyautogui; print('All libraries installed successfully!')"
```

If the command executes without errors, the environment is ready.

## ▶️ How to Run the Project

After completing the installation, execute the following command from the project directory:

```bash
python main.py
```

The webcam will start automatically.

### How to Use the Virtual Mouse

1. Position yourself in front of your webcam.
2. Make sure your face and eyes are clearly visible.
3. Maintain sufficient lighting for accurate eye detection.
4. Move your eyes to control the mouse cursor.
5. Close your left eye briefly to trigger a left mouse click.
6. To stop the program, return to the terminal and press `Ctrl + C`.

**Note:** The current implementation does not include a dedicated exit key in the camera window.

## ⚙️ Project Implementation

The application uses a combination of computer vision, facial landmark detection, and mouse automation.

### 1. Webcam Initialization

OpenCV accesses the computer's default webcam using:

```python
cam = cv2.VideoCapture(0)
```

The webcam continuously captures video frames for processing.

### 2. Facial Landmark Detection

MediaPipe Face Mesh is initialized to detect facial landmarks.

```python
face_mesh = mp.solutions.face_mesh.FaceMesh(
    refine_landmarks=True
)
```

The `refine_landmarks=True` option enables more detailed eye and iris landmark detection.

### 3. Eye and Iris Tracking

The application processes the detected facial landmarks to identify the iris position.

The iris landmarks are extracted using:

```python
landmarks[474:478]
```

These landmarks are used to estimate eye position.

### 4. Mouse Cursor Movement

The detected iris coordinates are converted into screen coordinates.

PyAutoGUI moves the system cursor according to the calculated screen position.

```python
pyautogui.moveTo(screen_x, screen_y)
```

This allows users to control the cursor through eye movements.

### 5. Eye-Closure Click Detection

The application uses two landmarks from the left eye to estimate eye closure.

The following condition checks the vertical distance between the selected eye landmarks:

```python
if (left[0].y - left[1].y) < 0.004:
    pyautogui.click()
    pyautogui.sleep(1)
```

When the condition is satisfied, the application performs a left mouse click.

A one-second delay helps reduce repeated clicks.

### 6. Live Video Display

OpenCV displays the camera feed with detected eye landmarks using:

```python
cv2.imshow('Eye controlled mouse', frame)
```

This allows users to observe the eye-tracking process in real time.

## 🔄 System Workflow

The overall project workflow is illustrated below:

```text
             START
               |
               v
        Initialize Webcam
               |
               v
        Capture Video Frame
               |
               v
       Process Image Using
             OpenCV
               |
               v
      Detect Facial Landmarks
          Using MediaPipe
               |
               v
       Identify Eye and Iris
             Landmarks
               |
          +----+----+
          |         |
          v         v
     Iris Tracking  Eye Closure
          |         |
          v         v
    Calculate      Check Eye
  Screen Position  Landmark Gap
          |         |
          v         v
    Move Cursor   Perform Click
          |         |
          +----+----+
               |
               v
       Display Live Preview
               |
               v
       Continue Processing
```

## 📁 Project Structure

```text
virtual-mouse-using-eye-detection/
│
├── main.py
│   └── Main Python application
│
├── README.md
│   └── Project documentation
│
├── Eye operations[1].pdf
│   └── Supporting project document
│
└── .idea/
    └── IDE configuration files
```

## 🔍 Troubleshooting

| Issue | Possible Solution |
|---|---|
| Webcam not opening | Check webcam connection and camera permissions. |
| MediaPipe installation error | Verify Python version and install the specified MediaPipe version. |
| Cursor not moving | Check eye visibility, camera positioning, and desktop accessibility permissions. |
| Eye detection is inaccurate | Improve lighting and maintain a suitable distance from the webcam. |
| Multiple clicks occurring | Check lighting and eye positioning. The current code uses a fixed eye-closure threshold. |
| Module not found error | Activate the virtual environment and reinstall the required packages. |
| Mouse control not working | Check operating system permissions for mouse automation. |

## 🔐 Privacy and Safety

- The application accesses the webcam locally through OpenCV.
- The current implementation does not upload camera frames to an external server.
- The application controls the actual system mouse while running.
- Keep a keyboard available to interrupt the application.
- Save important work before testing the virtual mouse.

## 🚀 Future Enhancements

The project can be extended with the following improvements:

- Calibration system for improved cursor accuracy.
- Right-click and double-click functionality.
- Drag-and-drop support using eye gestures.
- Cursor smoothing to reduce unwanted movements.
- Customizable blink detection thresholds.
- Improved eye-tracking accuracy under different lighting conditions.
- Graphical user interface for easier configuration.
- Keyboard shortcuts for controlling and stopping the application.

## 🤝 Contributing

Contributions are welcome!

To contribute to this project:

1. Fork this repository.
2. Create a new feature branch.
3. Make your changes.
4. Commit your changes.
5. Push your branch.
6. Submit a pull request.

Suggestions, bug reports, and improvements are always appreciated.

## 📄 License

No license has currently been specified for this repository. Please contact the repository owner for permission before reusing or redistributing the code.

## 👨‍💻 Author

**Tippi Srikar**

- GitHub: [@Tippisrikar](https://github.com/Tippisrikar)
- Project Repository: [Virtual Mouse Using Eye Detection](https://github.com/Tippisrikar/virtual-mouse-using-eye-detection)

---

<p align="center">
  <b>Built with Python ❤️ and Computer Vision.</b>
  <br>
  Making Human-Computer Interaction Smarter!
</p>
