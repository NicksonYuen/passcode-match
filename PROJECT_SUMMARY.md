# Passcode Match — project summary

Handover notes for continuing this project in a Claude Project. Upload this file and `index.html` as project files.

## What it is

An iPad game for my son YYY (8), and since v3 also my daughter YHT. A passcode appears at the top and he copies it on a keypad underneath. The goal is visual matching only, not memory. It runs as a web app hosted on GitHub Pages and installed to the iPad Home Screen.

## Requirements (agreed)

| Topic | Decision |
|---|---|
| Platform | Web app, iPad, portrait orientation |
| Skill trained | Matching only; the code stays on screen the whole time |
| Difficulty | 2–10 digits, set by the parent on the front page before play. Start at 2. No automatic level-up. |
| Next digit | Highlighted in yellow in both the code and the answer slot |
| Correct digit | Chime; the slot turns green |
| Wrong digit | Soft tone, says 「哎呀，請再試一次」, and the **whole code resets** (same code, start from the first digit) |
| Code completed | Fireworks, a 做得好！ banner and a background glow, plus 「你做得好好呀！你係個乖仔！」. A new code then starts automatically. |
| Session length | Continuous, no end screen |
| Timer | None. After 10 seconds without input, it reads the whole code in Cantonese, then says 「請再試一次」 |
| Read aloud | 聽密碼 button reads the full code; tapping one code digit reads that digit |
| Language | All speech in Cantonese (iPad voice: Chinese (Hong Kong), "Sinji") |
| Visual style | Simple, high contrast, no themed characters (no trains or dinosaurs) |
| Exit | Hold 按住返回 for 1.5 seconds, so a stray tap doesn't leave the game |
| Players (v3) | Entry page with two buttons: **YYY** (sees the code, original game) and **YHT** (hears the code). Each has their own digit setting and records. |
| YHT mode (v3) | Code boxes are hidden behind speaker icons; tapping a box reads that digit, 聽密碼 reads the whole code, and the full code is read out at the start of every round. A digit is revealed once she types it correctly. Win line: 「你做得好好呀！你真係個超級乖女！」 |
| Records | Simple local log per session: date, start time, digits, codes completed, wrong presses, time played. Stored on the iPad only. |

## Design (current version)

- **Entry page (v3):** title 密碼配對 and two big buttons, YYY (blue, 睇住密碼) and YHT (pink, 聽住密碼).
- **Player page:** ← 返回 to the entry page, the player's name tag, title 密碼配對, a grid of digit buttons (2–10), a 開始 button, plus 試聲 (sound test), 紀錄 (records) and a Cantonese voice status line.
- **Play screen, top to bottom:**
  1. Back button (hold) and 聽密碼 button.
  2. **Question card:** white card labelled 密碼 holding the code digits.
  3. A bold down arrow.
  4. **Calculator:** dark navy body, green LCD screen showing the answer slots, then white keys in phone layout (1-2-3 / 4-5-6 / 7-8-9 / 0).
- The card and the calculator are the same width, so each answer slot sits directly under its code digit.
- The calculator styling was added because, in v1, the code, the slots and the keypad all looked alike, and he couldn't tell where to type.
- Font: Atkinson Hyperlegible, chosen for clear digits.

## Technical notes

- Single file `index.html`: plain HTML, CSS and JavaScript, no build step.
- Speech uses the browser's built-in Web Speech API (`lang zh-HK`). Sounds are generated with Web Audio, so there are no audio files.
- Records are stored in `localStorage` under the key `pm_records`. Each record carries `player` (older records without it count as YYY). Last chosen level: `pm_level` (YYY) and `pm_level_yht` (YHT).
- Settings to edit, near the top of the script in `index.html`:
  - Spoken lines: `SAY_WRONG`, `SAY_WIN` (YYY), `SAY_WIN_YHT` (YHT), `SAY_RETRY`.
  - Player settings: the `PLAYERS` list just below them.
  - Idle delay: `IDLE_MS` (10000 = 10 seconds).
- The screen is kept awake during play where the iPad allows it.
- `manifest.webmanifest` and `icons/` let it install as a full-screen app. `sw.js` caches it so it works offline; bump the `CACHE` name (now `passcode-match-v3`) on each release.

## Files

| File | Purpose |
|---|---|
| `index.html` | The game |
| `manifest.webmanifest` | Home Screen app settings |
| `sw.js` | Offline cache |
| `icons/` | App icons (calculator design) |
| `.nojekyll` | GitHub Pages: serve files as-is |
| `README.md` | Deploy and iPad setup steps |
| `PROJECT_SUMMARY.md` | This file |

## Deployment

- Hosted on GitHub Pages from a **public** repo (e.g. `passcode-match`), branch `main`, folder `/ (root)`.
- Address: `https://<username>.github.io/passcode-match/`.
- Upload the files *inside* the folder, not the folder itself, or the site shows a 404.
- To update, edit or replace `index.html` on GitHub and commit. The iPad picks up the change on its next launch with internet.
- GitHub Pages free limits: 1 GB per site, 100 GB bandwidth a month, about 10 builds an hour, 25 MB per file uploaded through the browser. This project is about 80 KB.

## iPad setup checklist

- Open the site in Safari, then Share › Add to Home Screen.
- Tap 試聲. If the voice isn't Cantonese, go to Settings › Accessibility › Spoken Content › Voices › Chinese (Hong Kong) › Sinji.
- Turn the volume up, check the iPad isn't on silent, and turn on rotation lock in portrait.
- Guided Access: Settings › Accessibility › Guided Access, set a passcode, then triple-click the top or Home button inside the game.

## Version history

- **v1:** First build (landscape-friendly layout, plain keypad).
- **v2:** Portrait layout; dark calculator keypad with green LCD answer slots; code moved into its own white card; GitHub Pages package with app icon, manifest and offline cache.
- **v3 (current):** Entry page with YYY and YHT; YHT hidden-code listening mode with her own praise line; per-player digit setting and records.
