# DSIL UI Staging Deployment (Provide and Consume)

This project provides a Docker-based setup for running the **Provide** and **Consume** User Interfaces of the DSIL (Data Space Innovation Lab) locally, using staging images connected to hosted infrastructure (Broker, Identity Provider, and Connector).

## 🚀 Overview

This setup includes:
- **Provide User Interface** (`provide-user-interface`)
- **Consume User Interface** (`consume-user-interface`)

Each UI runs as a Django application inside a Docker container, configured via a shared `.env` file.

## 🛠 Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## 🧾 Environment Variables

Create a `.env` file in the root directory with the following content:

```env
# Django settings for Provide User Interface
DJANGO_SECRET_KEY=your-secret-key
DJANGO_DEBUG=True
DJANGO_ALLOWED_HOSTS=localhost,127.0.0.1
ALLOWED_HOSTS=localhost,127.0.0.1

# Database settings for Provide User Interface
DJANGO_DB_PATH=/app/db.sqlite3

# CORS settings for Provide User Interface
DJANGO_CORS_ALLOWED_ORIGINS=*

# Custom settings
AUTHORIZATION=Basic YWRtaW46cGFzc3dvcmQ=

CONNECTOR_URL=https://sandbox3.collab-cloud.eu
CONNECTOR_BASE=https://sandbox3.collab-cloud.eu

BASE_URL=https://sandbox3.collab-cloud.eu/  # Keep trailing slash
BROKER=https://broker.collab-cloud.eu/broker/infrastructure/    # Keep trailing slash

# SSL settings for Provide User Interface
REQUESTS_VERIFY_SSL=False
```

> ⚠️ Replace `your-secret-key` with a securely generated Django secret key.

## 🐳 Docker Compose Usage

Start both UI services:

```bash
docker-compose up
```

This will:
- Run the **Provide UI** on [http://localhost:8000](http://localhost:8000)
- Run the **Consume UI** on [http://localhost:8001](http://localhost:8001)

## 📦 Docker Images

- `ghcr.io/data-space-core/provide-user-interface/stage:latest`
- `ghcr.io/data-space-core/consume-user-interface-2/stage:latest`

These images are pulled from GitHub Container Registry and are pre-configured to communicate with the hosted connector and broker services.

## 🌐 Networking

Both services are attached to a local bridge network named `local`, allowing easy inter-container communication if needed.

## 🧪 Staging Details

These UI components connect to:
- Hosted **Connector** at `https://sandbox3.collab-cloud.eu`
- Hosted **Broker** at `https://broker.collab-cloud.eu/broker/infrastructure/`

Participants can run local UI interfaces while interacting with centralized services hosted on DSIL staging infrastructure.

## ❗ Notes

- This is a **staging environment** intended for beta testing only.
- There is **no issue tracking system** active; all feedback should be provided via **email**.
- Updates and pull schedules will be communicated manually.

## 🔜 Coming Soon

Planned next steps include:
- Multi-connector support (provider and consumer connectors separately)
- Hosted user interfaces mapped to locally run connectors
- Manual participant registration flow via the UI

---

For support or feedback, please contact the DSIL team directly.
