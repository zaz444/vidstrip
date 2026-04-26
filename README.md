# VidStrip

Batch convert MP4 files to MP3 in the browser — rename, convert, download as ZIP.

## Deploy to Netlify

1. Push this folder to a GitHub repo
2. Go to [netlify.com](https://netlify.com) → **Add new site → Import from Git**
3. Select your repo — no build command needed, publish directory is `/` (root)
4. Click **Deploy** — done!

The `netlify.toml` file automatically sets the required security headers for FFmpeg.wasm to work (`Cross-Origin-Opener-Policy` and `Cross-Origin-Embedder-Policy`).

## Local Testing

Open `index.html` directly in **Chrome or Edge**. Firefox may block SharedArrayBuffer without the correct headers, so use Netlify or a local server like:

```bash
npx serve .
```

## Features
- Drag & drop or multi-select MP4 files
- Rename each output file before converting
- Converts entirely in the browser — nothing is uploaded
- Downloads all MP3s in a single ZIP

## Tech
- [FFmpeg.wasm](https://github.com/ffmpegwasm/ffmpeg.wasm) — in-browser conversion
- [JSZip](https://stuk.github.io/jszip/) — ZIP generation
- Vanilla HTML/CSS/JS — no framework, no build step
