# SC HUB - Community Campus CMD Automation

A command-line tool for Windows Command Prompt. It opens a Chromium window where **you log in
yourself**, then watches the lesson video and (optionally) clicks **Next / Continue / Finish Topic**
once the video has genuinely finished. No GUI, no extension, no password handling.

## Installation (Windows CMD)

1. **Install Python 3.11 or newer** from https://www.python.org/downloads/
   (tick *Add python.exe to PATH* in the installer). Check with `python --version`.
2. **Open CMD in the project folder**: open the `SC-HUB` folder in File Explorer, click the address
   bar, type `cmd` and press Enter.
3. **Install dependencies**:
   ```
   pip install -r requirements.txt
   ```
4. **Install the Playwright Chromium browser**:
   ```
   python -m playwright install chromium
   ```
5. **Run it**:
   ```
   python sc_hub.py
   ```

## Using it

1. `[1] Connect to Community Campus` - opens the browser. Log in manually if asked. The session is
   saved in `browser_profile/`, so you normally log in only once.
2. Open the lesson you want to watch.
3. `[2] Start Video Monitoring` - live view, refreshed every second. Press any key to go back to the
   menu; monitoring keeps running in the background.
4. `[3] Enable Auto-Continue` - after a video finishes, waits the configured delay, clicks
   Next/Continue/Finish Topic, and confirms the next page loaded.

| Option | What it does |
|---|---|
| 1 Connect | Starts the browser (persistent profile) and opens Community Campus |
| 2 Start Video Monitoring | Starts background monitoring and shows the live view |
| 3 / 4 Auto-Continue | Turns automatic continuing on / off |
| 5 Manual Continue | Clicks Next/Continue now - refused while a video is unfinished |
| 6 View Current Video Information | One-off snapshot: title, time, %, status, nav button |
| 7 Configuration | Edit settings (saved to `config.json`) |
| 8 View Activity Logs | Last 40 lines of `logs/sc_hub.log` |
| 9 Stop Automation | Stops monitoring and turns Auto-Continue off (browser stays open) |
| 0 Exit | Stops everything and closes the browser |

## Safety rules built in

- Navigation is only clicked after the video has **ended or reached its end on two consecutive
  checks**, plus the navigation delay.
- Each video is clicked **at most once** automatically, with a minimum gap of 4 seconds between any
  two clicks (manual clicks included).
- After a click, SC HUB waits up to 15 s for the page to actually change. If it did not, it warns
  you instead of clicking again.
- Paused videos are started automatically (muted if the browser blocks sound), at most 3 tries per
  video. Turn this off in Configuration if you prefer to press play yourself.
- If it needs you (login required, no Next button after a finished video, click had no effect) it
  logs a warning and sounds an alarm.

## Configuration (`config.json`)

| Setting | Meaning |
|---|---|
| `campus_url` | Start page (edit in the file) |
| `auto_continue_default` | Auto-Continue state at startup |
| `navigation_delay` | Seconds to wait after a video finishes (0-60) |
| `refresh_interval` | Monitoring refresh in seconds (0.25-10) |
| `browser` | `chromium`, `chrome` or `msedge` (the last two must be installed) |
| `auto_play` | Start paused videos automatically |
| `alarm_on_attention` | Beep when SC HUB needs you |
| `custom_next_selector` | Optional CSS selector for the site's Next button, if the default text match misses it |
| `logging_enabled`, `log_level` | Log file on/off and verbosity |

## Project structure

```
SC-HUB/
  sc_hub.py          main app, menu, monitoring loop
  config.json        settings
  requirements.txt
  README.md
  logs/              sc_hub.log (rotating)
  modules/
    browser.py       Playwright persistent browser, page discovery, crash recovery
    monitor.py       video detection (page + embedded frames), shared state
    navigation.py    finding and safely clicking Next / Continue / Finish Topic
    settings.py      defaults, validation, config.json
    terminal.py      banner, menus, live view, input, alarm
```

## Troubleshooting

- **"Chromium is not installed"** - run `python -m playwright install chromium`.
- **Browser exits immediately** - another SC HUB or browser is using `browser_profile/`; close it.
- **"No video detected"** - the video may sit in a frame the site blocks, or the page has no video.
  Use `[5] Manual Continue` on non-video pages.
- **Next button not found** - inspect the button in the browser (F12), then set
  `custom_next_selector` in Configuration, e.g. `button.next-lesson`.
- **Characters look broken** - use Windows Terminal or CMD on Windows 10 or newer.
