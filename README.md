# KSA Days

A one-page, offline-capable web app that counts the days you spend **outside Saudi Arabia** in each calendar year, so you never exceed the **180-day** limit tied to Aramco family status. Days are marked directly on a year calendar that also shows the **St Christopher's School (Bahrain)** terms, half terms and public holidays.

No server, no account. Everything is stored in the browser on the device you use it on.

## The rule it enforces

- **Limit:** 180 days out of KSA per calendar year (1 Jan – 31 Dec). Nothing carries over.
- **Midnight rule:** a day counts as *in* KSA if you are inside the Kingdom at the midnight that closes it, otherwise it counts as *out*. Marking a day on the calendar means "I was / will be outside KSA at that midnight."
  - Exit day → out. Return day → in. A same-day Bahrain trip → in (don't mark it).
- Days up to today count as **actual**; later days count as **planned**. Both are included in the year-end total and the warning.
- Status colour: green (> 45 days left), amber (15–45), red (< 15 or over).

## Using it

- **Tap** a day to mark it out; tap again to clear. **Drag** across days to paint a whole trip.
- The top panel shows days out so far, days remaining after planned days, and the last date you could still return if you left today.
- The table under the calendar breaks days out down by school term / holiday.
- **Settings & backup** (bottom of page): language EN/IT, copy a backup, import on another device, clear a year.

### Phone + computer

Data lives in each browser separately. To move it: Settings → **Copy backup** on one device, paste into the box on the other → **Import · merge**. The backup is just a JSON list of dates, so it also pastes fine into Notes or an email.

## Deploy on GitHub Pages (about two minutes)

1. Create a new repository on GitHub (e.g. `ksa-days`), public or private.
2. Upload these files, keeping the folder structure:
   ```
   index.html
   manifest.webmanifest
   sw.js
   icons/icon.svg
   icons/icon-192.png
   icons/icon-512.png
   icons/apple-touch-icon.png
   ```
3. Repository **Settings → Pages → Build and deployment → Source: Deploy from a branch**, branch `main`, folder `/ (root)`. Save.
4. After a minute the app is live at `https://<your-username>.github.io/ksa-days/`.

### Install it like an app

- **iPhone (Safari):** open the URL → Share → **Add to Home Screen**.
- **Android (Chrome):** open the URL → menu → **Install app** / **Add to Home screen**.
- **Mac / Windows (Chrome or Edge):** open the URL → install icon in the address bar.

Once installed it works offline; the service worker refreshes files when you're online.

## Updating the school calendar

Term dates live at the top of `index.html` in the `SCHOOL` object. Each academic year has `terms`, `breaks`, `holidays` and `staff` arrays with inclusive `YYYY-MM-DD` dates. When St Chris publishes Autumn 2027's half term and end date, edit the `2027-28` entry (the term currently runs through 31 Dec as a placeholder with `tbc:true`) and bump `CACHE` in `sw.js` so installed copies pick up the change.

Source for the dates: <https://www.st-chris.net/term-dates>. Islamic holidays are subject to moon sighting.

## Self-tests

Bottom of the page → **Run tests**. They pin down the midnight rule, calendar-year boundaries, leap years, the 180 threshold and the "must be back by" maths.

## Licence

MIT — do what you like with it.
