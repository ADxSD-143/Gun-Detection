# Gun Detection

A Python and OpenCV notebook project that explores webcam-based object classification and **gun-type estimates**. It uses a CLIP-based zero-shot approach with an ONNX Runtime inference path.

> **Important limitation:** This is an experimental demo, not a firearm-specialized detector and not a safety-reliable system. Its labels and match scores are rough estimates from a general-purpose model. Do not use it for security decisions, threat assessment, or real-world enforcement.

## Features

- Webcam-based frame capture and image processing with OpenCV.
- Zero-shot text/image matching for these candidate labels:
  - Pistol
  - Revolver
  - Rifle
  - Shotgun
  - Submachine gun
  - Non-gun object
- Displays a predicted label and a match score/estimate.
- Uses ONNX Runtime for CPU-based inference, avoiding dependence on a working PyTorch installation.
- Downloads the required model files from Hugging Face on first run, where configured in the notebook.

## Project structure

```text
Gun-Detection/
├── main.ipynb       # Main notebook and demo workflow
├── requirements.txt # Python dependencies
├── cascade.xml      # Included cascade XML file
└── README.md        # Project documentation
```

## Requirements

- Python 3.11 is the environment used for the project.
- A webcam for the live demo.
- Internet access for the first model download.
- Windows, macOS, or Linux with a working OpenCV-compatible camera setup.

## Setup

Run these commands from the project directory.

### 1. Create and activate a virtual environment (recommended)

**Windows PowerShell**

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, you can run the environment's Python directly with `.venv\Scripts\python.exe`.

**macOS/Linux**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 2. Install dependencies

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

The dependencies include NumPy, OpenCV, imutils, Pillow, Hugging Face Hub, Transformers, Tokenizers, and ONNX Runtime.

### 3. Open and run the notebook

1. Open `main.ipynb` in PyCharm or Jupyter.
2. Select the virtual environment created above as the notebook kernel.
3. Run the cells **from top to bottom**.
4. On the first run, allow time for the notebook to download the model files.
5. Grant camera access if prompted.

To stop the live webcam loop, use the notebook's displayed stop control if available, or interrupt the running cell/kernel.

## How it works

```text
Webcam frame
    ↓
OpenCV image capture / preprocessing
    ↓
CLIP-based image and candidate-text matching
    ↓
ONNX Runtime inference
    ↓
Best-matching candidate label + match score
    ↓
Display result
```

The model compares the image with text labels; it does **not** establish with certainty that an object is a real firearm or determine whether a situation is dangerous. A high match score is not a calibrated probability of a gun being present.

## Troubleshooting

- **Webcam not opening:** Close other applications using the camera, check OS camera permissions, and verify the camera index used in the notebook.
- **Missing package/import error:** Activate the correct virtual environment and run `python -m pip install -r requirements.txt` again.
- **Model download fails:** Check internet access and rerun the relevant notebook cell.
- **Slow inference:** This project uses CPU-based ONNX inference in the current setup, so real-time performance depends on your CPU and frame processing settings.
- **Notebook errors after a partial run:** Restart the kernel and run all cells from the top.

## Tech stack

Python · OpenCV · NumPy · imutils · Pillow · Hugging Face Transformers · Hugging Face Hub · ONNX Runtime · Jupyter Notebook

## Future improvements

- Evaluate the model on a clearly documented, human-reviewed test set.
- Report precision, recall, false positives, and false negatives instead of relying only on match scores.
- Add robust camera/resource cleanup and clearer error handling.
- Compare the zero-shot baseline with a validated, task-specific model before making any performance claims.

## Disclaimer

This repository is for learning and experimentation. Predictions can be wrong, including confusing ordinary objects with firearms or failing to recognize a firearm. It must not be used as the sole basis for safety, security, or law-enforcement decisions.
