# WeatherX

A premium, responsive weather dashboard built with vanilla HTML, CSS and JavaScript (ES modules). Real-time conditions, a 24-hour forecast, a 7-day outlook and detailed atmospheric readings, all from the free [Open-Meteo](https://open-meteo.com) API. No frameworks, no build step, no API key.

## Features

- **Current conditions:** city, country, temperature, feels-like, condition, and today's high and low.
- **Animated illustrations:** sun, moon with stars, clouds, rain, snow, fog and lightning.
- **Dynamic backgrounds:** the gradient and ambient effects change with the weather (sunny, cloudy, fog, rain, snow, night, thunderstorm).
- **Worldwide city search:** type-ahead suggestions, keyboard navigation (arrow keys, Enter, Esc), `City, Country` filtering, and a clear message when a place is not found.
- **Geolocation:** the location button uses browser permission to detect where you are.
- **24-hour forecast:** horizontally scrollable, with temperature, condition, rain probability and wind.
- **7-day forecast:** day, date, condition, high and low, and rain probability.
- **Detail cards:** feels-like, humidity, wind speed and direction, pressure, visibility, UV index, cloud cover, dew point, sunrise and sunset.
- **Advisories:** derived from forecast values (thunderstorms, heavy rain, strong wind, high UV, freezing temperatures).
- **Preferences and lists:** °C/°F switching, dark and light themes, favorites (up to 12) and recent searches, all saved in LocalStorage.
- **Utilities:** refresh button, share (Web Share API or clipboard), loading state, error banners, and a `/` shortcut to focus search.
- **Accessibility:** semantic landmarks, ARIA combobox for search, visible focus rings, a skip link, and reduced-motion support.

## Technology stack

| Area | Technology |
| --- | --- |
| Markup | HTML5 |
| Styling | CSS3 (custom properties, glassmorphism, keyframe animations, responsive grid) |
| Logic | Vanilla JavaScript ES2020+ modules, `async`/`await`, Fetch API |
| Data | Open-Meteo Forecast and Geocoding REST APIs; BigDataCloud reverse geocoding for place names |
| Storage | LocalStorage |

## Project structure

```
weatherx/
├── index.html          # Application shell
├── css/
│   └── style.css       # Design tokens, themes, components, animations, responsive rules
├── js/
│   ├── app.js          # Entry point: state, events, search, favorites, startup
│   ├── weather.js      # Forecast fetching, normalization, caching, WMO code mapping
│   ├── location.js     # City search, browser geolocation, reverse geocoding
│   ├── ui.js           # DOM rendering and formatting helpers
│   ├── icons.js        # Line icons and animated SVG weather illustrations
│   └── config.js       # API endpoints, storage keys, limits
├── assets/
│   ├── images/         # Raster assets (none required)
│   └── icons/          # Reserved for exported icon assets
├── LICENSE
└── README.md
```

## Running locally

Browsers block ES modules opened from `file://`, so serve the folder over HTTP:

```bash
cd weatherx
python3 -m http.server 8080
# then open http://localhost:8080
```

Any static server works (`npx serve`, VS Code Live Server, etc.).

## API configuration

WeatherX needs **no API key**. Endpoints are defined in `js/config.js`:

- `forecast`: `https://api.open-meteo.com/v1/forecast`
- `geocoding`: `https://geocoding-api.open-meteo.com/v1/search`
- `reverseGeocode`: BigDataCloud client endpoint, used only to label your detected location. If it fails, the app shows "Your location".

To use a keyed provider such as OpenWeather, change the endpoints in `config.js` and update the `normalize()` function in `js/weather.js` to map that provider's fields.

Open-Meteo's free tier is intended for non-commercial use. Check its terms before commercial deployment.

## Live demo deployment

The site is static, so it can be hosted anywhere that serves files:

- **GitHub Pages:** push to GitHub, then go to *Settings → Pages*, choose the `main` branch and the root folder.
- **Netlify or Vercel:** drag the folder into the dashboard, or connect the repository. No build command is needed.
- **Cloudflare Pages:** connect the repository with an empty build command and output directory `/`.

Geolocation requires HTTPS, which all of these services provide.

## Screenshots

_Add screenshots to `assets/images/` and reference them here, for example:_

```markdown
![Dashboard](assets/images/dashboard.png)
```

## Browser support

Current versions of Chrome, Edge, Firefox, Safari (macOS and iOS) and Chromium on Android. `AbortSignal.any` requires Chrome 116+, Firefox 124+ or Safari 17.4+.

## License

Released under the [MIT License](LICENSE).
