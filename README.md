# I-CURE 2.0 –Intelligent Care and Unified Remote Emergency Response for epilepsy

**An IoT-based patient monitoring and emergency alert prototype designed to detect seizure-like movement patterns and notify caregivers.**

## Overview

I-CURE 2.0 is a smart healthcare monitoring prototype built using an ESP32 microcontroller and multiple sensors. It continuously collects patient-related readings, monitors movement patterns, and sends data to a web-based monitoring dashboard.

When the prototype detects a potentially abnormal movement pattern, it can activate a local buzzer and send an alert to a configured Telegram caregiver account through the backend.

The system aims to support faster caregiver awareness and demonstrate how IoT technology can contribute to remote patient monitoring.

## Key Features

- **Real-time sensor monitoring:** Collects readings from connected sensors using ESP32.
- **Movement monitoring:** Uses the MPU6050 accelerometer and gyroscope to monitor movement patterns.
- **Heart-rate monitoring:** Uses the MAX30102 sensor to measure heart-rate-related readings.
- **Environmental monitoring:** Uses the BMP280 sensor to measure temperature and atmospheric pressure.
- **OLED display:** Displays live sensor readings and detection status.
- **Local emergency alert:** Activates a buzzer when an alert condition is detected.
- **Web dashboard:** Displays patient readings and monitoring information.
- **Backend integration:** Uses FastAPI for communication between ESP32 and the dashboard.
- **Data storage:** Stores received readings using SQLite.
- **Telegram notifications:** Sends configured caregiver alerts when an alert condition is recognised.
- **Demo mode:** Helps demonstrate the alert workflow during project presentations.

## Hardware Components

| Component | Purpose |
|---|---|
| ESP32 Dev Module | Main microcontroller |
| MPU6050 | Motion and acceleration monitoring |
| MAX30102 | Heart-rate and optical sensor readings |
| BMP280 | Temperature and atmospheric pressure |
| SH110X OLED | Live display |
| Buzzer | Local audio alert |
| Push buttons | Demo and alert acknowledgement |

## Technology Stack

**Hardware and Embedded Systems**
- ESP32
- Arduino IDE
- C/C++
- I2C communication

**Backend**
- Python
- FastAPI
- Uvicorn
- SQLite

**Frontend**
- HTML
- CSS
- JavaScript

**Notifications**
- Telegram Bot API

## System Architecture

1. Sensors collect patient and movement-related readings.
2. ESP32 processes the sensor data and evaluates the configured detection conditions.
3. The ESP32 sends readings to the FastAPI backend over Wi-Fi.
4. FastAPI receives and stores the readings in SQLite.
5. The dashboard retrieves and displays the latest patient information.
6. When an alert condition is recognised, the backend can trigger a Telegram notification to the configured caregiver.

## Project Structure

```text
ICURE_2_0/
│
├── main.py                 # FastAPI backend
├── dashboard.html          # Patient monitoring dashboard
├── telegram_alerts.py      # Telegram notification logic
├── main_backup.py          # Backend backup
├── .env                    # Private configuration
├── .gitignore              # Git ignored files
├── requirements.txt         # Python dependencies
├── venv/                   # Python virtual environment
│
└── README.md               # Project documentation
```

*The project structure may vary depending on the files included in your local repository.*

## Installation and Setup

### 1. Clone the repository

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
cd ICURE_2_0
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

### 3. Activate the virtual environment

**Windows PowerShell:**

```powershell
.\venv\Scripts\Activate.ps1
```

### 4. Install dependencies

```bash
pip install -r requirements.txt
```

### 5. Configure environment variables

Create a `.env` file in the project directory and add your own Telegram configuration:

```env
TELEGRAM_BOT_TOKEN=your_bot_token
TELEGRAM_CHAT_ID=your_chat_id
```

Never upload your actual bot token or private credentials to GitHub.

### 6. Configure ESP32

- Connect the sensors to the ESP32 using the configured I2C pins.
- Configure the Wi-Fi SSID and password in the ESP32 firmware.
- Set the backend URL to your computer's local IPv4 address.

Example:

```cpp
const char* SERVER_URL = "http://YOUR_COMPUTER_IP:8000/api/readings";
```

Ensure that the ESP32 and computer are connected to the same Wi-Fi network.

### 7. Start the backend

```bash
python -m uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

### 8. Open the dashboard

Visit:

```text
http://127.0.0.1:8000/dashboard
```

The dashboard should display readings received from the ESP32.

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | Backend root endpoint, if configured |
| GET | `/health` | Backend health check |
| GET | `/dashboard` | Monitoring dashboard |
| POST | `/api/readings` | Receive ESP32 sensor readings |
| GET | `/api/latest` | Retrieve the latest reading |
| GET | `/api/history` | Retrieve stored readings |

## Alert System

The prototype evaluates movement-related conditions using its configured detection logic.

When a possible seizure-like activity condition is detected:

1. The detection status is updated.
2. The local buzzer can activate.
3. The ESP32 sends the alert status to the backend.
4. The backend processes the alert.
5. A Telegram notification can be sent to the configured caregiver.

## Future Improvements

- AI-based seizure detection using machine learning.
- Secure doctor and caregiver login dashboards.
- GPS-based emergency location sharing.
- Patient history and analytics.
- Cloud-based remote monitoring.
- Mobile application integration.
- Improved alert reliability and emergency response workflows.

## Safety Disclaimer

I-CURE 2.0 is an educational and hackathon prototype. It is not a certified medical device and has not been clinically validated. Its movement-based detection should not be considered a medical diagnosis or a replacement for professional medical care. Sensor readings and alerts may be inaccurate, and the system should not be relied upon as the sole method of seizure detection or emergency response.

## Project Goal

To demonstrate how embedded systems, IoT connectivity, real-time monitoring, and automated notifications can be combined to develop an accessible patient-monitoring prototype that supports caregiver awareness.

---

**Developed as an IoT healthcare innovation project – I-CURE 2.0.**
