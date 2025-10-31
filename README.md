# P2P Planning Poker

Live demo: https://cdekok.github.io/p2p-pp

A lightweight, peer‑to‑peer Planning Poker tool for agile teams. It runs entirely in your browser and connects participants directly using WebRTC (via PeerJS). No accounts, servers, or deployments required beyond static hosting.

## Features
- Peer‑to‑peer connections (no central server for messages)
- Create or join a session using a simple Session ID
- Choose your display name and optional moderator role
- Vote using common Planning Poker values (e.g., Fibonacci)
- Reveal votes together and see a quick summary
- Clean, responsive UI

## How it works
The app is a single static page (index.html) that uses PeerJS to establish direct WebRTC data connections between participants. One peer acts as the "host" that others connect to via its Peer ID/session ID. Messages (join, vote, reveal, reset) flow between peers in real time.

## Getting started (local)
You can open the app directly from the filesystem or run it with a simple static server.

Option A — open the file:
1. Clone/download this repository
2. Double‑click `index.html` to open it in your browser

Option B — serve locally:
- Using Python:
  - Python 3: `python3 -m http.server 8080`
  - Then open http://localhost:8080/index.html
- Using Node (serve):
  - `npx serve .`
  - Then open the printed URL (e.g., http://localhost:3000)

Note: Some browsers apply stricter rules for `file://` origins. If anything doesn’t work when opening the file directly, use a local server.

## Usage
1. Open the app (locally or the demo link above).
2. Enter a display name.
3. Create a new session to get a Session ID, or enter an existing ID to join.
4. Share the Session ID with your team.
5. Everyone selects a card/value but votes remain hidden until revealed.
6. Moderator reveals votes; discuss results; reset to start a new round.

## Tech stack
- HTML, CSS, JavaScript (no framework)
- [PeerJS](https://peerjs.com/) for WebRTC data channels

## Project structure
- `index.html` — the entire application (markup, styles, and scripts)

## Deployment
Because it’s a single static file, you can host it on any static hosting service (e.g., GitHub Pages, Netlify, Vercel, S3).

The public demo is deployed to GitHub Pages:
- https://cdekok.github.io/p2p-pp

## Contributing
Issues and pull requests are welcome. For larger changes, please open an issue first to discuss your ideas.


## License
This project is licensed under the MIT License. See the LICENSE file for details.
