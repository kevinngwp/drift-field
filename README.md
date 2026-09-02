# Drift Field

Static site source.

- `index.html` — the page (references `wordmark.png` as a relative path)
- `wordmark.png` — the wordmark currently used (matches what's live on Vercel today)
- `wordmark-highres.png` — a sharper 4x-scale export of the same wordmark, in case you want less pixelation on retina screens. To use it, either rename it to `wordmark.png` (replacing the current one) or edit the `src="wordmark.png"` reference in `index.html`.

## Deploy
Any static host works (Vercel, Netlify, GitHub Pages, etc.) — just serve this folder as-is.
