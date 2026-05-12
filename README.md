Danial Shakeel – BSCS23175

# PDC Assignment 2 – Building Resilient Distributed Systems

## Repository Name

PDC-Sp24-BSCS23175-Shakeel

---

# Project Overview

This project is based on a distributed FastAPI and React architecture inspired by the StudySync scenario from the assignment.

The system demonstrates how synchronization issues occur in distributed applications and implements a solution using Optimistic Locking to prevent the Lost Update anomaly.

The backend is built using FastAPI while the frontend is developed using React and Vite.

---

# Assignment Problem Implemented

## Synchronization Problem (Lost Update Anomaly)

When two users edit the same shared document simultaneously, one user's update may overwrite the other user's changes.

### Implemented Solution

Optimistic Locking using document version control.

Each document stores:
- content
- version number

Before updating:
1. Backend checks the document version.
2. If versions match:
   - update succeeds
   - version increments
3. If versions differ:
   - request is rejected
   - conflict response is returned

This prevents concurrent overwrite issues in distributed systems.

---

# Technologies Used

## Backend
- Python
- FastAPI
- Pydantic
- Requests
- SQLite

## Frontend
- React
- Vite

---

# Project Structure

```text
PDC-Sp24-BSCS23175-Shakeel/
│
├── backend/
│   ├── server.py
│   ├── test_challenge_fix.py
│   ├── database.db
│   ├── pyproject.toml
│   ├── src/
│   │   ├── app.py
│   │   ├── ai_generator.py
│   │   ├── utils.py
│   │   ├── database/
│   │   │   ├── db.py
│   │   │   └── models.py
│   │   └── routes/
│   │       ├── challenge.py
│   │       └── webhooks.py
│
├── frontend/
│   ├── package.json
│   ├── vite.config.js
│   ├── src/
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   ├── challenge/
│   │   ├── auth/
│   │   ├── history/
│   │   ├── layout/
│   │   └── utils/
│
└── README.md
```

---

# Backend Setup

## Step 1 – Open Backend Folder

```bash
cd backend
```

---

## Step 2 – Install Dependencies

```bash
pip install fastapi uvicorn requests pydantic
```

---

## Step 3 – Run FastAPI Server

```bash
uvicorn src.app:app --reload
```

Backend server will start at:

```text
http://127.0.0.1:8000
```

---

# Frontend Setup

## Step 1 – Open Frontend Folder

```bash
cd frontend
```

---

## Step 2 – Install Node Modules

```bash
npm install
```

---

## Step 3 – Start Frontend

```bash
npm run dev
```

Frontend will start at:

```text
http://localhost:5173
```

---

# API Endpoints

## GET /document

Returns current document data.

Example Response:

```json
{
  "id": 1,
  "content": "Initial Content",
  "version": 1
}
```

---

## PUT /document

Updates document using Optimistic Locking.

Example Request:

```json
{
  "content": "Updated Content",
  "version": 1
}
```

---

# Running Concurrent Test

To simulate concurrent users editing the same document:

```bash
python test_challenge_fix.py
```

---

# Expected Output

```text
User A: 200
Document updated successfully

User B: 409
Conflict detected. Document updated by another user.
```

This proves that the synchronization issue is handled correctly using Optimistic Locking.

---

# Middleware Requirement

According to assignment requirements, every API response includes the following custom header:

```text
X-Student-ID: BSCS23175
```

The header is implemented using FastAPI middleware.

---

# How to Verify Header

Open Swagger Docs:

```text
http://127.0.0.1:8000/docs
```

1. Open GET `/document`
2. Click "Try it out"
3. Click "Execute"
4. Check Response Headers

You will see:

```text
X-Student-ID: BSCS23175
```

---

# Distributed System Concepts Used

- Optimistic Locking
- Concurrency Control
- Synchronization
- Conflict Detection
- Middleware
- Distributed Coordination

---

# Demonstration

The demo video demonstrates:

1. Backend server running
2. Frontend application
3. Concurrent update simulation
4. Conflict prevention
5. Custom middleware header
6. Successful handling of synchronization issues

---

# Author

Danial Shakeel  
BSCS23175
