# FocusTime

> A simple mobile focus-timer app that helps you concentrate on one task at a time and keep a history of what you've worked on.

FocusTime is a cross-platform mobile application built with React Native and Expo. You enter the subject you want to focus on, start a countdown timer, and the app keeps you distraction-free until the session ends — playing a bell sound and vibrating when your time is up. Every completed or cancelled session is stored locally so you can review what you've focused on over time.

## Tech Stack

- **React Native** (Expo SDK 40)
- **Expo** — build, run, and manage the app across iOS, Android, and web
- **React** 16.13.1
- **react-native-paper** — Material Design UI components (`ProgressBar`, `TextInput`, `Text`)
- **expo-av** — audio playback for the end-of-session bell
- **expo-keep-awake** — keeps the screen on while a timer is running
- **@react-native-async-storage/async-storage** — local persistence of focus history
- **react-native-web** — web support via Expo

## Features

- **Set a focus subject** — type in what you want to focus on before starting a session.
- **Countdown timer** — a full-screen countdown that displays the remaining minutes and seconds.
- **Selectable session lengths** — quickly switch between 10, 15, and 20 minute timers.
- **Start / pause control** — start the timer or pause it at any point.
- **Progress bar** — a visual progress indicator that tracks how much of the session remains.
- **End-of-session alert** — plays a bell sound (`assets/bell.mp3`) and vibrates the device when the timer reaches zero.
- **Screen kept awake** — the display stays on during an active session so the timer is always visible.
- **Focus history** — completed and cancelled sessions are recorded and shown in a list, colour-coded green (completed) or red (cancelled).
- **Persistent storage** — history is saved to device storage with AsyncStorage, so it survives app restarts.
- **Clear history** — wipe the recorded focus history with a single button.

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) and npm
- [Expo CLI](https://docs.expo.dev/) — `npm install -g expo-cli`
- The [Expo Go](https://expo.dev/client) app on your iOS or Android device, or a configured simulator/emulator

### Installation

```bash
git clone https://github.com/AckerCoder/focusApp.git
cd focusApp
npm install
```

### Running the App

This is an Expo project. Start the development server and choose your target platform:

```bash
# Start the Expo dev server (opens the Metro bundler / dev tools)
npm start

# Run directly on a connected Android device or emulator
npm run android

# Run directly on an iOS simulator (macOS only)
npm run ios

# Run in the browser
npm run web
```

When you run `npm start`, scan the QR code with the Expo Go app to launch FocusTime on a physical device.

## Project Structure

```
focusApp/
├── App.js                          # Root component: wires up focus subject, timer, and history + AsyncStorage persistence
├── app.json                        # Expo app configuration (name, icons, splash, iOS/web settings)
├── babel.config.js                 # Babel configuration
├── package.json                    # Dependencies and Expo run scripts
├── assets/                         # App icons, splash screen, and the bell.mp3 alert sound
├── components/
│   └── AssetExample.js
└── src/
    ├── components/
    │   ├── Countdown.js            # Countdown logic and time display (mm:ss)
    │   └── RoundedButton.js        # Reusable circular button
    ├── features/
    │   ├── focus/
    │   │   ├── Focus.js            # Input for choosing a focus subject
    │   │   └── FocusHistory.js     # List of past sessions + clear button
    │   └── timer/
    │       ├── Timer.js            # Timer screen: countdown, progress bar, controls, end alert
    │       └── Timing.js           # 10 / 15 / 20 minute duration selector
    └── utils/
        ├── sizes.js                # Shared font and padding size constants
        └── uuid.js                 # UUID generator for history entries
```

## How It Works

1. On the home screen, enter what you'd like to focus on and tap **+** to start a session.
2. The timer screen appears. Pick a duration (10, 15, or 20 minutes) and tap **start**.
3. Watch the countdown and progress bar; tap **pause** to stop temporarily, or **-** to cancel and return home.
4. When the timer ends, the bell rings and the device vibrates. The session is added to your focus history.
5. Back on the home screen, review the **Things we've focused on** list, or tap **Clear** to reset it.
