# Image Baler

**Web-ready image compression done fast — no software required.**

Batch compress hundreds of images in seconds — no uploads, no installs, nothing leaves your device.

Built by [Ramblin Jackson](https://ramblinjackson.com) for internal team and vendor use.

---

## What It Does

Image Baler is not a replacement for Photoshop or Lightroom — it's what you use *after* those tools. Once photos have been edited and approved, Image Baler gets them web-ready fast without anyone needing to open expensive software.

---

## Features

- **Bulk compression** — process dozens or hundreds of images at once
- **Folder import** — drag & drop a folder or use the native folder picker; subfolders are traversed automatically
- **Auto ZIP naming** — folder name is detected and pre-fills the ZIP filename field automatically
- **HEIC / iPhone support** — `.heic` and `.heif` files are auto-converted in-browser before compression
- **Output format** — export as JPEG, WebP, or PNG
- **Quality control** — slider from 10–100%, defaults to 60%
- **Max width presets** — choose from 300px to 2560px or enter a custom value
- **Custom ZIP name** — name your download before exporting
- **CSV log** — a `baler-log.csv` is included in every ZIP with original filename, output filename, file sizes, savings %, date and time
- **Live stats** — per-image before/after file size, % saved, and aggregate totals
- **Step-by-step instructions** — built into the UI for first-time users
- **100% private** — images never leave your device; everything runs locally in the browser

---

## How To Use It

1. **Drop your images** — drag a folder or individual images into the drop zone. Works with JPEG, PNG, WebP, and iPhone HEIC photos.
2. **Choose your settings** — select output format, max width, and quality. The defaults are optimized for web use — leave them as-is if unsure.
3. **Compress All** — hit Compress All and wait for images to finish. File size savings update in real time.
4. **Download your ZIP** — name your ZIP file, then hit Download ZIP. Compressed images and a log file are bundled together.

---

## How It Was Built

Image Baler is a single-file HTML application with no build step, no framework, and no backend. It deploys to any static file host.

### Libraries

| Library | Version | Purpose |
|---|---|---|
| [browser-image-compression](https://github.com/Donaldcwl/browser-image-compression) | 2.0.2 | Core JPEG/WebP/PNG compression via Canvas API |
| [heic2any](https://github.com/alexcorvi/heic2any) | 0.0.4 | Client-side HEIC → JPEG conversion for iPhone photos |
| [JSZip](https://stuk.github.io/jszip/) | 3.10.1 | Packages compressed images into a downloadable `.zip` |

### Architecture

Everything runs in the browser — no Node.js, no server, no API.

**Compression pipeline:**
1. User drops images or a folder onto the drop zone
2. Folder name is detected and pre-populates the ZIP filename field
3. For HEIC files, `heic2any` converts them to JPEG in-browser
4. `browser-image-compression` compresses each image using the Canvas API
5. On download, `JSZip` bundles all compressed images plus a `baler-log.csv` into a named `.zip`

**No localStorage, no cookies, no analytics.** State lives only in memory for the duration of the session.

### Branding

- **Primary color** — `#f19a4c` (RJ Orange)
- **Background** — `#091c2f` with `#112d49` (RJ Blue) wood grain SVG texture
- **Logo font** — [Oswald](https://fonts.google.com/specimen/Oswald)
- **UI font** — [Open Sans](https://fonts.google.com/specimen/Open+Sans)

---

## Deployment

Rename `index.html` before deploying.

### GitHub Pages

```bash
git init
git add .
git commit -m "init"
git remote add origin https://github.com/rj-lou/baler.git
git branch -M main
git push -u origin main
```

Enable Pages in repo **Settings → Pages → Deploy from branch: main**.

### Netlify

Drag and drop `index.html` at [app.netlify.com/drop](https://app.netlify.com/drop).

---

## Local Development

```bash
git clone https://github.com/rj-lou/baler.git
cd baler
open index.html
```

> Chrome or Edge recommended for full HEIC and folder drag-and-drop support.

---

## Browser Compatibility

| Feature | Chrome | Firefox | Safari | Edge |
|---|---|---|---|---|
| Compression | ✅ | ✅ | ✅ | ✅ |
| Folder drag & drop | ✅ | ✅ | ✅ | ✅ |
| Folder picker | ✅ | ✅ | ✅ | ✅ |
| HEIC conversion | ✅ | ✅ | ✅ | ✅ |
| ZIP download | ✅ | ✅ | ✅ | ✅ |

> HEIC conversion is CPU-heavy on large batches. For 100+ iPhone photos, expect 2–4 minutes depending on device.

---

## Roadmap

- [ ] Preserve subfolder structure inside ZIP
- [ ] Per-image quality override
- [ ] Before/after preview comparison
- [ ] Individual image download without zipping
- [ ] Dark/light mode toggle

---

## License

Proprietary — built for internal use at [Ramblin Jackson](https://ramblinjackson.com).
