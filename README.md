# DermaSense AI — Live deployment package

This is a deployable full-stack version of the original frontend demo. It includes an Express backend, secure server-side OpenAI integration, AI skin-care guidance with optional image input, a general AI assistant, product filters, browser-local profile/history, and a health check.

## Deploy online with Render (no localhost required for visitors)

1. Extract this ZIP and push the `DermaSense_Live` folder to a GitHub repository.
2. Sign in to Render and choose **New + → Web Service**, then connect that repository and select this project folder as the root directory if prompted.
3. Build command: `npm install`; Start command: `npm start`. Node 20 or newer is required. The included `render.yaml` documents these settings.
4. In Render's **Environment** settings, add:
   - `OPENAI_API_KEY` = your secret OpenAI API key
   - `OPENAI_MODEL` = `gpt-4.1-mini` (or a vision-capable model available to your account)
5. Deploy. Render provides an HTTPS URL. Open it and check `/api/health`; `aiConfigured` should be `true`.

You must supply your own OpenAI API key and have API billing/access enabled. Do **not** put the key in `public/js/app.js`, HTML, GitHub, or chat. Add it only to the host's secret environment-variable settings. Do not commit `.env`.

## Test locally (optional, not required for deployment)

```bash
cp .env.example .env
# edit .env and add your API key
npm install
npm start
```
Then open `https://dermasense-ai-1.onrender.com`

## API routes
- `GET /api/health` — server and AI-key configuration status (never returns the key)
- `GET /api/products` — example product list
- `POST /api/assistant` — JSON `{ "message": "..." }`
- `POST /api/analyze-skin` — multipart form with `concern`, `skinType`, optional `age`, and optional `photo`

## Important limits and privacy
- AI responses are general educational wellness information, not a diagnosis. Seek a dermatologist for concerning or persistent symptoms.
- Uploaded images are sent to the configured AI provider for processing. This app does not write them to disk or retain them in a server database; browser profile/history use LocalStorage on that device.
- Product names and prices are illustrative examples, not verified listings, live inventory, or medical endorsements.
- Add authentication, a database, a privacy notice/consent flow, monitoring, and stricter per-user quotas before a public production launch. Rate limiting here is a basic abuse-control layer, not a full production security system.
