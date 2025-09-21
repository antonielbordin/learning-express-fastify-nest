# 📚 Learning Track - Mini Budget System

## 🎯 About the Project

This project is a practical application to learn and compare three popular Node.js frameworks: Express.js, Fastify, and NestJS. The system consists of a RESTful API for budget management, with user authentication and complete CRUD operations.

## 📋 Features

### 🔐 Authentication

  - User registration - POST /auth/register
  - JWT login - POST /auth/login
  - Route protection with authentication middleware

### 💰 Budget Management

  - Create budget - POST /budgets (authenticated)
  - List user budgets - GET /budgets
  - View specific budget - GET /budgets/:id
  - Update budget - PUT /budgets/:id
  - Delete budget - DELETE /budgets/:id

### 📦 Budget Items Management

  - Add item - POST /budgets/:id/items
  - List items - GET /budgets/:id/items
  - Remove item - DELETE /budgets/:id/items/:itemId

## 🗃️ Data Model

This application against the following entities: Users, budgets and Budget Items, follows the script for creating the database tables. In the study example, I will use MySQL.

```sql
-- Users Table
CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(30) NOT NULL,
  email VARCHAR(30) UNIQUE NOT NULL,
  password VARCHAR(100) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Budgets Table
CREATE TABLE budgets (
  id INT AUTO_INCREMENT PRIMARY KEY,
  userId INT NOT NULL,
  title VARCHAR(100) NOT NULL,
  total DECIMAL(10, 2) DEFAULT 0.00,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  FOREIGN KEY (userId) REFERENCES users(id) ON DELETE CASCADE
);

-- Budget Items Table
CREATE TABLE budget_items (
  id INT AUTO_INCREMENT PRIMARY KEY,
  budgetId INT NOT NULL,
  description TEXT NOT NULL,
  quantity INT DEFAULT 1,
  price DECIMAL(10, 2) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (budgetId) REFERENCES budgets(id) ON DELETE CASCADE
);
```

## 🚀 Technologies Used

  - Node.js - JavaScript runtime environment
  - Express.js - Minimalist web framework
  - Fastify - High-performance web framework
  - NestJS - TypeScript framework for scalable applications
  - JWT - Token authentication
  - MySQL - Relational database
  - Joi/Zod - Data validation (depending on framework)

## 📦 Project Structure

```text
learning-express-fastify-nest/
│
├── express-app/                 # Express.js implementation
│   ├── src/
│   │   ├── controllers/         # Route logic
│   │   ├── middleware/          # Authentication and validation
│   │   ├── models/              # Data models
│   │   ├── routes/              # Route definitions
│   │   └── config/              # Database configuration
│   ├── package.json
│   └── README.md
│
├── fastify-app/                 # Fastify implementation
│   ├── src/
│   │   ├── plugins/             # Fastify plugins
│   │   ├── routes/              # Routes with validation schemas
│   │   ├── services/            # Business logic
│   │   └── schemas/             # Validation schemas
│   ├── package.json
│   └── README.md
│
├── nestjs-app/                  # NestJS implementation
│   ├── src/
│   │   ├── auth/                # Authentication module
│   │   ├── budgets/             # Budgets module
│   │   ├── users/               # Users module
│   │   ├── shared/              # Shared resources
│   │   └── app.module.ts        # Main module
│   ├── package.json
│   └── README.md
│
├── LICENSE                      $ Using MIT
└── README.md                    # This file
```

## 🛠️ How to Run

### Prerequisites

  - Node.js (v16 or higher)
  - MySQL (v8 or higher)
  - npm or yarn or pnpm (my recomendation is pnpm)

### Database Setup

  1. Create a MySQL database
  2. Execute the SQL script provided above
  3. Configure environment variables in each project

### Running Each Implementation

Express.js

```bash
cd express-app
npm install
cp .env.example .env
# Configure environment variables
npm run dev
```

Fastify

```bash
cd fastify-app
npm install
cp .env.example .env
# Configure environment variables
npm run dev
```

NestJS

```bash
cd nestjs-app
npm install
cp .env.example .env
# Configure environment variables
npm run start:dev
```

## 📊 API Endpoints
Authentication

| Method | Endpoint | Description
| POST	| /auth/register	| Register new user
| POST	| /auth/login	| Login and obtain token

Budgets (requires authentication)

| Method | Endpoint | Description
| GET	| /budgets	| List user budgets
| POST	| /budgets	| Create new budget
| GET	| /budgets/:id	| Get specific budget
| PUT	| /budgets/:id	| Update budget
| DELETE	| /budgets/:id	| Delete budget

Budget Items (requires authentication)

| Method | Endpoint | Description
| GET	| /budgets/:id/items	| List budget items
| POST	| /budgets/:id/items	| Add item to budget
| DELETE	| /budgets/:id/items/:itemId	| Remove item from budget


## 🔐 Authentication

All protected routes require the authorization header:

```text
Authorization: Bearer <JWT_TOKEN>
```

## 🧪 Testing the API

User registration example:

```bash
curl -X POST http://localhost:3000/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "email": "john@email.com",
    "password": "password123"
  }'
```

Login example:

```bash
curl -X POST http://localhost:3000/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "john@email.com",
    "password": "password123"
  }'
```

Budget creation example:

```bash
curl -X POST http://localhost:3000/budgets \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <YOUR_JWT_TOKEN>" \
  -d '{
    "title": "Website Project",
    "total": 5000.00
  }'
```

## 🎯 Learning Objectives

  1. Express.js:
    - Middlewares and routing system
    - Node.js project structure
    - Database integration

  2. Fastify:
    - Built-in validation schemas
    - Performance and optimization
    - Plugin system

  3. NestJS:
    - Modular architecture
    - Dependency injection
    - Decorators and TypeScript
    - Enterprise approach

## 📈 Implementation Comparison

At the end of development, it will be possible to compare:

  - Amount of code required
  - Performance of each implementation
  - Ease of development and maintenance
  - Learning curve of each framework
  - Native features vs. external dependencies
 
## 📝 License

This project is intended for educational purposes.