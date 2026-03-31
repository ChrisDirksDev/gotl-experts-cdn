# gotl-experts-cdn

Static expert directory data for the gotl **expert-directory** component, served via [jsDelivr](https://www.jsdelivr.com/) from GitHub.

## Contents

- `data/experts.json` — JSON array of expert objects (`name`, `role`, `focusTags`, `location`, `details`, `bio`, `footerTags`, `image`, `bookUrl`, `linkedinUrl`, `email`, `openUrl`). Same shape as `DEFAULT_EXPERTS` in the component’s `script.js`.
- `admin/index.html` — browser editor for that JSON (download or copy the result and replace `data/experts.json` in git).

## Editing data locally

The admin UI loads `data/experts.json` via `fetch`, so open it over HTTP from the **repository root** (not as a `file://` URL). For example:

```bash
python3 -m http.server 8080
```

Then open [http://localhost:8080/admin/](http://localhost:8080/admin/). After editing, use **Download JSON** or **Copy JSON** and overwrite `data/experts.json` before you commit.

## jsDelivr URLs

After this repo is public on GitHub, replace `USER`, `REPO`, and the ref as needed.

**Latest on default branch** (e.g. `main`):

```text
https://cdn.jsdelivr.net/gh/USER/REPO@main/data/experts.json
```

**Pinned tag or commit** (recommended for production; avoids surprises when CDN/browser caches):

```text
https://cdn.jsdelivr.net/gh/USER/REPO@v1.0.0/data/experts.json
```

```text
https://cdn.jsdelivr.net/gh/USER/REPO@abc1234/data/experts.json
```

## Using with the component

1. Push this repository to GitHub (public).
2. On the directory root element, set `data-ghl-experts-json` to your jsDelivr URL, **or** set `window.__GHLEXPERTS_JSON_URL__` before the component script runs.
3. If the request fails or the payload is invalid, the component falls back to `window.__GHLEXPERTS__` or built-in defaults.

## Cache behavior

jsDelivr and browsers cache responses. When you update `experts.json`, publish a new **tag** or reference a new **commit SHA** in the embed URL so clients pick up the change predictably.
