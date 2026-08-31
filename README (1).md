# 🌤️ ClearSky (Mausam) — Live Weather App

A lightweight, single-file weather web app with live forecasts, hourly breakdowns, a 7-day outlook, city autocomplete search, geolocation support, and °C/°F toggle — all powered by the free [Open-Meteo](https://open-meteo.com/) API (no API key required).

![Stack](https://img.shields.io/badge/stack-HTML%20%2F%20CSS%20%2F%20JS-blue)
![API](https://img.shields.io/badge/API-Open--Meteo-green)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

---

## ✨ Features

- **Live current weather** — temperature, condition, "feels like", humidity, wind speed, and UV index
- **Hourly forecast (next 24 hours)** — temperature, condition emoji, and precipitation probability
- **7-day forecast** — high/low temps with a visual range bar and rain chance
- **City search with autocomplete** — type a city name, pick a suggestion from the dropdown
- **📍 "Use my location"** — one-click geolocation via the browser
- **°C / °F toggle** — instantly switches all displayed units
- **Auto-localised timezone** — forecast times are shown in the searched city's local time (`timezone=auto`)
- **Responsive, mobile-friendly UI** — clean card-based design that adapts to any screen size
- **Zero dependencies** — no frameworks, no build step, no API keys, no installation

---

## 🚀 Getting Started

### Option 1: Just open it (easiest)

1. Download `Mausam.html`
2. Double-click it — it opens in any modern browser (Chrome, Firefox, Edge, Safari)
3. That's it. No server, no install, no setup.

### Option 2: Serve it locally (optional)

If you prefer running it over `localhost` (or want to test geolocation, which requires a secure context):

```bash
# Python 3
python -m http.server 8000

# or Node.js
npx serve .
```

Then visit `http://localhost:8000`.

> **Note:** Geolocation works on `https://` or `localhost` only — that's a browser security rule, not an app limitation.

---

## 🧠 How It Works

The app talks to two free Open-Meteo endpoints:

| Purpose | Endpoint |
|---|---|
| Weather forecast (current, hourly, daily) | `https://api.open-meteo.com/v1/forecast` |
| City geocoding / autocomplete | `https://geocoding-api.open-meteo.com/v1/search` |

**Flow:**

1. The user picks a city (search/autocomplete) or shares their location (geolocation) → app gets `lat` / `lon`
2. A single API call fetches current conditions, hourly data, and 7-day daily data with `timezone=auto` so times are local to the city
3. The `wmo()` helper maps WMO weather codes (0–99) to human-readable descriptions and emoji (☀️ ⛅ 🌧️ ⛈️ ❄️ …)
4. Everything is rendered into the DOM with plain vanilla JavaScript — no template libraries

**Default city:** the app loads with **Bhiwani, India** (28.79° N, 76.14° E) on startup.

---

## 📁 File Structure

```
Mausam.html          # the entire app — styles, markup, and logic in one file
```

That's literally it. One file, ~18 KB.

---

## 🛠️ Customisation

All tweakable values live at the top of the `<script>` block:

| What | Where |
|---|---|
| **Default city** | `fetchWeather(28.79, 76.14, 'Bhiwani')` at the bottom of the script — change the lat/lon/name |
| **API endpoints** | `API` and `GEO` constants |
| **Theme colours** | CSS variables in `:root` (`--bg`, `--accent`, `--sun`, `--sky`, …) |
| **Brand name** | The `ClearSky` text in the header and footer |

Example — make **Delhi** the default:

```js
fetchWeather(28.61, 77.21, 'Delhi');
input.value = 'Delhi';
```

---

## ⚠️ Troubleshooting

| Symptom | Fix |
|---|---|
| "Couldn't reach live service" | The app needs internet to fetch from Open-Meteo. If you're opening the file from the sandboxed preview pane, open it in a real browser tab instead. |
| Location button does nothing | Geolocation needs `https://` or `localhost`. Search the city manually instead. |
| "City not found" | Try a bigger city or one with a different spelling (English names work best). |

---

## 📜 Credits

- **Data:** [Open-Meteo](https://open-meteo.com/) — free weather & geocoding API, no key needed
- **Weather codes:** [WMO weather interpretation codes](https://open-meteo.com/en/docs) as used by Open-Meteo

## 📄 License

MIT — use it, modify it, ship it. If you remix it, a shout-out to Open-Meteo is appreciated (they keep it free).
