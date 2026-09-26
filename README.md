# Agentic-Framework-An-intent-driven-multi-agent-computing-environment

A Voice-Enabled Multi-Agent System
Transforming traditional computing into an intelligent, intent-driven operating environment.


# What is Agentic Framework?

It is a speech-enabled, multi-agent system prototype that allows users to interact with their computer using natural language. Instead of manually switching between apps, the system: 
Understands your intent
Breaks down complex goals
Coordinates specialized agents
Executes tasks autonomously
Built entirely in Python with a modular architecture.

# Key Features

● Voice-First Interaction - Wake word activation (“Hey Agent”), Real-time Voice Activity Detection (VAD), Whisper-based offline speech recognition, Text-to-speech responses

● Multi-Agent Architecture - Planner Agent (central coordinator), Reminder Agent, File Manager Agent, Web Search Agent, Mail Agent (Gmail integration), Booking Agent, Browser Control Agent, Process Monitor Agent, Sleep / Wake Control Agent, App Close Agent

● Intelligent NLP Pipeline - Intent refinement engine, nlu, Entity extraction (spaCy), Fuzzy matching (RapidFuzz), Date parsing (dateparser), Structured command normalization

● Real-Time GUI (NiceGUI) - Live transcription, Siri-style audio animation, Agent state visualization, Structured logs

# Architecture Overview

![PHOTO-2025-11-10-10-31-52](https://github.com/user-attachments/assets/cb3a45eb-2cb8-4846-9f74-1f72a26a21e7)

# Getting Started

Prerequisites 

● Linux with a GNOME / X11 desktop (agents use xdg-open, nautilus, xdotool, wmctrl, systemd-inhibit)

● Python 3.10+

● OpenAI Whisper + ffmpeg

● A microphone

● Optional: MongoDB (reminders and logs), Gemini API key (transcript cleanup), Amadeus test API keys (flight search), Google OAuth client (Gmail)

# Setup 

    # Clone

    git clone https://github.com/panaum/Agentic-OS.git

    cd Agentic-OS

    # Create Virtual Environment

    python -m venv venv

    source venv/bin/activate

    # Install System Packages (Debian/Ubuntu)

    sudo apt install ffmpeg xdotool wmctrl espeak-ng portaudio19-dev

    # Install Dependencies (there is no requirements.txt yet)

    pip install openai-whisper sounddevice webrtcvad numpy spacy rapidfuzz dateparser python-dateutil pyttsx3 psutil requests duckduckgo-search nicegui python-dotenv pymongo google-auth google-auth-oauthlib google-api-python-client google-generativeai

    # Download spaCy model

    python -m spacy download en_core_web_sm

# Download OpenAi Whisper

    pip install git+https://github.com/openai/whisper.git 

It also requires the command-line tool ffmpeg to be installed on your system, which is available from most package managers:

    # on Ubuntu or Debian
    sudo apt update && sudo apt install ffmpeg

    # on Arch Linux
    sudo pacman -S ffmpeg

    # on MacOS using Homebrew (https://brew.sh/)
    brew install ffmpeg

    # on Windows using Chocolatey (https://chocolatey.org/)
    choco install ffmpeg

    # on Windows using Scoop (https://scoop.sh/)
    scoop install ffmpeg

# Configuration

Create a `.env` file in the project root (all values optional):

    MONGO_URI=mongodb://localhost:27017
    MONGO_DB_NAME=agentic_os
    GEMINI_ENABLED=true
    GEMINI_API_KEY=your-key

Some settings live directly in `config.py`: Whisper model size (`tiny.en`), hotwords, session end words, timezone (IST), Amadeus API keys and `GMAIL_SCOPES`.

For Gmail, save a Google OAuth desktop client as `credentials.json` in the project root. On first use a browser window opens for consent and the token is saved to `token.json`.

# Running

     # GUI Mode (dashboard at http://localhost:8080)

     python app_nicegui.py

     # Terminal

     python main.py

     # Sandbox payment page for the booking flow (separate terminal)

     python -m http.server 8000

Say "Hey Agent" to start a session and "Bye Agent" to end it. Logs are written to `nlu_log.jsonl` and `agent_log.jsonl`.

# Examples

● “Hey Agent, open Firefox”

● “Remind me to submit the report at 3 PM”

● “Search for multi-agent systems research”

● “Close Spotify”

● “Read my latest email”

● “Create a file called notes.txt on the desktop”

● “Find flights from Delhi to Mumbai tomorrow”

● “What's making my computer slow?”

# Why It’s Different

● Multi-agent orchestration

● Offline speech recognition

● Intent-driven execution

● Modular architecture

● Real-time GUI

# Known Issues

● `agents/mail_agent.py` is missing but is imported by `agents/__init__.py` and `agents/planner.py`, so the app fails to start until it is added

● `GMAIL_SCOPES` in `config.py` is empty, so Gmail auth fails until a scope is set (e.g. `https://www.googleapis.com/auth/gmail.readonly`)

● Amadeus keys are hard-coded as empty strings in `config.py` instead of read from `.env`

● The Gemini call uses an outdated `google-generativeai` API, so it usually falls back to local corrections

● Linux only; app names and window control are GNOME/X11 specific
    
# Future Improvements

● LLM-based reasoning layer

● Adaptive memory learning

● IoT device integration

● Reinforcement-learning planner




