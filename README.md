# 🌦️ Weather App | React + TypeScript + Redux Toolkit

A responsive weather application built **from scratch**. It fetches forecast data from **OpenWeatherMap**, shows a clean weather card with icons and temperature and lets you **save** results as cards on a separate page.

> **Solo project.** No test suite was developed for this app; the focus was on architecture, API integration and UX.

---

## ✨ Features
- 🔎 **City search** with inline validation and disabled state while fetching.
- ⚡ **Async data flow** via Redux Toolkit (`createSlice` + async thunks) and typed hooks (`useAppDispatch`, `useAppSelector`).
- 🧩 **Reusable UI**: `Button`, `Input`, `WeatherCard`, `ErrorCard` (consistent error/status handling).
- 💾 **Saved list**: store the current weather as a card; remove a single card or **delete all**.
- 🧭 **Routing**:  
  - `/` - search & show current result  
  - `/weather` - list of saved cards (read‑only)
- 🖼 **Adaptive UI**: gradient + blur (“glass”) backgrounds, full‑width background image, mobile‑first layout.
- 🧰 **Developer ergonomics**: modular Redux slices, clean typed hooks, and small, focused components.

---

## 🧱 Tech Stack
- **Frontend:** React 18, TypeScript, Emotion (CSS‑in‑JS), React Router (HashRouter), Vite
- **State Management:** Redux Toolkit with async thunks
- **HTTP:** Axios
- **API:** OpenWeatherMap (5‑day forecast)

---

## 🗺️ Architecture & Data Flow
- `SearchForm` ➜ dispatches `weatherActions.getWeatherByCity(trimmed)`
- `weatherSlice` thunk calls `https://api.openweathermap.org/data/2.5/forecast` and **maps** the heavy API payload to a compact shape:
  ```ts
  { name, sys: { country }, main: { temp }, weather: [{ icon, description }] }
  ```
- `Home` renders `WeatherCard` on success or `ErrorCard` on failure.
- “Save” ➜ `weatherActions.saveFromCurrent()` (creates a persistent card in Redux state).
- `/weather` page reads `saved` list, shows cards in read‑only mode, and can delete one or all.
- **Selectors**: `current`, `isFetching`, `error`, `list`, `hasAny` for clear UI bindings.
- **Styling**: Emotion with `clamp()` for fluid typography and spacing.

---

## 📁 Project Structure (key parts)
```
src/
  components/
    Button/          # reusable button with variants (size, red, fullWidth)
    Input/           # styled input with error state
    WeatherCard/     # weather info with icons + actions
    ErrorCard/       # uniform API error display
    Header/          # site title + NavLinks
    SearchForm/      # city input + submit button
  pages/
    Home/            # search + render current result (or error/loader)
    Weather/         # saved weather cards (read‑only)
  store/
    redux/
      weather/       # async thunk, reducers, selectors, types
  styles/GlobalStyles.tsx
  App.tsx / main.tsx
```

---

## ⚠️ Notes / Edge Cases
- OpenWeatherMap’s **rate limits** may cause temporary errors; the app surfaces a clean error card.
- Weather **icons** are loaded from OpenWeatherMap’s CDN. Consider switching to `https:` if your host enforces strict secure content.
- Saved cards are kept in Redux state only (no persistence). See “Roadmap” for ideas.

---

## 🧭 Roadmap / Ideas
- Persist saved cards to `localStorage`.
- Improve skeleton/loading states.
- Add 5‑day graph view (e.g., Recharts).
- i18n for city names and UI text.
- Better form validation and ARIA attributes.

---

## 📄 License
MIT © 2025 Artur Somov

---
