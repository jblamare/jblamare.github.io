# Jean-Baptiste Lamare

Personal website, live at [jblamare.github.io](https://jblamare.github.io).

It's a [Jekyll](https://jekyllrb.com/) site using the `jekyll-theme-minimal` theme, hosted on [GitHub Pages](https://pages.github.com/). Pushing to `master` rebuilds and redeploys the site automatically.

## Repository layout

| Path | Purpose |
| --- | --- |
| `index.md` | Main page content (Markdown) |
| `_config.yml` | Site title, theme, plugins, URL |
| `_layouts/default.html` | Page layout |
| `_includes/` | Reusable snippets (`projects.html`, `publications.html`) |
| `assets/css/style.scss` | Style overrides on top of the theme |
| `assets/img/` | Images and favicon |
| `assets/pdf/` | Resume (excluded from the sitemap) |
| `.well-known/` | Domain verification files (e.g. `atproto-did`) |
| `Gemfile` | Ruby dependencies |

## Testing locally

### Prerequisites

- Ruby (2.7+ recommended; 3.x works thanks to the `webrick` gem in the Gemfile)
- [Bundler](https://bundler.io/): `gem install bundler`

On macOS, the system Ruby is often too old or locked down. Consider installing a newer one with [Homebrew](https://brew.sh/), `rbenv`, or `asdf`.

### First-time setup

```bash
git clone https://github.com/jblamare/jblamare.github.io.git
cd jblamare.github.io
bundle install
```

### Run the site

```bash
bundle exec jekyll serve
```

Then open <http://localhost:4000>. The site rebuilds automatically when you edit files, so just refresh the browser.

Useful variations:

```bash
bundle exec jekyll serve --livereload   # auto-refresh the browser on changes
bundle exec jekyll serve --port 4001    # use a different port
bundle exec jekyll build                # build only; output goes to _site/
```

> **Note:** Changes to `_config.yml` are not picked up automatically. Stop the server (`Ctrl+C`) and restart it.

### Troubleshooting

- **`cannot load such file -- webrick`**: run `bundle install` again; `webrick` is listed in the Gemfile.
- **Dependency or version errors**: run `bundle update github-pages` to pull in the versions GitHub Pages uses.
- **Port already in use**: stop the other process or use `--port`.
- `Gemfile.lock` and `_site/` are git-ignored, so don't worry about committing them.

## Pushing changes

1. Make your edits and check them locally (see above).
2. Review what changed:
   ```bash
   git status
   git diff
   ```
3. Commit and push:
   ```bash
   git add -A
   git commit -m "Describe your change"
   git push origin master
   ```
4. GitHub Pages rebuilds automatically. This usually takes under a minute or two. Check progress under the repo's **Actions** tab (the `pages-build-deployment` workflow), then reload [jblamare.github.io](https://jblamare.github.io). You may need a hard refresh (`Cmd/Ctrl+Shift+R`) to bypass the browser cache.

If the build fails, the Actions tab shows the error. The most common causes are malformed YAML front matter or a broken Liquid tag in a layout or include.

## Common edits

- **Update the bio or text**: edit `index.md`.
- **Add or update publications/projects**: edit `_includes/publications.html` or `_includes/projects.html`.
- **Replace the resume**: overwrite `assets/pdf/resume_jblamare.pdf` keeping the same filename so existing links keep working.
- **Change the profile photo**: replace the file in `assets/img/` and update `logo:` in `_config.yml`.
- **Tweak styling**: edit `assets/css/style.scss`.