Hidden Impostor 🎭
A browser-based social-deduction party game for 2–8 players. Players join a room using a short room code, receive secret words, submit clues, discuss, and vote to identify the impostor(s).
Features
- Create a room and invite players with a room code
- Supports 2–8 players
- Secret roles and related secret words
- Turn-based clues, discussion, private voting, and results
- Scoring, multiple rounds, and rematches
- Netlify Function backend; no always-running Node.js server
- Netlify Blobs room storage with strong-consistency reads and conditional writes
Project structure
.
├── index.html
├── app.js
├── style.css
├── netlify.toml
├── package.json
├── package-lock.json
└── netlify/
    └── functions/
        └── game.ts
Deploy to Netlify
Important: This is a full-stack Netlify site. A static-only drag-and-drop upload does not build/deploy the serverless Function. Deploy through a Git repository connected to Netlify or through Netlify CLI.

1. Push this project to a GitHub repository with index.html, app.js, style.css, netlify.toml, and package.json at the repository root.
2. In the Netlify dashboard, choose Add new project → Import an existing project and select the repository.
3. Use the build settings from netlify.toml (publish directory .; Functions directory netlify/functions). The configured build command is npm run build.
4. Deploy the site and wait for the Functions build to finish.
5. Open the deployed URL in two or more browser sessions and test room creation, joining, clues, voting, and rematches.
Netlify Blobs stores room data in the hidden-impostor-rooms store. Confirm the deployment succeeds and test multiplayer behavior before sharing the URL publicly.
Local setup
Requires a supported Node.js version and npm.
npm install
npx netlify-cli dev
Open the local URL printed by Netlify CLI. Local Blobs data is separate from production data.
Gameplay notes
- At least two players are required to start.
- The game supports up to eight players.
- One impostor is assigned in smaller rooms; two are assigned when six or more players participate.
- Players submit clues in turn, discuss, then vote privately.
- The client polls the backend periodically to sync room state; it does not use WebSockets.

## 🎮 Live Demo

Play Hidden Impostor online:
https://comforting-monstera-e84238.netlify.app/
Troubleshooting
- Dependency install fails: check the latest Netlify build log and ensure package.json and package-lock.json are committed together.
- Function not found: confirm netlify/functions/game.ts exists in the repository and netlify.toml is at the repository root.
- Room does not sync: test with the deployed Netlify URL in two separate browser sessions and check the Function logs in Netlify.
- Typing/input issue: hard-refresh the browser after deployment (Ctrl+Shift+R).
License
Add a license file if you plan to distribute or open-source this project. Until then, no license is specified.
