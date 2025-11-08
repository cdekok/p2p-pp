# P2P Planning Poker

Live demo: https://cdekok.github.io/p2p-pp

A lightweight, peer‑to‑peer Planning Poker tool for agile teams. It runs entirely in your browser and connects participants directly using WebRTC (via Trystero). No accounts, servers, or deployments required beyond static hosting.

## Features
- Peer‑to‑peer connections (no central server for messages)
- Create or join a room using a simple Room ID
- Choose your display name
- Vote using common Planning Poker values (e.g., Fibonacci)
- Reveal votes together and see a quick summary
- Clean, responsive UI

## How it works
The app is a single static page (`index.html`) that uses [Trystero](https://github.com/dmotz/trystero) to establish direct WebRTC data connections between participants. Peers join the same "room" using a shared Room ID and exchange messages (join, vote, reveal, reset) in real time.

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
3. Create a new room to get a Room ID, or enter an existing Room ID to join.
4. Share the Room ID (or the full URL) with your team.
5. Everyone selects a card/value but votes remain hidden until revealed.
6. Reveal votes; discuss results; reset to start a new round.

## Tech stack
- HTML, CSS, JavaScript (no framework)
- [Trystero](https://github.com/dmotz/trystero) for WebRTC data channels

## Project structure
- `index.html` — main application (markup, scripts)
- `styles.css` — styles for the UI

## Deployment
Because it’s a static site, you can host it on any static hosting service (e.g., GitHub Pages, Netlify, Vercel, S3).

The public demo is deployed to GitHub Pages:
- https://cdekok.github.io/p2p-pp

## Contributing
Issues and pull requests are welcome. For larger changes, please open an issue first to discuss your ideas.

## License
This project is licensed under the MIT License. See the LICENSE file for details.
