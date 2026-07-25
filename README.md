# The Veto Royale

A for-fun reality-TV prediction pool (Big Brother / Survivor). Rank the
cast by predicted finish — lowest score wins. Static site on GitHub
Pages, backed by a Google Sheet via Google Apps Script. Players submit
and edit their own picks; the admin runs the season from the UI.

- **`index.html`** — the site. Deploy to GitHub Pages.
- **`apps-script/Code.gs`** — paste into Google Apps Script, run `setup()` once.
- **`SETUP.md`** — full deploy guide (Sheet + Apps Script + Pages).

Leave `API_URL` empty in `index.html` to preview on built-in demo data;
paste your Apps Script `/exec` URL to go live.
