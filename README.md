# sacbb.org — Sacramento Brick Builders

Static website for Sacramento Brick Builders, hosted free on GitHub Pages.

## Files

- `index.html` — the whole site (one page)
- `styles.css` — styling, based on the club logo's blue + yellow palette
- `logo.png` — club logo (used in hero + favicon)
- `CNAME` — tells GitHub Pages to serve this site at `sacbb.org`
- `.nojekyll` — disables Jekyll processing so files serve as-is

## Local preview

Just open `index.html` in a browser, or for the Facebook embed to render correctly run a tiny local server:

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

## Deploy to GitHub Pages

1. Create a public repo on GitHub (e.g. `sacbb-site`).
2. Push these files to the `main` branch.
3. In the repo: **Settings → Pages**
   - **Source:** Deploy from a branch
   - **Branch:** `main` / `/ (root)`
   - Click **Save**
4. Under **Custom domain**, enter `sacbb.org` and save. Check **Enforce HTTPS** once it becomes available (can take ~15 min after DNS propagates).

## DNS — point sacbb.org at GitHub Pages

At your domain registrar (where you bought sacbb.org), set these DNS records:

**Apex domain (`sacbb.org`)** — four A records pointing to GitHub Pages:

```
A    @    185.199.108.153
A    @    185.199.109.153
A    @    185.199.110.153
A    @    185.199.111.153
```

(Optional, IPv6:)
```
AAAA @    2606:50c0:8000::153
AAAA @    2606:50c0:8001::153
AAAA @    2606:50c0:8002::153
AAAA @    2606:50c0:8003::153
```

**`www` subdomain** — CNAME to your GitHub Pages site:
```
CNAME  www   <your-github-username>.github.io.
```

DNS can take 15 minutes to a few hours to propagate. Once it does, GitHub will issue a free Let's Encrypt cert automatically.

## Updating content

- **Calendar:** the embed pulls from the public Google Calendar — just add events in Google Calendar, the site updates automatically.
- **Membership form / Bylaws:** edit the URLs in `index.html` (search for `docs.google.com` and `drive.google.com`).
- **Facebook posts:** the Facebook Page Plugin pulls live from `facebook.com/sacbb`. New posts appear automatically.
- **Instagram:** currently a styled link to `@sac_bb`. To embed an actual feed, the simplest free option is [SnapWidget](https://snapwidget.com/) (free tier: 1 widget) — generate the embed code and replace the `<a class="ig-link">` block in `index.html` with it. A real live Instagram feed otherwise requires the Instagram Graph API + a small backend, which we'd be moving off "free static hosting" to add.
- **Logo / colors:** swap `logo.png` to update the logo. To shift the palette, edit the `:root` variables at the top of `styles.css`.

## Notes

- The Facebook embed uses Meta's Page Plugin SDK. It loads from `connect.facebook.net` — visitors with strict tracker blockers may not see it, but the link to the page still works.
- The site has no build step and no JavaScript framework — it's pure HTML + CSS + a tiny vanilla `<script>` for the footer year. Easy to maintain.
