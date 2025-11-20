# 🎰 crash-game-qa-lab

**Crash Game API & Frontend (QA & E2E Testing)**

[![Node.js](https://img.shields.io/badge/Node.js-18+-green.svg)](https://nodejs.org/)  
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-DB-blue.svg)](https://www.postgresql.org/)  
[![React](https://img.shields.io/badge/Frontend-React-61DAFB.svg)](https://reactjs.org/)  
[![Cypress](https://img.shields.io/badge/Cypress-E2E-orange.svg)](https://www.cypress.io/)  
[![Coverage](https://img.shields.io/badge/Coverage-95%25-brightgreen.svg)](cypress/reports/index.html)  

This project was developed as a **realistic QA and E2E environment**, simulating a *Crash Game* with a complete backend, real data persistence (PostgreSQL), and real-time WebSocket. Ideal for:

* **Functional and E2E Automation Testing** (Cypress, Playwright, Robot Framework)  
* **Financial Reconciliation** and data integrity  
* **Resilience Testing** with simulated failures  
* **Critical Business Flow Validation**  

---

## ✨ Main Features

* **Real Data Persistence**  
  Tables (`users`, `wallet`, `bets`) allow integrity and financial reconciliation tests.  

* **Real Transaction Flow**  
  The `/bet/place` endpoint verifies balance, debits the account, and records the bet.  

* **E2E WebSockets**  
  Real-time updates on the frontend.  

* **Resilience and Error Testing**  
  Dedicated routes simulate server failures and transaction rollbacks.  

* **JWT Authentication**  
  Allows testing token injection and authentication flows.

---

## 🛠 Technologies Used

| Component       | Technology                 | Details                           |
|-----------------|----------------------------|----------------------------------|
| Backend          | Node.js, Express           | API and WebSocket                |
| Database         | PostgreSQL                 | Real data persistence            |
| DB Connection    | `pg`                       | Efficient connection pool        |
| Frontend         | React, Vite                | Modern UI                        |
| Automation       | Cypress / Robot Framework  | Functional and integration tests |

---

## ⚙ Repository Structure

backend/        # API + WebSocket server

frontend/       # React/Vite frontend

cypress/        # Cypress tests

tests/          # Robot / integration tests

README.md

---

## 💾 PostgreSQL Setup

1. Install PostgreSQL or use a cloud service (Railway, Supabase).  

2. Create the database:

```sql
CREATE DATABASE fast_game;

3.  Create the tables:
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  email TEXT NOT NULL,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

CREATE TABLE wallet (
  id SERIAL PRIMARY KEY,
  user_id INT REFERENCES users(id),
  balance NUMERIC DEFAULT 1000,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

CREATE TABLE bets (
  id SERIAL PRIMARY KEY,
  user_id INT REFERENCES users(id),
  round_id INT,
  amount NUMERIC NOT NULL,
  multiplier NUMERIC,
  created_at TIMESTAMPTZ DEFAULT NOW()
);
```
4. Configure the .env file in the backend:
```sql
DB_HOST=localhost
DB_PORT=5432
DB_USER=postgres
DB_PASSWORD=your_supersecretpassword
DB_NAME=crash_game
JWT_SECRET=your_secret_key
```

5.	Run the backend:
cd backend
npm install
npm run dev

6.	Run the frontend:
cd frontend
npm install
npm run dev



## 🧪 Test Scenarios (QA / E2E)

| Scenario             | Description                                    | Expected Result                          |
|---------------------|------------------------------------------------|------------------------------------------|
| **Valid Bet**        | Logged-in user with enough balance bets $100  | Correct debit and bet recorded           |
| **Invalid Bet**      | Logged-in user with insufficient balance bets $1000 | Bet rejected, balance unchanged      |
| **Simulated Error**  | Force error via `/debug/simulate-error`       | Rollback applied, balance integrity maintained |
| **WebSocket**        | Open 2 tabs, place a bet in one               | Real-time update reflected in the other tab |
| **Data Reconciliation** | Compare `bets` and `wallet` after multiple bets | Data consistency ensured               |



📊 Reports, Coverage, and Screenshots
	•	Cypress Report: Click here￼
	•	Test Coverage: 
	•	Screenshots:
	•	Bet Success￼
	•	Bet Failure￼
	•	WebSocket Update￼

⸻

🎯 Project Purpose
	•	Demonstrate advanced QA and E2E automation
	•	Financial reconciliation and data integrity
	•	Resilience testing and error handling
	•	Validate complex backend + frontend real-time flows

⸻

💡 GitHub Pages Tip:
If you place this README in the main branch and enable GitHub Pages, all badges, reports, and screenshots will be clickable and interactive, creating a professional online portfolio.
