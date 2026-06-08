# 🌀 Fan Stop Detection

A real-time motion analysis tool built with Python and OpenCV that monitors a fan (or any rotating object) in a video and automatically detects when it **stops moving** — with configurable sensitivity and a built-in alarm system.

---

## ✨ Features

- 🔍 **Motion scoring** — measures per-frame pixel difference to quantify movement
- ⏱️ **Sustained stop detection** — only triggers alarm after the fan has been still for a configurable duration
- 📊 **Live motion bar** — visual indicator of current motion level with threshold marker
- 🎨 **Annotated output video** — saves a fully annotated `.mp4` with status overlay
- 📈 **Progress bar** — shows processing progress at the bottom of each frame
- 🚨 **Color-coded status** — Green (running) → Orange (stopping...) → Red (STOPPED!)

---

## 🛠️ Requirements

- Python 3.8+
- OpenCV (`opencv-python`)
- NumPy

Install dependencies:

```bash
pip install opencv-python numpy
```

---

## 🚀 Usage

1. Place your input video in the project directory and update the config at the top of the script:

```python
INPUT_VIDEO  = 'fan.mp4'
OUTPUT_VIDEO = 'fan_output.mp4'
```

2. Run the script:

```bash
python fan_stop_detection.py
```

3. A window will show the annotated video in real time. Press **`ESC`** to stop early.
4. The annotated output video is automatically saved to `fan_output.mp4`.

---

## ⚙️ Configuration

| Parameter | Default | Description |
|-----------|---------|-------------|
| `STOP_THRESHOLD` | `10000` | Motion score below this value is considered "stopped" |
| `STOP_DURATION` | `1.0` s | How long motion must stay below threshold to trigger alarm |
| `BLUR_KERNEL` | `(7, 7)` | Gaussian blur kernel — increase to reduce noise sensitivity |
| `INPUT_VIDEO` | `fan.mp4` | Path to input video file |
| `OUTPUT_VIDEO` | `fan_output.mp4` | Path to save annotated output video |

---

## 🧠 How It Works

| Step | Description |
|------|-------------|
| **Frame diff** | Computes absolute difference between consecutive grayscale frames |
| **Motion score** | Sums pixel differences (normalized by 255) as a motion intensity metric |
| **Sliding window** | Averages scores over a rolling window equal to `fps × STOP_DURATION` |
| **Threshold check** | If average score stays below `STOP_THRESHOLD` for the full duration, alarm triggers |
| **UI overlay** | Draws status text, motion bar, threshold line, and progress bar onto each frame |
| **Video export** | Writes every annotated frame to the output `.mp4` file |

---

## 🖥️ Output Preview

The output video includes:
- **Top bar** — current status (`Fan Running` / `Stopping... Xs` / `FAN STOPPED!`)
- **Motion bar** — real-time motion level with a yellow threshold marker
- **Bottom bar** — overall processing progress percentage

---

## 📁 Project Structure

```
├── fan_stop_detection.py   # Main script
├── fan.mp4                 # Input video (not included)
├── fan_output.mp4          # Annotated output (generated)
└── README.md
```

---

## 📌 Notes

- Tune `STOP_THRESHOLD` based on your video's lighting and camera noise — run once and observe the `Motion:` value in the top-right corner to find a good baseline.
- Works for any periodic motion (conveyor belts, motors, spinning machinery), not just fans.
- Output codec is `mp4v`; rename to `.avi` and switch codec to `XVID` if compatibility issues arise.

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).
