Sizzles Hub
A Windows CMD Python command centre for Community Campus session monitoring, a separate work timer, and a local Ollama study assistant.
Included
Red/cyan glitch startup animation and refreshed CMD dashboard.
Playwright browser with two separate persistent browser profiles.
Manual login; browser sessions/cookies remain in each profile.
No Community Campus passwords are stored by Sizzles Hub.
Video status monitoring and completion detection.
Navigation checks for Next, Finish Topic, and Continue.
Auto-Continue enabled by default; Auto-Next and Early Next disabled by default.
Session-expiry detection pauses monitoring actions and plays a four-second alarm; log in manually to resume.
Local Qwen 2.5 7B through Ollama; manually entered questions and options.
Independent custom work timer with start, pause, resume, reset, countdown and completion alert.
Logs in `logs/sizzles_hub.log`.
Requirements
Windows 10/11 and Python 3.10+
Google Chrome/Chromium support via Playwright
Ollama installed locally for AI features
Install
Extract the ZIP.
Open Command Prompt in the extracted `sizzles_hub` folder.
Run:
```bat
   py -m pip install -r requirements.txt
   py -m playwright install chromium
   ```
For local AI, install/start Ollama and run:
```bat
   ollama pull qwen2.5:7b
   ```
Edit `config.json` or enter your Community Campus URL in Settings.
Start:
```bat
   py sizzles_hub.py
   ```
Accounts and privacy
Choose Account 1 or Account 2. Each uses a separate Playwright profile under `browser_profile/`. Sign in manually in the browser. The app does not ask for or save account passwords. Browser sessions are stored by Chromium in those profile folders.
Important behaviour
`Early Next` is OFF by default.
`Auto-Next` is OFF by default. When disabled, the monitor will not click a `Next` button.
Completion detection uses the HTML video element's ended/current-time state and a small set of visible completion phrases. Some learning platforms use custom video players or unusual page markup; those may need site-specific selectors.
Navigation clicks are attempted once per detected activity URL/video duration, then the page is checked for a load. This is a best-effort general integration, not a guarantee for every Community Campus layout.
The local AI answers questions you type in. It does not read hidden assessment data, fill forms, submit answers, or bypass platform controls. Use it to understand the material.
Session expiry pauses automatic navigation until manual login is restored.
Project layout
```text
sizzles_hub/
  sizzles_hub.py
  config.json
  requirements.txt
  README.md
  modules/
    app.py
    alarm.py
    ai.py
    auto_continue.py
    browser.py
    completion.py
    navigation.py
    settings.py
    startup.py
    terminal.py
    timer.py
  logs/
  browser_profile/
```
Troubleshooting
`Playwright is missing`: run `py -m pip install -r requirements.txt`.
Chromium missing: run `py -m playwright install chromium`.
Ollama connection error: start Ollama and confirm `http://localhost:11434` is available.
If the dashboard colours do not render, use Windows Terminal or enable ANSI/VT support in CMD.
