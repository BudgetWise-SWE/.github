# BudgetWise

**BudgetWise** is a full-stack personal budgeting platform. Track income and expenses, set budget limits, visualize spending patterns, and save toward financial goals — all through a clean, responsive interface.

---

## Repositories

### [BudgetWise-BackEnd](https://github.com/BudgetWise-SWE/BudgetWise-BackEnd)

The API and business logic layer, built with **Django REST Framework** and deployed on Vercel.

| Technology | Purpose |
|---|---|
| Python / Django REST Framework | API server & business logic |
| PostgreSQL (Supabase) | Relational data store |
| Vercel | Hosting & deployment |
| MkDocs / OpenAPI (Swagger/ReDoc) | API documentation |

**Modules:**

| Module | Responsibility |
|---|---|
| `accounts` | Session-based authentication, custom user profiles, currency config |
| `finance` | Transaction CRUD, categorical classification, budget allocation |
| `planning` | Savings goals, spending limits |
| `analytics` | Dashboard summaries, spending distributions, trend reports |
| `notifications` | Event-driven alerts for budget thresholds and milestones |

**[→ Backend Repository](https://github.com/BudgetWise-SWE/BudgetWise-BackEnd)** · [Live API](https://budget-wise-back-end.vercel.app/api/docs/) · [Documentation](https://MuhammaddFouadd.github.io/BudgetWise-BackEnd/)

---

### [BudgetWise-FrontEnd](https://github.com/BudgetWise-SWE/BudgetWise-FrontEnd)

A modular client-side application built with **vanilla HTML, CSS, and JavaScript (ES modules)**.

| Technology | Purpose |
|---|---|
| HTML5 | Page structure |
| CSS3 (Flexbox / Grid) | Responsive layouts |
| JavaScript (ES modules) | Interactivity, state management, API integration |
| Material Symbols | Iconography |
| Chart.js | Spending visualizations |

**Pages:**

| Page | Description |
|---|---|
| `index` | Landing page |
| `login` / `signup` | Authentication with token-based session |
| `dashboard` | Overview — total balance, income, expenses, recent transactions |
| `transaction` | Add and view income/expense records with category selection |
| `budgets` | Monthly budget limits with visual status indicators |
| `savings` | Savings goal creation and progress tracking |
| `history` | Full transaction history with pagination |

**[→ Frontend Repository](https://github.com/BudgetWise-SWE/BudgetWise-FrontEnd)**

---

## Architecture

### System Overview

```mermaid
graph TB
    subgraph Client["Browser"]
        FE["BudgetWise-FrontEnd<br/><small>HTML / CSS / JS</small>"]
    end

    subgraph Vercel["Vercel (Hosting)"]
        API["BudgetWise-BackEnd<br/><small>Django REST Framework</small>"]
    end

    subgraph Supabase["Supabase (Cloud)"]
        DB[("PostgreSQL<br/><small>Database</small>")]
    end

    FE -->|"REST API (JSON)"| API
    API -->|"ORM"| DB
```

### Request Flow

```mermaid
sequenceDiagram
    actor U as User
    participant FE as Frontend<br/>(Browser)
    participant API as Django REST API
    participant Auth as Accounts Module
    participant Fin as Finance Module
    participant DB as PostgreSQL

    U->>FE: Interacts with UI
    FE->>API: HTTP Request (JSON)
    API->>Auth: Authenticate & Authorize
    Auth->>DB: Verify Session
    DB-->>Auth: Session Valid
    Auth-->>API: User Context
    API->>Fin: Process Transaction / Budget
    Fin->>DB: CRUD Operation
    DB-->>Fin: Result Set
    Fin-->>API: Response Data
    API-->>FE: JSON Response
    FE-->>U: Render Updated View
```

### Backend Module Interactions

```mermaid
graph LR
    subgraph API["Django REST Framework"]
        A["Accounts<br/><small>Auth & Profiles</small>"]
        F["Finance<br/><small>Transactions & Budgets</small>"]
        P["Planning<br/><small>Goals & Limits</small>"]
        N["Notifications<br/><small>Alerts</small>"]
        AN["Analytics<br/><small>Reports</small>"]
    end

    A -->|"User Context"| F
    A -->|"User Context"| P
    F -->|"Transaction Data"| AN
    P -->|"Goal Progress"| AN
    F -->|"Budget Events"| N
    P -->|"Milestone Events"| N
    N -->|"Alerts"| F
```

---

## Getting Started

**Backend**
```bash
git clone https://github.com/BudgetWise-SWE/BudgetWise-BackEnd.git
cd BudgetWise-BackEnd
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
```

**Frontend**
```bash
git clone https://github.com/BudgetWise-SWE/BudgetWise-FrontEnd.git
cd BudgetWise-FrontEnd
# Open index.html in your browser, or use Live Server
```

---

## License

All repositories are licensed under the [MIT License](https://opensource.org/licenses/MIT).
