# 📚 StudyBuddy — Real-Time Study Collaboration Platform & Desktop App

[![Live Web Demo](https://img.shields.io/badge/Live%20Demo-Cloudflare%20Pages-brightgreen)](https://studybuddy-app-e1a.pages.dev)
[![Electron](https://img.shields.io/badge/Desktop-Electron-47848F?logo=electron&logoColor=white)](https://www.electronjs.org/)
[![Node.js](https://img.shields.io/badge/Backend-Node.js%20%26%20Express-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![Socket.io](https://img.shields.io/badge/Realtime-Socket.io-010101?logo=socket.io&logoColor=white)](https://socket.io/)
[![WebRTC](https://img.shields.io/badge/Video-WebRTC-333333?logo=webrtc&logoColor=white)](https://webrtc.org/)

An all-in-one productivity and peer-accountability study platform built as a cross-platform desktop application using **Electron** with an embedded **Node.js/Express** server, and also deployable as a standalone web application.

🔗 **Live Web Demo:** [https://studybuddy-app-e1a.pages.dev](https://studybuddy-app-e1a.pages.dev)

---

## 🌟 Key Features

- **👥 Peer-Pressure Study Rooms (WebRTC & Socket.io):**
  - Multi-user virtual study rooms with camera/audio stream management via WebRTC mesh connections.
  - Real-time room presence, chat, and status indicators synchronized using Socket.io.
- **🧠 Distraction Memo & Quick Capture:**
  - Floating distraction logger allowing learners to offload random thoughts without breaking concentration.
  - Tagging, priority sorting, and post-session review workflows.
- **⏱️ Deep Focus Mode & Pomodoro Engine:**
  - Full-screen distraction-free focus workspace with customizable session timers.
  - Ambient background sound player (Lo-fi, White Noise, Nature sounds) for focus enhancement.
- **📊 Focus Analytics Dashboard:**
  - Session statistics, daily focus graphs, and habit streaks stored locally using **IndexedDB**.
- **🖥️ Native Desktop OS Integration:**
  - **System Tray Support:** Minimize the app to the taskbar system tray during study sessions with quick action menus.
  - **Single-Instance Lock:** Prevents redundant processes from running concurrently.
  - **IPC Bridge (`preload.js`):** Secure context-isolated bridge between Electron main process and renderer.

---

## 🏗️ Architecture Overview

StudyBuddy utilizes a hybrid embedded architecture:

```
┌─────────────────────────────────────────────────────────────┐
│                      Electron Wrapper                       │
│                                                             │
│   ┌────────────────────┐            ┌───────────────────┐   │
│   │ Main Process       │◄─── IPC ───┤ Renderer Process  │   │
│   │ (Tray, Window, OS) │            │ (UI, WebRTC, SPA) │   │
│   └─────────┬──────────┘            └─────────┬─────────┘   │
│             │                                 │             │
│             ▼                                 │             │
│   ┌────────────────────┐                      │             │
│   │ Embedded Express   │◄── Socket.io / HTTP ─┘             │
│   │ & Socket Server    │                                    │
│   └────────────────────┘                                    │
└─────────────────────────────────────────────────────────────┘
```

The application can also run purely in web mode without Electron:
- **Renderer (`public/`):** Pure vanilla JavaScript + modular CSS architecture for maximum performance and zero build dependencies.
- **Storage:** Local-first architecture using `localStorage` and `IndexedDB`.

---

## 🚀 Getting Started

### Prerequisites
- Node.js 18.x or newer
- npm or yarn

### Installation

```bash
# Clone the repository
git clone https://github.com/hoangdangwd/studybuddy-desktop-app.git
cd studybuddy-desktop-app

# Install dependencies
npm install
```

### Running the App

#### Option A: Run as Desktop App (Electron)
```bash
npm run dev
```

#### Option B: Run as Web-Only Mode
```bash
npm run web
# Open http://localhost:3000 in your browser
```

---

## 📁 Project Structure

```
├── main.js                   # Electron main process (lifecycle, system tray, window)
├── preload.js                # Secure ContextBridge for native OS capabilities
├── server.js                 # Embedded Express + Socket.io signaling server
├── public/                   # Frontend SPA assets
│   ├── index.html            # Main single-page application entry point
│   ├── memo.html             # Standalone distraction memo interface
│   ├── css/                  # Modular styling (variables, room, focus, toast, etc.)
│   ├── js/
│   │   ├── app.js            # App controller and router
│   │   ├── services/         # Socket.io, WebRTC, Media, Audio services
│   │   ├── pages/            # Home, room, focus, memo view logic
│   │   └── utils/            # IndexedDB storage and UI helpers
│   └── assets/               # Audio files and icons
```

---

## 📄 License
MIT License. Free for personal and commercial study productivity.
