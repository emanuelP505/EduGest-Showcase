# EduGest — System Architecture Diagram

## Overview

This diagram represents the high-level architecture of EduGest, showing the relationship between the frontend, deployment platform, backend API, domain services and PostgreSQL database.

## Architecture

```mermaid
flowchart TB
    USER["User"]

    subgraph FRONTEND["Frontend Layer"]
        UI["HTML5 / CSS3 / JavaScript"]
        PAGES["Application Pages"]
        CLIENT["Client-side Modules"]
        UI --> PAGES
        UI --> CLIENT
    end

    subgraph PLATFORM["Deployment Platform"]
        VERCEL["Vercel"]
        SERVERLESS["Serverless Functions"]
        VERCEL --> SERVERLESS
    end

    subgraph BACKEND["Backend Layer"]
        API["Node.js API"]
        AUTH["Authentication Utilities"]
        SERVICES["Domain Services"]
        API --> AUTH
        API --> SERVICES
    end

    subgraph DOMAINS["Business Domains"]
        ACADEMIC["Academic Management"]
        FINANCIAL["Financial Management"]
        ADMIN["Administrative Management"]
        COMMUNICATION["Communication"]
    end

    subgraph PERSISTENCE["Persistence Layer"]
        DB["PostgreSQL"]
        PG["Node.js PostgreSQL Client (pg)"]
        PG --> DB
    end

    USER --> UI
    CLIENT --> VERCEL
    SERVERLESS --> API
    SERVICES --> ACADEMIC
    SERVICES --> FINANCIAL
    SERVICES --> ADMIN
    SERVICES --> COMMUNICATION
    SERVICES --> PG
```

## Architectural Characteristics

- Modular monolithic backend.
- Native frontend technologies.
- Centralized API request handling.
- Domain-oriented business services.
- PostgreSQL relational persistence.
- Serverless backend deployment through Vercel.

**Note:** The business domains represent functional responsibilities rather than independently deployed services.