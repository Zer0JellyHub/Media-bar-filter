# 🎬 Jellyfin Media Bar – Random + Filters Mod

A client-side JavaScript mod for **Jellyfin** that replaces the default media bar with a randomised, filterable showcase of your library. No server changes required — just drop it in as a custom script.

![License](https://img.shields.io/badge/license-MIT-blue) ![Jellyfin](https://img.shields.io/badge/Jellyfin-compatible-00A4DC)

---

## ✨ Features

| Feature | Details |
|---|---|
| 🎲 **Random Selection** | Pulls a random set of items from your library on every load |
| ⭐ **Minimum Rating** | Filter by community rating (0 – 10, steps of 0.5) |
| 📅 **Release Year Range** | Set a From / To year window; max always equals the current year automatically |
| 🔢 **Item Count** | Choose how many items to load (5 – 50) |
| ⏱️ **Slide Interval** | Control how fast the carousel rotates (3 – 60 seconds) |
| 🎭 **Media Type** | Show All, Movies only, or Series only |
| ⚙️ **Gear Settings Panel** | Floating settings pill with auto-close countdown |
| ◀ ▶ **Navigation Arrows** | Appear on hover/touch, hide after 2.5 s of inactivity |
| 💾 **Per-User Persistence** | All settings saved to `localStorage`, scoped per Jellyfin user ID |

---

## 📦 Installation

### Option A — Jellyfin Custom Script (recommended)

1. In your Jellyfin admin panel go to **Dashboard → General → Custom CSS / Scripts**.
2. Paste the full contents of `mediabar-mod.js` into the **Custom JavaScript** field.
3. Save and reload the page.

### Option B — Browser Extension (Tampermonkey / Violentmonkey)

1. Install [Tampermonkey](https://www.tampermonkey.net/) or [Violentmonkey](https://violentmonkey.github.io/).
2. Create a new script and paste the contents of `mediabar-mod.js`.
3. Add the following header at the top:

```js
// ==UserScript==
// @name         Jellyfin Media Bar Mod
// @match        http://YOUR-JELLYFIN-URL/*
// @grant        none
// ==/UserScript==
```

4. Save and navigate to your Jellyfin instance.

---

## ⚙️ Settings Reference

Open the settings panel by clicking the **⚙ gear icon** in the bottom-right corner of the media bar.

| Setting | Default | Description |
|---|---|---|
| Minimum Rating | – (off) | Hides items below this community rating |
| Number of Items | 20 | How many random items to fetch |
| Slide Interval | 8 s | Time between automatic slide transitions |
| Release Year – From | 1900 | Earliest production year to include |
| Release Year – To | *current year* | Latest production year to include; updates automatically each year |
| Media Type | All | Filter to Movies, Series, or both |

Click **🔄 Load New Random Selection** to apply and reload with a fresh random set.

The panel closes automatically after **10 seconds** of inactivity (a purple countdown bar shows the remaining time). Any interaction resets the timer.

---

## 🗂️ localStorage Keys

Settings are stored per user. The keys follow the pattern `key_userId`.

| Key | Type | Description |
|---|---|---|
| `jf_mbrf_minRating` | `number` | Minimum community rating |
| `jf_mbrf_count` | `number` | Number of items to fetch |
| `jf_mbrf_type` | `string` | `"All"`, `"Movie"`, or `"Series"` |
| `jf_mbrf_interval` | `number` | Slide interval in seconds |
| `jf_mbrf_yearFrom` | `number` | Release year range start |
| `jf_mbrf_yearTo` | `number` | Release year range end |

---

## 🛠️ How It Works

1. On load the script waits for `window.ApiClient` and a valid user session.
2. It calls `/Items` on the Jellyfin API with `SortBy=Random` and the active filter parameters (`MinCommunityRating`, `MinYear`, `MaxYear`, `IncludeItemTypes`, `Limit`).
3. Custom slide `<div>` elements are injected into `#jf-media-bar`, each with a backdrop image, logo, rating, genre tags, overview snippet, and action buttons.
4. Built-in prev/next arrow buttons from the original bar are hidden via CSS; the mod creates its own arrows that are only visible on hover or touch.

---

## 🧩 Compatibility

- Jellyfin **10.8+** (tested on 10.9)
- Works with the default **Jellyfin Web** client
- No plugins or server-side changes required
- Does **not** modify any server files

---

## 📄 License

MIT — do whatever you like, attribution appreciated.
