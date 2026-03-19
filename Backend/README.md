# Backend

A scalable Node.js/TypeScript backend application with a modular directory architecture designed for maintainability and growth.

## Table of Contents

- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Available Scripts](#available-scripts)
- [Environment Variables](#environment-variables)
- [Architecture Overview](#architecture-overview)
- [Adding New Features](#adding-new-features)

## Technology Stack

| Technology | Purpose |
|------------|---------|
| [Node.js](https://nodejs.org/) | JavaScript runtime |
| [TypeScript](https://www.typescriptlang.org/) | Type-safe JavaScript |
| [Express](https://expressjs.com/) | Web framework |
| [ts-node](https://typestrong.org/ts-node/) | TypeScript execution engine |
| [nodemon](https://nodemon.io/) | Development hot-reload |

## Project Structure

```
Backend/
├── src/
│   ├── @types/           # Global TypeScript type definitions
│   ├── configs/          # Application configuration files
│   ├── controllers/      # Request handlers (MVC pattern)
│   ├── database/         # Database connection & migrations
│   ├── middlewares/      # Express middleware functions
│   ├── models/           # Data models/entities
│   ├── routes/           # API route definitions
│   ├── services/         # Business logic layer
│   ├── utils/            # Utility functions & helpers
│   ├── validations/      # Input validation logic
│   └── index.ts          # Application entry point
├── .env                  # Environment variables (local development)
├── .sample.env           # Environment variables template
├── package.json          # Dependencies and scripts
└── tsconfig.json         # TypeScript configuration
```

### Directory Purpose

| Directory | Description |
|-----------|-------------|
| [`src/@types/`](src/@types/) | Global TypeScript interfaces, types, and type declarations |
| [`src/configs/`](src/configs/) | Configuration modules (e.g., database config, app settings) |
| [`src/controllers/`](src/controllers/) | Handle incoming requests, process logic, return responses |
| [`src/database/`](src/database/) | Database connection setup, ORM/migration configurations |
| [`src/middlewares/`](src/middlewares/) | Express middleware (auth, logging, error handling, etc.) |
| [`src/models/`](src/models/) | Data models/schemas representing database entities |
| [`src/routes/`](src/routes/) | API route definitions and route mappings |
| [`src/services/`](src/services/) | Business logic and reusable services |
| [`src/utils/`](src/utils/) | Helper functions, constants, and utilities |
| [`src/validations/`](src/validations/) | Request validation schemas and rules |

## Getting Started

### Prerequisites

- Node.js (v18 or higher)
- npm or yarn

### Installation

```bash
# Navigate to Backend directory
cd Backend

# Install dependencies
npm install
```

### Configuration

1. Copy the sample environment file:

```bash
# Windows
copy .sample.env .env

# Linux/MacOS
cp .sample.env .env
```

2. Edit `.env` and configure your database and application settings:

```env
PORT=3001
DATABASE_NAME=your_db_name
DATABASE_USER=your_db_user
DATABASE_PASSWORD=your_db_password
DATABASE_HOST=localhost
DATABASE_PORT=5432
NODE_ENV=development
```

### Development

Start the development server with hot-reload:

```bash
npm run dev
```

The server will start on `http://localhost:3001` (or the port specified in `.env`).

### Production Build

```bash
# Compile TypeScript
npm run build

# Start production server
npm start
```

## Available Scripts

| Script | Description |
|--------|-------------|
| `npm run dev` | Start development server with hot-reload |
| `npm run build` | Compile TypeScript to JavaScript |
| `npm start` | Start production server |

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `PORT` | Server port number | `3001` |
| `DATABASE_NAME` | Database name | - |
| `DATABASE_USER` | Database username | - |
| `DATABASE_PASSWORD` | Database password | - |
| `DATABASE_HOST` | Database host | `localhost` |
| `DATABASE_PORT` | Database port | - |
| `FORCE_DROP_TABLES` | Drop all tables on startup (dangerous) | `false` |
| `FORCE_ALTER_TABLES` | Force alter tables on startup | `false` |
| `NODE_ENV` | Environment mode (`development`, `production`) | - |

## Architecture Overview

### Design Pattern: MVC with Service Layer

This project follows a modified MVC (Model-View-Controller) pattern with an additional service layer for better separation of concerns:

```
Request → Routes → Controllers → Services → Models → Database
                ↓
            Middlewares
                ↓
            Validations
```

### Layer Responsibilities

1. **Routes** - Define API endpoints and map to controllers
2. **Controllers** - Handle HTTP requests/responses, orchestrate flow
3. **Services** - Contain business logic, reusable operations
4. **Models** - Define data structures and database schemas
5. **Middlewares** - Process requests before they reach controllers
6. **Validations** - Validate incoming request data
7. **Utils** - Shared helper functions
8. **Configs** - Application-wide configuration

### Benefits of This Architecture

- **Scalability** - Each layer has a single responsibility, making it easy to add new features
- **Testability** - Services and utilities can be unit tested independently
- **Maintainability** - Clear separation of concerns
- **Team Collaboration** - Multiple developers can work on different layers simultaneously

## Adding New Features

### Example: Creating a New API Endpoint

1. **Create a Model** (optional, if database is involved):

```typescript
// src/models/User.ts
export interface User {
  id: string;
  name: string;
  email: string;
  createdAt: Date;
}
```

2. **Create a Service**:

```typescript
// src/services/userService.ts
import { User } from '../models/User';

export const userService = {
  async getAllUsers(): Promise<User[]> {
    // Business logic here
    return [];
  },
  
  async getUserById(id: string): Promise<User | null> {
    // Business logic here
    return null;
  }
};
```

3. **Create a Controller**:

```typescript
// src/controllers/userController.ts
import { Request, Response } from 'express';
import { userService } from '../services/userService';

export const userController = {
  async getAllUsers(req: Request, res: Response) {
    try {
      const users = await userService.getAllUsers();
      res.json(users);
    } catch (error) {
      res.status(500).json({ error: 'Failed to fetch users' });
    }
  }
};
```

4. **Create a Route**:

```typescript
// src/routes/userRoutes.ts
import { Router } from 'express';
import { userController } from '../controllers/userController';

const router = Router();

router.get('/users', userController.getAllUsers);

export default router;
```

5. **Register the Route** in `src/index.ts`:

```typescript
import express from 'express';
import userRoutes from './routes/userRoutes';

const app = express();

app.use('/api', userRoutes);

app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

---

Built with TypeScript ❤️
