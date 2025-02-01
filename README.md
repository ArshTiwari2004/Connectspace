# Connectspace

## Problem solved:

In today's remote work and education environment, there is a growing need for accessible, low-latency, and privacy-focused real-time communication tools that cater to underserved communities such as rural areas, low-bandwidth regions, and non-technical users. Existing solutions like Zoom, Google Meet, or Microsoft Teams are often resource-heavy, require high bandwidth, and rely on third-party servers, making them inaccessible or inefficient for users with limited internet connectivity or those who prioritize data privacy.

## Gaps in the industry :

1. High Bandwidth Dependency: Most video conferencing tools require stable, high-speed internet, which is not available in rural or low-income areas.

2. Privacy Concerns: Many platforms store data on third-party servers, raising concerns about data security and privacy.

3. Complexity for Non-Technical Users: Existing tools often have steep learning curves, making them difficult for non-tech-savvy users to adopt.

4. Lack of Integrated Collaboration Tools: While some platforms offer video calling and chat, they lack integrated, lightweight collaborative tools like whiteboards or screen sharing optimized for low-bandwidth environments.

5. Cost Barriers: Many professional tools are expensive or require subscriptions, making them inaccessible to individuals or small organizations with limited budgets.

## Solution : 

A peer-to-peer (P2P) real-time communication platform designed specifically for low-bandwidth environments and non-technical users. It will offer:

- Low-Bandwidth Video/Audio Calls: Optimized WebRTC implementation for stable communication even on slow networks.

- Screen Sharing: Lightweight screen sharing for remote collaboration.

- Collaborative Whiteboard: A simple, intuitive whiteboard for real-time brainstorming or teaching.

- Text Chat: End-to-end encrypted chat for secure communication.

- Offline-First Approach: Ability to save chat logs and whiteboard data locally for users with intermittent connectivity.

- No Third-Party Servers: Fully P2P architecture to ensure data privacy and reduce dependency on centralized servers.


### Why to build this ?

Accessibility: Targets underserved communities (rural areas, low-income regions) who lack access to high-speed internet or expensive tools.

Privacy-First: No third-party servers mean user data stays between participants, addressing growing privacy concerns.

Cost-Effective: Free to use, with no subscriptions or hidden costs, making it ideal for individuals, small businesses, and schools.

Unique Niche: While many video conferencing tools exist, none are specifically optimized for low-bandwidth, privacy-focused, and non-technical users.

Real-World Impact: This tool can empower remote education, small businesses, and community organizations in developing regions.



## Tech Stack 

#### Frontend:

React.js

WebRTC for real-time video, audio, and data sharing

Canvas API for the collaborative whiteboard

#### Backend:

Node.js for signaling server (to establish P2P connections)

Socket.IO for real-time communication (chat, whiteboard updates)

#### Database:

Local Storage: For saving chat logs and whiteboard data offline.

IndexedDB: For storing larger amounts of data locally.

Lightweight Cloud Database: For user authentication or persistent storage (e.g., Firebase or MongoDB).

#### Hosting:

A lightweight Node.js server hosted on a low-cost platform Vercel.

## Website Flow & Architecture:

#### User Flow:

Landing Page: Simple, intuitive interface with options to "Start a Call" or "Join a Call."

Call Setup: Users enter a unique room ID to create or join a session.

Main Interface:

Video/Audio call section (WebRTC).

Sidebar for text chat (Socket.IO).

Collaborative whiteboard (Canvas API).

Screen sharing button (WebRTC).

Offline Mode: If connectivity is lost, users can continue working on the whiteboard or chat, with data syncing once reconnected.

Architecture:

Frontend:

Handles UI/UX, video/audio rendering, whiteboard drawing, and chat display.

Backend:

Signaling server (Node.js + Socket.IO) to facilitate P2P connections.

Manages room creation, user authentication (if needed), and chat history.

Database:

Local storage for offline data.

Optional cloud database for persistent storage.

P2P Communication:

WebRTC establishes direct connections between users, reducing latency and server dependency.

Socket.IO is used only for signaling (initial connection setup) and chat synchronization.


### Low level System Design Overview :

The system will consist of the following components:

Frontend (Client-Side): Handles the UI, video/audio rendering, whiteboard, and chat.

Backend (Server-Side): Manages signaling, room creation, and user authentication.

Database: Firebase for persistent storage (user data, chat logs, etc.).

WebRTC: Handles peer-to-peer video/audio and data sharing.

Socket.IO: Enables real-time signaling and chat synchronization.

Deployment: Hosted on a scalable platform like Firebase Hosting, Vercel, or AWS.

### Diagram :

Will update this later .


### Client side and server side architecture in detail :

#### Frontend (Client-Side)
Tech Stack: React.js , WebRTC, Canvas API.

Components:

Video/Audio Call: WebRTC handles real-time video and audio streaming.

Chat: Socket.IO enables real-time text messaging.

Whiteboard: Canvas API allows users to draw collaboratively.

Screen Sharing: WebRTC’s getDisplayMedia API captures and shares the screen.

Flow:

User opens the website and enters a room ID.

The frontend connects to the backend (Firebase) for signaling and room setup.

Once connected, WebRTC establishes a P2P connection with other users in the room.

#### Backend (Server-Side)
Tech Stack: Firebase (Firestore, Firebase Functions), Socket.IO.

Components:

Signaling Server: Firebase Functions + Socket.IO to exchange WebRTC signaling data (SDP, ICE candidates).

Room Management: Firebase Firestore stores room IDs and user metadata.

Authentication: Firebase Authentication for user login/signup (optional).

Flow:

When a user creates or joins a room, the backend generates a unique room ID and stores it in Firestore.

Socket.IO relays signaling data between peers to establish WebRTC connections.


### WebRTC and Socket.IO implementation :

#### WebRTC (Peer-to-Peer Communication)

Components:

Signaling: Exchange SDP (Session Description Protocol) and ICE (Interactive Connectivity Establishment) candidates via Socket.IO.

Media Streams: Video, audio, and screen sharing streams are transmitted directly between peers.

Data Channels: Used for sending whiteboard data or file sharing.

Flow:

User A sends an offer (SDP) to User B via the signaling server.

User B responds with an answer (SDP) and ICE candidates.

Once the connection is established, media streams flow directly between User A and User B.

#### Socket.IO (Real-Time Signaling & Chat)

Components:

Signaling: Relays WebRTC signaling data (SDP, ICE candidates) between peers.

Chat: Synchronizes text messages between users in real-time.

Flow:

When a user sends a chat message, it’s emitted to the server via Socket.IO.

The server broadcasts the message to all users in the room.



