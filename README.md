# Translate Project

Video transcription and subtitle translation pipeline — upload a video, get an SRT file, and translate it from English to French using AI.

## What it does

1. **Transcribe** — Extracts speech from video files and generates SRT subtitles using Whisper
2. **Enhance** — Cleans and splits subtitle segments for readability
3. **AI Enhancement** — Refines subtitles using Mistral 7B (local LLM via llama.cpp)
4. **Translate** — Translates SRT files from English to French using Meta's M2M100 model

## Architecture

```
backend/          → FastAPI server with /transcribe and /translate_srt endpoints
frontend/         → Streamlit UI for uploading videos and downloading subtitles
translator/       → Core translation and enhancement logic
  ├── translator.py              → M2M100-based EN→FR translation
  ├── subtitle_splitter.py       → SRT cleanup and segment splitting
  └── subtitle_enhancer_ai.py    → Mistral 7B subtitle refinement
srt_files/        → Raw SRT output directory
```

## Tech Stack

- **FastAPI** + **Uvicorn** — Backend API
- **Streamlit** — Frontend UI
- **faster-whisper** — Speech-to-text transcription
- **M2M100** (Hugging Face Transformers) — Multilingual translation
- **Mistral 7B** (llama.cpp) — Local LLM for subtitle enhancement
- **PyTorch** — Model inference

## Setup

```bash
pip install -r requirements.txt
```

> The Mistral model (`mistral-7b-instruct-v0.2.Q4_K_M.gguf`) must be placed in `translator/model/`. It is not included in the repo due to its size.

## Usage

**Run the backend:**
```bash
cd backend
uvicorn app.main:app --reload
```

**Run the frontend:**
```bash
cd frontend
streamlit run app.py
```

**Or run locally (CLI):**
```bash
python main.py
```

## Team

Built as a university project at UTT.
