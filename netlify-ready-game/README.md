# Hidden Impostor — Netlify-ready

A 2–8 player social deduction game with the original design and gameplay, now using a Netlify Function and Netlify Blobs for shared persistent room state. No always-on Node server is required.

## Drag-and-drop deploy

1. Extract `netlify-ready-game.zip`.
2. In Netlify, create a new site by deploying the extracted project folder (or drag the ZIP into the manual deploy area if your Netlify UI accepts ZIP uploads).
3. For this full-stack version, ensure Netlify processes the project build/functions. If your account's manual deploy workflow only uploads static files, connect the folder/repository for a deploy that runs Netlify Functions; static-only deploys cannot run the game backend.
4. Open the deployed site and create a room. Room state is stored in the `hidden-impostor-rooms` Netlify Blobs store.

## Local development

Requires Node.js 20+ recommended.

```bash
npm install
npm run dev
```

Netlify Dev emulates the Function and Blobs locally. Production room data is separate from the local development store.

## Technical notes

- Frontend assets: root `index.html`, `style.css`, `app.js`.
- Serverless API: `netlify/functions/game.ts`.
- Room reads request strong consistency; updates use ETag-based conditional writes (`onlyIfMatch`) with bounded retries to prevent concurrent room updates from silently overwriting each other. Room creation uses `onlyIfNew`.
- Room data persists in the site-wide Netlify Blobs store across function invocations and deploys.
- Clients poll the function once per second. This is lightweight HTTP polling, not WebSockets.
