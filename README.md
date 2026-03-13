# Uptime Kuma API v2 - CoPaw Skill

[![OpenClaw Skill](https://img.shields.io/badge/OpenClaw-Skill-blue)](https://github.com/openclaw/openclaw)
[![Python](https://img.shields.io/badge/Python-3.8%2B-green)](https://www.python.org/)

OpenClaw/CoPaw skill for Uptime Kuma API v2 - Manage your monitors without Socket.IO client.

## Features

- ✅ **Complete Monitor Management**: Create, edit, delete, pause, resume
- ✅ **Tag Support**: Add, delete, replace monitor tags with custom colors
- ✅ **Bearer Token Authentication**
- ✅ **2FA/TOTP Support**
- ✅ **Auto-reconnection**: Persistent connection with automatic reconnect
- ✅ **Zero Extra Dependencies**: Basic usage requires no additional packages

## Installation

```bash
pip install "python-socketio[client]" websocket-client pyotp
```

## Quick Start

1. Copy `.env.example` to `.env` and configure:

```env
BRIDGE_HOST=127.0.0.1
BRIDGE_PORT=9911
BRIDGE_TOKEN=your-secret-token

KUMA_URL=http://your-kuma-server:3001
KUMA_USERNAME=admin
KUMA_PASSWORD=your-kuma-password

# Only needed if 2FA is enabled
KUMA_2FA_SECRET=

# Socket.IO call timeout (default 60 seconds)
KUMA_TIMEOUT=60
```

2. Start the service:

```bash
python uptime_kuma.py
```

## API Endpoints

All endpoints accept and return `application/json`.

Success: `{"ok": true}`
Failure: `{"ok": false, "error": "..."}`

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/health` | GET | Health check |
| `/monitors/list` | POST | List all monitors |
| `/monitors/find` | POST | Find monitor by URL |
| `/monitors/add` | POST | Add new monitor |
| `/monitors/edit` | POST | Edit monitor |
| `/monitors/delete` | POST | Delete monitor |
| `/monitors/pause` | POST | Pause monitor |
| `/monitors/resume` | POST | Resume monitor |
| `/monitors/status` | POST | Get monitor status/hearbeats |
| `/tags/list` | POST | List all tags |
| `/monitors/tags/set` | POST | Add tag to monitor |
| `/monitors/tags/delete` | POST | Remove tag from monitor |
| `/monitors/sniff` | POST | Debug: capture raw payload |

## Usage Examples

### List all monitors

```bash
curl -X POST http://localhost:9911/monitors/list \
  -H "Authorization: Bearer your-secret-token" \
  -H "Content-Type: application/json"
```

### Add a new monitor

```bash
curl -X POST http://localhost:9911/monitors/add \
  -H "Authorization: Bearer your-secret-token" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "My Website",
    "type": "http",
    "url": "https://example.com"
  }'
```

### Pause a monitor

```bash
curl -X POST http://localhost:9911/monitors/pause \
  -H "Authorization: Bearer your-secret-token" \
  -H "Content-Type: application/json" \
  -d '{"id": 1}'
```

## Using as a CoPaw Skill

This skill wraps the uptime-kuma-api-v2 bridge service, allowing direct management of Uptime Kuma through CoPaw.

## Credits

Based on [uptime-kuma-api-v2](https://github.com/pr1ncey1987/uptime-kuma-api-v2) by pr1ncey1987.

## License

MIT License