# PipeLog Pro

**Speech-to-text supply list tracker for plumbers and pipefitters.**

Built for the trade. Captures spoken material lists, parses measurements
(½", 3/4", 1' 6"), auto-categorizes by trade (pipe / fittings / valves /
hangers / etc.), and tags recognized brands (Victaulic, Viega, SharkBite,
Watts, Nibco, Grundfos, Milwaukee, Ridgid…). Exports to PDF or iMessage.

## Features

- 🎙️ **Continuous voice recording** — runs until you stop it, auto-restarts on dropout
- 📏 **Smart measurement parsing** — converts spoken dimensions ("three quarter inch", "two and a half feet") into proper notation with configurable precision and format
- 🏷️ **Auto-categorization** — sorts items into 13 trade categories as you speak
- 🏭 **Brand recognition** — 19 manufacturers automatically tagged with color-coded pills
- ✏️ **Inline editing** — tap any item to edit; re-categorization runs automatically
- 🔍 **Search & filter** — instant search, plus filters for Open / Filled / Measured items
- 📂 **Collapsible category groups** — manage 100–200+ item lists without losing your place
- 💾 **Local persistence** — list survives browser refresh; nothing sent to a server
- 📱 **PWA-ready** — install to home screen, works offline
- 📄 **PDF export** — print-ready supply order with job/PO info
- 💬 **iMessage / SMS export** — one tap to share

## Project structure

```
pipelog-deploy/
├── index.html       The entire app (single file — HTML + CSS + JS)
├── manifest.json    PWA install manifest
├── sw.js            Service worker (offline support)
├── vercel.json      Vercel routing & headers (mic permission, caching)
├── .gitignore
└── README.md
```

## Deploy in 5 minutes (GitHub → Vercel)

### 1. Create a GitHub repository

```bash
cd pipelog-deploy
git init
git add .
git commit -m "Initial commit"
git branch -M main
```

Now create a new empty repo on GitHub (call it `pipelog-pro`). Then:

```bash
git remote add origin https://github.com/YOUR_USERNAME/pipelog-pro.git
git push -u origin main
```

### 2. Deploy on Vercel

1. Go to **[vercel.com/new](https://vercel.com/new)** and sign in with GitHub
2. Click **Import** next to your `pipelog-pro` repository
3. Leave all settings at defaults — Vercel auto-detects this is a static site
4. Click **Deploy**

You'll get a live URL like `pipelog-pro.vercel.app` in about 30 seconds.

### 3. (Recommended) Use a custom domain

In your Vercel project → Settings → Domains → add your domain.
Microphone access requires HTTPS, which Vercel provides automatically.

### 4. Install to phone home screen

Open the deployed URL on iPhone / Android, then:

- **iPhone (Safari):** Share button → "Add to Home Screen"
- **Android (Chrome):** Menu → "Install app"

Now it launches like a native app, with the mic button right there.

## Browser requirements

Speech recognition needs:

- **Chrome / Edge** (desktop or Android) — full support, best accuracy
- **Safari** (iOS 14.5+ or macOS) — supported
- **Firefox** — ❌ no speech recognition (use Chrome / Edge instead)

The mic must have **HTTPS** to work, which Vercel handles automatically.

## Permissions

- **Microphone** — required for voice recording. Browser asks once on first record.
- **localStorage** — used to save your list across reloads. ~5MB available; can hold thousands of items.

No data ever leaves your device. Everything runs locally in the browser.

## Adding icons (optional, for PWA install)

To customize the home-screen icon, drop two PNG files into the root:

- `icon-192.png` (192×192 px)
- `icon-512.png` (512×512 px)

Then redeploy. The site works fine without them; the favicon is built in as inline SVG.

## Updates

To push an update after the initial deploy:

```bash
git add .
git commit -m "Your change description"
git push
```

Vercel auto-deploys every push to `main` in about 30 seconds.

## Keyboard shortcuts

- **Spacebar** — toggle recording (when not typing in an input)
- **Enter** in the manual-add field — add the typed item
- **Enter** while editing an item — commit edit

## Tips for accurate dictation

1. Speak in short, clear bursts — pause briefly between items so the engine knows where one item ends
2. Say "and" for compound measurements: *"two and a half inch elbow"*
3. Brand names should be spoken clearly: *"Viega ProPress half inch coupling"*
4. If the engine mis-hears a word, just tap the item and type the correction — re-categorization happens automatically
5. For very loud sites, raise the **Confidence Filter** in Settings to reject low-confidence guesses

## Troubleshooting

**"Microphone access denied"** — Check browser permissions for your site URL. On iOS you may need Settings → Safari → Microphone.

**Recording stops on its own** — This is usually iOS Safari going to background or the screen locking. The app auto-restarts when it can. For long sessions, keep the screen on (in iOS Settings → Display → Auto-Lock → Never).

**PDF export does nothing** — Wait a moment for the html2pdf library to finish loading (first visit only).

**List didn't survive refresh** — Check Settings → "Auto-save to Browser" is on. If you're in Private Browsing, localStorage is disabled.

## License

Private project — feel free to fork for personal use.
