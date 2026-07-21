# Synced Lyrics Display
Synced Lyrics Display is a desktop application written in **Python** and **HTML/JS** that listens to whatever's playing on your speakers, identifies the song, and displays real-time synced lyrics in a clean, vinyl-record-style UI.

---

## Table of Contents
- [Overview](#overview)  
- [Features](#features)  
- [Motivation & Learning Goals](#motivation--goals)  
- [Technical Details](#technical-details)  
- [Installation](#installation)  
- [Setting Up a Free ACRCloud Server](#setting-up-a-free-acrcloud-server)  
- [Future Improvements](#future-improvements)  

---

## Overview
Synced Lyrics Display is designed to provide a passive, always-on "now playing" screen — no need to connect a Spotify or Apple Music account. It listens to your speakers through your microphone, identifies the currently playing song via ACRCloud, fetches the album art and lyrics automatically, and scrolls the lyrics in sync with the music on a Apple Music inspired display. Settings like audio input device, timing offset, and WebSocket port are all configurable and saved between sessions.

---

## Features
- **Passive Song Recognition** – Identifies whatever's playing through your speakers using ACRCloud, no streaming service API required.  
- **Synced Scrolling Lyrics** – Lyrics scroll and highlight in time with the song as it plays.   
- **Apple Music inspired Display** – Animated spinning vinyl with fetched album art as the label.  
- **Auto-Fetched Metadata** – Album art and duration pulled automatically via iTunes API.  
- **Configurable Settings** – Choose your audio input device, adjust timing offset, and change WebSocket port from an in-app settings panel.  
- **Persistent Credentials** – ACRCloud credentials are entered once and saved locally.  
- **Auto-Reconnect** – WebSocket connection between the Python backend and the display automatically reconnects if dropped.  

---

## Motivation & Goals
I made this project because I wanted a way to see the lyrics of songs I played on my Alexa without Shazaming or Googleing them.
1. Real-time audio processing and fingerprinting via a third-party API.  
2. WebSocket-based communication between a Python backend and an HTML/JS frontend.  
3. Threaded/async programming for concurrent recording, identification, and UI updates.  
4. Building a polished, animation-heavy UI from scratch (no frameworks).  
5. Working with external APIs (ACRCloud, iTunes, lyrics providers) and handling their failure cases gracefully.

This project was especially useful for getting comfortable working with an html file and pythong file that need to talk to each other.

---

## Technical Details
- **Language:** Python 3 (backend), HTML/CSS/JS (frontend)  
- **Audio Capture:** `pyaudio`  
- **Song Recognition:** ACRCloud API (HMAC-signed requests)  
- **Lyrics Source:** `syncedlyrics`  
- **Album Art / Duration:** iTunes Search API  
- **Communication:** WebSocket server (`websockets`) between Python and the display  
- **Data Storage:** JSON (`credentials.json`, `settings.json`)  
- **Concurrency:** `threading` for recording/identification, `asyncio` for the WebSocket server  

---

## Installation
1. Download the `.zip` file (or clone the repo).  
2. Extract it to your desired location.  
3. Run `SyncedLyricsDisplay.exe`.  
4. On first launch, a setup window will ask for your ACRCloud credentials — see below for how to get these for free.  
5. Once entered, the display will start listening and identifying songs automatically.  

---

## Setting Up a Free ACRCloud Server
ACRCloud offers a free tier that's more than enough for personal use. Here's how to get your credentials:

1. Go to **[acrcloud.com](https://www.acrcloud.com/)** and click **Sign Up** to create a free account.  
2. Once logged in, go to your **Console** and select **Audio & Video Recognition** → **Create a Project**.  
3. Give the project a name (e.g. "Lyrics Display") and choose **Audio Recognition** as the type.  
4. After the project is created, open it and go to the **Access Key** tab. You'll find three values you need:  
   - **Host** (e.g. `identify-us-west-2.acrcloud.com`)  
   - **Access Key**  
   - **Secret Key**  
5. Copy these into the setup popup when you first launch the app.  
6. The free tier includes a limited number of recognitions per month — plenty for personal desktop use, but keep an eye on usage if you're running it constantly all day.  

That's it — no money required for the free tier.

---

## Future Improvements
- Support for additional song recognition providers as a fallback  
- Cross-platform support (currently Windows-focused for device handling)  
- Better handling of songs with no lyrics available  
- Customizable themes for the display  
- Option to manually correct a misidentified song
