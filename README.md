# Inai — Emergency Communication Prototype

A hackathon demo featuring a mobile SOS interface, press-and-hold voice messages, a desktop command center, real-time Socket.IO updates, emergency triage, simulated vehicle updates, and a controllable multi-hop mesh visualization.

## Run locally

Requirements: Node.js 18+.

```powershell
npm install
npm start
```

Open:
- Mobile app: http://localhost:3000
- Desktop command center: http://localhost:3000/dashboard

To open on a phone on the same Wi-Fi, find your laptop's LAN IPv4 address with `ipconfig`, then visit `http://YOUR-LAPTOP-IP:3000` on the phone. This requires the laptop and phone to share a network and Windows Firewall to permit Node.js. Browser microphone/location permissions may require HTTPS on remote deployments; localhost is generally treated as a secure context.

## Demo flow
1. Open the mobile app and dashboard in separate browser tabs/devices.
2. Tap **Send SOS** once to send a text SOS.
3. Press and hold **Hold to record** to record audio; release to stop and upload.
4. In the dashboard, toggle a mesh node offline and send a demo alert to show rerouting or delivery failure.
5. Change a response vehicle's status to show the client update.
6. Use demo controls to seed/reset incidents.

## Important limitations
- The mesh is a graph-based simulation, not real radio/phone-to-phone mesh networking.
- Browser clients connect to the Node.js server via Socket.IO. If that connection is lost, the server cannot receive new alerts.
- Geolocation is real only when the user grants browser permission. Demo devices use labeled sample coordinates.
- Battery readings are browser-dependent and commonly unavailable; the UI labels simulated values.
- Vehicle movement and ETA are simulated. No real emergency service is contacted.
- The built-in triage is a transparent rules-based demo, not a truth detector. Human review is required.
- JSON persistence is suitable only for a local prototype. Uploaded audio and data may be lost on hosts with ephemeral storage. Use persistent storage and appropriate access controls before real deployment.
- Do not use this demo for real emergencies.

## GitHub
```powershell
git init
git add .
git status
git commit -m "Initial commit: Inai emergency prototype"
git branch -M main
git remote add origin YOUR_GITHUB_REPOSITORY_URL
git push -u origin main
```
Replace the URL with the repository URL from GitHub. For later changes:
```powershell
git add .
git commit -m "Describe your changes"
git push
```

## Deploying
Deploy as a Node.js web service on a provider such as Render. Build command: `npm install`; start command: `npm start`. The server reads `PORT` from the environment. Use HTTPS for browser microphone and geolocation access on deployed URLs. Configure persistent storage before expecting JSON records or audio uploads to survive restarts. Never commit secrets, real locations, or private voice recordings.


## Master SOS broadcast
Open the command center at `/dashboard`, select **SOS Broadcast**, enter a message, and send it. The server sends a real-time Socket.IO event to open mobile clients registered to online demo devices, and the command-center browser also shows the popup. This is a connected software demo: it does not deliver alerts when devices have no network connection and does not contact emergency services.

## Dashboard pages
Use the sidebar to open separate Overview, Incidents, Mesh network, Connected devices, and Response units views. The circular mobile SOS button supports tap-to-send and press-and-hold voice recording.
