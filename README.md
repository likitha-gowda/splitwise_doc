Project Requirements – Splitwise Clone (Full-Stack)
1. Core Functional Requirements
   ---------------------------

User Authentication

Register (username, email, password)

Login (JWT authentication)

Password hashing (bcrypt)

Authorization middleware (protect routes)

User & Group Management

Create group (assign a name, description, base currency)

Add/remove members to a group

List groups a user belongs to

Expense Management

Add expenses (amount, description, payer, date, category, currency)

Split logic (equal, percentage, or custom)

View all expenses in a group

Edit/delete expenses (by creator or admin)

Balance & Settlement

Show balances per group (who owes whom)

Record settlements (payment between two users)

View settlement history

Currency Conversion

Convert expenses to group’s base currency (using API like exchangerate.host
)

Show balances in unified currency

Expense Insights

Charts: Monthly expense trends, per-category distribution

Expense history timeline

2. Non-Functional Requirements
   ---------------------------

Performance

Optimize DB queries (indexes where needed)

Pagination for expenses

Security

Use JWT securely

Store passwords as hashed (bcrypt)

Prevent SQL injection (ORM or parameterized queries)

CORS setup

Scalability

Modular backend structure (controllers, services, routes, middleware)

Reusable React components

3. Database Schema (PostgreSQL)
   -------------------------

Users
(id, username, email, password, created_at)

Groups
(id, name, base_currency, created_by, created_at)

GroupMembers
(id, group_id, user_id, joined_at)

Expenses
(id, group_id, paid_by, amount, currency, description, category, created_at)

Settlements
(id, group_id, payer_id, receiver_id, amount, currency, settled_at)

4. Frontend (React + Vite + Tailwind)
   -------------------------------------

Pages:

Register, Login

Dashboard (list groups)

Group Detail (expenses, balances, settlements)

Add Expense

Expense Insights (charts)

Components:

Navbar, Auth forms, GroupCard, ExpenseForm, BalanceCard

State management: Context API or Redux

API calls: Axios

Testing: Jest + React Testing Library

Deployment: Vercel/Netlify

5. Backend (Node.js + Express)
   ----------------------------

Routes:

/auth/register, /auth/login

/groups/create, /groups/my, /groups/:id/members

/expenses/add, /expenses/:groupId

/settlements/add, /settlements/:groupId

Middleware:

Auth (JWT validation)

Error handler

Logging (Morgan/Winston)

DB integration: Sequelize or Knex.js

Testing: Jest + Supertest

Deployment: Render/Railway

6. DevOps Requirements
   ------------------

Docker

Dockerfile for frontend & backend

Docker Compose (frontend + backend + PostgreSQL + pgAdmin)

Kubernetes

Deployments (frontend, backend, postgres)

Services (ClusterIP, NodePort, LoadBalancer)

ConfigMaps & Secrets (env vars)

CI/CD

GitHub Actions pipeline:

Run tests (frontend + backend)

Build Docker images

Push to DockerHub

Deploy to Kubernetes/Render

Monitoring

Logging: Winston (backend)

Metrics: Prometheus + Grafana (stretch goal)

7. AI Integration (Optional / Stretch Goals)
   --------------------------------------

Expense Categorization: Use OpenAI API to auto-tag expenses (e.g., “Uber ride” → Travel, “Pizza” → Food).

Smart Insights: AI suggestions like “Your biggest expense last month was dining, consider budgeting.”

Chatbot Integration: Ask AI “How much do I owe John this month?” and get quick answers.

8. Testing Requirements
   -------------------

Frontend

Unit tests: Form validation, component rendering

Integration tests: Login → Dashboard navigation

Backend

Unit tests: Controllers, services

API tests: Supertest for routes (/auth, /groups, /expenses)

CI/CD: Run all tests before deployment

9. Deliverables
    -------------

Fully working Splitwise clone

Auth + Groups + Expenses + Settlements

Currency conversion

Charts & insights

Deployed frontend (Vercel/Netlify)

Deployed backend (Render/Railway)

PostgreSQL (Supabase/Railway)

Docker & Kubernetes setup

CI/CD pipeline (GitHub Actions)

Unit & integration tests

AI integration (optional)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------

Day 1 – Project Setup & Architecture
----------------------------------

🔹 Goals: Lay foundation for frontend, backend, and DB.

Create repo with client/ (React) + server/ (Node/Express) + db/ (SQL migrations).

Setup PostgreSQL in Docker Compose (postgres + pgAdmin).

Backend setup: express, dotenv, sequelize/knex, cors.

Frontend setup: vite, tailwind, axios, react-router-dom.

Create ERD & migrations (Users, Groups, GroupMembers, Expenses, Settlements).

📚 Learn:

Sequelize basics
 or Knex.js

Docker Compose for Postgres

Day 2 – Authentication (JWT)
--------------------------

🔹 Goals: Secure user management.

Backend:

/auth/register, /auth/login

Hash passwords (bcrypt)

JWT issue & verify (access token)

Middleware: Auth validation.

Frontend:

Register & Login pages

Store JWT in localStorage

Protected routes (React Router).

Tests:

Backend: Jest + Supertest (/auth endpoints).

Frontend: Form validation unit tests.

📚 Learn:

JWT Auth in Node.js

React Private Routes

Day 3 – Groups & Members
------------------------

🔹 Goals: Add collaboration features.

Backend:

/groups/create, /groups/my

/groups/:id/members (add/remove)

DB: Groups & GroupMembers tables.

Frontend:

Dashboard with group list

Create group form/modal.

Tests:

Backend: Group API with mock users.

Frontend: GroupCard component test.

📚 Learn:

Express Router

React Context API
 (for auth/group state)

Day 4 – Expenses
----------------

🔹 Goals: Core functionality.

Backend:

/expenses/add, /expenses/:groupId

Balance calculation logic.

Frontend:

Expense form (who paid, amount, description)

Expense list per group.

Tests:

Backend: Supertest API test (/expenses)

Frontend: Render expense list with mock API.

📚 Learn:

Postgres transactions

React forms

Day 5 – Settlements + Currency Conversion
-----------------------------------------

🔹 Goals: Handle debts & currency.

Backend:

/settlements/add, /settlements/:groupId

Integrate ExchangeRate API for currency conversion.

Frontend:

Show balances (“You owe …”)

Settlement button to mark payments.

Expense insights → Recharts (pie, bar, line).

Tests:

Backend: Test settlement API with balance updates.

Frontend: Test currency display logic.

📚 Learn:

exchangerate.host API

Recharts

Day 6 – DevOps (Docker + Kubernetes + CI/CD)
--------------------------------------------

🔹 Goals: Production-ready setup.

Dockerize backend (Node Alpine image).

Dockerize frontend (multi-stage build → nginx).

Docker Compose: Full stack (frontend, backend, postgres, pgAdmin).

Kubernetes:

deployment.yaml (FE, BE, DB)

service.yaml (ClusterIP, NodePort, LoadBalancer)

configmap.yaml, secret.yaml

CI/CD with GitHub Actions:

Run tests → Build Docker images → Push to DockerHub → Deploy.

📚 Learn:

Dockerizing Node.js

Kubernetes basics

GitHub Actions CI/CD

Day 7 – Testing, Monitoring & Deployment
----------------------------------------

🔹 Goals: Final polish + Deployment.

Tests:

Backend: Jest coverage report.

Frontend: RTL snapshot tests.

Logging: Morgan (HTTP logs), Winston (structured logs).

Deployment:

Frontend → Vercel/Netlify

Backend → Render/Railway

DB → Supabase/Railway

Monitoring (stretch goal): Prometheus + Grafana.

AI Integration (optional):

OpenAI API → auto-categorize expenses (“Pizza → Food”).

Natural language queries: “How much do I owe John?”


--------------------------------------------------------------------------------------------------------------------------------------------------------

Project Architecture
--------------------

          ┌────────────────────────────┐
          │        Frontend (React)    │
          │  - Login, Dashboard, UI    │
          │  - Fetch/POST APIs         │
          └─────────────▲──────────────┘
                        │
                        ▼
          ┌────────────────────────────┐
          │    Backend (Node.js API)   │
          │  Auth, Groups, Expenses    │
          │  Balances, Settlements     │
          │  Currency Conversion       │
          │  AI Categorization Proxy   │
          └───────▲───────────┬────────┘
                  │           │
                  │           │
                  ▼           ▼
    ┌──────────────────┐   ┌────────────────────┐
    │   PostgreSQL DB   │   │  External Services │
    │ Users, Groups,    │   │ - Currency API     │
    │ Expenses, Shares  │   │ - AI Categorizer   │
    └───────────────────┘   └────────────────────┘

                  │
                  ▼
        ┌───────────────────────┐
        │   CI/CD + Deployment  │
        │ Docker / Kubernetes   │
        │ GitHub Actions, AWS   │
        └───────────────────────┘

------------------------------------------------------------------------------------------------------------------------------------------------------------



