# The Veto Royale — setup

Two pieces: a **Google Sheet + Apps Script** (the data) and a **static `index.html`** (the site).
Same shape as your family-reunion site, minus the manual spreadsheet work.

---

## 1. Backend (Google Sheet + Apps Script)

1. Create a new **Google Sheet** (name it whatever — you'll never open it by hand).
2. **Extensions → Apps Script**. Delete the sample, paste in **`Code.gs`**, Save.
3. Run the **`setup`** function once (pick it from the function dropdown → Run).
   Authorize when Google asks. This builds all the tabs and loads Season 28.
4. Set your admin passphrase, kept out of the code:
   **Project Settings (⚙️) → Script Properties → Add script property**
   - Name: `ADMIN_PASSPHRASE`
   - Value: whatever you want to type when running the season
5. **Deploy → New deployment → Web app**
   - Execute as: **Me**
   - Who has access: **Anyone**
   - Deploy, copy the **Web app URL** (ends in `/exec`).

> Changed `Code.gs` later? **Deploy → Manage deployments → edit (✏️) → Version: New → Deploy.** Same gotcha as the reunion site.

---

## 2. Frontend (the site)

1. Open **`index.html`**, find this line near the top of the script:
   ```js
   const API_URL = "";
   ```
   Paste your `/exec` URL between the quotes. Save.
2. Host it exactly like the reunion site:
   **GitHub → new repo → upload `index.html` → Settings → Pages → main branch.**
   Link is `https://ty1erdav1s.github.io/REPO-NAME/`.

Leave `API_URL` empty and the site runs on built-in demo data — handy for previewing the look before the backend is wired.

---

## Running a season

- **Players:** open the link → **Submit / edit my picks** → pick their name, rank the cast, answer the yes/no questions. First save on a device locks their name to that browser (the edit token). They can re-open and edit from the same device.
- **You:** **Admin** → type the passphrase (remembered on your device) → record an eviction, resolve a circumstantial question, add/remove a player, bump the episode number. Standings, win odds, and the memory wall recompute the moment you save.

Add players *before* asking people to submit, so their name is in the dropdown.

---

## New season later

Duplicate the pattern: change `CURRENT` at the top of `Code.gs`, add a matching row to the **seasons** tab (with its own theme colors) and its **cast**/**questions**. Swap the `:root` palette + fonts in `index.html` for the show's look. The rest of the code doesn't change.

---

## Notes on the security model

- Reads are public — anyone with the link sees standings. That's intended.
- Admin actions are gated by the passphrase, **verified server-side in `Code.gs`**, not in the page. A determined person could POST to the endpoint, but nothing writes without the passphrase or a valid player token.
- The passphrase lives only in Script Properties and (optionally) your own browser — never in the repo.
