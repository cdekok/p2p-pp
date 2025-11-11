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

## Connectivity on restrictive networks (NAT/Firewall)
WebRTC usually connects peer‑to‑peer using STUN servers to learn public addresses. On some corporate, hotel, or carrier‑grade NAT networks, direct connections fail unless a TURN relay is available.

This project now supports configurable ICE (STUN/TURN) servers without rebuilding code.

- Defaults: multiple public STUN servers are used automatically.
- TURN: you can supply your own TURN server via URL parameters or persistent local storage.

### Quick usage with URL parameters
Share a link that includes your room and TURN info so everyone inherits the same connectivity settings:

- `turn`: TURN host with optional port, e.g. `turn=turn.example.com:3478`
- `turnUser`: TURN username
- `turnPass`: TURN password
- `ice`: URI‑encoded JSON array of ICE servers if you want full control (advanced)

Example URL:
```
https://your-host/index.html?room=ABC123&turn=turn.example.com:3478&turnUser=myuser&turnPass=mypassword
```

Advanced `ice` override example:
```
https://your-host/index.html?room=ABC123&ice=%5B%7B%22urls%22%3A%22stun%3Astun.cloudflare.com%3A3478%22%7D%2C%7B%22urls%22%3A%22turn%3Aturn.example.com%3A3478%22%2C%22username%22%3A%22myuser%22%2C%22credential%22%3A%22mypassword%22%7D%5D
```

Notes:
- The app will also persist these values in `localStorage` so you don’t need to re‑append them every time.
- The share link shown in the UI will keep only the relevant parameters: `room`, `turn`, `turnUser`, `turnPass`, `ice`.

### Running your own TURN (coturn)
You can deploy a TURN server using [coturn](https://github.com/coturn/coturn). Minimal example on a public VM:

1. Install coturn (Ubuntu):
```
sudo apt-get update && sudo apt-get install -y coturn
```
2. Create `/etc/turnserver.conf` (basic static credentials):
```
listening-port=3478
tls-listening-port=5349
realm=example.com
fingerprint
no-cli
log-file=/var/log/turnserver/turn.log
simple-log
user=myuser:mypassword
# Recommended for WebRTC
no-udp-relay
no-tcp-relay
# If behind NAT, set your public IP
# external-ip=YOUR_PUBLIC_IP
```
3. Open firewall ports: UDP/TCP 3478, TCP 5349 (TLS), and ensure the VM has a public IP.
4. Start coturn:
```
sudo systemctl enable coturn
sudo systemctl start coturn
```
5. Use the app with:
```
?turn=turn.example.com:3478&turnUser=myuser&turnPass=mypassword
```

Tips:
- Browsers prefer `turns:` (TLS) on 5349 when available. If your TURN supports TLS, the app will attempt both `turn:` and `turns:` automatically.
- The site should be served over HTTPS for best WebRTC compatibility.
- Some networks block UDP; TURN over TCP/TLS is the fallback for such cases.

### Troubleshooting
- If participants can’t see each other, try adding a TURN server as described above.
- Open DevTools Console: you should see `[RTC] Using rtcConfig: ...` with the ICE servers in use.
- Ensure both sides load the app with the same connectivity parameters (use the share URL from the app after creating a room).
- Corporate proxies/firewalls may still block WebRTC; in that case, only a properly reachable TURN relay will work.

## Contributing
Issues and pull requests are welcome. For larger changes, please open an issue first to discuss your ideas.

## License
This project is licensed under the MIT License. See the LICENSE file for details.
