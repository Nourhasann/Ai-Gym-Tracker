# AI Gym Tracker — Pose Estimation with MediaPipe & OpenCV

A real-time bicep curl counter built with **MediaPipe Pose** and **OpenCV**. The app uses your webcam to detect body landmarks, calculates the elbow joint angle, and automatically counts reps as you curl.



## Demo Overview

- Detects 33 body landmarks in real time from a webcam feed
- Calculates the angle at the elbow joint (shoulder → elbow → wrist)
- Tracks curl stage (`up` / `down`) and counts completed reps
- Renders a live skeleton overlay, current angle, rep count, and stage on screen

## Repository Contents

| File | Description |
|---|---|
| `Bicep_Curl_Counter_Tutorial.ipynb` | Step-by-step tutorial notebook. Builds up the project piece by piece: webcam feed → pose detection → joint extraction → angle calculation → full curl counter. Good for learning how it works. |
| `ai_gym_tracker.py` | Final, clean, standalone script. Just the finished curl counter — run it and go. |
| `requirements.txt` | Pinned dependency versions known to work together. |



## Usage

Run the final script directly:

```bash
python ai_gym_tracker.py
```

- A window will open showing your webcam feed with the pose skeleton overlaid.
- Perform bicep curls with your **left arm** in view of the camera.
- Rep count and current stage (`up`/`down`) are displayed in the top-left corner.
- Press **`q`** to quit.

Alternatively, open `Bicep_Curl_Counter_Tutorial.ipynb` in Jupyter to walk through each step interactively:

```bash
jupyter notebook Bicep_Curl_Counter_Tutorial.ipynb
```

## How It Works

1. **Video capture** — OpenCV grabs frames from the webcam.
2. **Pose detection** — Each frame is passed to MediaPipe's Pose model, which returns 33 body landmarks (x, y, visibility).
3. **Joint extraction** — The left shoulder, elbow, and wrist coordinates are pulled out.
4. **Angle calculation** — A trigonometry function (`arctan2`) computes the angle at the elbow.
5. **Rep counting logic** — Angle > 160° marks the "down" position; angle < 30° while previously "down" marks a completed rep and flips to "up".
6. **Rendering** — OpenCV draws the skeleton, angle, rep counter, and stage back onto the video frame.

## Known Limitations

- Tracks only the **left arm** by default (can be adapted for right arm or both).
- Accuracy depends on lighting, camera angle, and how much of your body is in frame.
- Not tested against every OS/Python/MediaPipe combination — if you hit dependency errors.

## Acknowledgements

Built by following the MediaPipe Pose tutorial approach for real-time exercise tracking, adapted and documented here for learning purposes.

## License

MIT — feel free to use, modify, and build on this project.

