# Computational Workshops

Source for the workshop site, built with Jekyll + Minimal Mistakes and deployed via GitHub Pages.

## Local development

### Environment setup

Requires conda. Create and activate the environment:

```bash
conda env create -f environment.yml
conda activate local_dev
bundle install
```

Then serve the site locally:

```bash
bundle exec jekyll serve
```

Site runs at `http://localhost:4000/workshops`.

### Reproducing the exact environment

A `conda-lock.yml` is provided for fully pinned, cross-platform reproducibility:

```bash
conda lock install conda-lock.yml
conda activate local_dev
bundle install
```

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