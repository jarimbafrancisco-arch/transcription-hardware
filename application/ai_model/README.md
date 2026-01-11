# 🎙️ Advanced AI Voice Transcriptor (Google Chirp V2)

This module is the core audio-to-text engine for **Project 5**. It transforms real-time vocal input into highly accurate, punctuated text using Google's state-of-the-art Universal Speech Model.

---

## 🌟 Project Concept: The "Invisible Bridge"
The philosophy behind this project is to create a seamless, zero-latency bridge between human thought and digital text. Unlike traditional recorders that save files to a hard drive and upload them later, this application uses **In-Memory Streaming Logic**.

It keeps the microphone "warm" and ready in the background, but only captures data when you command it. By leveraging the **Google Chirp (V2)** model, the system doesn't just recognize words—it understands context, detects multiple languages automatically, and applies professional punctuation in real-time.



---

## 📖 Technical Code Breakdown

### 1. The "Traffic Light" (Threading Logic)
The program uses a threading system to ensure the user interface (keyboard) and the audio capture (hardware) never block each other.
* **`recording_event = threading.Event()`**: Acts as a global signal. When you press Enter, the light turns **Green** (`set()`). When you press it again, it turns **Red** (`clear()`).
* **`audio_data = []`**: Our temporary "storage vault" that holds audio samples only when the light is green.

### 2. The "Background Worker" (The Callback)
```python
def audio_callback(indata, frames, time, status):
    if recording_event.is_set():
        audio_data.append(indata.copy())