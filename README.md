# 💸 E-Invoice Processing API

A RESTful API for generating, transforming, validating, and delivering e-invoices.

Developed for **SENG2021**, this project implements a complete, production-style invoice processing pipeline using FastAPI, structured APIs, and modern backend practices.

---

## 🚀 Overview

This API provides an end-to-end workflow for handling invoices:

1. **Generation** – Convert human-readable input into structured invoice data  
2. **Transformation** – Convert structured data into UBL-compliant XML  
3. **Validation** – Validate invoices using internal rules and external APIs  
4. **Delivery** – Send validated invoices via email  

The API is versioned:

- **v1** → baseline implementation  
- **v2** → improved validation, storage, and delivery features  

---

## 🛠 Tech Stack

- **Backend:** FastAPI (Python 3.12)
- **Database:** PostgreSQL (via SQLAlchemy ORM) *(SQLite used in testing)*
- **Authentication:** JWT Bearer Tokens
- **External Integration:** DevEx validation API
- **Deployment:** Render
- **CI/CD:** GitLab CI (lint + test pipeline)
- **Documentation:** OpenAPI 3 (Swagger UI)

---

## 📦 Features

- RESTful, versioned API (`/v1`, `/v2`)
- Full invoice lifecycle pipeline
- JWT authentication with Swagger integration
- XML transformation and validation
- External validation proxy (DevEx API)
- Email delivery (v2)
- Structured error handling and response models
- Modular architecture (routes, services, schemas)
- Automated testing with `pytest`
- Linting with `ruff`

---

## 📁 Project Structure

```
app/
├── routes/           # API endpoints (generation, transform, validate, deliver)
├── services/         # Business logic layer
├── schemas/          # Pydantic request/response models
├── models/           # SQLAlchemy ORM models
├── db.py             # Database setup and session management
├── auth.py           # JWT authentication dependency
├── config.py         # Application configuration
├── templates/        # HTML templates (landing page)
├── main.py           # FastAPI entry point

alembic/              # Database migrations
alembic.ini           # Alembic configuration

.gitlab-ci.yml        # CI pipeline (lint + tests)
```

---

## ⚙️ Local Setup

This project provides a setup script to initialise the development environment.

### Run the setup script

```bash
bash setup_local.sh
```

This will:

- Create and activate a virtual environment  
- Install all required dependencies  
- Configure environment variables (if applicable)  

---

## ▶️ Running the Application

```bash
uvicorn app.main:app --reload
```

Then open:

- Swagger UI: http://127.0.0.1:8000/docs  
- Health check: http://127.0.0.1:8000/health  
- DB check: http://127.0.0.1:8000/db/ping  

---

## 🔐 Authentication

This API uses **JWT Bearer authentication**.

### Using Swagger:

1. Click **Authorize**
2. Enter:

```
Bearer <your_token>
```

3. Access protected endpoints

---

## 📘 API Endpoints

### Generation
- `POST /v1/generation/invoices`
- `POST /v2/generation/invoices`

### Transformation
- `POST /v1/transform/invoices/{invoice_id}`
- `POST /v2/transform/invoices/{invoice_id}`

### Validation
- `POST /v1/validate/invoices/{invoice_id}`
- `POST /v2/validate/invoices/{invoice_id}`
- `POST /v2/validate` *(raw XML validation)*

### External Validation (DevEx Proxy)
- `POST /external/validate-doc/{document_type}`

### Delivery (v2 only)
- `POST /v2/deliver/invoices/{invoice_id}`

---

## 🧪 Testing

Testing is automated using **pytest** and integrated into CI.

Run locally:

```bash
pytest
```

Tests include:

- Route testing with FastAPI `TestClient`
- Service layer validation
- Mocked external dependencies
- Auth overrides for isolated testing

---

## 🔄 CI/CD Pipeline

GitLab CI pipeline includes:

- Dependency installation
- Linting with `ruff`
- Automated testing with `pytest`

Pipeline runs on pushes to `main`.

---

## 🧱 Database & Migrations

This project uses **Alembic** for database migrations.

### Run migrations:

```bash
alembic upgrade head
```

### Create a new migration:

```bash
alembic revision --autogenerate -m "description"
```

---

## 📊 API Design Notes

- Built using **OpenAPI 3 specification**
- Strong typing via Pydantic schemas
- Consistent response models across endpoints
- Clear error handling (400, 401, 404, 500)
- Separation of concerns:
  - routes → HTTP layer
  - services → business logic
  - schemas → validation

---

## 🤝 Contributing

1. Create a feature branch  
2. Make changes  
3. Run lint + tests  
4. Submit a merge request  

---

## 👥 Authors

- Dollarsigns Team (SENG2021)

---

## 📄 License

This project is for academic purposes only.
