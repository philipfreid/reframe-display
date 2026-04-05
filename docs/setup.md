# ReFrame Display Setup Prerequisites

This guide outlines the essential setup steps for developers and users to get ReFrame Display running. These steps ensure secure access to Google Calendar and Photos APIs via OAuth 2.0. The process is designed for self-hosted, personal use but can scale for open-source sharing.

## For All Users (Developers and End-Users)

### 1. Hardware and Software Basics
- **Raspberry Pi Setup**: Use Raspberry Pi 5 with Raspberry Pi OS (Bookworm or later). Ensure Docker is installed (`sudo apt update && sudo apt install docker.io`).
- **Tablet/Device**: An old iPad, Android tablet, or similar with HDMI output and web browser support. For HDMI mode, ensure full-screen compatibility (test with adapters).
- **Network**: Local WiFi access for the Pi and tablet. Static IP recommended for consistent web app access.
- **Python Environment**: Install Python 3.9+ on the Pi. Use virtualenv for isolation: `python3 -m venv reframe-env && source reframe-env/bin/activate`.

### 2. Google Cloud Project and API Access
ReFrame Display requires a Google Cloud project to access Calendar and Photos APIs. This is free for basic use (up to quotas).

- **Create a Google Cloud Project**:
  - Go to [Google Cloud Console](https://console.cloud.google.com/).
  - Create a new project (e.g., "ReFrame-Display").
  - Note the Project ID (e.g., `reframe-display-12345`).

- **Enable Required APIs**:
  - In the Cloud Console, go to "APIs & Services" > "Library".
  - Search for and enable:
    - Google Calendar API.
    - Google Photos Library API (for app-managed photos; use Picker API for user selections).
  - Optionally, Google Photos Picker API if implementing user photo selection.

- **Create OAuth 2.0 Credentials**:
  - Go to "APIs & Services" > "Credentials".
  - Click "Create Credentials" > "OAuth 2.0 Client IDs".
  - Choose "Web application" as application type.
  - Set authorized redirect URIs to `http://localhost:8000/oauth2callback` (for local testing) and your Pi's IP (e.g., `http://192.168.1.100:8000/oauth2callback`).
  - Download the JSON credentials file (contains Client ID, Client Secret). Store securely on the Pi (e.g., in `~/.config/reframe/credentials.json`).

- **Configure OAuth Consent Screen**:
  - In "APIs & Services" > "OAuth consent screen", set up for "External" user type.
  - App name: "ReFrame Display".
  - User support email: Your email.
  - Scopes: Add `https://www.googleapis.com/auth/calendar.readonly` and `https://www.googleapis.com/auth/photoslibrary.readonly`.
  - Submit for verification if publishing (not needed for personal use).

### 3. Install Dependencies
- **Python Libraries**: Run `pip install fastapi uvicorn google-api-python-client google-auth-oauthlib google-auth-httplib2 sqlalchemy` (for backend).
- **Frontend**: Node.js for React (if building locally): `sudo apt install nodejs npm`.
- **Docker**: Pull base images if using containers: `docker pull python:3.9-slim` and `docker pull node:18-alpine`.

### 4. Clone and Configure the Project
- **Clone Repository**: `git clone https://github.com/philipfreid/reframe-display.git`.
- **Environment Variables**: Create a `.env` file with:
  ```
  GOOGLE_CLIENT_ID=your_client_id
  GOOGLE_CLIENT_SECRET=your_client_secret
  DATABASE_URL=sqlite:///./reframe.db
  REDIRECT_URI=http://your_pi_ip:8000/oauth2callback
  ```
- **Database**: SQLite will auto-create on first run.

### 5. Run Initial Setup
- **Backend**: `uvicorn main:app --host 0.0.0.0 --port 8000` (FastAPI server).
- **OAuth Flow**: Visit `http://your_pi_ip:8000/auth` in a browser to authorize Google access. Tokens will be stored securely.
- **Frontend**: Build React app (`npm run build`) and serve via FastAPI or Nginx.

### 6. Test and Configure Modes
- **HDMI Mode**: Connect tablet via HDMI, run kiosk script (e.g., Chromium in full-screen).
- **Web App Mode**: Access via browser on any device.
- **Settings**: Use JSON config for modes, refresh intervals, etc.

## Additional Notes for Open-Source Users
- **Quotas and Limits**: Monitor Google API usage (free up to 10k/day for Calendar, 25k for Photos). Upgrade via Google Cloud billing if needed.
- **Security**: Never share credentials. Use HTTPS locally if exposing externally.
- **Troubleshooting**: Check logs for OAuth errors. Ensure firewall allows port 8000.
- **Contributing**: If sharing, include this guide in `docs/setup.md`.