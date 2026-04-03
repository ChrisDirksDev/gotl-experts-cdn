# gotl-experts-cdn

Static expert directory data for the gotl **expert-directory** component, served via [jsDelivr](https://www.jsdelivr.com/) from GitHub.

## Contents

- `data/experts.json` — JSON array of expert objects (see **Schema** below). Same general shape as `DEFAULT_EXPERTS` in the component’s `script.js`; extend the component when you need `quote`, `heroImage`, `social`, or `media` in the UI.
- `admin/index.html` — browser editor for that JSON (download or copy the result and replace `data/experts.json` in git).

## Schema

Each item is a plain object. **All fields are optional for consumers** except that a useful card usually needs at least `name` and some display text.

### Core (existing)

| Field | Type | Notes |
| ----- | ---- | ----- |
| `name` | string | |
| `role` | string | |
| `location` | string | |
| `bio` | string | |
| `image` | string | Profile / card image URL |
| `bookUrl` | string | |
| `linkedinUrl` | string | Legacy top-level link; see `social.linkedin` |
| `email` | string | |
| `openUrl` | string | e.g. GOTL profile page |
| `focusTags` | string[] | |
| `details` | string[] | |
| `footerTags` | string[] | |

### Quote & hero

| Field | Type | Notes |
| ----- | ---- | ----- |
| `quote` | string | Short pull quote |
| `heroImage` | string | Larger header image; **`image`** remains the profile/card photo |

### `social` (optional object)

String URL per platform. **No key is required** — omit a key or leave its value empty when unused.

Supported keys (consumers / admin may expose any subset):

`instagram`, `facebook`, `twitter`, `tiktok`, `linkedin`, `youtube`, `threads`, `pinterest`, `bluesky`, `mastodon`, `github`, `snapchat`

If both `linkedinUrl` and `social.linkedin` exist, consumers may prefer `social.linkedin` and fall back to `linkedinUrl`.

### `media` (optional object)

```json
{
  "spotifyUrl": "",
  "youtube": {
    "channelUrl": "",
    "videoUrls": [],
    "reelUrls": []
  },
  "gallery": []
}
```

- `spotifyUrl`: one link (show, artist, episode, etc.).
- `youtube.channelUrl`: channel page.
- `youtube.videoUrls` / `youtube.reelUrls`: arrays of video or Shorts URLs.
- `gallery`: array of `{ "url": "…", "alt": "…" }` (`alt` optional / may be empty).

### Demo / placeholder data

The committed `experts.json` may use obvious placeholders (`example.com`, `picsum.photos`, `Demo City, ST`, `@example.com` emails) for local previews. Replace with real values before production.

## Editing data locally

The admin UI loads `data/experts.json` via `fetch`, so open it over HTTP from the **repository root** (not as a `file://` URL). For example:

```bash
python3 -m http.server 8080
```

Then open [http://localhost:8080/admin/](http://localhost:8080/admin/). After editing, use **Download JSON** or **Copy JSON** and overwrite `data/experts.json` before you commit.

## jsDelivr URLs

After this repo is public on GitHub, adjust the ref (`master`, tag, or commit SHA) as needed.

**Latest on default branch** (e.g. `master`):

```text
https://cdn.jsdelivr.net/gh/ChrisDirksDev/gotl-experts-cdn@master/data/experts.json
```

**Pinned tag or commit** (recommended for production; avoids surprises when CDN/browser caches):

```text
https://cdn.jsdelivr.net/gh/ChrisDirksDev/gotl-experts-cdn@v1.0.0/data/experts.json
```

```text
https://cdn.jsdelivr.net/gh/ChrisDirksDev/gotl-experts-cdn@abc1234/data/experts.json
```

## Using with the component

1. Push this repository to GitHub (public).
2. On the directory root element, set `data-ghl-experts-json` to your jsDelivr URL, **or** set `window.__GHLEXPERTS_JSON_URL__` before the component script runs.
3. If the request fails or the payload is invalid, the component falls back to `window.__GHLEXPERTS__` or built-in defaults.

## Cache behavior

jsDelivr and browsers cache responses. When you update `experts.json`, publish a new **tag** or reference a new **commit SHA** in the embed URL so clients pick up the change predictably.
