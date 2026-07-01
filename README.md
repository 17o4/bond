# Investment Diary (Bondbazaar Logbook)

Responsive web app (mobile-friendly) to manually track:
- Wallet funds (manual)
- Buy trades with **T+1** settlement
- Maturity events that **reduce Portfolio value only**

Data is saved locally in your browser (localStorage). You can also connect it to a free Supabase database.

## Supabase setup
1. Create a free Supabase project.
2. Open the SQL editor and run `supabase-schema.sql`.
3. Copy `.env.example` to `.env`.
4. Fill in:
   - `VITE_SUPABASE_URL`
   - `VITE_SUPABASE_ANON_KEY`
5. Restart the dev server.

The app will then:
- load the latest diary from the database on startup
- auto-save changes to the database
- keep a local browser copy as backup

Use Settings → Export for an offline backup too.

## Run locally
```bash
npm install
npm run dev
```

Open the URL printed in the terminal.

## Deploy to GitHub Pages
This repo includes a GitHub Actions workflow for Pages deployment.

### One-time GitHub setup
1. Open repo `Settings` → `Secrets and variables` → `Actions`.
2. Add these repository secrets:
   - `VITE_SUPABASE_URL`
   - `VITE_SUPABASE_ANON_KEY`
3. Open `Settings` → `Pages`.
4. Under `Build and deployment`, set `Source` to `GitHub Actions`.

### Deploy
Push to `main`, or run the `Deploy to GitHub Pages` workflow manually.

Expected site URL:
`https://mithi0209.github.io/bond/`

## MVP calculation rules
- **Funds (date D):** Wallet += amount  
- **Trade placed (T):** Wallet −= amount, Reserved += amount  
- **Settlement (T+1):** Reserved −= amount, Portfolio += amount  
- **Maturity (date M):** Portfolio −= matured amount (Wallet unchanged)

## Notes
- INR only
- No sell trades (yet)
- No fees field (per your request)
- Current free-database mode uses one shared public diary record in Supabase
