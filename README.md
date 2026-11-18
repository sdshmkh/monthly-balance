# Monthly Balance Calculator

A single-page calculator that shows how far in the hole you are each month, and how to climb out.

- **Income, loans and fixed liabilities**, each row in its own currency (INR, USD, EUR, GBP, AED, SGD, CAD, AUD) with editable exchange rates.
- **Loans** take principal, annual rate and EMI. Each row shows the monthly payment and how much of it is interest.
- **The hole**: liabilities dig the pit, income builds the ladder. With a surplus, a path leads to your goals: savings in a year, a 6-month safety net, and your debt-free date.
- **Payoff planner**: avalanche vs snowball vs EMIs only, with a timeline of total debt and the order each loan clears.
- Works on phones, installs to the home screen, and works offline after the first visit.
- Everything is stored in the browser's `localStorage`. Nothing is sent anywhere.

## Project layout

```
site/
  index.html             the whole app (HTML, CSS, JS in one file)
  manifest.webmanifest   home-screen install settings
  sw.js                  offline cache
  icons/                 app icons
.github/workflows/
  deploy.yml             publishes site/ to GitHub Pages on every push to main
```

## Run locally

No build step. Serve the `site` folder with any static server:

```bash
cd site
python3 -m http.server 8000
# open http://localhost:8000
```

Opening `index.html` directly also works, but offline mode needs a server.

## Deploy to GitHub Pages

1. Create a new repository on GitHub and push this folder to the `main` branch:
   ```bash
   git init
   git add .
   git commit -m "Monthly balance calculator"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repo-name>.git
   git push -u origin main
   ```
2. In the repository, open **Settings → Pages** and set **Source** to **GitHub Actions**.
3. The **Deploy to GitHub Pages** workflow runs on every push to `main` (or manually from the **Actions** tab).
4. Your site goes live at `https://<your-username>.github.io/<repo-name>/`.

## Updating

Edit `site/index.html` and push. When you change cached files, bump `CACHE` in `site/sw.js` (for example `balance-v2`) so installed copies pick up the new version straight away.

## Notes

- Exchange rates are not fetched live. The starting rates are approximate for November 2026; edit them in the page.
- The payoff plan assumes interest rates and exchange rates stay constant, and that a cleared loan's EMI rolls onto the next one.
