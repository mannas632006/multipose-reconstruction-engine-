# Multipose Reconstruction Engine By Muhammad Anas

Automated 3D reconstruction system that turns a set of photos of an object into a downloadable 3D model (`.glb`). It combines an Arduino-controlled turntable, live webcam capture, and the Tripo3D cloud API for multi-view-to-3D reconstruction, all wrapped in a PyQt6 desktop app with a built-in WebGL viewer.

## Features

- **Live camera feed** — view and capture directly from a webcam (laptop or external), switchable in-app
- **Two scan modes**
  - **Auto Turntable**: sends rotation commands to an Arduino over serial, automatically capturing a frame after each step
  - **Manual Scan**: capture a configurable number of views by hand at your own angles
- **Cloud 3D reconstruction** via the [Tripo3D](https://www.tripo3d.ai/) API — uploads sampled images and polls until a `.glb` mesh is ready
- **Built-in 3D viewer** — renders the resulting model using Three.js with orbit controls, served locally through a lightweight embedded HTTP server
- **Re-process mode** — recompile a model from previously captured images without re-scanning
- **Configurable settings** — API key, Arduino COM port & baud rate, camera index, number of images, export directory, and team member roster, all stored in `config.json`
- **Load external models** — open any existing `.glb` file in the viewer

## Tech Stack

| Component | Technology |
|---|---|
| GUI | PyQt6 |
| Camera capture | OpenCV |
| Hardware control | pyserial (Arduino) |
| 3D reconstruction | Tripo3D REST API |
| 3D viewer | Three.js (bundled, offline) |
| Local web server | Python `http.server` |
| Packaging | PyInstaller |

## Requirements

- Python 3.9+
- An Arduino (for Auto Turntable mode) running the included turntable sketch
- A Tripo3D API key ([get one here](https://www.tripo3d.ai/))
- A webcam

Install dependencies:
```bash
pip install PyQt6 PyQt6-WebEngine opencv-python pyserial requests
```

## Setup

1. Clone the repo:
```bash
   git clone https://github.com/mannas632006/multipose-reconstruction-engine-.git
   cd multipose-reconstruction-engine-
```
2. (Optional) Upload the Arduino sketch in `arduino_button/` to your microcontroller if using Auto Turntable mode.
3. Run the app:
```bash
   python scanner_v3.py
```
4. Open **Settings (⚙)** and enter your Tripo3D API key, Arduino COM port, and other preferences.

## Usage

1. Choose a scan mode: **Auto Turntable** or **Manual Scan**.
2. Capture images of your object from multiple angles.
3. Click **Execute Hardware Loop** (Auto) or **Compile Manual Views** (Manual) to upload and reconstruct.
4. Once processing completes, the resulting 3D model opens automatically in the built-in viewer — drag to orbit, scroll to zoom.
5. Use **Re-Process Existing Images** to rebuild a model from a previous capture without rescanning.

## Project Structure

├── scanner_v3.py # Main application
├── config.json # User settings (API key, Arduino config, etc.)
├── viewer.html # Standalone 3D viewer page
├── three.min.js # Three.js library (bundled)
├── OrbitControls.js # Three.js orbit camera controls
├── GLTFLoader.js # Three.js GLB/GLTF loader
├── arduino_button/ # Arduino turntable control sketch
└── scanner.spec # PyInstaller build spec


## Notes

- Requires a valid Tripo3D API key to perform 3D reconstruction — the app will not compile models without one.
- Auto Turntable mode requires the Arduino to be connected and running the matching sketch.
- Windows paths are used by default for capture/export folders; adjust for other platforms if needed.

# For Queries or More info, contact at mannas.632006@gmail.com
