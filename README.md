# DV100 — Texas Disabled Veteran Benefits Reference

An installable, offline-capable reference for Texas disabled-veteran benefits, scoped to the Austin metro (Hays and Travis counties) with federal and statewide entries that apply anywhere.

**Public build.** No personal information, no figures tied to one person's loan or property. Set your rating in the header and the page filters to what you actually qualify for.

## What makes it different from the usual list

Every entry carries a verification grade. **✓ Verified** was confirmed against a primary statutory or `.gov` source. **? Verify** is plausible but unconfirmed and needs a phone call first. There is also a **Don't chase these** section for claims that are repeated confidently across veteran discount lists and SEO content farms but do not survive a primary source — Blue Star Museums for veterans, an H-E-B military discount, a Texas vehicle sales tax exemption, a 10% homestead penalty, MoPac being free with DV plates.

The **Homestead** tab covers the trap in the biggest benefit: §11.131 exempts 100% of a homestead's appraised value, but it is a *homestead* exemption, not a veteran-status one — §11.13(j)(1)(D) requires owner occupancy as a principal residence. A three-question decision tree walks through what happens if the property gets rented out, including the §11.13(l) temporary-absence defense and the §11.43(i) lookback.

## Deploying to GitHub Pages

```bash
git init
git add .
git commit -m "DV100 Texas disabled veteran benefits reference"
git branch -M main
git remote add origin https://github.com/<you>/<repo>.git
git push -u origin main
```

Then **Settings → Pages → Source: Deploy from a branch → `main` → `/ (root)` → Save**. Live in a minute or two at `https://<you>.github.io/<repo>/`.

Every path in this bundle is relative (`./`), so it works from a repo subpath without changes. `.nojekyll` is included so GitHub serves the files as-is instead of running them through Jekyll.

**GitHub Pages is public.** On a free account, a Pages site is publicly reachable and indexable even when the repo is private. That is fine and intended for this build — it contains nothing personal. Do not add personal figures, an address, or a rating decision to a repo you publish this way.

## Installing on a phone

1. Open the Pages URL in **Chrome** (Samsung Internet works the same way).
2. Tap **Install** in the app header, or **⋮ → Add to Home screen → Install**.
3. It opens standalone, no browser chrome. Long-press the icon for shortcuts into **Homestead**, **Actions**, or **Contacts**.

Open it once online so the service worker caches everything; after that it runs with no signal. Layout has its own breakpoints for a narrow phone, a folding phone's cover screen, and the wide-but-short unfolded screen — nav moves to a thumb-reachable bottom bar below 760px.

A service worker only registers over HTTPS or `localhost`, never `file://`. Opened as a downloaded file the app still works and still remembers your rating; it just cannot install or cache.

## Updating

Edit `index.html`, then **bump the `CACHE` constant at the top of `sw.js`** — `dv100-pub-2026.09.11` → `dv100-pub-2026.12.01`, say. The old cache is deleted on activate and installed copies pull the new version on next launch. Skipping the bump is the most common reason a PWA update looks like it didn't take.

### When to update the content

| When | What changes |
|---|---|
| December 1 | VA COLA — compensation, SMC, Chapter 35 DEA, clothing allowance |
| October 1 | Federal fiscal year — SAH/SHA/TRA maximums, auto allowance |
| September 1, odd years | Texas legislative effective dates |
| January | County appraisal notices; verify the exemption block |
| April 30 | Exemption filing deadline; §11.43(g) notice due before May 1 |

Also bump the `REV` date in the header (`.ident-sub`) so readers can tell how stale the figures are.

### Adding or editing entries

Everything is data at the top of the inline `<script id="app">` block — no build step, no framework, no dependencies.

- `BENEFITS[]` — the reference cards. `c` is the category, `min` is the rating floor, `pt:true` gates on Permanent & Total, `tags` carry the verification grade, `s` is the source line.
- `TASKS[]` — the checklist. `tier` 1/2/3, `sev` controls the left edge stripe.
- `LADDER[]` — the threshold rungs. `v` is the numeric floor used to compute "you are here".
- `DEBUNK[]` — the screened-out claims.
- `CALLS[]`, `MONTHS[]`, `TREE`/`OUTCOMES` — contacts, calendar, decision tree.

If you add an entry, add its source. The verification grade is the whole point of this thing; an ungraded entry makes the graded ones worth less.

## Files

```
index.html                 the app — all HTML, CSS and JS, no dependencies
manifest.webmanifest       name, icons, standalone display, shortcuts
sw.js                      service worker — offline cache
.nojekyll                  tell GitHub Pages not to run Jekyll
icon-192.png  icon-512.png
icon-maskable-192.png  icon-maskable-512.png    Android adaptive icons
apple-touch-icon.png
```

No analytics, no telemetry, no backend, no cookies. Your rating and checkbox progress live in your own browser's local storage and are never transmitted. The only external request is Google Fonts, which the service worker caches on first load; the page has real fallback stacks if it never arrives.

## Not legal or tax advice

A research summary compiled from primary sources with a second adversarial verification pass. Your facts are not the facts this was written against — property tax in particular turns on ownership and occupancy on January 1 of each specific tax year, and thresholds differ program by program in ways that are easy to conflate. A county Veteran Service Officer is free, accredited, and the right first call; the numbers are on the Contacts tab. A disputed property tax exemption is worth an hour of a Texas property tax attorney's time.

Corrections are welcome and wanted.

---

Compiled by **Rowan Risk Solutions LLC**, Buda TX — published for other veterans because this information is hard to assemble and easy to get wrong.
