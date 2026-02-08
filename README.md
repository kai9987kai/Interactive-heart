# Interactive-heart

A lightweight **browser-based interactive heart project** built as a minimal static site.  
This repo ships as a simple HTML app and uses the **Gemini API** for AI-powered explanations/interaction.

> ⚠️ You must provide **your own Gemini API key** before the AI features will work.

---

## Repo contents

- `index.html` — the full web app (UI + logic)
- `README.md` — setup notes

This project is intentionally minimal (no build tools, no framework, no bundler).

---

## Quick start

### Option A — Open directly
1. Download/clone the repo
2. Open `index.html` in a modern browser

### Option B — Run with a local server (recommended)
Some browsers apply stricter rules under `file://`. Use a tiny local server:

**Python**
```bash
python -m http.server 8080
