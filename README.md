# Academic homepage

A small, plugin-free Jekyll site for GitHub Pages with four pages:

| Page | Edit content in |
|---|---|
| Home (`/`) | `index.md` (about, research interests, news) and the `author` / `links` block in `_config.yml` |
| Research (`/research/`) | interests text in `research.md`, publications in `_data/publications.yml` |
| Education & Experience (`/cv/`) | `_data/cv.yml` |
| Teaching (`/teaching/`) | intro text in `teaching.md`, courses in `_data/teaching.yml` |

## Customising

- **Name, position, email, links:** `_config.yml`.
- **Photo:** put a square image in `assets/img/` (e.g. `me.jpg`) and set `author.photo: /assets/img/me.jpg`.
- **CV PDF:** put it in `assets/files/` and set `author.cv_pdf: /assets/files/cv.pdf` — a download button appears on the CV page.
- **Colours and fonts:** variables at the top of `assets/css/style.css`. Changing `--accent` re-themes the site. Dark mode follows the visitor's system setting.
- **Maths:** MathJax is on (`mathjax: true`), so `$x^2$` and `$$ \int f $$` work in any Markdown page.
- **Navigation:** `_data/navigation.yml`.

## Previewing locally

With Ruby and Jekyll installed (`gem install jekyll`):

```bash
jekyll serve
```

Then open http://localhost:4000.
