# CST8913-Lab6
# Assessing the Existing Architecture

## 1. Frontend (React)

### Source Files:

- `/frontend/src/` (React)
- `/Views/` (ASP.NET MVC)
- `/public/` (Static assets, HTML, CSS, JS)

---

## 2. Backend

(Identify backend business logic, API endpoints, controllers, and services.)

### Source Files:

- `/backend/src/` (Node.js)
- `/Controllers/` (ASP.NET Web API)
- `/Services/` (Business logic and helper functions)
- `/routes/` (Express.js )

---

## 3. Database

(Identify how the database is structured and how queries are managed.)

### Source Files:

- `/database/schema.sql` (Database schema and table definitions)
- `/database/migration.sql` (Migration scripts for database changes)
- `/backend/config/database.js` (Database connection settings for Node.js)
- `/appsettings.json` (Database connection string in .NET)
- `/models/` (ORM models, e.g., Entity Framework, Sequelize, Django models)

---

## 4. Background Jobs

(Identify scheduled tasks, worker services, or batch jobs.)

### Source Files:

- `/functions/` (Azure Functions for background tasks)
- `/jobs/` (Custom background workers, Quartz.NET)
- `/backend/workers/` (Worker processes in Node.js)
- `IHostedService` in `/Services/` (For background tasks in .NET)

---

# Plan the Refactoring Strategy

## 1. Break Down the Monolithic Application into Microservices

- Identify tightly coupled components and separate them into independent services.
- Convert large modules into **independent microservices** with their own APIs.
- Ensure each service has **clear boundaries and responsibilities**.

### Source Files:

- `/backend/services/` (New microservices for different business logic)
- `/backend/routes/` (Reorganized API routes for microservices)
- `/frontend/src/services/` (Frontend service calls to new microservices)

---

## 2. Select Appropriate Azure Services

- **Azure App Service** → Host the frontend and backend microservices.
- **Azure SQL Database** → Replace the on-premises SQL Server.
- **Azure Functions** → Handle background tasks and event-driven processes.
- **Azure Blob Storage** → Store static assets, logs, and media files.
- **Azure API Management** → Manage and secure API endpoints.

### Source Files:

- `/azure-config/app-service.json` (Configuration for Azure App Service)
- `/azure-config/sql-database.json` (Configuration for Azure SQL Database)
- `/azure-config/functions.json` (Setup for Azure Functions)
- `/azure-config/blob-storage.json` (Blob Storage setup)
- `/backend/api-gateway/` (API gateway implementation)

---

## 3. Define Authentication and Authorization Strategy using Azure AD

- Integrate **Azure Active Directory (Azure AD)** for authentication.
- Implement **OAuth 2.0** and **OpenID Connect** for secure API access.
- Configure **Role-Based Access Control (RBAC)** for different user roles.

### Source Files:

- `/backend/config/auth.js` (OAuth and Azure AD configuration for Node.js)
- `/appsettings.json` (Azure AD settings for .NET backend)
- `/frontend/src/auth/` (Frontend authentication logic)

---

# Implement Refactoring Changes

## 1. Deploy the Frontend to Azure App Service

- Configure Azure App Service to host the frontend.
- Update environment variables for API endpoints.
- Ensure CI/CD pipelines are set up for automated deployments.

### Source Files:

- `/frontend/src/` (React UI components)
- `/public/` (Static assets, HTML, CSS, JS)

---

## 2. Migrate the Database to Azure SQL Database

- Export data from VM-hosted SQL Server.
- Use **Azure Database Migration Service** to transfer data.
- Update connection strings to point to **Azure SQL Database**.

### Source Files:

- `/database/schema.sql` (Database schema)
- `/database/migration.sql` (Migration scripts)
- `/backend/config/database.js` (Database connection settings for Node.js)
- `/appsettings.json` (Database connection string in .NET)

---

## 3. Convert Background Processing Tasks into Azure Functions

- Identify scheduled tasks and worker processes.
- Refactor them into **serverless Azure Functions**.
- Deploy functions using Azure Function App.

### Source Files:

- `/functions/` (Azure Functions for background tasks)
- `/jobs/` (Custom background workers, Quartz.NET)
- `/backend/workers/` (Worker processes in Node.js)

---

## 4. Store Static Content and Logs Using Azure Blob Storage

- Move static assets (e.g., images, logs) to **Azure Blob Storage**.
- Configure backend services to access files from **Azure Storage Account**.

### Source Files:

- `/storage/` (Static assets and logs)
- `/public/uploads/` (User-uploaded content)
- `/logs/` (Application logs)

---

# Optimize and Test

## 1. Implement Auto-Scaling for the Web Application

- Enable **Azure App Service Auto-Scaling** based on CPU/memory usage.
- Configure **Azure Functions Auto-Scaling** to handle workload spikes.

### Source Files:

- `/azure-config/auto-scaling.json` (Scaling rules and policies)
- `/backend/config/appsettings.json` (App Service configurations)

---

## 2. Configure Logging and Monitoring Using Azure Monitor and Application Insights

- Enable **Application Insights** for detailed telemetry and logging.
- Configure **Azure Monitor** to track infrastructure health and performance.

### Source Files:

- `/backend/config/logging.json` (Logging configuration)
- `/azure-config/monitoring.json` (Azure Monitor setup)

---

## 3. Test the Application’s Performance, Reliability, and Scalability

- Conduct **load testing** using **Azure Load Testing**.
- Perform **failover testing** to ensure high availability.
- Validate **response times and performance metrics**.

### Source Files:

- `/tests/performance/` (Load and stress testing scripts)
- `/tests/integration/` (Integration and failover tests)
- `/backend/config/test-config.json` (Test environment setup)

# Architecture diagram before:
📦 Company-Application

├── 📁 frontend/              # Frontend code (React, ASP.NET MVC)

│   ├── 📁 src/               # React components

│   ├── 📁 Views/             # ASP.NET MVC views

│   ├── 📁 public/            # Static assets (HTML, CSS, JS)

│   ├── package.json          # React dependencies

│   ├── webpack.config.js     # Webpack configuration

│   └── README.md
│

├── 📁 backend/               # Backend code (Node.js, ASP.NET Web API)

│   ├── 📁 src/               # Node.js application files

│   ├── 📁 Controllers/       # ASP.NET Web API controllers

│   ├── 📁 Services/          # Business logic and helper functions

│   ├── 📁 routes/            # Express.js route handlers

│   ├── server.js             # Express.js server entry point

│   ├── appsettings.json      # Configuration settings

│   ├── package.json          # Backend dependencies

│   └── README.md

│
├── 📁 database/              # Database-related files

│   ├── schema.sql            # SQL schema for database tables

│   ├── migration.sql         # Database migration scripts

│   ├── config/database.js    # Database connection settings (Node.js)

│   ├── appsettings.json      # Database connection string in .NET

│   └── README.md

│
├── 📁 background-jobs/       # Background jobs & scheduled tasks

│   ├── job1.js               # Example background job

│   ├── job2.js               # Another scheduled job

│   ├── trigger.js            # Triggers for background tasks

│   ├── IHostedService.cs     # Background worker service in .NET

│   └── README.md

│
├── 📁 storage/               # Static files, logs, and uploads

│   ├── 📁 logs/              # Application logs

│   ├── 📁 uploads/           # User-uploaded content

│   └── README.md

│
├── 📁 tests/                 # Testing files

│   ├── 📁 integration/       # Integration tests

│   ├── 📁 performance/       # Load & stress testing

│   ├── test-config.json      # Test environment configurations

│   └── README.md

│
├── .gitignore                # Git ignore file

├── README.md                 # Project documentation

└── LICENSE                   # License file


# Architecture diagram after:
=======

# Architecture diagram


/repo-root

│── /frontend

│ ├── src/

│ ├── package.json

│ ├── .env

│── /backend

│ ├── src/

│ ├── appsettings.json

│ ├── Dockerfile

│── /functions

│ ├── ProcessEmails/

│ ├── BackgroundJobs/

│── /database

│ ├── migration.sql

│ ├── schema.sql

│── /storage

│── /infra

│ ├── /terraform/

│ │ ├── main.tf

│ │ ├── variables.tf

│ │ ├── outputs.tf

│ ├── /bicep/

│── /docs

│ ├── original-architecture.png

│ ├── refactored-architecture.png

│── .github/workflows/deploy.yml

│── azure-pipelines.yml

│── README.md
