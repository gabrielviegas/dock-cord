**Docker Container Monitoring with Discord Webhooks**

DockCord is a lightweight Python tool that monitors your Docker environment in real-time. It detects container events and instantly sends a notification to your Discord server whenever a container stops or crashes.

Perfect for Homelabs, local dev environments, and simple DevOps monitoring.

## Features

* **Real-time Detection:** Listens specifically for the `die` event (container stopped/killed).
* **Instant Alerts:** Sends a formatted message to Discord with the Container Name, ID, and Timestamp.
* **Lightweight:** Built with the Docker SDK for Python.

## Prerequisites

* **Linux/Ubuntu** (or any system with Docker installed)
* **Python 3.6+**
* **Docker** running with remote API enabled (TCP)

## Installation

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/gabrielviegas/dock-cord.git](https://github.com/gabrielviegas/dock-cord.git)
    cd dock-cord
    ```

2.  **Set up a Virtual Environment (Recommended):**
    ```bash
    python3 -m venv .venv
    source .venv/bin/activate
    ```

3.  **Install Dependencies:**
    ```bash
    pip install docker requests
    ```

## 🔧 Configuration

### 1. Configure Docker Daemon
Since the script uses `tcp://127.0.0.1:2375` to connect, you must enable the TCP socket in Docker.

Edit your daemon config:
```bash
sudo nano /etc/docker/daemon.json
```
Add or modify the hosts line:
```bash
sudo systemctl restart docker
```

### 2. Configure the Script
Open events.py and replace the webhook_url variable with your actual Discord Webhook URL:
```bash
webhook_url = "YOUR_DISCORD_WEBHOOK_URL_HERE"
```

## Usage
Run the script inside your virtual environment:
```bash
python3 events.py
```

## Troubleshooting
Permission Denied?
If you get permission errors regarding the Docker socket, ensure your user is in the docker group:
```bash
sudo usermod -aG docker $USER
newgrp docker
```

## Connection refused?
Verify that Docker is listening on port 2375:
```bash
sudo netstat -tulpn | grep dockerd
```

## License
This project is licensed under the MIT License.
