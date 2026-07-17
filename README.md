# -NovaVoice-AI-Production-Grade-Gemini-Live-API-Voice-Agent-Platform
 NovaVoice AI — Production-Grade Gemini Live API Voice Agent Platform Ultra-low latency, real-time conversational AI voice platform powered by Gemini Live API, FastAPI, WebSockets, and modular voice infrastructure.
🚀 Step 0 — Clone the Repository
First, clone the repository locally:

git clone https://github.com/coder-irwin/voice_ai_agents_using-Gemini_live_api.git
Move into the project directory:

cd voice_ai_agents_using-Gemini_live_api
📦 Step 1 — Create Virtual Environment

Windows

python -m venv venv

venv\Scripts\activate
macOS / Linux

python3 -m venv venv

source venv/bin/activate
NovaVoice is an ultra-low latency, bidirectional streaming voice assistant that integrates the Gemini Live API (BidiGenerateContent WebSocket protocol) with Google Calendar for automated schedule checking and meeting booking.

This repository contains the production-ready full-stack core, split into:

Interactive Glassmorphic UI (Frontend): Manages user media devices, WebRTC audio streams, continuous WebSocket piping, active barge-in (interruption), and a visual visualizer orb.
Secure Python Gateway (Backend): Protects long-term OAuth keys (token.json) and handles standard API calendar queries.
🗺️ Architectural Flow
Here is how NovaVoice orchestrates real-time communication between your web browser, Google's Gemini Bidirectional WebSocket service, a local API bridge, and the Google Calendar API:

🗣️ User (Voice/Mic) 
       │
       ▼ (16kHz PCM Mono)
🖥️ Web Browser UI (index.html on Port 8000) ───[WebSocket WSS]───► 🤖 Gemini Live API
       │                                                                │
       ▼ (Intercepts function call JSON)                                ▼ (Emits toolCall event)
🐍 Python API Server (api_server.py on Port 5000) ◄───────────────────────┘
       │
       ▼ (Google API Call with token.json)
📅 Google Calendar
🚀 Installation & Prerequisites
To run this application independently and hassle-free on any device (Windows, macOS, or Linux), follow the step-by-step setup below.

Step 1: Install Dependencies
Open your terminal inside the project directory and run the command matching your operating system to install the required Python packages:

Windows:
pip install -r requirements.txt
macOS / Linux:
pip3 install -r requirements.txt
Note

The dependencies include flask, flask-cors, google-api-python-client, google-auth-oauthlib, and other standard helpers required to securely bridge the browser to the calendar APIs.

🔑 Google Cloud API Credentials Configuration
Step 2: Configure your .env File
Create a file named .env in the root directory of your project and populate it with the following configuration variables:

GOOGLE_CLIENT_ID=your_google_oauth_client_id
GOOGLE_CLIENT_SECRET=your_google_oauth_client_secret
GOOGLE_REDIRECT_URI=http://localhost:8000/auth/callback
HOST_CALENDAR_ID=your_email@gmail.com
HOST_EMAIL=your_email@gmail.com
FRONTEND_URL=http://localhost:8000
SECRET_KEY=your_random_secret_key_for_sessions
Step 3: Enable Google Calendar API
Go to the Google Calendar API page in the Google Cloud Console: 👉 Google Calendar API Console
Select your Google Cloud Project.
Click the blue Enable button.
After enabling, click Manage, and select the Credentials tab from the left sidebar.
Step 4: Create OAuth 2.0 Credentials
Click + Create credentials at the top of the Credentials page, then select OAuth client ID.
For Application type, select Web application.
Name your application Calendar Integration.
Scroll down to configure the redirect paths:
Authorized JavaScript origins:
http://localhost:8000
Authorized redirect URIs:
http://localhost:8000/auth/callback
Click Create and copy your Client ID and Client Secret into your .env file.
Enable User Access: In the Cloud Console left sidebar, click OAuth consent screen. Scroll to the Test users section, click Add Users, and enter your login email address (the calendar account you want to give access to).
Step 5: Generate OAuth Credentials (token.json)
The backend needs local calendar write authorization. We spin up a temporary authentication listener to retrieve the secure token.

Start the authentication server:

Windows:
python auth_server.py
macOS / Linux:
python3 auth_server.py
Open http://localhost:8000 in your browser.
Click Authorize Google Calendar and sign in using your designated Google account.
Once the dashboard shows success, close the page and press Ctrl+C in your terminal to shut down the server.
A secure token.json file will now be populated in your project root!
🎙️ Running the Live Assistant
To initiate the fully autonomous real-time voice experience, start both the secure Python calendar controller and serve the UI:

1. Launch the Secure Calendar API Bridge (Terminal Window 1)
Windows:
python api_server.py
macOS / Linux:
python3 api_server.py
(Starts the bridge listening securely on port 5000)

2. Serve the UI Dashboard (Terminal Window 2)
Windows:
python -m http.server 8000
macOS / Linux:
python3 -m http.server 8000
(Serves your interactive interface on port 8000)

3. Connect & Converse!
Navigate to: http://localhost:8000 in Google Chrome. (Always access using localhost so the browser allows microphone media stream access over HTTP).
Paste your Gemini API Key into the prompt and click connect.
Click the 🎙️ button and speak naturally:
"Hi Charon, check if my calendar is free tomorrow, and if I have time in the afternoon, please book a NovaVoice demo!"

View the scrolling console logs and interactive tool cards in real-time as Gemini checks slots, determines availability, and pushes the booking to your Google Calendar!
