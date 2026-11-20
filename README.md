# QR Generator

A tiny, self-contained web app that generates QR codes from URLs and decodes QR codes from images.
No build step, no backend — a single `index.html`.

Live:
- https://qr.bconf.com (custom domain via `CNAME`)
- https://mikhail-angelov.github.io/qr/ (GitHub Pages)

## Features

**Generate tab**
- Type or paste a URL — a QR code is rendered instantly (error correction level H, 256×256)
- Download as PNG
- Copy the QR image to the clipboard
- Copy a ready `<img src="data:image/png;base64,…">` tag with the QR embedded

**Decode tab**
- Drop a PNG/JPG or pick it from disk
- The decoded text is shown; links are clickable and open in a new tab
- Copy the decoded text with one click

**Quick links**
- Preset chips under the input generate a QR in one tap
- `Redmi` → `https://mikhail-angelov.github.io/qr/`, so the app can be opened on the phone by scanning

## How it works

- `index.html` — markup, styles and logic in one file
- QR generation: [qrcodejs](https://cdn.jsdelivr.net/npm/qrcodejs@1.0.0/qrcode.min.js)
- QR decoding: [jsQR](https://cdn.jsdelivr.net/npm/jsqr@1.4.0/dist/jsQR.js)
- Both libraries are loaded from jsDelivr, so an internet connection is required

## Run locally

```bash
git clone https://github.com/mikhail-angelov/qr.git
cd qr
python3 -m http.server 8000
# open http://localhost:8000
```

Opening `index.html` directly via `file://` also works.

## Add a quick link

Add one line inside `<div class="presets" id="presets">` in `index.html`:

```html
<button class="chip" data-url="https://example.com">Name</button>
```

The click handler picks up every `.chip` with a `data-url` — no extra JavaScript needed.

## Deployment

Pushing to `master` triggers GitHub Pages; the site is published within a minute or two.
The custom domain is configured by the `CNAME` file (`qr.bconf.com`).
