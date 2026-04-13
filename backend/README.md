# AURA Backend

This directory contains the FastAPI backend for **AURA (Automated Unified Recovery Agent)**. The backend is responsible for processing return data, running decision logic, integrating computer vision outputs, and generating explainable recovery recommendations.

---

## 📁 Project Structure

```
app/
├── routes/      # API layer (HTTP endpoints)
├── services/    # Core business logic
├── models/      # Data schemas (Pydantic)
└── data/        # Mock / seed data
```

---

## 📂 Folder Responsibilities

### 🔹 `routes/`

* Defines API endpoints (e.g., `/decision`)
* Handles request and response flow
* Should NOT contain business logic

**Example responsibilities:**

* Accept request input
* Call appropriate service
* Return structured response

---

### 🔹 `services/`

* Contains all core logic of the system
* This is the most important layer

**Includes:**

* Decision engine (resell / repair / recycle logic)
* Optimization logic (ranking repair centers, buyers)
* Explainability generation
* CV integration wrapper (`cv_service`)

---

### 🔹 `models/`

* Defines request and response schemas using Pydantic

**Purpose:**

* Input validation
* Clear API contracts
* Auto-generated API documentation

---

### 🔹 `data/`

* Stores mock or seed data for development

**Examples:**

* Repair center data
* Buyer / scrap vendor data

⚠️ This will be replaced by a database in later stages.

---

## 🧠 Design Principles

* Keep **routes thin** → no logic inside routes
* Keep logic inside **services/**
* Maintain **clear separation of concerns**
* Build the system as **modular components**

---

## ⚙️ System Flow

```
Request → Route → Service Layer → Decision Engine → Optimization → Response
```

---

## 🚀 Running the Server

```bash
uvicorn app.main:app --reload
```

Access API docs at:

* [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

---

## ⚠️ Best Practices

* Do NOT place business logic inside `routes/`
* Do NOT tightly couple CV logic with decision logic
* Always return structured and explainable responses
* Keep functions small and modular
* Use mock data through `data/` instead of hardcoding values

---

## 🐳 Notes for Future
* Database layer will be added later (PostgreSQL)
* External APIs will replace mock data where applicable