# learning-german

My German course, built with [KB4IT](https://github.com/t00m/KB4IT) 0.12.0 and the [deutschkurs](https://github.com/t00m/kb4it-theme-deutschkurs) theme 0.3.0. Translations are in English.

Site: https://t00m.github.io/learning-german/

## Layout

- `source/`: course entries, one Markdown file each. Photos go in `source/resources/photos/`.
- `config/deutschkurs.json`: settings for the incremental build.
- `config/deutschkurs_force_mode.json`: the same settings with `"force": true`.
- `docs/`: the generated site, served by GitHub Pages.
- `var/`: KB4IT build state (cache, database, logs).

## Builds

GitHub Actions builds the site and commits `docs/` and `var/`:

- `update-course-incremental.yml` runs when `source/` changes.
- `update-course-force.yml` runs when `config/` or a workflow changes, and rebuilds every page.

Both can also be started by hand from the Actions tab. The KB4IT and theme versions are set in `env` at the top of each workflow.

## Local build

```bash
uv tool install "git+https://github.com/t00m/KB4IT@0.12.0"
kb4it install-theme https://github.com/t00m/kb4it-theme-deutschkurs/releases/download/v0.3.0/deutschkurs-0.3.0.zip
kb4it build config/deutschkurs.json
```
