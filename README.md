
# SC HUB 2.1

### Community Campus Automation — Python Edition

A Windows CMD automation tool inspired by SC Hub Edge.

## Features
- Chromium browser integration
- Video playback monitoring
- Automatic video playback attempts
- Video completion detection
- Automatic Next / Continue navigation
- Auto-Continue toggle
- Optional Early Next
- Configurable navigation delay
- Activity logging
- Persistent browser profile

## Installation

### 1. Install Python
Install Python 3.11 or newer.

### 2. Download the repository
```bash
git clone YOUR_REPOSITORY_URL
cd SC-HUB-2.1
```

### 3. Install dependencies
```bash
py -m pip install -r requirements.txt
```

### 4. Install Chromium
```bash
py -m playwright install chromium
```

### 5. Launch SC HUB
```bash
py sc_hub.py
```

## Commands

| Command | Description |
|---|---|
| `py sc_hub.py` | Launch SC HUB |
| `py -m pip install -r requirements.txt` | Install dependencies |
| `py -m playwright install chromium` | Install browser |
| `py -m pip install --upgrade playwright` | Update Playwright |

## Usage

1. Launch SC HUB.
2. Connect to Community Campus.
3. Sign in normally.
4. Open your course.
5. Start video monitoring.
6. Configure Auto-Continue.

## Project Structure

```text
SC-HUB/
├── sc_hub.py
├── config.json
├── requirements.txt
├── README.md
├── modules/
│   ├── browser.py
│   ├── settings.py
│   └── terminal.py
├── logs/
└── browser_profile/
```

## Disclaimer

SC HUB is an independent community project.
Use only with authorised accounts and follow your institution's rules.
