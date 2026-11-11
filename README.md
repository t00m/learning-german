# learning-german

My German course, built with [KB4IT](https://github.com/t00m/KB4IT) 0.12.0 and the latest release of the [deutschkurs](https://github.com/t00m/kb4it-theme-deutschkurs) theme. Translations are in English.

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

Both can also be started by hand from the Actions tab.

### Theme version

Every build installs the latest deutschkurs release and writes its version to `var/deutschkurs-theme.version`:

- When the latest release differs from that file, the incremental workflow forces a full build.
- The incremental workflow also runs every hour. It builds only when a new theme release is out.
- If a release does not support the KB4IT version in `KB4IT_REF`, KB4IT stops the build and the run fails.

## Local build

```bash
uv tool install "git+https://github.com/t00m/KB4IT@0.12.0"
v=$(gh release view --repo t00m/kb4it-theme-deutschkurs --json tagName --jq .tagName)
kb4it install-theme "https://github.com/t00m/kb4it-theme-deutschkurs/releases/download/$v/deutschkurs-${v#v}.zip"
kb4it build config/deutschkurs.json
```
