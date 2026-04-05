# ReFrame Display

Under Development!

A configurable smart display system for home/office use, integrating Google Photos and Calendar (extensible to Spotify/Apple) with dual HDMI/web app modes. Built with FastAPI, React, and SQLite for self-hosted operation.

## Overview

ReFrame Display repurposes old tablets/iPads into smart displays, promoting sustainability by reusing e-waste. It supports two modes:
- **HDMI Kiosk Mode**: Direct connection to a tablet for passive, full-screen display.
- **Web App Mode**: Remote access via any device/browser for flexible, touch-interactive viewing.

Key features:
- Google Calendar integration for event displays.
- Google Photos slideshows.
- Configurable refresh intervals and modes.
- Self-hosted with OAuth for privacy.
- Open-source and extensible.

## Architecture

- **Backend**: FastAPI (Python) for API integrations and data serving.
- **Frontend**: React for display interfaces.
- **Database**: SQLite for local data persistence.
- **Deployment**: Docker for containerization.
- **Hardware**: Raspberry Pi 5 + HDMI-connected tablet.

## Getting Started

See [Setup Prerequisites](docs/setup.md) for detailed setup instructions, including Google Cloud configuration.

## Project Status

Under active development. Currently planning architecture and initial implementation.

## Contributing

Contributions welcome! See [Setup Prerequisites](docs/setup.md) for development setup.

## License

MIT License - see [LICENSE](LICENSE) for details.
