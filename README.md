# Mini-Agent-Platform
通用智能体开发平台（Mini-Agent Platform）

## MVP implementation

This repository starts as a runnable backend-first MVP. It provides a FastAPI service with SQLite persistence, encrypted-at-rest provider keys, admin JWT authentication, configurable agents and model endpoints, document ingestion (TXT/Markdown/HTML/CSV/DOCX/PDF), local hashed bag-of-words retrieval, and OpenAI-compatible chat with optional RAG. Qdrant and Redis are optional deployment services; local SQLite and an on-disk vector index keep the demo usable without them.

### Run locally

```bash
cd backend
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
uvicorn app.main:app --reload
```

On first launch an admin account and demo agent are created from `ADMIN_USERNAME` and `ADMIN_PASSWORD` (defaults are for local development only). API documentation is available at `/docs`. Configure an encryption key and JWT secret before deployment. Model keys are write-only: responses only indicate whether a key is configured.

Create an admin JWT via `POST /api/v1/auth/admin/login`, then send it as `Authorization: Bearer <token>`. Configure a model, attach it to an agent, create a knowledge base, and upload documents to its `/documents` route. Chat endpoints return actual provider responses and source references; no provider configured means an explicit service error.

### Scope

This MVP intentionally delivers the backend runtime and REST interfaces first. Native WeChat mini-program and Vue administration clients, MySQL/Redis production deployment, durable background workers, and Qdrant-backed retrieval are follow-up work and are not represented as implemented here. SQLite processing is synchronous for local development.
