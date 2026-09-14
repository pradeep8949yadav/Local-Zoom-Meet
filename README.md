# LAN Collab: Secure Local Area Network Conferencing Suite

**LAN Collab** is a robust, offline-first collaboration tool designed for secure communication within a Local Area Network (LAN). Built with Python and PyQt6, it provides a complete suite of features including real-time video conferencing, low-latency audio mixing, screen sharing, instant messaging, and secure file transfer without requiring an internet connection.

## 📂 Project Structure

* **`lan_s29.py` (The Server)**
    * The central hub of the application. It acts as the "meeting room" host.
    * **Responsibilities:**
        * Manages TCP/TLS secure control connections.
        * Handles high-speed UDP packet routing for video.
        * Performs server-side audio mixing (combining multiple audio streams into one).
        * Manages the central file transfer relay.
        * Provides a GUI Control Panel for the host to monitor active clients and logs.
        
* **`lan_c29.py` (The Client)**
    * The user application for joining meetings.
    * **Features:**
        * Grid-based video display with active speaker highlighting.
        * H.264 video encoding for efficient bandwidth usage.
        * Screen sharing capabilities (full screen or region).
        * Chat interface and file upload/download manager.
        
* **`generate_certs.py` (Security Utility)**
    * A critical setup script that generates advanced self-signed X.509 SSL/TLS certificates (`server.crt`) and private keys (`server.key`).
    * Ensures all control traffic and file transfers are encrypted.
    
* **`auth_utils2.py` (Helper Utilities)**
    * Contains logic for IP address detection (auto-detecting the LAN IP).
    * Generates deterministic "Meeting Codes" based on the host machine's unique MAC address, ensuring the room code stays the same for the same server machine.

---

## 🚀 Features

### 1. 📹 Real-Time Video Conferencing
* **H.264 Encoding:** Uses `PyAV` (FFmpeg wrapper) to compress video streams, ensuring smooth performance even on slower networks.
* **Smart Grid Layout:** The client UI automatically adjusts the video grid based on the number of participants.
* **Active Speaker Detection:** The current speaker is highlighted with a visual border using RMS amplitude analysis.

### 2. 🎙️ Low-Latency Audio
* **Server-Side Mixing:** The server mixes incoming audio streams and sends a single combined stream back to each client. This reduces bandwidth and processing load on clients.
* **Mu-Law Compression:** Audio is compressed using the G.711 µ-law algorithm (similar to standard telephony) to minimize network packet size.

### 3. 🖥️ Screen Sharing
* **High Performance:** Utilizes `mss` for ultra-fast screen capturing.
* **Smart Window Filtering:** Uses `PyGetWindow` to filter out junk windows (overlays, system menus) during selection.

### 4. 🔒 Security First
* **TLS/SSL Encryption:** All control commands (login, chat, file initiation) and file transfers occur over an encrypted TCP socket wrapped in SSL.
* **Authentication:** Simple username checks prevent duplicate users.

### 5. 📁 File Transfer
* **Chunked Transfer:** Files are split into 4KB chunks for reliability.
* **Visual Progress:** Clients see a real-time progress bar for uploads and downloads.
* **Dedicated Port:** File transfers occur on a separate TCP port (default `9100`) to prevent blocking chat or video data.

---

## 🛠️ Prerequisites & Installation

### System Requirements
* **Python:** Version 3.8 or higher.
* **OS:** Windows (recommended for full High-DPI support), macOS, or Linux.
* **Audio Backend:**
    * **Windows:** Usually pre-installed.
    * **Linux:** You may need to install PortAudio (`sudo apt-get install libportaudio2`).
    * **macOS:** `brew install portaudio`

### Installation Steps

1.  **Clone or Extract the Project** to a folder on your machine.
2.  **Install Python Dependencies:**
    Open your terminal/command prompt in the project directory and run:
    ```bash
    pip install -r requirements.txt
    ```

---

## 📖 Usage Guide

### Step 1: Generate Security Certificates (One-time Setup)
Before running the server for the first time, you must generate the SSL certificates.

1.  Run the generator script:
    ```bash
    python generate_certs.py
    ```
2.  This will create two files in your directory:
    * `server.crt` (The Public Certificate)
    * `server.key` (The Private Key - **Keep this secure!**)

### Step 2: Start the Server
The person hosting the meeting must run the server script.

1.  Run the server:
    ```bash
    python lan_s29.py
    ```
2.  A **Control Panel** window will appear.
3.  **Note the "Meeting Code"**: This is a code like `123-456-789` displayed in the server log. It is derived from your machine's hardware ID.
4.  **Note the IP Address**: The server log will also display the LAN IP (e.g., `192.168.1.X`).

### Step 3: Join as a Client
Participants (and the host, if they want to be in the meeting) run the client script.

1.  Run the client:
    ```bash
    python lan_c29.py
    ```
2.  **Login Screen:**
    * **Username:** Enter a unique name.
    * **Join Code:** Enter the Meeting Code (e.g., `123-456-789`) **OR** the Server's IP address.
3.  Click **Connect**.
4.  Once connected, you can toggle your Camera, Mic, or Share Screen using the bottom control bar.

---

## ⚙️ Technical Configuration

If you need to modify ports or settings, look for the `--- Configuration ---` block at the top of `lan_s29.py` and `lan_c29.py`.

* **`TCP_PORT` (Default 9090):** Main control channel (Auth, Chat, Signaling).
* **`UDP_PORT` (Default 9091):** Media channel (Video/Audio packets).
* **`FILE_TCP_PORT` (Default 9100):** Dedicated channel for file transfers.
* **`DISCOVERY_PORT` (Default 9092):** Used for auto-discovery broadcasts.
* **`AUDIO_SAMPLE_RATE` (Default 16000Hz):** Lower quality but lower bandwidth. Can be increased to 44100Hz for music quality.

---

## 🔧 Troubleshooting

**Issue: "Connection Refused" or "Server not found"**
* Ensure the Server is running.
* Ensure both computers are on the **same Wi-Fi/Ethernet network**.
* **Firewall:** Windows Firewall often blocks Python network scripts.
    * Allow `python.exe` through the firewall on both Server and Client machines.
    * Ensure ports 9090, 9091, and 9100 are open.

**Issue: "Could not load SSL context"**
* You skipped Step 1. Run `python generate_certs.py` to create the missing `.crt` and `.key` files.

**Issue: Audio is choppy or lagging**
* This is often due to network packet loss (UDP). Try moving closer to the router or using a wired Ethernet connection.

**Issue: Video is black**
* Ensure the webcam is not being used by another application (like Zoom or Teams).
* Check the client log for "Camera fail" messages.
