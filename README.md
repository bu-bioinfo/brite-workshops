# Computational Workshops

Source for the workshop site, built with Jekyll + Minimal Mistakes and deployed via GitHub Pages.

## Local development

```bash
bundle install
bundle exec jekyll serve
```

Site runs at `http://localhost:4000/workshops`.

## Adding a workshop

1. Create `_workshops/workshop-NN.md` using the existing file as a template.
2. Add a row to the table in `index.md`.
3. Add an entry under `Workshops` in `_data/navigation.yml`.

## Deployment

Pushes to `main` trigger the GitHub Actions workflow and deploy automatically.
Before first deploy: go to **Settings → Pages** and set the source to **GitHub Actions**.

## Configuration

Update `_config.yml`:
- `baseurl` — your repo name (e.g. `/workshops`)
- `url` — your GitHub Pages root (e.g. `https://your-org.github.io`)
