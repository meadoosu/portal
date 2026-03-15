# Portal Display

A self-hosted browser app that turns any screen into an ambient photo frame with Spotify, live weather, and an hourly forecast. 

I tested this on a **Facebook Portal 2nd generation 10"** i thrifted

![Portal Display](https://img.shields.io/badge/built%20with-HTML%20%7C%20CSS%20%7C%20JS-1DB954?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)

---

## Setup (follow closely or else your device will self destrucut and turn evil) 

### 1. Add your photos

Drop your photos into the `photos/` folder, then list them in `config.json`:

```json
"google": {
  "photos": [
    "photos/beach.jpg",
    "photos/family.jpg",
    "photos/dog.jpg"
  ]
}
```

Keep filenames simple with no spaces — use underscores or dashes instead (e.g. `snow-day.jpg`).

> If you have 10+ pictures, this app is not recommended. Since you'll need to map a bunch of images, its not sastifactory

---

### 2. Configure `config.json`

Fill in the following fields:

```json
{
  "spotify": {
    "clientId": "YOUR_SPOTIFY_CLIENT_ID",
    "redirectUri": "https://your-hosted-url.com"
  },
  "google": {
    "photos": [
      "photos/photo1.jpg",
      "photos/photo2.jpg"
    ]
  },
  "weather": {
    "lat": "41.8800",
    "lon": "-88.0075",
    "units": "imperial",
    "cityLabel": "Your City, ST"
  },
  "slideshow": {
    "intervalSeconds": 12,
    "transitionSeconds": 1.5
  }
}
```

#### Spotify setup

1. Go to [developer.spotify.com/dashboard](https://developer.spotify.com/dashboard) and log in with your regular Spotify account
2. Click **Create App** — give it any name, enable **Web API** and **Web Playback SDK**
3. Under **Redirect URIs**, add the URL you'll be hosting this on (e.g. `https://your-site.com`) — must match `redirectUri` in `config.json` exactly, including or excluding a trailing slash
4. Copy your **Client ID** and paste it into `config.json`

> Spotify Premium is required for the Web Playback SDK. This is a Spotify limitation, not ours.

#### Weather setup

No API key needed. Just set your coordinates and preferred units:

- `units`: `"imperial"` for °F, `"metric"` for °C
- Find your `lat`/`lon` at [latlong.net](https://www.latlong.net)

---

### 3. Host it

This is a static site — you can host it anywhere that serves HTML files.

**Free hosting options:**
- [Netlify](https://netlify.com) — drag and drop the folder, instant deploy
- [Cloudflare Pages](https://pages.cloudflare.com) — connect a GitHub repo
- [GitHub Pages](https://pages.github.com) — free with any public repo

**Self-hosted / local:**
```bash
cd portal
python3 -m http.server 8000
```
Then open `http://localhost:8000` or `http://YOUR_IP:8000` from any device on your network.

> If hosting locally, use [ngrok](https://ngrok.com) to get an HTTPS URL for Spotify's redirect URI requirement.

---

### 4. First-time login

On first load you'll see a setup screen — connect Spotify and you're in. Tokens are stored locally and refresh automatically so you'll only need to do this once.

After the app loads, **tap anywhere on the screen once** to activate the screen keep-alive (required by the browser to start background media).

---

## Keeping the screen on (Facebook Portal / kiosk devices)

The Facebook Portal has a hardcoded idle timeout that's difficult to fully disable through settings alone. This app uses a silent background YouTube video ([7-day timer](https://www.youtube.com/watch?v=gSvU-flG6FY)) to set the OS "media playing" flag, which suppresses the sleep timer indefinitely. Credit to the Home Assistant community for figuring this out.

---

## File structure

```
portal/
├── index.html
├── config.json        ← your credentials (keep this private!)
├── photos/            ← drop your photos here
├── css/
│   └── styles.css
└── js/
    ├── app.js         ← main orchestrator
    ├── spotify.js     ← Spotify OAuth + playback
    ├── photos.js      ← slideshow
    ├── weather.js     ← Open-Meteo weather
    ├── clock.js       ← live clock
    ├── ambient.js     ← color extraction from photos/album art
    └── player.js      ← full-screen player UI
```



