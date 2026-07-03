# PollPulse

A polling application built with Spring Boot that lets users create polls, vote, and see results refresh automatically as votes come in.

## Overview

PollPulse is a backend service for creating and managing polls with vote tracking. Built with clean REST API design on a Spring Boot + MySQL stack, it exposes endpoints for creating polls, casting votes, and retrieving live vote counts — the frontend polls the results endpoint periodically to keep counts up to date.

## Features

- 🗳️ **Create Polls** — Create polls with multiple options
- ✅ **Vote on Polls** — Cast a vote for a given poll and option via REST API
- 📊 **Live-Updating Results** — Frontend polls the results endpoint at intervals to reflect new votes
- 🗄️ **MySQL Persistence** — Relational schema for polls and options using Spring Data JPA

## Tech Stack

- **Language:** Java
- **Framework:** Spring Boot
- **Database:** MySQL
- **ORM:** Spring Data JPA
- **Build Tool:** Maven 

## Architecture

```
Client (Web/Postman)
      │
      ▼
 REST Controllers  ──►  Service Layer  ──►  Repository Layer  ──►  MySQL
      │
      ▼
Client polls GET /api/polls/{id} at intervals to refresh vote counts
```

## API Endpoints

| Method | Endpoint           | Description                                  |
|--------|---------------------|-----------------------------------------------|
| POST   | `/api/polls`        | Create a new poll                             |
| GET    | `/api/polls`        | Get all polls                                 |
| GET    | `/api/polls/{id}`   | Get a specific poll by ID (includes vote counts) |
| POST   | `/api/polls/vote`   | Cast a vote (body: `pollId`, `optionIndex`)   |

*No authentication is currently enforced on these endpoints.*

## Getting Started

### Prerequisites
- Java 17+
- MySQL 8+
- Maven 

### Setup

1. Clone the repository
```bash
   git clone https://github.com/yourusername/pollpulse.git
   cd pollpulse
```

2. Configure your database in `application.properties`
```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/pollpulse
   spring.datasource.username=your_username
   spring.datasource.password=your_password
```

3. Run the application
```bash
   ./mvnw spring-boot:run
```

4. The API will be available at `http://localhost:8080`

## Future Improvements

- JWT-based authentication to secure poll creation and voting
- WebSocket/STOMP push for true real-time results instead of client-side polling
- Prevent duplicate voting per user/session
- Poll expiration and scheduling
- Docker support for easier deployment
