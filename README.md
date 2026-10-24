# Hikma Reading App

Hikma is a no-build static website. It does not require `server.js`, a Node runtime, an API server, or environment variables to run after deployment. Stories, preferences, recordings, and cached files remain in the browser's local storage/IndexedDB.

## Deploy

### GitHub Pages

Publish the repository root (or the `main` branch root) as the Pages source. Keep `index.html`, `settings.js`, `public-data.js`, `restored-features.js`, `voices.json`, and `test-sentences.json` together. The app resolves scripts and JSON relative to its current URL, including a repository subpath such as `/project-name/`.

### Vercel

Import the repository as a static site. Use no build command and set the output directory to `.`. Do not add environment variables or secrets to the browser build.

### Local preview

Use any static file server, for example Python's built-in server:

```powershell
py -m http.server 8000
```

Then open `http://localhost:8000`. Direct `file://` opening may block JSON fetches in browsers, so use a static HTTP preview.

## Public JSON

`public-data.js` fetches only same-origin `voices.json` and `test-sentences.json`, using `document.baseURI` so deployments under a path prefix work. Both files are public and must never contain API keys, private recordings, or other secrets. Friend voice entries are disabled placeholders; the static app uses device speech only.

## Static-mode limitations

- The activation screen permits the explicit demo flow only. A PIN/code embedded in static files cannot be securely validated; real product activation needs a separate authenticated service.
- Translation is manual. Cloud translation and neural speech were removed because browser JavaScript cannot safely hold Azure/LLM secrets.
- URL import, ISBN catalog lookup, server-side OCR, account sync, parent PIN, and friend-voice synthesis require services that are not part of this static deployment. Device-native image OCR is offered only when the browser implements `TextDetector`.
- Local stories and settings do not sync between devices. Browser speech quality and available voices vary by device.

## Tests

Node is optional for hosting. For development checks, use Node 20+ and run:

```powershell
npm test
```

The tests cover settings migration and the bilingual speech quality-set structure. The quality sentences are available in the voice settings for local device-speech review; human scoring is still required.

See [ACCESSIBILITY-TESTING.md](ACCESSIBILITY-TESTING.md) for the TalkBack, VoiceOver, NVDA, and planned axe-core checklist. No full assistive-technology or axe audit is claimed.
