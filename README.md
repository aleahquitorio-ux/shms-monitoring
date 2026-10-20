# Server Health Monitoring System (SHMS)

SHMS is a browser-based monitoring website with user registration/login, an administrator dashboard, device management, health history, and a consent-based Windows monitoring agent. The website itself is not a desktop/mobile application.

## Requirements

- Node.js LTS: https://nodejs.org/en/download
- npm (included with the Node.js installer)

## Run the website locally

1. Extract this folder.
2. Open a terminal in the `systemmonitoring` folder.
3. Install backend dependencies: `npm install` (PowerShell users can use `npm.cmd install`).
4. Start the server: `npm start` (PowerShell users can use `npm.cmd start`).
5. Open `http://localhost:3000`.

The public home page explains the monitoring setup and links to the official Node.js download and the SHMS Windows agent ZIP.

## Create an administrator account

Run `npm run create-admin` (PowerShell: `npm.cmd run create-admin`) and follow the prompts. Then use the Administrator login link on the website. Do not use the regular user login for an admin account.

## Set up monitoring on a Windows computer

1. Install Node.js LTS from the official Node.js website.
2. From the SHMS home page, download and extract `shms-windows-agent.zip`.
3. In PowerShell, open the extracted agent folder and run `npm.cmd install`.
4. Register a device in SHMS. Copy the agent command shown after registration and run it in the extracted agent folder. The command should start with `node agent.js --server ... --token ...`.
5. Read the consent prompt on the target computer and type `YES` only if you authorize monitoring. The agent sends supported CPU, RAM, disk, uptime, OS, and CPU information every 10 seconds. Press Ctrl+C to stop it.

For a computer on the same machine as the server, `http://localhost:3000` can be used. For a different computer, use the server computer's reachable LAN address or deployed HTTPS URL. `localhost` always means the current computer, not a remote server. Keep pairing tokens private.

## Admin dashboard

The administrator dashboard displays device counts, average metrics from online agents, recent performance samples collected during the current dashboard session, device details, registered devices, and recent alerts. Metrics are shown as unavailable until an authorized agent reports them; the website does not fabricate readings.

## Production note

Before exposing SHMS to the internet, deploy behind HTTPS, set a strong `SESSION_SECRET`, configure trusted proxy handling as appropriate, and review session, authentication, and device-token security. Local development is not production hardening.
