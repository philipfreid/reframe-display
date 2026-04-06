# ReFrame Display - AI Context & Project Log

## Project Identity
- **Name**: ReFrame Display
- **Vision**: A configurable smart display system for home/office use, integrating Google Photos and Calendar (extensible to Spotify/Apple), self-hosted, low-cost/low-power, touch-interactive with passive mode, documented for open-source sharing, and serving as an AI-assisted product engineering learning project.
- **Sustainability Focus**: Reuse old devices like iPads/tablets to reduce e-waste.
- **GitHub**: https://github.com/philipfreid/reframe-display.git
- **Developer**: Phil Reid

## Core Requirements
1. Integrate Google Photos and Calendar APIs for display
2. Self-hosted solution with local OAuth
3. Dual-mode operation: HDMI kiosk (passive) and web app (interactive)
4. Touch-interactive capability (web app mode)
5. Configurable settings (modes, refresh intervals, etc.)
6. Low-cost, low-power design
7. Open-source documentation for sharing
8. Learning project with AI assistance for product engineering

## Technical Stack

### Hardware
- **Primary**: Raspberry Pi 5 (backend processing)
- **Display**: HDMI-connected tablet (Android/iPad) for kiosk mode, or any device via web app
- **Network**: Local WiFi for web app access
- **Display Adapters**: USB-C to HDMI adapters (tablets don't have native HDMI ports)

### Software Architecture
- **Backend**: Python FastAPI + SQLite for data persistence and OAuth
- **Frontend**: React app (works in Chromium kiosk or web browser)
- **Deployment**: Docker containerization
- **Data Sources**: Google Photos/Calendar APIs (OAuth 2.0)
- **Configuration**: JSON settings for mode switching, refresh intervals, interactive/passive modes

### Dual-Mode Design

#### HDMI Kiosk Mode
- Direct HDMI connection from Pi to tablet display
- Video-only protocol (no native touch support)
- Passive slideshow/calendar display
- Full-screen HDMI display with resolution matching via `underscan` config
- Note: Touch requires external USB/serial input (not primary use case)

#### Web App Mode
- Remote access via browser on any device
- Full touch support via HTTP/WebSocket
- Device-agnostic (tablets, phones, laptops)
- Full-screen capability via JavaScript `requestFullscreen()` API
- Recommended for interactive use

## Key Insights & Design Decisions

### Why Dual Modes?
User preference for flexibility—HDMI mode for passive kitchen/hallway display, web app for interactive office access.

### Why Web App for Touch?
HDMI is video-only; web app provides superior touch support and device flexibility.

### OAuth Strategy
Google Photos Picker API lets users select media from their library (privacy-respecting). Calendar API uses read-only scopes.

### API Quotas
- Calendar: 10k read queries/day (free tier)
- Photos: 25k requests/day (free tier)
- Sufficient for personal niche use

### Device Reuse
Old tablets become smart displays. Reduces e-waste.

## Current Status

### Completed
- Hardware/tech stack finalized
- Dual-mode architecture validated
- Project name: ReFrame Display
- GitHub repo created
- Setup prerequisites documented
- Project structure initialized

### Pending
1. Backend implementation (FastAPI OAuth)
2. Frontend implementation (React components)
3. Docker deployment scripts
4. Testing and debugging

### Next Immediate
Create backend scaffold with config loader and health endpoint.

## Architecture Overview

```
Google APIs → Raspberry Pi 5 → HDMI Tablet | Web Browser
              (FastAPI + SQLite)
              ├─ OAuth Handler
              ├─ Google API Client
              ├─ Data Caching
              └─ REST Endpoints
```

Canonical diagram and lifecycle flow are maintained in `docs/architecture.md`.

## Configuration Structure (Future JSON)

```json
{
  "display_mode": "web_app" | "hdmi_kiosk",
  "refresh_interval_seconds": 900, // 15 min default, easily changed
  "calendar": { "enabled": true },
  "photos": { "enabled": true },
  "web_app": { "port": 8000, "fullscreen": true },
  "hdmi_kiosk": { "resolution": "1920x1080" }
}
```

## Important Notes for Future Sessions

### To Resume
1. Load reframe-display in VS Code
2. Read this file for full context
3. Check chat_log.json for conversation details
4. Continue with next pending task

### Key Files
- **Repo**: `/Users/phil/dev-projects/reframe-display`
- **Setup Docs**: `docs/setup.md`
- **Backend**: `backend/` (awaiting code)
- **Frontend**: `frontend/` (awaiting code)
- **Config**: `config/` (awaiting JSON structure)
- **Deploy**: `deploy/` (awaiting Docker scripts)

### Chat Context Saved
Full conversation log persisted in chat_log.json with all decisions, alternatives considered, and design rationale.