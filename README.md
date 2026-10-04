# NerdMarket

NerdMarket is a stock-market-style trading card marketplace for **Pokémon, Magic: The Gathering, and Yu-Gi-Oh!** cards. It combines live card data, personal collections, price tracking, image-based card matching, and real-time community features in one platform.

Built as a team project for **COM S 309 – Software Development Practices** at Iowa State University.

## Demo

[Watch the application demo on YouTube](https://youtu.be/El1KD3GnCjg)

## Core Features

- **Unified card marketplace** for Pokémon, MTG, and Yu-Gi-Oh! cards
- **Live pricing and price tracking** across multiple card data sources
- **Personal binders and portfolios** for saved cards
- **OpenCV card scanning** to match physical card photos with marketplace listings
- **Real-time chat** using WebSockets
- **Price alerts** for significant card value changes
- **Automated CI/CD** for backend and application builds

## Tech Stack

**Backend:** Java, Spring Boot, Spring Data JPA, Hibernate  
**Database:** MySQL  
**Computer Vision:** OpenCV  
**Real-Time Communication:** WebSockets, STOMP  
**Frontend:** Android / Java  
**Build & DevOps:** Maven, Gradle, GitLab CI/CD  
**External APIs:** TCGdex, Scryfall, YGOPRODeck

## Architecture

The backend follows a service-based Spring Boot architecture with separate components for:

- Users and authentication
- Marketplace data
- Personal binders
- Price tracking
- Chat
- Notifications
- Card scanning

External card APIs are normalized into a shared marketplace model and stored in MySQL.

REST APIs support marketplace and user features, while WebSockets handle real-time chat and notifications.

## Key Technical Features

### Multi-API Card Database

The application combines data from three external trading card APIs into a unified database containing more than **90,000 cards**.

This allows users to search and compare cards across multiple trading card games from one application.

### OpenCV Card Scanning

OpenCV is used to compare uploaded card images with known marketplace cards.

The system extracts image features and attempts to match a physical card photo with the corresponding marketplace listing.

### Real-Time Chat

WebSockets and STOMP messaging support live marketplace chat rooms.

Messages are persisted so users can continue conversations across sessions.

### Price Tracking

Scheduled backend jobs monitor card prices and track changes over time.

Users can receive notifications when cards experience significant price movement.

## Running the Project

### Backend Requirements

- Java 21
- Maven
- MySQL

From the `Backend` directory:

```bash
./mvnw spring-boot:run
```

Configure the MySQL connection in the Spring application configuration before starting the server.

### Frontend

The Android client is located in the `Frontend` directory.

Open the project in Android Studio or build it using Gradle:

```bash
cd Frontend
./gradlew build
```

## Repository Structure

```text
NerdMarket/
├── Backend/      # Spring Boot backend and APIs
├── Frontend/     # Android application
├── Documents/    # Project documentation
└── .gitlab-ci.yml
```

## What This Project Demonstrates

NerdMarket demonstrates full-stack development across:

- REST API development
- Relational databases
- Third-party API integration
- Real-time communication
- Computer vision
- Backend automation
- CI/CD
