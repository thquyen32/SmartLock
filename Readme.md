## 📖 Overview

**Smart Lock** is an IoT-based security system built with **ESP32**, **RFID card**, **keypad**, and **LCD display (16x2)** that communicates with a **Node.js server** and a **mobile app**.  
It provides **multiple unlocking methods** and real-time **lock status synchronization** via **HTTP** and **WebSocket** protocols.

Users can unlock the door using:
1. **RFID card**
2. **Keypad password**
3. **Android mobile app**

All lock and unlock activities are displayed on the **LCD screen** and kept in sync between hardware and app.

---

## ⚙️ Key Features

- 🪪 **RFID Unlocking**  
  - Scan your RFID card.  
  - ESP32 sends the card ID to the server via **HTTP**.  
  - If valid → lock opens.  

- 🔢 **Keypad Unlocking**  
  - Enter password via keypad.  
  - ESP32 sends it to the server for verification.  
  - If correct → lock opens.  

- 📱 **Android App Unlocking**  
  - Log in to your **family account** on the Android app.  
  - Send password (same as keypad method) via **HTTP request**.  
  - If valid → server commands ESP32 to unlock.  

- 🌐 **Real-time Synchronization**  
  - The system uses **WebSocket** to keep door status (LOCKED / UNLOCKED)  synchronized between the hardware and mobile app instantly.  

- 🖥️ **LCD Display (16x2)**  
  - Shows current status: `LOCKED`, `UNLOCKED`, `ACCESS DENIED`, etc.  

---


---

## 🛠️ Hardware Components

| Component | Description |
|------------|-------------|
| **ESP32** | Main microcontroller (WiFi + WebSocket capable) |
| **RFID RC522** | Reads RFID card IDs |
| **Keypad (4x4)** | For password input |
| **LCD Display 16x2** | Displays door status and messages |
| **Relay / Solenoid Lock** | Controls physical lock mechanism |
| **Power Supply (5V/12V)** | Powers the circuit |

---

## 💻 Software Components

| Component | Description |
|------------|-------------|
| **Node.js Server** | Handles authentication, database, and synchronization |
| **Database** | Stores RFID IDs, user passwords, and app accounts |
| **ESP32** | Manages inputs, communicates with server, drives LCD and lock |
| **Android App** | Provides remote unlocking and real-time status updates |

---

## 🔄 System Workflow

### 🪪 Method 1 – RFID Card
1. User scans an RFID card.  
2. ESP32 sends **card ID** to the server via HTTP.  
3. Server checks the database.  
4. If valid → returns **OK**, ESP32 unlocks door.  
5. Status “UNLOCKED” appears on LCD and app.

---

### 🔢 Method 2 – Keypad Password
1. User enters password on the keypad.  
2. ESP32 sends password via HTTP to the server.  
3. Server validates it.  
4. If correct → unlock door + update LCD + notify app through WebSocket.

---

### 📱 Method 3 – Android App
1. User logs into **family account** on Android app.  
2. App sends unlock password to the server.  
3. Server sends WebSocket event to ESP32.  
4. ESP32 unlocks the door and updates LCD + app status.

---

## 🌐 Communication Protocols

- **HTTP** – Used for authentication (RFID or password validation).  
- **WebSocket** – Used for real-time door status synchronization between ESP32 and mobile app.  

---

## 📱 Android App

- Allows family members to log in and unlock remotely.  
- Shows live lock/unlock status.  
- Connects securely to the Node.js backend using REST + WebSocket.
