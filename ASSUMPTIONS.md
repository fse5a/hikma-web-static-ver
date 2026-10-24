# Static Deployment Assumptions

- This build is intentionally frontend-only. There is no Node runtime, API route, private environment variable, database, identity provider, or server-side storage in the deployed app.
- `voices.json` and `test-sentences.json` are public static assets loaded with same-origin URLs relative to `document.baseURI`. Never put API keys, private recordings, or confidential data in these files.
- The only activation path is a clearly labeled local demo. Any code check in browser JavaScript or a public JSON file can be bypassed, so this is not product activation or authentication.
- Automatic cloud translation, Azure/LLM speech, URL fetching, and ISBN catalog lookup are unavailable because secrets and safe outbound-fetch controls require a trusted service. Manual translations and device speech remain available.
- Friend voice entries have `consent: false` and are metadata only. This static build does not synthesize cloned voices. Do not upload recordings without explicit consent and legal review.
- The app uses localStorage and IndexedDB. User libraries, recordings, and settings do not sync between browsers or devices.
- Browser-native `TextDetector` may provide local OCR in supported browsers; it is not broadly available and no OCR success is claimed when absent.
- Hosting works under a site path prefix when scripts and JSON stay beside `index.html`. Use an HTTP static preview; browsers may block `fetch()` from `file://` pages.
- Physical TalkBack, VoiceOver, NVDA, Android audio timing, axe-core combinations, and human voice-quality review still require separate verification.