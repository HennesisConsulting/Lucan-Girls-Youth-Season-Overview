# Lucan Utd Youths — Web Output (auto-publishing setup)

This folder is a ready-to-use GitHub repository. Once it's on GitHub, every
time you drag an updated `Season_Data_Collection.xlsx` into the `workbook`
folder, the site rebuilds and republishes itself automatically — usually
within 1–2 minutes. Nobody needs to touch HTML, JSON, or code.

**A note on privacy before you start:** GitHub Pages sites are publicly
accessible on the internet to anyone with the link — there's no password or
login option on the free plan. The build script already strips out specific
injury/absence reasons (players will show as "Unavailable" only, never the
detail), and the site is marked so search engines won't index it. But the
link itself isn't private, so only share it with people you're comfortable
having access, and don't rely on it being "hidden."

---

## One-time setup (about 15 minutes)

### 1. Create a GitHub account
Go to [github.com/signup](https://github.com/signup) and create a free
account if you don't have one.

### 2. Create a new repository
- Click the **+** in the top-right corner → **New repository**
- Name it something like `lucan-youths-web-output`
- Set it to **Public** (required for free GitHub Pages hosting — see the
  privacy note above)
- Don't check any of the "initialize with..." boxes
- Click **Create repository**

### 3. Upload this entire folder
On the new repository's page:
- Click **uploading an existing file** (or **Add file → Upload files**)
- Drag in *everything* from this folder, keeping the folder structure:
  - `workbook/Season_Data_Collection.xlsx`
  - `template/dashboard_template.html`
  - `scripts/build.py`
  - `.github/workflows/deploy.yml`
  - `docs/robots.txt`
  - This `README.md`
- Scroll down, click **Commit changes**

> If the drag-and-drop tool flattens folders, create the repository with
> GitHub Desktop instead (free app) — it handles folder structure
> automatically. Ask me if you'd like those steps instead.

### 4. Turn on GitHub Pages
- In the repository, go to **Settings → Pages**
- Under **Source**, choose **GitHub Actions**
- Save

### 5. Run the workflow once
- Go to the **Actions** tab → click **Rebuild and publish Web Output** on
  the left → click **Run workflow** → **Run workflow**
- Wait ~1 minute, refresh — you should see a green checkmark
- Go back to **Settings → Pages** — your live link will be shown at the top,
  something like:
  `https://<your-username>.github.io/lucan-youths-web-output/`

That link is what you share. Bookmark it, send it to parents/coaches —
whatever suits you.

---

## Updating the data from now on

1. In Excel, make your changes and **save** the workbook
2. In your web browser, go to your repository → open the `workbook` folder
3. Click **Add file → Upload files**, drag in the saved `.xlsx`, click
   **Commit changes** (this replaces the old file automatically)
4. Wait 1–2 minutes — the **Actions** tab will show a build running, then a
   green checkmark. Refresh your live link to see the update.

That's it — no other steps, no need to touch any code.

---

## If something goes wrong

Check the **Actions** tab — click the failed run (red ✗) to see exactly
what the build script printed. The most common causes:

- **"no .xlsx file found"** — make sure the file is actually inside the
  `workbook` folder, not the repository root
- **"workbook has no sheet named 'Web Output'"** — the uploaded file isn't
  the right workbook, or that sheet got renamed/deleted
- **"cell A4 does not contain valid JSON"** — open the workbook, go to the
  Web Output sheet, and press F9 (or Ctrl+Alt+F9) to force Excel to
  recalculate before saving — the formulas may not have refreshed

## Files in this repository

| Path | What it's for |
|---|---|
| `workbook/Season_Data_Collection.xlsx` | The source file — replace this whenever data changes |
| `template/dashboard_template.html` | The page design. Only touch this if you want the look changed |
| `scripts/build.py` | Reads the workbook, redacts sensitive fields, builds the page |
| `.github/workflows/deploy.yml` | Tells GitHub to run the build automatically |
| `docs/index.html` | The actual published page — generated automatically, don't edit by hand |
| `docs/robots.txt` | Keeps the page out of search engine indexes |
