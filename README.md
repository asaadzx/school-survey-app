# School Improvement Field Survey

> A fast, zero-dependency offline field survey web app with local storage, instant CSV export, and raw-text fallback for school data collection.

[**Live on GitHub Pages**](https://asaadzx.github.io/school-survey-app/) · Zero backend · Zero dependencies · No build step

---

## Overview

School Improvement Field Survey is a lightweight, zero-dependency web application designed for rapid offline data collection in the field. Built with standard HTML5, CSS3, and ES5 JavaScript, it allows survey collectors to record responses locally on mobile devices without an active internet connection. Features include automatic localStorage persistence, an offline-safe CSV export engine with UTF-8 BOM encoding for seamless Excel import, and an integrated raw-text backup system to prevent data loss on restricted mobile WebViews.

## Features

- **Offline-first** — the whole app is a single `index.html`; once loaded, it runs with no network and no backend.
- **Sub-45-second interviews** — large touch targets, tap-to-select buttons, and a one-screen form flow built for on-the-street speed.
- **Automatic persistence** — every response is written to `localStorage` immediately (`egypt_school_survey` key), so nothing is lost between reloads.
- **Instant CSV export** — generates a UTF-8 `data:` URI directly via `encodeURIComponent()` instead of `Blob` + `createObjectURL()`, avoiding pitfalls on restricted mobile WebViews.
- **Raw-text backup modal** — if a file download is blocked, collectors can open the full CSV in a selectable on-screen `<textarea>` and copy it manually. No data loss, ever.
- **Excel-ready CSV** — UTF-8 BOM prefix plus proper quoting that escapes `"` and strips newlines, so commas and quotes never break rows.
- **Bulletproof JavaScript** — ES5-compatible syntax, defensive `try-catch` around all storage and download logic, and a garbled-storage fallback that never crashes the app.
- **Mobile-responsive CSS** — fast rendering on small screens, high-contrast action buttons, and accessible checkboxes.

## Quick Start (offline use)

1. Download or clone this repository.
2. Open `index.html` in any modern mobile or desktop browser.
3. Enter a collector name/ID and start interviewing. Responses are saved locally as you go.
4. Reached your target? Tap **DOWNLOAD CSV DATA**. If the browser blocks the download, tap **SHOW BACKUP CSV TEXT** and copy the raw CSV from the modal.

> The app can also be hosted anywhere static files are served (GitHub Pages, nginx, a USB drive). There is no server-side code.

## CSV Output

Exported rows use these columns:

`Collector, Gender, Classroom_Issue, Separated_Classes, Facility_Need, Canteen_Pref, Brands_Requested, Canteen_Fix, Schedule_Pref, Academic_Struggle, Timestamp`

- The file starts with a UTF-8 BOM so Excel opens it correctly.
- Text fields are quoted and escaped (`"` → `""`); line breaks are normalized so every row stays intact.

## Reliability & Error-Proofing

- `localStorage` reads/writes are wrapped in `try-catch`; corrupt or oversized storage degrades gracefully instead of crashing the script.
- The CSV download uses a `data:` URI and is guarded by `try-catch` that automatically falls back to the raw-text modal.
- Legacy Android WebViews are supported via ES5-only syntax (no template literals, `Array.from`, or arrow functions in app code).

## Deployment (GitHub Pages)

The app is already deployed at:

```
https://asaadzx.github.io/school-survey-app/
```

To redeploy after changes:

```bash
git add -A
git commit -m "your change"
git push origin main
```

Pages is configured to build from the `main` branch `/` (root) directory, so an authenticated push is all it takes.

## Tech Stack

`HTML5` · `CSS3` · Vanilla `ES5` JavaScript · `localStorage` · `GitHub Pages`

No frameworks, no package manager, no build tooling — just open and run.

## License

Unlicensed — internal tooling for the school field-data project. Share freely within the team.