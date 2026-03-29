# Mood Music Player

AI mood detection + Spotify soundtracks in one page.

## How it works
- You describe how you feel (a short sentence is enough).
- The app sends your text to Anthropic and expects strict JSON back (mood, label, reflection, search query, intensity).
- Based on the detected mood, the app queries Spotify and shows preview tracks.

## Setup (local development)

### 1) Install dependencies

```bash
npm install
```

### 2) Configure Anthropic

Create `.env.local` in the project root:

```env
REACT_APP_ANTHROPIC_API_KEY=sk-ant-...
```

Notes:
- Do not commit secrets. This project uses `.env.local` (and it is typically gitignored).
- After editing `.env.local`, restart the dev server so CRA can load the new env vars.

### 3) Run the app

```bash
npm start
```

Open:
- `https://localhost:3001`

## HTTPS / “Not secure” warning

This repo is configured to run the dev server over HTTPS. If your browser still warns:

```bash
mkcert -install
mkcert -cert-file certs/localhost.crt -key-file certs/localhost.key localhost 127.0.0.1 ::1
```

Then restart `npm start`.

## Spotify token (paste in the UI)

When you open the app, paste your Spotify access token on the setup screen.

If you see errors like “Spotify token expired”, paste a fresh token.

## Common errors

- `invalid x-api-key`
  - Your Anthropic API key is incorrect. Anthropic keys should start with `sk-ant-`.

- “Set REACT_APP_ANTHROPIC_API_KEY…”
  - `.env.local` is missing or the dev server was not restarted after updating it.

- “Could not analyze mood…”
  - The Anthropic response was not valid JSON or the request failed. Check the Anthropic key first.

## Security note

This demo calls Anthropic directly from the browser, which exposes your key to anyone who can access the frontend bundle. For a public deployment, move the Anthropic call to a backend and keep secrets server-side.
