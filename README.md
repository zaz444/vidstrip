# VidStrip

Batch convert MP4 files to MP3 in the browser — rename, convert, download as ZIP.

## Deploy to GitHub Pages

1. Push this folder to a GitHub repo
2. Go to **Settings → Pages → Source** and select **Deploy from a branch**
3. Choose `main` (or `master`) and `/ (root)` → click **Save**
4. Your site will be live at `https://<your-username>.github.io/<repo-name>/`

> **How cross-origin isolation works on GitHub Pages:**  
> FFmpeg.wasm needs `SharedArrayBuffer`, which requires `Cross-Origin-Opener-Policy` and  
> `Cross-Origin-Embedder-Policy` headers. GitHub Pages can't set custom headers, so  
> `coi-serviceworker.js` is registered on first load to inject them via a Service Worker.  
> On the very first visit the page reloads once automatically — that's normal.

## Deploy to Netlify (also supported)

1. Push this folder to a GitHub repo
2. Go to [netlify.com](https://netlify.com) → **Add new site → Import from Git**
3. Select your repo — no build command needed, publish directory is `/` (root)
4. Click **Deploy** — done!

On Netlify, the `netlify.toml` sets the required headers natively and the service worker is registered but effectively a no-op.

## Local Testing

Serve with a local server (opening `index.html` directly won't work due to service worker scope):

```bash
npx serve .
```

Then open `http://localhost:3000` in **Chrome or Edge**.  
Firefox may block SharedArrayBuffer without the correct headers.

## Files

| File | Purpose |
|------|---------|
| `index.html` | Main app — all UI and conversion logic |
| `coi-serviceworker.js` | Injects COOP/COEP headers for GitHub Pages compatibility |
| `netlify.toml` | Sets headers natively for Netlify deployments |

## Features
- Drag & drop or multi-select MP4/MOV/MKV/WEBM/AVI files
- Rename each output file before converting
- Converts entirely in the browser — nothing is uploaded
- Downloads all MP3s in a single ZIP

## Tech
- [FFmpeg.wasm](https://github.com/ffmpegwasm/ffmpeg.wasm) — in-browser conversion
- [JSZip](https://stuk.github.io/jszip/) — ZIP generation
- [coi-serviceworker](https://github.com/gzuidhof/coi-serviceworker) — GitHub Pages COOP/COEP headers
- Vanilla HTML/CSS/JS — no framework, no build step
