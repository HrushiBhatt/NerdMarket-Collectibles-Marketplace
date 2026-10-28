<div align="center">

<img src="assets/nerdmarket-banner.svg" alt="NerdMarket — Discover, track, and collect trading cards" width="100%" />

A trading-card marketplace with stock-market-style discovery
Explore cards · Monitor prices · Build collections · Scan cards · Chat in real time






▶ Watch demo · Features · Architecture · Getting started
</div>

Overview
NerdMarket brings together Pokémon, Magic: The Gathering, and Yu-Gi-Oh! cards in a single Android application. Designed around a stock-market-inspired browsing experience, it combines card discovery and pricing information with personal binders, image-based card recognition, and community messaging.

The application was developed as a team project for COM S 309 — Software Development Practices at Iowa State University. This repository contains the Android client, a Java/Spring Boot backend, and supporting project documentation.
Watch the demo
<div align="center">


▶ Watch the complete NerdMarket demo on YouTube
</div>

Features
<div align="center">
<img src="assets/feature-tour.gif" alt="Animated visual overview of NerdMarket features: browse cards, track prices, scan cards, and chat" width="100%" />
</div>

Feature	What it does	Technical implementation
Unified card discovery	Search and browse cards across three major trading card games	Integrates TCGdex, Scryfall, and YGOPRODeck data through backend services
Market data & price tracking	View card prices and follow changes in card value	Spring Boot market and price-tracking services backed by MySQL
Personal binders	Organize saved cards and manage collections	Dedicated binder API, service, and persistence layer
Image-based card matching	Identify a card using an image	OpenCV-based scanning and matching service
Live chat	Participate in community conversations	WebSockets/STOMP with persistent chat messages
Notifications	Receive updates, including price-related events	Notification service, scheduler, and WebSocket messaging


Visual note: The animation above is an illustrative feature tour—not a recording of the application UI. The linked video shows the original project demo.

System architecture
<div align="center">
<img src="assets/architecture.svg" alt="NerdMarket architecture: Android application calls Spring Boot REST and WebSocket services; backend persists data to MySQL, communicates with card APIs, and uses OpenCV for image matching" width="100%" />
</div>

Request flow: The Android client sends HTTP requests to the backend's REST controllers for user, market, binder, price, and scanning functionality. WebSocket controllers support live messaging and notifications. Spring services coordinate database access and external card-data integrations.
Key engineering components
- Layered Spring Boot backend: Separate controllers, services, and repositories for core domains such as users, market listings, binders, chat, and notifications.
- Third-party data integration: Card information from TCGdex, Scryfall, and YGOPRODeck provides coverage across multiple games; the original project reports a combined catalog of 90,000+ cards.
- Computer vision: An OpenCV-powered scanning service attempts to match card images to known card records.
- Real-time communication: WebSocket/STOMP endpoints support live community chat and notifications; chat messages are stored for later retrieval.
- Scheduled price monitoring: Backend price-tracking and notification components support monitoring of changes in card value.
Technology stack
Layer	Technologies
Android client	Java, Android SDK, Gradle
Backend	Java 21, Spring Boot, Spring MVC, Spring Data JPA, Hibernate
Database	MySQL (H2 dependency is also included for development/testing)
Real-time communication	WebSockets, STOMP
Computer vision	OpenCV
Card data sources	TCGdex, Scryfall, YGOPRODeck
Build / project tooling	Maven Wrapper, Gradle Wrapper, GitLab CI configuration


Repository layout
NerdMarket/
├── Backend/
│   ├── src/main/java/NerdMarket/
│   │   ├── users/             # User domain
│   │   ├── market/            # Marketplace data
│   │   ├── binders/           # Collections and binders
│   │   ├── prices/            # Price tracking
│   │   ├── scanning/          # Card image matching
│   │   ├── chat/              # Chat and WebSocket handlers
│   │   └── notifications/     # Alerts and notification handlers
│   ├── src/main/resources/
│   └── pom.xml
├── Frontend/                 # Android/Gradle projects and sources
├── Documents/                # Design notes and project documentation
├── Experiments/              # Coursework experiments / prototypes
├── assets/                   # README graphics (add from this package)
└── README.md
Getting started
Prerequisites
- JDK 21
- Android Studio with the Android SDK
- MySQL with a database and credentials configured for the backend
- Git
1. Clone the repository
git clone git@github.com:HrushiBhatt/NerdMarket.git
cd NerdMarket
2. Configure and start the backend
Review Backend/src/main/resources/application.properties and supply the appropriate local database settings. Do not commit passwords, tokens, or machine-specific secrets. Prefer environment variables or ignored local configuration for credentials.
cd Backend
./mvnw spring-boot:run
The backend requires a reachable database and any other environment-specific configuration expected by the application. A successful startup depends on that setup.

3. Open and run the Android application
Open Frontend/ in Android Studio, allow Gradle to synchronize, select the intended Android app module, and run it on an emulator or connected device. Verify that the app's configured backend base URL points to your running backend. For an Android emulator connecting to a backend on your Mac, the host is commonly reachable as 10.0.2.2 rather than localhost.

For command-line build checks:
cd Frontend
./gradlew build
This repository contains additional Android projects and experiments. Choose the app module you intend to demonstrate when running from Android Studio.

Project context and contributions
NerdMarket originated as a team-built university software project. This repository preserves the project and its original contributor history. Individual commits and the Git history provide a record of contributions; any subsequent independent refactoring can be documented separately.
<div align="center">

NerdMarket — A connected marketplace for collectors.

Back to top
</div>
