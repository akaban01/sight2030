# sight2030.com

The landing page for the sight2030 workshop — a single static `index.html`
served by GitHub Pages.

## Editing the app list

The cards on the homepage are **not** hardcoded in `index.html`. They are read
at page load from [`data/apps.json`](data/apps.json), so adding, removing or
reordering an app means editing that one file.

### With Pages CMS (no code)

1. Go to [app.pagescms.org](https://app.pagescms.org) and sign in with GitHub.
2. Grant it access to this repository and open it.
3. Pick **Apps** in the sidebar — every card is a row you can edit, reorder by
   dragging, add or delete.
4. Save. Pages CMS commits to this repo, GitHub Pages redeploys, and the
   homepage picks up the change.

The form is defined by [`.pages.yml`](.pages.yml). Cards appear on the page in
the same order they appear in the list.

### By hand

Edit `data/apps.json` directly. Each entry looks like this:

```json
{
  "name": "Prism QR Studio",
  "url": "https://qr.sight2030.com/",
  "description": "A free, frontend-only QR code generator …",
  "accent": "#22d3ee",
  "icon": "qr",
  "status": "live",
  "hidden": false
}
```

| Field | Notes |
| --- | --- |
| `name` | Card heading. |
| `url` | Full link. The card displays the domain, derived from this. |
| `description` | One or two sentences. |
| `accent` | Hex colour for the icon tile, glow and hover border. Invalid values fall back to the theme default. |
| `icon` | One of the built-in icons below. Anything else falls back to `globe`. |
| `status` | `live`, `beta` or `soon`. |
| `hidden` | `true` keeps the entry in the file but off the page. |

Available icons: `beads`, `dumbbell`, `document`, `checklist`, `image`, `qr`,
`chart`, `calendar`, `home`, `layout`, `globe`, `book`, `clock`, `chat`,
`folder`, `sparkle`. They are defined in the `ICONS` map at the bottom of
`index.html` — add a new one there if you need a shape that isn't listed.

## Running locally

`data/apps.json` is loaded with `fetch`, which the browser blocks over
`file://`. Serve the folder instead:

```sh
python3 -m http.server 8000
```

Then open <http://localhost:8000>.
