# TEN Network Association — Notices

Static Jekyll site for publishing official notices and announcements of TEN Network Association (a Swiss Verein). Hosted on GitHub Pages.

## Adding a new notice

A template lives in `_drafts/example-notice.md`. Files in `_drafts/` are **not deployed** by GitHub Pages — they exist only as a reference and for local preview.

To publish:

1. Copy the template to `_posts/` with a real date in the filename:
   ```sh
   cp _drafts/example-notice.md _posts/2026-01-15-board-resolution.md
   ```
   Filename convention: `YYYY-MM-DD-short-kebab-slug.md`. The date determines publication order; the slug becomes part of the permalink.

2. Edit the front matter and body:

   ```yaml
   ---
   title: "Termination of Operator Licence"
   ref: TNA-2026-003
   category: Legal       # Legal | Governance | Financial | Operational
   summary: "One-line summary used on the index page and in <meta description>."
   ---
   ```

3. Commit and push to `main`. GitHub Pages rebuilds the site within a minute.

That's it. The index page regenerates itself; you don't edit it.

## Permalinks

Each notice is served at `/notices/YYYY-MM-DD-slug/`. Once a notice is published, **do not rename or move its file** — that URL is the permalink and may be cited externally.

For corrections, publish a new notice (e.g. *"Corrigendum to TNA-2026-003"*) referencing the original, rather than editing it silently. Git history serves as the audit trail; protect `main` against force-pushes in repo settings.

## Local preview (optional)

Requires Ruby 3+ and Bundler.

```sh
bundle install
bundle exec jekyll serve --drafts   # --drafts shows the example for reference
# → http://localhost:4000
```

## Deploying to GitHub Pages

1. Push to a public repo, e.g. `ten-network/notices`.
2. **Settings → Pages** → Source: *Deploy from a branch* → Branch: `main` / `(root)` → Save.
3. Site goes live at `https://<org>.github.io/<repo>/` within a minute.
4. (Recommended) Add a custom domain like `notices.ten.network` via **Settings → Pages → Custom domain**, then point a `CNAME` DNS record at `<org>.github.io`.

## Files to update before going live

Search the repo for `[Canton]`, `[Street, Postal Code, City]`, and `notices@example.org` — these placeholders are in `_layouts/default.html` and `index.html`. Replace with the Association's actual registered office and contact address.

## Why Jekyll, why this minimal

Jekyll is built into GitHub Pages: no build action to maintain, no JS dependency to age out. Plain markdown + a tiny config means anyone with repo access can publish a notice, and the site will keep rendering as long as GitHub Pages exists.
