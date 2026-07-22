# PTA @ NeurIPS 2026 — website

This is the GitHub Pages version of the workshop site
(migrated from https://sites.google.com/view/pta-neurips2026/home).

It's a plain [Jekyll](https://jekyllrb.com/) site — GitHub Pages builds it
automatically, **you do not need Node, npm, or any build step**. You only
need Ruby/Jekyll if you want to preview it on your own computer before
pushing.

## Site structure

```
_config.yml              site title/description, contact email, baseurl
_layouts/default.html    shared page shell (header + footer)
_includes/               header.html, footer.html, head.html
assets/css/style.css     all styling
assets/images/           speaker & organizer photos live here
_data/speakers.yml       invited speaker list (edit this to add photos/info)
_data/organizers.yml     organizer list (edit this to add photos/info)
_data/schedule.yml       schedule rows (edit this to update the program)
index.html               Home page
call-for-papers.html     Call for Papers page
schedule.html            Schedule page
speakers.html            Invited Speakers page
organizers.html          Organizers page
404.html                 Not-found page
original-google-sites-embeds/   your original banner.html/schedule.html,
                                 kept for reference only, not published
```

## 1. Adding invited speaker / organizer photos, affiliations & links

This is the part you said you'd fill in yourself. Everything is driven by
two simple YAML files — no HTML editing needed:

- `_data/speakers.yml`
- `_data/organizers.yml`

Each person is a block like:

```yaml
- name: "Sherry Yang"
  affiliation: "NYU Courant / Google DeepMind"
  url: "https://sherryy.github.io/"
  image: /assets/images/placeholder-avatar.svg
```

To add a real photo:

1. Save the photo (square photo works best, e.g. 400×400px) into
   `assets/images/speakers/` (or `assets/images/organizers/`), e.g.
   `assets/images/speakers/sherry-yang.jpg`.
2. Change that person's `image:` line to point at it:
   `image: /assets/images/speakers/sherry-yang.jpg`
3. Update `affiliation`/`url` (or `title`/`url` for organizers) if anything
   needs to change.

I pre-filled both files with the names/affiliations/personal-page links that
were already public on your Google Sites page, so you don't have to retype
them — you only need to swap in real photos. Add, remove, or reorder people
by adding/removing `- name: ...` blocks.

Until you add real photos, every card shows a generic gray placeholder
avatar (`assets/images/placeholder-avatar.svg`) so nothing looks broken.

## 2. Editing the schedule

Edit `_data/schedule.yml`. Each row is:

```yaml
- time: "8:40–9:10"
  event: "Invited talk 1"
  type: talk   # one of: break | talk | session (controls the row color)
```

## 3. Editing the Call for Papers / key dates

The submission deadline says OpenReview will be used, but no link was
published yet on the original site — I left a highlighted "TODO" callout
box on `call-for-papers.html`. Once you have the OpenReview submission link,
open that file and replace the placeholder link.

## 4. Publishing to GitHub Pages

1. Create a new GitHub repository (if you haven't already).
   - If you want the site at `https://<your-username>.github.io/`, name the
     repo exactly `<your-username>.github.io`.
   - If you want it at `https://<your-username>.github.io/<repo-name>/`,
     name it anything, e.g. `PTA_new`, and then open `_config.yml` and set:
     ```yaml
     baseurl: "/PTA_new"
     ```
     (must match your repo name exactly, case-sensitive).
2. Push this folder's contents to that repo's default branch (`main`):
   ```bash
   git init
   git add .
   git commit -m "Migrate PTA workshop site from Google Sites"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repo-name>.git
   git push -u origin main
   ```
3. On GitHub: go to the repo → **Settings → Pages** → under "Build and
   deployment", set **Source: Deploy from a branch**, branch: `main`,
   folder: `/ (root)` → **Save**.
4. Wait a minute or two, then visit the URL GitHub shows you on that same
   Pages settings screen.

Every time you `git push` new changes (e.g. after adding photos), GitHub
Pages automatically rebuilds the live site within a minute or two.

## 5. (Optional) Preview locally before pushing

Requires [Ruby](https://www.ruby-lang.org/) installed once.

```bash
gem install bundler
bundle install
bundle exec jekyll serve
```

Then open http://localhost:4000 in your browser. Stop with `Ctrl+C`.

## 6. What got carried over from Google Sites

- Home page: workshop description + key dates (from the Home page).
- Call for Papers: submission format + timeline (from the CFP page).
- Invited Speakers & Organizers: names, affiliations/titles, and personal
  page links (scraped from your live Home page) — photos are placeholders,
  see section 1 above.
- Schedule: your draft table design/rows from `schedule.html`
  (the actual Google Sites Schedule page was still empty, so these are the
  same placeholder rows you had designed — edit `_data/schedule.yml` once
  the real program is set).
- Visual design (colors, fonts, hero banner, schedule table styling) is
  carried over from your `banner.html` / `schedule.html` embed files, now
  kept in `original-google-sites-embeds/` for reference.

## Things I wasn't sure about — please double check

- **Contact email**: using `pta.workshop2026@gmail.com` from the original
  site (set in `_config.yml` → `contact_email`).
- **OpenReview link**: not published yet on the original site — placeholder
  left in `call-for-papers.html`.
- **Repo type / baseurl**: see step 1 in "Publishing to GitHub Pages" above
  — I don't know your GitHub username or whether this will be a user site
  or project site, so double check `_config.yml`'s `baseurl` before you go
  live.
