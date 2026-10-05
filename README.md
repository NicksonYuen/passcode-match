# 密碼配對 Passcode Match

A passcode matching game for iPad (portrait). The code shows at the top; the child copies it on the calculator keypad below. Cantonese voice feedback, 2–10 digit levels, fireworks on success, and a simple play record.

## Files

| File | What it does |
|---|---|
| `index.html` | The whole game |
| `manifest.webmanifest` | Lets the iPad install it as a full-screen app |
| `sw.js` | Offline cache, so the game opens without internet |
| `icons/` | Home Screen icons |
| `.nojekyll` | Tells GitHub Pages to serve the files as-is |

## Deploy on GitHub Pages

1. On github.com, click **New repository**. Name it `passcode-match`, set it to **Public**, and click **Create repository**.
2. Click **uploading an existing file**. Drag in everything from this folder, including the `icons` folder, then click **Commit changes**.
3. Go to **Settings › Pages**. Under *Build and deployment*, set Source to **Deploy from a branch**, Branch to **main** and folder to **/ (root)**. Click **Save**.
4. Wait 1–2 minutes. The address appears at the top of the Pages screen:
   `https://<your-username>.github.io/passcode-match/`

Note: `.nojekyll` starts with a dot, so your computer may hide it. The game works without it.

## Install on the iPad

1. Open the address in **Safari**.
2. Tap **Share › Add to Home Screen › Add**.
3. Open the game from the new icon. It runs full screen, with no Safari bar.

## Before the first game

- **Cantonese voice:** tap 試聲 on the front page. If the voice isn't Cantonese, go to Settings › Accessibility › Spoken Content › Voices › Chinese (Hong Kong) and download **Sinji**.
- **Sound:** turn the volume up and make sure the iPad isn't on silent.
- **Portrait lock:** turn on rotation lock in Control Centre.
- **Guided Access:** go to Settings › Accessibility › Guided Access and set a passcode. In the game, triple-click the top (or Home) button to lock the iPad into the game. Triple-click again to exit.

## Playing

- Choose 2–10 digits, then tap 開始 to start.
- Hold 按住返回 for 1.5 seconds to go back to the front page.
- Tap 紀錄 on the front page to see past sessions.

## Good to know

- Play records are stored on the iPad only, inside the Home Screen app. Deleting the app's icon deletes the records.
- To change the game, edit `index.html` on GitHub and commit. The iPad picks up the new version the next time the game opens with internet. If it doesn't, close the app fully and reopen it.
- Spoken lines are at the top of the script in `index.html` (`SAY_WRONG`, `SAY_WIN`, `SAY_RETRY`), and the idle delay is `IDLE_MS` (10000 = 10 seconds).
