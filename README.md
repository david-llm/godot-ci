# godot-ci

Shared GitHub Actions workflow that exports a Godot project for the web and deploys it to GitHub Pages.

## Add a game

1. Copy [`examples/deploy-web.yml`](examples/deploy-web.yml) into the game repo at `.github/workflows/deploy-web.yml`.
2. Set `godot-version` to the exact version your editor uses (e.g. `4.7.2`). The export templates must match it.
3. Commit `export_presets.cfg` with a Web preset. Its name must match `export-preset` (default `Web`).
4. In the game repo, go to **Settings → Pages → Source** and choose **GitHub Actions**.

Every push to `main` then builds and deploys to `https://david-llm.github.io/<repo>/`.

## Inputs

| Input | Default | Description |
|---|---|---|
| `godot-version` | (required) | Godot version, e.g. `4.7.2` |
| `release-flavor` | `stable` | `stable`, `rc1`, `beta2`, ... |
| `project-path` | `.` | Folder containing `project.godot` |
| `export-preset` | `Web` | Name of the Web export preset |
| `debug` | `false` | Use `--export-debug` |

## Notes

- Single-threaded exports (the default since Godot 4.3) need no special headers and run on Pages as is.
- For Thread Support, turn on **Progressive Web App → Enable** and **Ensure Cross Origin Isolation Headers** in the game's export preset. GitHub Pages can't send COOP/COEP headers itself.
- Public game repos can only call this workflow while this repo is public.
- Changes here reach every game on its next push. To control when a game picks up changes, tag releases (e.g. `v1`) and point callers at `@v1`.
