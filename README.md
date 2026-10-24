# 🧭 Pathora — AI-Powered Group Travel Planning & Collaboration Ecosystem

<div align="center">

[![Live Demo](https://img.shields.io/badge/Live_Demo-Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white)](https://pathora-travel-ai.vercel.app)
[![Backend API](https://img.shields.io/badge/Backend_API-Render-46E3B7?style=for-the-badge&logo=render&logoColor=white)](https://pathora-backend-9jfw.onrender.com/health)
[![Stack](https://img.shields.io/badge/Stack-MERN_Fullstack-10b981?style=for-the-badge&logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![React](https://img.shields.io/badge/React-18.3-61dafb?style=for-the-badge&logo=react&logoColor=black)](https://react.dev/)
[![Node.js](https://img.shields.io/badge/Node.js-18+-339933?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Express-4.19-000000?style=for-the-badge&logo=express&logoColor=white)](https://expressjs.com/)
[![Socket.IO](https://img.shields.io/badge/Socket.IO-4.8-010101?style=for-the-badge&logo=socket.io&logoColor=white)](https://socket.io/)
[![Google Gemini AI](https://img.shields.io/badge/AI-Google_Gemini_1.5_Flash-8E75C2?style=for-the-badge&logo=google&logoColor=white)](https://ai.google.dev/)
[![Tailwind CSS v4](https://img.shields.io/badge/Tailwind_CSS-v4.1-38bdf8?style=for-the-badge&logo=tailwindcss&logoColor=white)](https://tailwindcss.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](./LICENSE)

### *Every Journey Has a Path.*

**A production-ready, full-stack travel orchestration platform combining real-time geospatial intelligence, generative AI day-clustering, full-duplex WebSocket group communication, and enterprise 3-tier Role-Based Access Control (RBAC).**

[Live Application](https://pathora-travel-ai.vercel.app) • [Backend Health](https://pathora-backend-9jfw.onrender.com/health) • [Architecture](#6-system-architecture) • [Database Design](#8-database-design) • [API Documentation](#10-api-documentation) • [Interview Walkthrough](#21-interview-preparation-section)

</div>

---

## 📑 Table of Contents

1. [Project Overview & Technical Value](#1-project-overview--technical-value)
2. [Live Deployments & Project Links](#2-live-deployments--project-links)
3. [Key Features](#3-key-features)
4. [Application Interface & Verified Screens](#4-application-interface--verified-screens)
5. [Technology Stack](#5-technology-stack)
6. [System Architecture](#6-system-architecture)
7. [Detailed Backend Architecture](#7-detailed-backend-architecture)
8. [Database Design](#8-database-design)
9. [Core Workflows & Sequence Diagrams](#9-core-workflows--sequence-diagrams)
10. [API Documentation](#10-api-documentation)
11. [Project Structure](#11-project-structure)
12. [Installation & Local Setup](#12-installation--local-setup)
13. [Environment Variables](#13-environment-variables)
14. [Security Implementation](#14-security-implementation)
15. [Error Handling & Fault Tolerance](#15-error-handling--fault-tolerance)
16. [Testing & Code Quality](#16-testing--code-quality)
17. [Deployment Guide](#17-deployment-guide)
18. [Performance & Scalability](#18-performance--scalability)
19. [Engineering Decisions & Trade-offs](#19-engineering-decisions--trade-offs)
20. [Known Limitations & Technical Roadmap](#20-known-limitations--technical-roadmap)
21. [Interview Preparation Section](#21-interview-preparation-section)
22. [License & Acknowledgments](#22-license--acknowledgments)

---

## 1. Project Overview & Technical Value

### The Problem
Planning group travel is notoriously fragmented. Travelers navigate a disconnected maze of tools:
- **Generic search engines** that output hallucinations or outdated tourist spots.
- **Scattered messaging apps** where booking details, links, and schedules get lost.
- **Unverified crowd logistics**, where trip organizers lack dedicated governance tools to vet incoming participants, approve join requests, or moderate itinerary visibility.

### The Pathora Solution
**Pathora** unifies the complete travel lifecycle into a cohesive, intelligent platform:
1. **Hybrid Geospatial AI Pipeline**: Instead of letting an LLM hallucinate locations from scratch, Pathora uses **OpenStreetMap Nominatim** to geocode coordinates, queries the **Overpass API** to extract real, operating hotels and tourist attractions within geographic radii, enriches them with cultural context via the **Wikipedia REST API**, and prompts **Google Gemini 1.5 Flash** strictly to cluster, schedule, and theme those real places into a balanced daily itinerary.
2. **Session-Authenticated Real-Time Group Chat**: Integrates **Socket.IO** directly with `express-session` cookies across distributed cross-origin domains. Chat rooms (`trip_{tripId}`) are restricted exclusively to approved travelers and administrators, supporting base64 multimedia photo sharing, live presence, and MongoDB TTL auto-expiring messages.
3. **Event-Driven Push Notifications**: Actions like booking submissions, status approvals, rejections, and new messages automatically emit targeted WebSocket alerts to private user channels (`user_{userId}`).
4. **Three-Tier Role-Based Governance**: Dedicated, isolated workspaces for **Users**, **Organisers**, and **Administrators** with complete cascade data cleanup on deletions.

---

## 2. Live Deployments & Project Links

| Resource | Environment | URL | Status |
|---|---|---|---|
| **Frontend Application** | Production (Vercel) | [https://pathora-travel-ai.vercel.app](https://pathora-travel-ai.vercel.app) | Live |
| **Backend API Service** | Production (Render) | [https://pathora-backend-9jfw.onrender.com](https://pathora-backend-9jfw.onrender.com) | Live |
| **Backend Health Check** | Production (Render) | [https://pathora-backend-9jfw.onrender.com/health](https://pathora-backend-9jfw.onrender.com/health) | Live (`status: ok`) |
| **GitHub Repository** | Source Code | [https://github.com/vivekVerma2806/pathora](https://github.com/vivekVerma2806/pathora) | Public |

---

## 3. Key Features

### 🤖 1. Hybrid AI & Geospatial Itinerary Orchestration
- **Deterministic-Generative Hybrid Engine**: Real coordinates (Nominatim) + real attractions (Overpass) + real encyclopedic descriptions (Wikipedia) + generative clustering (Gemini 1.5 Flash).
- **Multi-Day & Budget Adaptability**: Generates 1 to 7 day plans segmented into morning, afternoon, and evening phases across *Budget*, *Standard*, and *Luxury* spending tiers.
- **Resilient Fallback Mechanism**: Structured procedural fallbacks ensure trip delivery even during third-party API rate limits or network degradation.

### 🏨 2. Real-World Accommodation & Attraction Intelligence
- **Live Overpass Queries**: Dynamically queries hotel, guest house, museum, viewpoint, and landmark nodes within 5km–10km radiuses.
- **Enriched Place Profiles**: Estimated ticket prices, simulated travel times from center, opening hours, and Unsplash/LoremFlickr imagery.
- **Interactive Visualizers**: Swiper carousels showcasing hotel cards, amenities tags, and collapsible daily timelines.

### 👥 3. Three-Tier Role-Based Access Control (RBAC)
- **Standard User**: Search destinations, generate AI trips, save favorites, submit join requests, chat with verified group members, and manage personal bookings.
- **Trip Organiser**: Request elevation from administrators, manage assigned expeditions under `/organiser`, audit incoming join requests, and coordinate group schedules.
- **Platform Administrator**: Access `/admin` dashboard to verify or revoke user access, moderate pending public trips, audit all system bookings, and trigger cascade deletions.

### 💬 4. Real-Time Group Chat with Auto-Expiring Messages
- **Strict Room Isolation**: Users can only join `trip_{tripId}` WebSocket rooms if they are the creator, an admin, or hold an `approved` booking.
- **Multimedia Sharing**: Supports real-time text transmission and base64-encoded photo uploads with interactive emoji picker integration.
- **24-Hour TTL Auto-Purge**: When a chat notification is marked read, the system assigns a 24-hour expiration timestamp (`expiresAt`), prompting MongoDB's TTL index to permanently delete the message.

### 🔔 5. Real-Time Event-Driven Notifications
- **Private Socket Channels**: Real-time push alerts routed to private `user_{userId}` rooms.
- **Interactive Header Dropdown**: Unread badge counters, instant status updates, and single/batch read markers.
- **Audit Triggers**: Instant alerts on booking submissions, organizer approvals/rejections, and group chat broadcasts.

### 🧭 6. Community Trip Discovery & Exploration
- **Curated Public Feed**: Browse verified community itineraries on `/explore`.
- **Multi-Parameter Search**: Instant live filtering by destination keyword regex, duration (min/max days), and budget tier.
- **Join Request Workflow**: Interactive simulated checkout modal enabling travelers to submit join applications.

---

## 4. Application Interface & Verified Screens

Pathora features a modern aesthetic built with **Tailwind CSS v4**, the **Plus Jakarta Sans** and **Inter** typography pairing, smooth micro-animations, and responsive cards:

1. **Landing Page (`/`)**: High-impact hero section with dynamic search input, curated trending destinations, platform statistics, and value propositions.
2. **Trip Generation Wizard (`/create-trip`)**: Multi-step interactive form selecting destination (with Nominatim autocomplete), trip duration (1–7 days), spending tier (Cheap, Mid-range, Luxury), and companion type (Solo, Couple, Family, Friends).
3. **Trip Presentation View (`/view-trip/:id`)**: Comprehensive itinerary dashboard with interactive hotel Swiper carousel, day-wise timeline cards, geo-coordinates, and "Request to Join" checkout trigger.
4. **Community Explore Feed (`/explore`)**: Filterable grid displaying public trips with duration tags, organizer badges, and budget indicators.
5. **Real-Time Group Chat (`/chat?tripId=...`)**: Full-screen or modal group chat window with room member rosters, message bubbles, image previews, and integrated emoji picker.
6. **Unified Auth Portal (`/login` & `/register`)**: Role-swapping authentication tabs (User, Organiser, Admin) with instant input validation, password toggle, and admin auto-verification.
7. **Organiser Management Hub (`/organiser`)**: Dedicated workspace to review participant applications, inspect traveler profiles, and approve/reject memberships.
8. **Admin Moderation Portal (`/admin`)**: High-privilege tabbed interface to manage user verification, publish/reject submitted itineraries, and audit platform-wide bookings.

---

## 5. Technology Stack

### Frontend Architecture
| Technology | Version | Purpose in Pathora |
|---|---|---|
| **React** | `18.3.1` | Component-driven UI hierarchy, declarative rendering, hooks-based state management |
| **Vite (Rolldown)** | `7.2.5` | Next-generation build tool providing near-instant HMR and optimized production bundles |
| **React Router DOM** | `7.10.1` | Client-side declarative routing, nested route layouts (`Layout.jsx`), dynamic param matching |
| **Tailwind CSS** | `4.1.18` | Modern utility-first styling engine utilizing native CSS theme variables and `@tailwindcss/vite` |
| **Radix UI Primitives** | Latest | Accessible unstyled primitives: Dialog (`@radix-ui/react-dialog`), Dropdown Menu, Scroll Area |
| **Lucide React** | `0.561.0` | Comprehensive iconography set for consistent navigation and status indicators |
| **Swiper** | `12.0.3` | Mobile-optimized, touch-enabled carousels for hotel galleries and place showcases |
| **Axios** | `1.13.2` | HTTP client configured with `withCredentials: true` for automatic session cookie transport |
| **Socket.IO Client** | `4.8.1` | Persistent WebSocket client enabling real-time chat and instantaneous push notifications |
| **Google Generative AI** | `0.24.1` | Official SDK calling Gemini 1.5 Flash for itinerary day-clustering and structuring |
| **Emoji Picker React** | `4.16.1` | Embedded client-side emoji selector for interactive chat messaging |

### Backend Architecture
| Technology | Version | Purpose in Pathora |
|---|---|---|
| **Node.js** | `18+` / `20+` | Asynchronous, non-blocking JavaScript server runtime (ES Modules format) |
| **Express.js** | `4.19.2` | Minimalist HTTP web framework powering REST API routes, controllers, and middleware |
| **Socket.IO** | `4.8.1` | Bi-directional, event-driven WebSocket server sharing session middleware with Express |
| **MongoDB** | Cloud Atlas | Scalable document database storing users, trips, bookings, messages, and sessions |
| **Mongoose** | `8.2.4` | Object Data Modeling (ODM) library providing strict schemas, validation, and lifecycle hooks |
| **express-session** | `1.18.2` | Production-grade cookie-based session management |
| **connect-mongo** | `6.0.0` | MongoDB-backed session store offloading session state from server memory |
| **bcryptjs** | `2.4.3` | Secure password hashing using 10 salt rounds before database persistence |
| **cors** | `2.8.5` | Configurable Cross-Origin Resource Sharing middleware with dynamic origin resolver |
| **dotenv** | `16.4.5` | Zero-dependency environment variable loader from local `.env` files |

### Geospatial & Third-Party APIs
| Service | API Endpoint | Responsibility in Pathora |
|---|---|---|
| **OpenStreetMap Nominatim** | `nominatim.openstreetmap.org` | Reverse geocoding, coordinate resolution, and address hierarchy lookup |
| **Overpass API** | `overpass-api.de/api/interpreter` | High-performance spatial querying of verified hotels, viewpoints, and attractions |
| **Wikipedia REST API** | `en.wikipedia.org/api/rest_v1` | Contextual encyclopedic extraction for landmark cultural summaries |
| **Google Gemini AI** | `gemini-1.5-flash` | Contextual clustering of real tourist places into logical daily thematic itineraries |

---

## 6. System Architecture

Pathora operates on a distributed client-server architecture:
- A Single Page Application (SPA) hosted on **Vercel**.
- An API and WebSocket service hosted on **Render**.
- A managed **MongoDB Atlas** database cluster.
- External geospatial and LLM APIs called at orchestration boundaries.

```mermaid
graph TD
    subgraph ClientLayer ["Frontend Client Layer (Vercel SPA)"]
        UI["React 18.3 UI (Tailwind CSS v4)"]
        Router["React Router v7"]
        AuthCtx["AuthContext (useReducer + Session Check)"]
        GeoService["Geospatial Service (Nominatim Autocomplete)"]
        AIService["AI Orchestrator (AIModel.jsx)"]
        SocketClient["Socket.IO Client (withCredentials: true)"]
    end

    subgraph ExternalAPIs ["External Intelligence APIs"]
        OSM["OpenStreetMap Nominatim API<br/>(Geocoding)"]
        Overpass["Overpass API<br/>(Hotels & Attractions)"]
        Wiki["Wikipedia REST API<br/>(Cultural Summaries)"]
        Gemini["Google Gemini 1.5 Flash<br/>(Itinerary Scheduling)"]
    end

    subgraph ServerLayer ["Backend Application Layer (Render Web Service)"]
        ExpressApp["Express.js Server (index.js)"]
        CORS["Dynamic CORS Origin Handler"]
        SessionMgr["express-session + MongoStore"]
        RBAC["RBAC Middleware (verifyToken, verifyAdmin, verifyOrganiser)"]
        APIRouters["REST Routers (/auth, /trips, /bookings, /users, etc.)"]
        SocketServer["Socket.IO Server (Port 5001 / WSS)"]
        AutoBoot["Admin Auto-Bootstrap on Mongo Connect"]
    end

    subgraph DataLayer ["Data Layer (MongoDB Atlas Cluster)"]
        DBUsers[("users")]
        DBTrips[("trips")]
        DBBookings[("bookings")]
        DBMessages[("messages (TTL Index)")]
        DBNotifs[("notifications")]
        DBSessions[("sessions (14-day TTL)")]
    end

    %% Client flows
    UI --> Router
    Router --> AuthCtx
    UI --> GeoService
    GeoService -->|HTTP Search| OSM
    UI --> AIService
    AIService -->|Spatial Query| Overpass
    AIService -->|Landmark Summary| Wiki
    AIService -->|Day Clustering Prompt| Gemini
    UI -->|REST with Cookie| ExpressApp
    SocketClient <-->|WSS Duplex Handshake| SocketServer

    %% Server flows
    ExpressApp --> CORS
    CORS --> SessionMgr
    SessionMgr <-->|Session Read/Write| DBSessions
    SessionMgr --> RBAC
    RBAC --> APIRouters
    APIRouters --> DBUsers
    APIRouters --> DBTrips
    APIRouters --> DBBookings
    APIRouters --> DBMessages
    APIRouters --> DBNotifs
    ExpressApp --> AutoBoot
    AutoBoot --> DBUsers
    SocketServer -->|Handshake Session Validation| SessionMgr
    SocketServer --> DBMessages
    SocketServer --> DBNotifs
```

---

## 7. Detailed Backend Architecture

### 1. Server Entry Point & Lifecycle (`server/index.js`)
When `server/index.js` initializes:
1. **Load Environment**: `dotenv.config()` loads variables (`PORT`, `MONGO_URI`, `SESSION_SECRET`, `CLIENT_URL`).
2. **Reverse Proxy Trust**: Sets `app.set('trust proxy', 1)` to allow Render's load balancers to correctly forward secure HTTPS cookies.
3. **CORS Whitelist Handler**: A custom `corsOriginHandler` inspects incoming request origins:
   - Grants access if origin is explicitly in `allowedOrigins` (`localhost:5173`, `CLIENT_URL`).
   - Automatically permits Vercel preview URLs via `origin.endsWith(".vercel.app")`.
   - Permits non-production requests or headless tool requests without an origin header (e.g., health probes).
4. **Session Middleware**:
   Configured with `connect-mongo`:
   ```javascript
   const sessionMiddleware = session({
       secret: process.env.SESSION_SECRET,
       resave: false,
       saveUninitialized: false,
       store: MongoStore.create({
           mongoUrl: process.env.MONGO_URI,
           collectionName: 'sessions',
           ttl: 14 * 24 * 60 * 60 // 14-day TTL
       }),
       cookie: {
           maxAge: 1000 * 60 * 60 * 24 * 14,
           httpOnly: true,
           secure: process.env.NODE_ENV === 'production',
           sameSite: process.env.NODE_ENV === 'production' ? 'none' : 'lax'
       }
   });
   ```
5. **Socket.IO Session Bridge**:
   Socket.IO wraps `sessionMiddleware` via:
   ```javascript
   const wrap = middleware => (socket, next) => middleware(socket.request, {}, next);
   io.use(wrap(sessionMiddleware));
   ```
   This passes the decrypted `socket.request.session.user` to the socket handshake without requiring secondary JWT headers.
6. **MongoDB Connection & Startup Auto-Bootstrap**:
   Upon `mongoose.connect()`, the server executes an auto-bootstrap check: if `admin@travelai.com` does not exist, it hashes `Admin@123` via `bcrypt` and creates the verified platform administrator account on the fly.
7. **Production Static Fallback vs API Mode**:
   If a client build exists locally at `../client/dist`, Express serves static assets; otherwise, it operates as a dedicated API gateway, exposing `/health` and JSON endpoints.

```mermaid
graph TD
    Req[Incoming HTTP Request] --> Proxy[Render Load Balancer / Trust Proxy 1]
    Proxy --> CORS[CORS Origin Handler]
    CORS --> ExpressJSON[express.json Payload Parser]
    ExpressJSON --> SessMid[Session Middleware / Cookie Inspection]
    SessMid <--> MongoStore[(MongoDB sessions collection)]
    SessMid --> RouterSelect{Route Match}

    RouterSelect -->|/api/auth| AuthRouter[Auth Router]
    RouterSelect -->|/api/trips| TripsRouter[Trips Router]
    RouterSelect -->|/api/bookings| BookingsRouter[Bookings Router]
    RouterSelect -->|/api/organiser| OrganiserRouter[Organiser Router]
    RouterSelect -->|/api/users| UsersRouter[Users Router]
    RouterSelect -->|/api/messages| MessagesRouter[Messages Router]
    RouterSelect -->|/api/notifications| NotifRouter[Notifications Router]
    RouterSelect -->|/health| HealthCheck[Health Check 200 OK]

    AuthRouter --> AuthMid{authMiddleware}
    TripsRouter --> AuthMid
    BookingsRouter --> AuthMid
    OrganiserRouter --> AuthMid
    UsersRouter --> AuthMid
    MessagesRouter --> AuthMid
    NotifRouter --> AuthMid

    AuthMid -->|verifyToken| VerifyUser["Check req.session.user"]
    AuthMid -->|verifyAdmin| VerifyAdmin["Check role: admin"]
    AuthMid -->|verifyOrganiser| VerifyOrg["Check role: organiser or admin"]

    VerifyUser --> Controller[Route Controller Logic]
    VerifyAdmin --> Controller
    VerifyOrg --> Controller

    Controller <--> Mongoose[(Mongoose ODM / MongoDB Atlas)]
    Controller --> Res[JSON HTTP Response]
```

---

## 8. Database Design

Pathora utilizes a structured document schema with Mongoose ODM in **MongoDB Atlas**:

```mermaid
erDiagram
    User ||--o{ Trip : "creates / owns"
    User ||--o{ Booking : "submits"
    User ||--o{ Message : "sends"
    User ||--o{ Notification : "receives"
    User }o--o{ Trip : "favorites"
    Trip ||--o{ Booking : "has"
    Trip ||--o{ Message : "contains"
    Message ||--o| Notification : "triggers relatedId"

    User {
        ObjectId _id PK
        string username "unique, required"
        string email "unique, required"
        string password "bcrypt hash, required"
        string role "user | organiser | admin"
        boolean isVerified "default: false"
        string bio
        string phone
        string avatar
        ObjectId[] favorites "ref: Trip"
        Date createdAt
        Date updatedAt
    }

    Trip {
        ObjectId _id PK
        ObjectId userId FK "ref: User, required"
        string destination "required"
        Object tripData "JSON: locationInfo, hotels, itinerary"
        number duration
        string budget "Cheap | Mid-range | Luxury"
        boolean isPublic "default: true"
        string status "pending | approved | rejected"
        number capacity "default: 10"
        number price
        boolean requestOrganiser "default: false"
        string organiserStatus "pending | approved | rejected"
        Date createdAt
        Date updatedAt
    }

    Booking {
        ObjectId _id PK
        ObjectId userId FK "ref: User, required"
        ObjectId tripId FK "ref: Trip, optional"
        string destination "required"
        string hotelId
        string hotelName
        string hotelImage
        string hotelAddress
        string price
        string userName
        string userEmail
        string status "pending | approved | rejected | revoked"
        Date createdAt
        Date updatedAt
    }

    Message {
        ObjectId _id PK
        ObjectId tripId FK "ref: Trip, required"
        ObjectId userId FK "ref: User, required"
        string username "required"
        string message "optional if image"
        string type "text | image"
        string imageUrl "base64 / URL"
        Date expiresAt "TTL Index: expires after 0s"
        Date createdAt "default: Date.now"
    }

    Notification {
        ObjectId _id PK
        ObjectId userId FK "ref: User, required"
        string type "booking_request | booking_status | system | chat_message"
        ObjectId relatedId "ref: Message, optional"
        string message "required"
        string link "URL navigation path"
        boolean isRead "default: false"
        Date createdAt
        Date updatedAt
    }

    Session {
        string _id PK "Session ID"
        Date expires "TTL Index"
        string session "JSON serialized user payload"
    }
```

### Schema & Index Specifications

1. **`User` Collection**:
   - `username`: Indexed, unique constraint, sanitized trim.
   - `email`: Indexed, unique constraint, lowercased trim.
   - `role`: Enum `["user", "organiser", "admin"]`.
   - `isVerified`: Boolean flag used by the admin dashboard to moderate platform participants.
   - `favorites`: Array of ObjectIds referencing `Trip` documents for one-click bookmarking.

2. **`Trip` Collection**:
   - `userId`: ObjectId reference to trip creator (`User`).
   - `tripData`: Semi-structured schema containing `locationInfo` (lat, lng, photoUrl), `hotels` array (names, addresses, pricing, ratings), and `itinerary` (day number, theme, places).
   - `status`: Moderation flag (`pending` -> `approved` -> `rejected`). Only `approved` trips appear on the `/explore` community feed.
   - `organiserStatus`: Indicates whether the creator has been elevated to an organizer for this specific trip.

3. **`Booking` Collection**:
   - Links traveler (`userId`) to a trip (`tripId`) or general destination.
   - Status transitions: `pending` (initial application) -> `approved` (member admitted to chat) / `rejected` (declined).

4. **`Message` Collection**:
   - Real-time chat record containing text or base64 image data.
   - **TTL Auto-Purge**: Contains an `expiresAt` field with index `{ expires: 0 }`. When a chat notification is marked as read, `expiresAt` is set to `Date.now() + 24h`, triggering MongoDB's background thread to permanently purge the message 24 hours later.

5. **`Notification` Collection**:
   - Real-time alerts for booking status updates, join requests, or new chat mentions.
   - Indexed on `userId` and `createdAt` for rapid lookup in the header bell dropdown.

6. **`Session` Collection (`sessions`)**:
   - Managed directly by `connect-mongo` with native 14-day document TTL (`ttl: 1209600`).

---

## 9. Core Workflows & Sequence Diagrams

### Workflow 1: Hybrid AI Itinerary Generation
This journey demonstrates how Pathora combines deterministic geospatial querying with generative LLM clustering.

```mermaid
sequenceDiagram
    autonumber
    actor User as Traveler
    participant Client as React SPA (CreateTrip.jsx)
    participant Model as AIModel.jsx
    participant Nominatim as OSM Nominatim API
    participant Overpass as OSM Overpass API
    participant Wiki as Wikipedia REST API
    participant Gemini as Google Gemini 1.5 Flash
    participant Server as Express Backend (/api/trips)
    participant DB as MongoDB (trips)

    User->>Client: Enters Location, Days (3), Budget (Standard), Traveler (Couple)
    Client->>Model: generateTripPlan(location, days, budget, traveler)
    
    Model->>Nominatim: GET /search?q={location}&format=json
    Nominatim-->>Model: { lat: 35.6762, lon: 139.6503, displayName: "Tokyo, Japan" }

    par Parallel Data Fetch
        Model->>Overpass: POST interpreter (hotel/guest_house within 5km radius)
        Overpass-->>Model: Raw OSM Hotel Elements
        Model->>Overpass: POST interpreter (tourism/historic/leisure within 10km radius)
        Overpass-->>Model: Raw OSM Landmark Elements
    end

    loop For Each Top Landmark
        Model->>Wiki: GET /page/summary/{wikiTagTitle}
        Wiki-->>Model: Cultural Extract & Historical Summary
    end

    Model->>Gemini: Prompt with exact places list: "Cluster into 3 balanced days by proximity"
    Gemini-->>Model: Structured JSON Array of Day Plans [ { day: 1, theme, places: [...] } ]

    Model->>Client: Compiled Unified Trip Plan Object
    Client->>User: Renders Interactive Day Timeline & Hotel Cards
    User->>Client: Clicks "Save Itinerary"
    Client->>Server: POST /api/trips { tripData, destination, duration, budget }
    Server->>DB: Trip.create(status: "pending")
    DB-->>Server: Saved Trip Document
    Server-->>Client: 201 Created { _id: "..." }
```

---

### Workflow 2: Cross-Origin Session Authentication & Socket Bridge
Illustrates how the frontend establishes an HTTP session cookie on Render and bridges it into WebSocket connections.

```mermaid
sequenceDiagram
    autonumber
    actor User as User / Admin
    participant Client as React SPA (Login.jsx)
    participant AuthContext as AuthContext.jsx
    participant Server as Express Server (index.js)
    participant Store as MongoStore (sessions)
    participant Socket as Socket.IO Server

    User->>Client: Submits email + password (loginType: 'admin')
    Client->>Server: POST /api/auth/login { email, password }
    Server->>Server: bcrypt.compare(password, user.password)
    Server->>Store: req.session.user = { id, role, isVerified }
    Store-->>Server: Session Stored in MongoDB
    Server-->>Client: HTTP 200 OK (Set-Cookie connect.sid, SameSite=None, Secure)
    Client->>AuthContext: dispatch({ type: "LOGIN_SUCCESS", payload: user })

    Note over Client,Socket: Real-Time WebSocket Connection
    Client->>Socket: io.connect("wss://backend", { withCredentials: true })
    Socket->>Server: io.use(wrap(sessionMiddleware))
    Server->>Store: Validates connect.sid from handshake cookie
    Store-->>Server: Resolves session.user
    Socket-->>Client: Connection Accepted (socket.user = user)
    Socket->>Socket: socket.join("user_" + user.id)
```

---

### Workflow 3: Join Request, Organiser Approval & Notification Dispatch
Illustrates how a traveler requests to join an organized expedition and receives live notification updates.

```mermaid
sequenceDiagram
    autonumber
    actor Traveler as Traveler
    participant Client as React SPA
    participant Server as Express API (/api/bookings)
    participant Socket as Socket.IO Server
    actor Organiser as Trip Organiser
    participant DB as MongoDB Atlas

    Traveler->>Client: Clicks "Request to Join" on Tokyo Expedition
    Client->>Server: POST /api/bookings/join { tripId, destination, price }
    Server->>DB: Booking.create(status: "pending")
    Server->>DB: Notification.create(userId: organiserId, type: "booking_request")
    Server->>Socket: io.to("user_" + organiserId).emit("notification_new", notif)
    Socket-->>Organiser: Live Badge Update on Notification Bell 🔔
    Server-->>Client: 201 Created (Booking Pending)

    Organiser->>Server: PUT /api/organiser/requests/:id/validate { status: "approved" }
    Server->>DB: Booking.findByIdAndUpdate(status: "approved")
    Server->>DB: Notification.create(userId: travelerId, type: "booking_status")
    Server->>Socket: io.to("user_" + travelerId).emit("notification_new", notif)
    Socket-->>Traveler: Instant Notification: "Your request has been approved!"
    Traveler->>Client: Navigates to /chat?tripId={id}
    Client->>Socket: emit("join_chat", { tripId })
    Socket->>DB: Booking.findOne({ tripId, userId, status: "approved" })
    DB-->>Socket: Verified Approved Member
    Socket->>Socket: socket.join("trip_" + tripId)
    Socket-->>Client: emit("joined_room", { room: "trip_{tripId}" })
```

---

### Workflow 4: Real-Time Chat & 24-Hour Message TTL Purge
Shows how active group members communicate and how messages auto-expire once read.

```mermaid
sequenceDiagram
    autonumber
    actor MemberA as Traveler A
    participant Socket as Socket.IO Server
    participant DB as MongoDB (messages / notifs)
    actor MemberB as Traveler B
    participant ClientB as Traveler B Client

    MemberA->>Socket: emit("send_message", { tripId, message: "Meet at Senso-ji!", type: "text" })
    Socket->>DB: Message.create({ tripId, userId, message, type })
    DB-->>Socket: Saved Message Document (_id)
    Socket->>Socket: io.to("trip_" + tripId).emit("receive_message", payload)
    Socket-->>MemberB: Message appears in chat window

    Socket->>DB: Notification.create(type: "chat_message", relatedId: message._id)
    Socket->>MemberB: emit("notification_new", notif)

    MemberB->>ClientB: Clicks Notification Bell -> "Mark as Read"
    ClientB->>Socket: PUT /api/notifications/:id/read
    Socket->>DB: Notification.findByIdAndUpdate(isRead: true)
    Socket->>DB: Message.findByIdAndUpdate(relatedId, { expiresAt: Date.now() + 24h })
    
    Note over DB: 24 Hours Later
    DB->>DB: MongoDB TTL Index background process deletes Message document
```

---

## 10. API Documentation

All routes are mounted under `/api`. Sessions are automatically validated via the `connect.sid` cookie.

### 🔑 Authentication Routes (`/api/auth`)

| Method | Endpoint | Access | Parameters / Body | Successful Response | Error Status Codes |
|---|---|---|---|---|---|
| `GET` | `/api/auth/me` | Authenticated | None | `200 OK`: `{ user: { id, username, role, isVerified } }` | `401 Unauthorized` |
| `POST` | `/api/auth/register` | Public | `{ username, email, password, role }` | `201 Created`: `{ message: "..." }` | `400 Bad Request` |
| `POST` | `/api/auth/login` | Public | `{ email, password }` | `200 OK`: `{ message: "Login successful", user: {...} }` | `400 Bad Request`, `500` |
| `POST` | `/api/auth/logout` | Authenticated | None | `200 OK`: `{ message: "Logout successful" }` | `500 Server Error` |
| `GET` | `/api/auth/test-db` | Public | None | `200 OK`: `{ message: "Database connected", state: 1 }` | `500 Server Error` |

#### Sample Login Request & Response
```bash
# Request
curl -X POST https://pathora-backend-9jfw.onrender.com/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"admin@travelai.com","password":"Admin@123"}'

# Response (200 OK)
# Set-Cookie: connect.sid=s%3A...; Path=/; HttpOnly; Secure; SameSite=None
{
  "message": "Login successful",
  "user": {
    "id": "6adca964c4702dfb02ae0b76",
    "username": "admin",
    "role": "admin",
    "isVerified": true
  }
}
```

---

### 🗺️ Trips Routes (`/api/trips`)

| Method | Endpoint | Access | Parameters / Body | Description |
|---|---|---|---|---|
| `POST` | `/api/trips` | Authenticated | `{ tripData, destination, duration, budget, capacity, price, requestOrganiser }` | Saves newly generated trip (status defaults to `pending`) |
| `GET` | `/api/trips` | Public | Query: `?query=Tokyo&minDays=3&maxDays=7&budget=Standard` | Returns approved public trips with regex destination filtering |
| `GET` | `/api/trips/user-trips` | Authenticated | None | Returns trips created by current logged-in user |
| `GET` | `/api/trips/:id` | Public | Path: `id` (24-char ObjectId) | Retrieves full trip document with hotel & itinerary data |
| `DELETE` | `/api/trips/:id` | Owner / Admin | Path: `id` | Cascades delete to all associated bookings, messages, and favorites |
| `GET` | `/api/trips/admin/all` | Admin Only | None | Lists all platform trips with populated creator details |
| `PATCH` | `/api/trips/:id/status` | Admin Only | `{ status: "approved" \| "rejected" }` | Approves or rejects trip for public explore listing |
| `PATCH` | `/api/trips/:id/organiser-status`| Admin Only | `{ status: "approved" \| "rejected" }` | Approves organizer status; automatically elevates user to `organiser` |

---

### 📅 Bookings & Join Requests (`/api/bookings`)

| Method | Endpoint | Access | Parameters / Body | Description |
|---|---|---|---|---|
| `POST` | `/api/bookings/join` | Authenticated | `{ destination, tripId, hotelName, hotelAddress, price }` | Submits join request; prevents duplicate submissions |
| `GET` | `/api/bookings/status/:destination` | Authenticated | Path: `destination` | Checks whether current user already holds a booking for destination |
| `GET` | `/api/bookings/user-bookings` | Authenticated | None | Returns all bookings submitted by the authenticated user |
| `GET` | `/api/bookings/creator-requests` | Authenticated | None | Returns incoming join requests for trips created by the user |
| `GET` | `/api/bookings/trip/:tripId/members`| Authenticated | Path: `tripId` | Returns all approved members (`status: "approved"`) for a trip |
| `DELETE` | `/api/bookings/:id` | Owner | Path: `id` | Cancels and deletes the traveler's own booking application |
| `GET` | `/api/bookings/admin/all` | Admin Only | None | Audits all bookings across all trips on the platform |
| `GET` | `/api/bookings/admin/pending` | Admin Only | None | Returns all pending bookings awaiting moderation |
| `PUT` | `/api/bookings/admin/validate/:id` | Admin Only | `{ status: "approved" \| "rejected" }` | Sets booking status and pushes live notification to traveler |
| `DELETE` | `/api/bookings/admin/:id` | Admin Only | Path: `id` | Permanently deletes a booking record |

---

### 🛡️ Organiser Management (`/api/organiser`)

| Method | Endpoint | Access | Parameters / Body | Description |
|---|---|---|---|---|
| `GET` | `/api/organiser/my-managed-trips` | Organiser / Admin | None | Retrieves trips assigned to and managed by the organizer |
| `GET` | `/api/organiser/join-requests` | Organiser / Admin | None | Returns join requests for trips owned by this organizer |
| `PUT` | `/api/organiser/requests/:id/validate` | Organiser / Admin | `{ status: "approved" \| "rejected" }` | Validates booking ownership, updates status, and notifies user |

---

### 👤 Users & Profiles (`/api/users`)

| Method | Endpoint | Access | Parameters / Body | Description |
|---|---|---|---|---|
| `GET` | `/api/users/profile` | Authenticated | None | Returns profile info excluding password hash |
| `PUT` | `/api/users/profile` | Authenticated | `{ bio, phone, avatar, username }` | Updates profile metadata |
| `PUT` | `/api/users/change-password` | Authenticated | `{ currentPassword, newPassword }` | Validates old password with bcrypt, hashes new password |
| `POST` | `/api/users/favorites/:tripId` | Authenticated | Path: `tripId` | Toggles trip ObjectId in user's `favorites` array |
| `GET` | `/api/users` | Admin Only | None | Returns all regular users for admin review |
| `PATCH` | `/api/users/:id/verify` | Admin Only | Path: `id` | Sets `isVerified: true` |
| `PATCH` | `/api/users/:id/revoke` | Admin Only | Path: `id` | Sets `isVerified: false` |
| `DELETE` | `/api/users/:id` | Admin Only | Path: `id` | Cascades delete across user's trips, bookings, messages, notifs |

---

### 💬 Chat Messages (`/api/messages`) & 🔔 Notifications (`/api/notifications`)

| Method | Endpoint | Access | Description |
|---|---|---|---|
| `GET` | `/api/messages/:tripId` | Approved Member / Admin | Returns chronological message history for verified trip room |
| `GET` | `/api/notifications` | Authenticated | Retrieves up to 20 recent notifications sorted by creation date |
| `PUT` | `/api/notifications/:id/read` | Authenticated | Marks notification as read; triggers 24h message TTL |
| `PUT` | `/api/notifications/mark-all-read` | Authenticated | Marks all unread user notifications as read |

---

## 11. Project Structure

```text
Travel-ai/
├── package.json                 # Monorepo task orchestration (concurrently, install-all)
├── vercel.json                  # Root Vercel build output & SPA rewrites configuration
├── render.yaml                  # Render Infrastructure-as-Code blueprint
├── README.md                    # Comprehensive technical documentation
├── LICENSE                      # MIT Open Source License
│
├── client/                      # Frontend Application (React 18 + Vite + Tailwind v4)
│   ├── index.html               # Single Page Application HTML root
│   ├── vite.config.js           # Vite config with @tailwindcss/vite & path aliases
│   ├── jsconfig.json            # Path resolution mappings (@ -> src)
│   ├── package.json             # Frontend dependencies & scripts
│   ├── public/                  # Public assets (logo, fallback images)
│   └── src/
│       ├── main.jsx             # React 18 DOM mount & createBrowserRouter routing tree
│       ├── App.jsx              # Landing page component
│       ├── Layout.jsx           # Global layout wrapper housing persistent Header
│       ├── index.css            # Tailwind CSS v4 design tokens & theme directives
│       │
│       ├── chat/                # Real-time WebSocket chat views
│       │   └── index.jsx        # Group chat page with room roster & message composer
│       │
│       ├── components/          # Reusable UI & presentation components
│       │   ├── custom/          # Custom brand components (Header, Hero, TripFilters)
│       │   ├── ui/              # Radix UI primitives (button, dialog, dropdown, scroll-area)
│       │   ├── ItinerarySection.jsx     # Daily itinerary timeline with bookmark toggles
│       │   ├── NominatimAutocomplete.jsx # Real-time OpenStreetMap search input
│       │   ├── NotificationDropdown.jsx  # Interactive live notification bell dropdown
│       │   └── PaymentModal.jsx          # Simulated credit card checkout modal
│       │
│       ├── constants/
│       │   └── options.jsx      # Traveler selection lists & budget tier constants
│       │
│       ├── context/
│       │   └── AuthContext.jsx  # Session Auth Context provider, reducer, and useAuth hook
│       │
│       ├── create-trip/
│       │   └── index.jsx        # Interactive trip generation wizard form
│       │
│       ├── my-trips/
│       │   └── index.jsx        # Dashboard for created itineraries & submitted bookings
│       │
│       ├── pages/               # Main application route views
│       │   ├── AdminDashboard.jsx     # High-privilege admin moderation dashboard
│       │   ├── Explore.jsx            # Community trip explorer with multi-param filters
│       │   ├── Login.jsx              # Unified role-switching session login form
│       │   ├── OrganiserDashboard.jsx # Organiser participant management hub
│       │   ├── Profile.jsx            # User profile editor & password changer
│       │   └── Register.jsx           # Account creation form with auto-verify logic
│       │
│       ├── service/
│       │   ├── AIModel.jsx      # Hybrid AI orchestrator (Nominatim + Overpass + Wiki + Gemini)
│       │   └── api.jsx          # Axios instance configured with withCredentials: true
│       │
│       └── view-trip/
│           ├── index.jsx        # Full trip itinerary viewer with hotel galleries
│           └── ViewDetails.jsx  # Detailed modal for specific places and hotels
│
└── server/                      # Backend REST API & WebSocket Server (Node.js + Express)
    ├── index.js                 # Server entry point, Socket.IO, DB connect & auto-bootstrap
    ├── package.json             # Backend dependencies, start, and seed scripts
    ├── seed.js                  # Database seeder provisioning admin, users, trips, & chats
    │
    ├── middleware/
    │   └── authMiddleware.js    # RBAC verifiers: verifyToken, verifyAdmin, verifyOrganiser
    │
    ├── models/                  # Mongoose data schemas
    │   ├── Booking.js           # Reservation & join application schema
    │   ├── Message.js           # Chat message schema with 24h TTL index
    │   ├── Notification.js      # System and user notification schema
    │   ├── Trip.js              # Full itinerary schema storing JSON trip data
    │   └── User.js              # User schema with roles, bcrypt passwords, & favorites
    │
    └── routes/                  # Modular Express router endpoints
        ├── auth.js              # Registration, session login, logout, & /auth/me
        ├── bookings.js          # Booking join requests & admin status validation
        ├── messages.js          # Trip chat history retrieval
        ├── notifications.js     # User notification queries & read status updates
        ├── organiser.js         # Managed trip retrieval & join request moderation
        ├── trips.js             # Trip creation, public filtering, approval, & deletion
        └── users.js             # User administration, profile updates, & password changes
```

---

## 12. Installation & Local Setup

### Prerequisites
- **Node.js**: `v18.0.0` or higher
- **npm**: `v9.0.0` or higher
- **MongoDB**: Local MongoDB instance (`mongodb://127.0.0.1:27017`) or free [MongoDB Atlas Cluster](https://www.mongodb.com/atlas/database)
- **Google Gemini API Key**: Free key from [Google AI Studio](https://aistudio.google.com/)

---

### Step-by-Step Local Setup

#### 1. Clone Repository
```bash
git clone https://github.com/vivekVerma2806/pathora.git
cd pathora
```

#### 2. Install All Dependencies
Execute the monorepo installer from the repository root:
```bash
npm run install-all
```
*(Installs root dependencies, `client/node_modules`, and `server/node_modules` sequentially).*

#### 3. Configure Environment Variables
Create `.env` in `server/`:
```env
PORT=5001
MONGO_URI=mongodb://127.0.0.1:27017/travelai
SESSION_SECRET=travel_ai_local_dev_secret_key_1234567890_super_secure
NODE_ENV=development
CLIENT_URL=http://localhost:5173
```

Create `.env` in `client/`:
```env
VITE_GOOGLE_GEMINI_AI_API_KEY=your_actual_gemini_api_key_here
VITE_BACKEND_URL=http://localhost:5001
```

#### 4. Seed the Database
Populate the database with sample users (admin, organiser, travelers), destinations (Tokyo, Paris, Interlaken, Bali), bookings, and messages:
```bash
npm run seed
```

#### 5. Launch Development Servers
Run both client (`vite` on port 5173) and server (`nodemon` on port 5001) concurrently:
```bash
npm run dev
```

Visit `http://localhost:5173` in your browser.

---

### Seed Testing Credentials

| Role | Email Address | Password | Portal Access |
|---|---|---|---|
| 👑 **Administrator** | `admin@travelai.com` | `Admin@123` | Full access to `/admin` dashboard |
| 🎒 **Trip Organiser** | `organiser@travelai.com` | `Organiser@123` | Access to `/organiser` management hub |
| 👤 **Regular Traveler** | `user@travelai.com` | `User@123` | Tokyo Expedition chat & booking access |
| 👤 **Regular Traveler 2**| `elena@travelai.com` | `User@123` | Standard community participant |

---

## 13. Environment Variables

### Backend Configuration (`server/.env`)

| Variable Name | Required | Default / Example | Purpose |
|---|---|---|---|
| `PORT` | Optional | `5001` (Render provides `10000`) | Network port on which the Express server listens |
| `MONGO_URI` | **Yes** | `mongodb+srv://user:pass@cluster.mongodb.net/travelai` | MongoDB Atlas connection string |
| `SESSION_SECRET`| **Yes** | `32+_random_character_string` | Secret key used to encrypt `express-session` cookies |
| `NODE_ENV` | **Yes** | `development` \| `production` | Enables secure HTTPS-only cookies in production |
| `CLIENT_URL` | **Yes (Prod)**| `https://pathora-travel-ai.vercel.app` | Whitelisted origin for CORS and Socket.IO |
| `ALLOWED_ORIGINS`| Optional | `https://custom.com,https://preview.vercel.app` | Comma-separated list of secondary allowed origins |

---

### Frontend Configuration (`client/.env`)

| Variable Name | Required | Default / Example | Purpose |
|---|---|---|---|
| `VITE_GOOGLE_GEMINI_AI_API_KEY` | **Yes** | `AIzaSy...` | API key from Google AI Studio for Gemini 1.5 Flash |
| `VITE_BACKEND_URL` | **Yes (Prod)**| `https://pathora-backend-9jfw.onrender.com` | URL of the deployed Express backend (no trailing slash) |
| `VITE_API_URL` | Optional | `${VITE_BACKEND_URL}/api` | Explicit override for REST base URL |

---

## 14. Security Implementation

1. **Session Cookies over Plain JWTs**:
   - Instead of storing JWTs in browser `localStorage` (vulnerable to XSS attacks), Pathora uses HTTP-only, encrypted session cookies (`connect.sid`).
   - In production (`NODE_ENV=production`), cookies enforce `secure: true` (HTTPS only) and `sameSite: 'none'` (cross-site Vercel-to-Render transport).
   - Instant server-side revocation: sessions can be destroyed immediately in the `sessions` collection on logout or user deletion.

2. **Bcrypt Password Encryption**:
   - Passwords are salt-hashed using `bcryptjs` with 10 rounds prior to database insertion. Raw passwords are never stored or returned in API responses (`select("-password")`).

3. **Dynamic CORS Whitelist**:
   - `corsOriginHandler` in `server/index.js` restricts cross-origin resource requests strictly to verified domains, explicitly preventing unauthorized domains while dynamically permitting Vercel preview environments (`.endsWith('.vercel.app')`).

4. **Role-Based Access Control (RBAC)**:
   - Three tiered middleware functions (`verifyToken`, `verifyAdmin`, `verifyOrganiser`) inspect `req.session.user` and reject unauthorized attempts with `401 Unauthorized` or `403 Forbidden`.

5. **Socket.IO Handshake Authentication**:
   - Socket connections pass through `io.use(wrap(sessionMiddleware))`. Unauthenticated sockets or unverified non-admin users are rejected at the TCP handshake stage before entering any rooms.

6. **Relational Cascade Cleanup**:
   - Deleting a user or trip triggers an atomic cascade cleanup in `server/routes/users.js` and `server/routes/trips.js`, removing orphaned bookings, messages, notifications, and pulling references from all users' `favorites` arrays.

---

## 15. Error Handling & Fault Tolerance

1. **Deterministic Fallbacks for External APIs**:
   - If the OpenStreetMap Overpass API experiences high latency or rate limits, `AIModel.jsx` intercepts the error and transparently injects structured fallback hotel and landmark templates.
   - If Google Gemini AI encounters a quota limit, `defaultItineraryGrouping()` algorithmically distributes places across days using geographic heuristics.

2. **Mongoose CastError Prevention**:
   - All dynamic ObjectId routes (e.g., `/api/trips/:id`, `/api/messages/:tripId`) pre-validate ID length and hexadecimal structure (`/^[0-9a-fA-F]{24}$/`) before issuing database queries, preventing uncaught 500 CastErrors.

3. **Graceful Startup Auto-Bootstrap**:
   - The database startup handler in `server/index.js` wraps the admin auto-bootstrap check in a `try...catch` block, ensuring that any temporary index conflict does not crash the server process.

---

## 16. Testing & Code Quality

### Current Status
- **Linting**: Configured with **ESLint 9** (`client/eslint.config.js`) adhering to modern React Hooks and React Refresh rules.
- **Syntax Validation**: Both client and server codebases enforce strict ECMAScript 2022 module standards.

### Recommended Test Suite Roadmap
To elevate test coverage for enterprise benchmarks, the following suite is recommended:
- **Unit Testing**: Vitest + React Testing Library for UI components and hooks (`AuthContext.test.jsx`, `TripFilters.test.jsx`).
- **Integration Testing**: Supertest against Express routes with an in-memory MongoDB runner (`mongodb-memory-server`) to validate auth, trip creation, and RBAC cascades.
- **End-to-End Testing**: Playwright tests simulating the complete user journey: Registration -> AI Trip Generation -> Join Request -> Admin Approval -> Group Chat.

---

## 17. Deployment Guide

Pathora is designed for split deployment:
- **Frontend SPA**: Hosted on **Vercel** with global CDN distribution.
- **Backend API & WebSockets**: Hosted on **Render** (Node.js web service).
- **Database**: Hosted on **MongoDB Atlas**.

```mermaid
flowchart TD
    User([End User Browser])
    Vercel["Vercel Edge Network<br/>(pathora-travel-ai.vercel.app)"]
    Render["Render Web Service<br/>(pathora-backend-9jfw.onrender.com)"]
    Atlas[("MongoDB Atlas Cloud<br/>(M0 Cluster)")]
    GoogleAI(["Google Gemini AI<br/>(gemini-1.5-flash)"])

    User -->|1. HTTPS: Fetch SPA Assets| Vercel
    User -->|2. HTTPS REST Calls with connect.sid| Render
    User <-->|3. WSS: Full-Duplex WebSockets| Render
    Vercel -->|4. AI Day-Clustering Prompt| GoogleAI
    Render <-->|5. ODM Queries & Session Store| Atlas
```

### Deployment Configuration Reference
- **Frontend (`vercel.json`)**:
  ```json
  {
    "buildCommand": "cd client && npm install && npm run build",
    "outputDirectory": "client/dist",
    "rewrites": [{ "source": "/(.*)", "destination": "/index.html" }]
  }
  ```
- **Backend (`render.yaml`)**:
  ```yaml
  services:
    - type: web
      name: travel-ai-backend
      runtime: node
      rootDir: server
      buildCommand: npm install
      startCommand: node index.js
      healthCheckPath: /health
  ```

---

## 18. Performance & Scalability

1. **Offloading Sessions to MongoStore**:
   - Storing session states in MongoDB (`connect-mongo`) eliminates memory leaks in the Node.js process and allows the server to restart or scale without terminating active user logins.

2. **MongoDB TTL Indexes**:
   - The `Message` collection utilizes a background TTL index (`{ expires: 0 }` on `expiresAt`) that automatically garbage-collects read messages, capping database growth.

3. **Parallel Asynchronous Fetching**:
   - In `AIModel.jsx`, hotel queries and attraction queries are executed concurrently via `Promise.all([fetchRealHotels(), fetchTouristPlaces()])`, halving initial itinerary generation time.

4. **Selective Query Projections**:
   - User lookups routinely specify `.select("-password")` to minimize payload serialization overhead and prevent accidental exposure of password hashes.

---

## 19. Engineering Decisions & Trade-offs

### 1. Cookie-Based Sessions vs. Stateless JWTs
- **Decision**: Implemented `express-session` with `connect-mongo` instead of storing JWTs in `localStorage`.
- **Benefits**: Eliminates XSS vulnerabilities associated with JavaScript-accessible token storage; enables immediate server-side revocation on logout or account termination.
- **Trade-off**: Requires cross-origin cookie negotiation (`SameSite=None; Secure`) and an external store query for session validation.

### 2. Client-Side AI & Geospatial Orchestration vs. Server Proxy
- **Decision**: Executed Nominatim geocoding, Overpass queries, and Gemini day-clustering directly from the client service (`AIModel.jsx`).
- **Benefits**: Distributes heavy JSON parsing and external API latency to client threads, preventing the free-tier Node backend from blocking on large XML/JSON responses.
- **Trade-off**: Requires exposing the Gemini API key to client builds (mitigated via Google Cloud domain referrer restrictions).

### 3. Semi-Structured MongoDB Document vs. Strict Relational Schema
- **Decision**: Stored generated itineraries as a flexible `tripData: Object` inside MongoDB.
- **Benefits**: Accommodates varying destination schemas (cities, islands, rural regions with different amenity tags) without requiring complex multi-table joins.
- **Trade-off**: Schema enforcement on nested places relies on application logic rather than database constraints.

---

## 20. Known Limitations & Technical Roadmap

| Current Limitation | Root Cause | Proposed Roadmap Solution |
|---|---|---|
| **Base64 Chat Images** | Media sent as base64 strings in Socket payloads | Integrate AWS S3 / Cloudinary with pre-signed URLs to store only image URIs |
| **Single-Node Socket.IO** | In-memory socket room adapters | Implement `@socket.io/redis-adapter` with Redis Pub/Sub for horizontal server scaling |
| **Client-Side Gemini Key** | API key initialized in Vite bundle | Migrate AI orchestration to a dedicated server endpoint (`POST /api/trips/generate`) |
| **API Rate Limiting** | OpenStreetMap Overpass rate throttles | Implement server-side Redis caching for popular destination queries |

---

## 21. Interview Preparation Section

*Use this section as a quick reference during technical interviews to articulate the architectural decisions, trade-offs, and implementation details of Pathora.*

### ⏱️ 30-Second Elevator Pitch
> *"Pathora is a full-stack group travel planning platform built on the MERN stack. Unlike generic travel apps that generate hallucinated itineraries, Pathora uses a hybrid geospatial pipeline: it resolves real coordinates via OpenStreetMap Nominatim, queries real operating hotels and attractions through the Overpass API, enriches them with Wikipedia cultural context, and uses Google Gemini 1.5 Flash strictly to cluster and schedule those real places into balanced daily itineraries. It also features session-authenticated Socket.IO group chats with 24-hour auto-expiring messages and an enterprise 3-tier RBAC system."*

---

### ⏱️ 2-Minute Architectural Deep-Dive
> *"Architecturally, Pathora is divided into an SPA on Vercel and an Express/Socket.IO backend on Render, connected to MongoDB Atlas.*
>
> *On the frontend, we use React 18 with Vite, Tailwind CSS v4, and React Router v7. For itinerary generation, we avoid pure LLM generation to prevent hallucinations. Instead, our `AIModel.jsx` service runs parallel queries to the Overpass API for real attractions within 10km and real hotels within 5km, pulls encyclopedic summaries from Wikipedia REST endpoints, and then prompts Gemini 1.5 Flash with structured JSON schemas to cluster those real attractions by day, theme, and opening hours.*
>
> *On the backend, rather than storing JWTs in localStorage where they are vulnerable to XSS, we use `express-session` backed by `connect-mongo`. To support cross-origin requests between Vercel and Render, our cookies use `SameSite=None; Secure`. Socket.IO wraps the session middleware during its handshake, allowing it to authenticate incoming WebSocket connections without requiring duplicate tokens.*
>
> *We've also implemented an event-driven notification engine and room-based group chat (`trip_{tripId}`) restricted to verified travelers. When notifications are marked read, a MongoDB TTL index automatically schedules the underlying chat messages to purge after 24 hours. Finally, administrative deletions enforce complete relational cascade cleanups across all five collections."*

---

### 💡 Core Engineering Challenges & Solutions

1. **Cross-Origin Cookie Negotiation Across Vercel & Render**:
   - *Problem*: Modern browsers block third-party cookies by default when the frontend (`vercel.app`) and backend (`onrender.com`) reside on different domains.
   - *Solution*: Configured `trust proxy: 1` on Express, set cookie parameters to `SameSite=None; Secure: true`, and implemented a dynamic CORS whitelist resolver supporting Vercel preview deploys.

2. **WebSocket Authentication Without Duplicate Token Systems**:
   - *Problem*: Standard WebSocket implementations often require passing separate JWTs in query params or socket headers.
   - *Solution*: Shared Express session middleware with Socket.IO via `io.use(wrap(sessionMiddleware))`. The socket handshake extracts and verifies the session directly from the cookie jar.

3. **Eliminating LLM Hallucinations in Itinerary Generation**:
   - *Problem*: LLMs frequently invent non-existent hotels, incorrect addresses, or permanently closed attractions.
   - *Solution*: Grounded the AI pipeline in deterministic geospatial data. Overpass API fetches real coordinates and verified landmarks first; Gemini 1.5 Flash is strictly confined to logical day-clustering and thematic sequencing.

---

### ❓ 16 Project-Specific Technical Interview Q&As

#### Q1: Why did you choose cookie-based sessions with MongoStore over stateless JWTs?
> **Answer**: JWTs stored in `localStorage` are vulnerable to XSS attacks, while JWTs in cookies cannot be easily revoked server-side without maintaining a token blacklist. By using `express-session` with `connect-mongo`, we achieve server-side revocation on logout or account ban, prevent JavaScript access via `HttpOnly`, and offload session memory from the Node heap to MongoDB.

#### Q2: How does Socket.IO authenticate users without a JWT header?
> **Answer**: In `server/index.js`, we wrap the session middleware using a bridge function (`wrap = mw => (socket, next) => mw(socket.request, {}, next)`). When a client connects with `withCredentials: true`, Socket.IO passes the incoming cookies to `express-session`, which extracts the session from MongoDB and attaches `socket.request.session.user`. If the session is absent or unverified, the handshake is rejected.

#### Q3: How do you handle cross-origin cookie restrictions between Vercel and Render?
> **Answer**: We set `app.set('trust proxy', 1)` so Express respects the `X-Forwarded-Proto` header from Render's load balancer. In production, cookies are flagged with `secure: true` (only sent over HTTPS) and `sameSite: 'none'` (permits cross-site context). The CORS configuration dynamically whitelists the Vercel domain and allows credentials.

#### Q4: How does the hybrid AI pipeline prevent travel hallucinations?
> **Answer**: Instead of prompting Gemini to "invent a trip to Tokyo", `AIModel.jsx` first calls OpenStreetMap Nominatim for coordinates and Overpass API for real hotel/attraction nodes within 5–10km. It enriches landmarks with real Wikipedia extracts. Gemini is only fed the verified list of place names and instructed to cluster them into morning/afternoon/evening slots based on proximity and opening hours.

#### Q5: How does the 24-hour message expiration (TTL) work in MongoDB?
> **Answer**: The `Message` schema defines `expiresAt: { type: Date, index: { expires: 0 } }`. Initially, `expiresAt` is undefined. When a user marks a chat notification as read via `PUT /api/notifications/:id/read`, the server sets `message.expiresAt = new Date(Date.now() + 24 * 60 * 60 * 1000)`. MongoDB's background TTL thread periodically purges expired documents.

#### Q6: How do you prevent data orphans when a user or trip is deleted?
> **Answer**: In `server/routes/users.js` and `trips.js`, deletion handlers execute sequential cascade cleanups using Mongoose `deleteMany()`: deleting a user cascades to all their trips, all bookings made by or for them, their chat messages, their notifications, and pulls their trip IDs from all other users' `favorites` arrays via `$pull`.

#### Q7: How is Role-Based Access Control enforced on the backend?
> **Answer**: We use tiered Express middleware: `verifyToken` checks that `req.session.user` exists. `verifyAdmin` executes `verifyToken` and verifies that `req.user.role === 'admin'`. `verifyOrganiser` checks that `role === 'organiser' || role === 'admin'`. Unauthenticated or unauthorized requests immediately return 401 or 403 status codes.

#### Q8: How do you prevent Mongoose CastErrors when invalid IDs are passed?
> **Answer**: In routes like `GET /api/trips/:id` and `GET /api/messages/:tripId`, we run regex validation (`/^[0-9a-fA-F]{24}$/`) before querying Mongoose. If invalid, the endpoint immediately returns `400 Bad Request` instead of allowing Mongoose to throw an uncaught 500 CastError.

#### Q9: What happens if the Overpass API is slow or rate-limited?
> **Answer**: `AIModel.jsx` implements structured fault tolerance. If Overpass fails or returns fewer than 3 hotels, `getFallbackData()` injects curated destination fallbacks with Unsplash imagery. If Gemini fails, `defaultItineraryGrouping()` mathematically distributes places across days, ensuring the user always receives a functional itinerary.

#### Q10: Why store `tripData` as an `Object` instead of normalizing it into relational tables?
> **Answer**: A travel itinerary contains heterogeneous geographic data: cities have subway proximity, rural regions have trail access, hotels have variable amenity tags. Storing the verified itinerary as a semi-structured JSON document allows the UI to render flexible timeline components without executing expensive multi-table joins.

#### Q11: How do you prevent a user from joining a group chat room without approval?
> **Answer**: In `server/index.js`, when a socket emits `join_chat` with `{ tripId }`, the server queries the `Booking` collection to verify an `approved` status for that `userId` and `tripId`, or confirms the user is the trip creator or an admin. If validation fails, it emits an `error` event and aborts `socket.join()`.

#### Q12: How does the startup auto-bootstrap work?
> **Answer**: In `server/index.js`, right inside `mongoose.connect().then()`, we query `User.findOne({ email: "admin@travelai.com" })`. If not found, it generates a salt, hashes `Admin@123`, and creates the superadmin record with `role: "admin"` and `isVerified: true`. This guarantees fresh deployments are immediately usable.

#### Q13: What is the bottleneck if 10,000 users connect to Socket.IO concurrently?
> **Answer**: Currently, Socket.IO runs on a single Node process storing room assignments in memory. Under high concurrency, the single event loop will saturate. The solution is to introduce `@socket.io/redis-adapter` with a Redis Pub/Sub cluster, enabling horizontal scaling across multiple containerized Node instances.

#### Q14: Why is sending base64 images over WebSockets a technical debt item?
> **Answer**: Base64 encoding inflates binary payload size by approximately 33%, consuming server bandwidth and bloating MongoDB document sizes. The production solution is to upload directly to S3 or Cloudinary via pre-signed URLs, transmitting only lightweight CDN URLs over Socket.IO.

#### Q15: How does Pathora maintain fast search on the Explore feed?
> **Answer**: The `/api/trips` endpoint applies a compound filter: `{ isPublic: true, status: "approved" }`. Query parameters like `minDays`, `maxDays`, and `budget` append range filters (`$gte`, `$lte`), while destination search uses case-insensitive regex indexing, returning only public approved trips.

#### Q16: How does the frontend handle session restoration on page reload?
> **Answer**: In `AuthContext.jsx`, an `useEffect` hook fires `checkAuth()` on mount, sending `GET /api/auth/me`. If the session cookie is valid, the server returns the user profile, dispatching `LOGIN_SUCCESS`. If the cookie is expired or invalid, it dispatches `LOGOUT`, clearing loading states without relying on insecure `localStorage`.

---

## 22. License & Acknowledgments

### License
This project is licensed under the **MIT License** — see the [`LICENSE`](./LICENSE) file for details.

### Acknowledgments
- [OpenStreetMap Nominatim](https://nominatim.org/) & [Overpass API](https://overpass-api.de/) for open geospatial data.
- [Wikimedia Foundation](https://www.mediawiki.org/wiki/API:REST_API) for the Wikipedia REST API.
- [Google AI](https://ai.google.dev/) for the Gemini 1.5 Flash generative engine.
- [Radix UI](https://www.radix-ui.com/) & [Lucide Icons](https://lucide.dev/) for accessible interface primitives.

<div align="center">

**Developed with ❤️ by [Vivek Kumar Verma](https://github.com/vivekVerma2806)**

⭐ *If you find Pathora insightful or useful for your engineering interviews, please consider starring the repository!* ⭐

</div>
