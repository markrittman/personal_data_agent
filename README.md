# personal_data_agent

A multi-user SaaS chatbot application that enables users to query their structured personal data (fitness, location, messages, music history, etc.) using natural language. This application leverages Google Cloud Platform (BigQuery, Vertex AI, Cloud Storage) for secure, scalable storage and processing, and provides a conversational interface built with modern web technologies.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [User Personas](#user-personas)
- [Data Sources](#data-sources)
- [Security Model](#security-model)
- [Deployment Plan](#deployment-plan)
- [Development Roadmap](#development-roadmap)
- [Example User Queries](#example-user-queries)
- [License](#license)

---

## Overview

This application allows authenticated users to:

- Upload structured datasets (e.g. CSVs of Strava workouts, Apple Music play history, exported message logs, etc.).
- Ask natural language questions about their data (e.g. "What was my longest ride last year?" or "How has my weight changed since increasing my cycling distance?").
- Receive analytical answers backed by SQL queries executed in BigQuery and explained via LLM-powered responses.

The application is designed for privacy-conscious individuals who track their personal data and want to explore patterns, trends, and insights through a user-friendly conversational interface.

---

## Features

### ✅ Core Features (MVP)

- User authentication (Firebase Auth)
- Data ingestion (CSV, JSON uploads)
- Schema auto-detection and registration
- BigQuery storage (per-user datasets)
- Vertex AI-powered query planner and response generator
- Natural language Q&A interface (chatbot)

### 🚀 Planned Features (Post-MVP)

- Semantic search on message content via vector embeddings
- Rich visualisations (charts, graphs)
- Multi-dataset joins (e.g. sleep vs activity)
- In-app dataset versioning and updating
- Connectors for API-based ingestion (e.g. Strava, Fitbit, Spotify)

---

## Architecture

### Frontend

- React + TypeScript SPA
- Firebase Auth for secure login
- Chat interface with persistent conversation history (local)
- Axios or Fetch for API communication

### Backend

- FastAPI (Python)
- REST API endpoints:
  - `POST /data/upload`
  - `GET /data/list`
  - `POST /query`
- Firebase Admin SDK to verify ID tokens
- Google Cloud clients (BigQuery, Vertex AI)

### GCP Services

- **BigQuery** – storage and querying of user datasets
- **Cloud Storage** – staging area for uploaded files
- **Vertex AI** – LLM orchestration (e.g. Gemini, PaLM)
- **(Optional) Firestore** – user metadata registry

### Multi-tenancy Design

- Per-user isolation via BigQuery dataset naming (`user_<uid>`)
- IAM policies restrict data access to only the authenticated user
- Metadata registry tracks datasets and schemas per user

---

## User Personas

| Persona | Description | Example Queries |
|--------|-------------|-----------------|
| Quantified Selfer | Tracks everything (fitness, sleep, diet) | "How does my sleep affect my running distance?" |
| Fitness Fanatic | Focused on workouts & recovery | "Did I burn more calories on cardio days?" |
| Music Lover | Links mood or workouts to music | "What genre do I listen to most while running?" |
| Productivity Nerd | Tracks meetings, comms, and time | "Who did I message the most last month?" |

---

## Data Sources

Example dataset categories:

- `fitness.csv` — date, activity, duration, distance, calories
- `weight.json` — timestamp, weight, fat %, muscle mass
- `messages.csv` — timestamp, sender, recipient, content
- `locations.csv` — timestamp, lat/lng, place_name
- `music.json` — timestamp, artist, track, duration

Users can upload datasets via CSV/JSON, and schema is auto-detected. Data is stored in user-specific BigQuery datasets.

---

## Security Model

- Firebase Auth to authenticate all users
- Backend verifies tokens with Firebase Admin SDK
- Per-user data isolation in BigQuery (dataset per UID)
- All data encrypted at rest (GCP-managed keys or CMEK)
- No data is used for training models (Vertex AI private invocation)
- Role-based access to GCP services via service accounts
- GDPR-compliant: user data export and deletion supported

---

## Deployment Plan

- **Frontend**: Firebase Hosting or Cloud Storage static bucket
- **Backend**: Containerised FastAPI app on Cloud Run
- **CI/CD**: GitHub Actions to build and deploy on merge to main
- **Secrets**: GCP Secret Manager + Replit/CI secrets

---

## Development Roadmap

| Phase | Duration | Milestone |
|-------|----------|-----------|
| MVP | 4–6 weeks | Upload + chatbot with simple answers |
| Beta | 2–3 months | Multiple dataset joins + clarifications |
| GA | 6 months | Visualisations, integrations, pricing tiers |

---

## Example User Queries

- "What was my average pace in June 2023?"
- "Compare my sleep before and after I started cycling."
- "When did I visit Paris in the last 2 years?"
- "Which genre did I listen to most while working out?"

---

## License

This project is licensed under the MIT License. See `LICENSE.md` for details.

---

For issues, enhancements or contributions, please open a GitHub Issue or pull request.

