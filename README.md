# Treinschema — Mechelen ⇄ Leuven

A single-file webapp that shows your regular commute train times, pulled live
from [iRail](https://docs.irail.be/) (the open data API behind
belgiantrain.be). No backend, no build step — it's one `index.html` file,
which is what makes it possible to host it for free on GitHub Pages and open
it from any device.

## What it does

- Shows departures for two time windows you configure: a morning route and
  an afternoon route.
- Automatically picks the right window depending on when you open it
  (before/after noon), with a toggle to switch manually.
- Refreshes every 60 seconds and shows live delays, platform, and train
  number.
- Everything you'd ever want to change lives in one clearly marked block at
  the top of `index.html`.

## Publishing it on GitHub Pages

You only need a (free) GitHub account. No command line required — everything
below can be done in the browser.

1. **Create a repository.**
   Go to [github.com/new](https://github.com/new). Give it a name (e.g.
   `train-schedule`), leave it **Public** (GitHub Pages on a free account
   requires public repos), and click **Create repository**.

2. **Upload the file.**
   On the new repo's page, click **Add file → Upload files**, drag in
   `index.html`, and click **Commit changes**.
   > The file must be named exactly `index.html` — that's the name GitHub
   > Pages looks for by default.

3. **Turn on GitHub Pages.**
   Go to the repo's **Settings → Pages** (in the left sidebar). Under
   **Build and deployment → Source**, choose **Deploy from a branch**. Under
   **Branch**, choose `main` and folder `/ (root)`, then click **Save**.

4. **Get your link.**
   Reload the **Settings → Pages** screen after a minute — GitHub will show
   a banner: *"Your site is live at `https://YOUR-USERNAME.github.io/REPO-NAME/`"*.
   That's your permanent link. It usually takes 1–2 minutes after the first
   publish to go live.

5. **Open it from anywhere.**
   Bookmark that link, or turn it into a home-screen/desktop icon (see
   below). Every time you open it, it fetches live data — you never need to
   re-upload anything unless you change the config.

## Updating it later

Whenever you want to change a station or time window (see below), edit the
file locally, then on the repo page click into `index.html` → the pencil
(✎) **Edit** icon → paste your changes → **Commit changes**. The live page
updates automatically within a minute or two, no re-publishing step needed.

## Editing your stations and time windows

Open `index.html` in any text editor and look at the very top of the file —
you'll see a block that starts with `const CONFIG = {`. It looks like this:

```js
const CONFIG = {
  morning: {
    from:  'Mechelen',   // vertrekstation 's ochtends
    to:    'Leuven',     // aankomststation 's ochtends
    start: '07:20',      // begin van het tijdvenster
    end:   '09:00'       // einde van het tijdvenster
  },
  afternoon: {
    from:  'Leuven',     // vertrekstation 's namiddags
    to:    'Mechelen',   // aankomststation 's namiddags
    start: '15:00',      // begin van het tijdvenster
    end:   '17:30'       // einde van het tijdvenster
  }
};
```

Change the station names or the `start`/`end` times (24-hour `UU:MM`
format) and save — everything else in the app (titles, button labels, the
data it fetches) updates automatically from these six values. Nothing else
in the file needs to change.

## Adding a home-screen / desktop icon

Once the GitHub Pages link works in your browser:

**Phone:** open the link, then use your browser's share/menu button →
**Add to Home Screen**.

**Computer (Chrome/Edge):** open the link, then use the browser menu →
**More tools / Apps → Create shortcut / Install this site as an app**, and
check "Open as window" for an icon that opens without browser chrome.

## Data source

Live train data comes from the [iRail API](https://docs.irail.be/), a free,
open community project providing Belgian railway data. No API key is
needed. Requests are capped at 3/second per IP — this app makes a handful
of calls once a minute at most, well within that limit.

## Notes

- If iRail's API is briefly down, the app shows an error message rather
  than stale data.
- This is a personal tool, not affiliated with NMBS/SNCB or iRail.
