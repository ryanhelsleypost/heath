# Updating Heath — The For-Dummies Guide

Keep this handy. Any time Claude gives you a new `index.html`, this is the whole process.

---

## The 3-Step Update (do this every time)

**Step 1 — Upload the new file**
1. Go to **github.com/ryanhelsleypost/heath**
2. Click **Add file → Upload files** (top right, next to the green Code button)
3. Drag the new `index.html` into the drop zone
   - It must be named exactly `index.html` — lowercase, no `(1)` in the name
   - Same name = it automatically replaces the old one
4. Click the green **Commit changes** button at the bottom

**Step 2 — Wait for the green check**
1. Click the **Actions** tab
2. A new run appears at the top of the list ("Add files via upload")
3. Wait ~30–60 seconds for a green ✅
   - Green ✅ → done, go to Step 3
   - Red ❌ → go to Troubleshooting below

**Step 3 — Refresh your devices**
- **Computer:** go to ryanhelsleypost.github.io/heath/ and hard-refresh with **Cmd+Shift+R**
- **Phone:** close the Heath tab/app completely, reopen it, pull down to refresh once or twice

Your data is never touched by updates — it lives in Firebase, not in the file. Updates only change the app itself.

---

## Troubleshooting (in order — stop when it works)

### Fix #1 — Fresh run (fixes it 80% of the time)
A red ❌ deploy usually just needs a *fresh* run — NOT a re-run.
1. **Actions** tab
2. Left sidebar → click **"Deploy static content to Pages"** (the workflow name)
3. Right side → click the **Run workflow** dropdown → keep branch `main` → green **Run workflow** button
4. Wait for the new run to go green

> **Rule of thumb: never use "Re-run jobs."** Re-runs of this workflow trip over their own leftovers (the "Multiple artifacts named github-pages" error). Always use **Run workflow** instead.

### Fix #2 — Reset the Pages environment
If a fresh run still fails with "Deployment failed, try again later":
1. Repo **Settings → Pages**
2. Change Source to **"Deploy from a branch"** → Save
3. Change it right back to **"GitHub Actions"**
4. Go do Fix #1 again (Run workflow)

This tears down and rebuilds the deployment machinery. This is what fixed it on day one.

### Fix #3 — Check if GitHub itself is broken
Go to **githubstatus.com**. If "Pages" or "Actions" isn't green, it's not you — wait 20–30 minutes and do Fix #1 again.

### Fix #4 — Read the actual error
1. Click the red run → click the red **deploy** job on the left
2. Click the failing step (red ❌) to expand its log
3. The red **Error:** lines tell the real story — screenshot them and send to Claude
   - Ignore the yellow "Node.js 20 is deprecated" warning — it's harmless noise, always there

### Fix #5 — Nuclear option (5 min, always works)
Nothing of value lives in the repo — data is in Firebase, the file is on your computer. So:
1. Repo **Settings** → bottom → **Danger Zone → Delete this repository** → confirm
2. Create a new repo with the **exact same name: `heath`** (same name = same URL, phone icon keeps working)
3. Upload `index.html` → Commit
4. Create the empty `.nojekyll` file: **Add file → Create new file** → name it `.nojekyll` → Commit
5. **Settings → Pages** → Source: **GitHub Actions** → choose **Static HTML** → Configure → **Commit changes**
6. Green check → live

---

## Things that look scary but are fine

- **Yellow "Node.js deprecated" warning** — ignore forever
- **The old "pages build and deployment" run stuck at "Queued"** — orphaned ghost from day one, can't be cancelled, hurts nothing
- **A failed deploy** — the live site keeps serving the last good version; nothing breaks while you troubleshoot
- **The blank $0 app when someone else visits the URL** — correct and intentional; your data only appears after sync connects

## Things to never do

- **Never put your Firebase config or sync code inside the HTML file.** They belong only in the ☁ Sync screen. The file is public; the settings are not.
- **Never rename the repo casually** — it changes the URL and breaks the phone icon (fixable, but annoying)
- **Never use "Re-run jobs"** — Run workflow instead (see Fix #1)

## The keys to the kingdom (keep safe)

| Thing | Where it lives | If lost |
|---|---|---|
| Sync code | Password manager / your head | Data unreachable — keep this safe! |
| Firebase config | Firebase console → ⚙ → Project settings → Your apps | Always retrievable |
| The app URL | ryanhelsleypost.github.io/heath/ | It's this |
| Your data | Firebase (+ each device's browser) | Export a JSON backup occasionally |
