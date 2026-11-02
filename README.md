# Backend REST API (Node.js, Express & MongoDB)

A complete RESTful backend API built with **Node.js**, **Express.js**, and **MongoDB Atlas** (using **Mongoose** ODM).

Developed by **Vaibhav Saini**.

---

## Architecture & Features

This project implements an **MVC (Model-Route-Controller)** architecture:

- **Authentication Module**:
  - `POST /api/v1/users/register`: Registers a new user with salted password hashing via `bcrypt`.
  - `POST /api/v1/users/login`: Validates user credentials with hashed password comparison.
  - `POST /api/v1/users/logout`: Handles user logout workflow.
- **CRUD Posts Module**:
  - `POST /api/v1/posts/create`: Create a new character/entity post.
  - `GET /api/v1/posts/getPosts`: Fetch all stored posts from MongoDB.
  - `PATCH /api/v1/posts/update/:id`: Update post fields by ID with Mongoose schema validation.
  - `DELETE /api/v1/posts/delete/:id`: Delete a post document by ID.

---

## Project Structure

```text
yay webdev/
├── backend/
│   ├── src/
│   │   ├── config/         # Database connection logic & constants
│   │   │   ├── constants.js
│   │   │   └── database.js
│   │   ├── controllers/    # Business logic & request handling
│   │   │   ├── user.controller.js
│   │   │   └── post.controller.js
│   │   ├── models/         # Mongoose data schemas
│   │   │   ├── user.model.js
│   │   │   └── post.model.js
│   │   ├── routes/         # Express endpoint definitions
│   │   │   ├── user.route.js
│   │   │   └── post.route.js
│   │   ├── app.js          # Express app configuration & middleware
│   │   └── index.js        # Server entry point & DB bootstrap
│   ├── .env.example        # Environment variable template
│   ├── .gitignore          # Git exclusion rules
│   └── package.json        # Project metadata & npm scripts
├── postman/                # Ready-to-import Postman collections
│   ├── Users.postman_collection.json
│   └── CRUD.postman_collection.json
└── Readme.md
```

---

## Setup & Running Locally

### 1. Prerequisites
- **Node.js** (v18 or higher recommended; check with `node -v`)
- A **MongoDB Atlas** account (free M0 cluster)
- **Postman** (for testing API endpoints)

### 2. Install Dependencies
```bash
cd backend
npm install
```

### 3. Configure Environment Variables
Inside the `backend/` folder, create a `.env` file from `.env.example`:
```env
MONGODB_URL=mongodb+srv://<username>:<password>@<cluster>.mongodb.net/?retryWrites=true&w=majority
PORT=4000
```
> **Security Note:** Replace `<username>` and `<password>` with your MongoDB Atlas database user credentials. Never commit `.env` to Git.

### 4. Start the Server
Development mode (auto-reloads on file changes via `nodemon`):
```bash
npm run dev
```

Production start:
```bash
npm start
```

When connected, terminal outputs:
```text
Connecting to MongoDB (1/5)...
MongoDB connected!!! Host: ...
Server is running on port 4000
```

---

## API Documentation

Base URL: `http://localhost:4000`

### Authentication Endpoints (`/api/v1/users`)

| Method | Endpoint | Description | Sample Request Body |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/v1/users/register` | Register new user | `{"username": "vaibhav", "email": "vaibhav@example.com", "password": "SecurePass123"}` |
| `POST` | `/api/v1/users/login` | Login user | `{"email": "vaibhav@example.com", "password": "SecurePass123"}` |
| `POST` | `/api/v1/users/logout` | Logout user | `{"email": "vaibhav@example.com"}` |

### CRUD Post Endpoints (`/api/v1/posts`)

| Method | Endpoint | Description | Sample Request Body / Param |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/v1/posts/create` | Create a post | `{"name": "Vaibhav", "description": "Full Stack Dev", "age": 21}` |
| `GET` | `/api/v1/posts/getPosts` | Retrieve all posts | None |
| `PATCH` | `/api/v1/posts/update/:id` | Partial update | `{"description": "Lead Architect", "age": 22}` (Pass `_id` in URL) |
| `DELETE` | `/api/v1/posts/delete/:id` | Delete post by ID | None (Pass `_id` in URL) |

---

## Postman Testing
Pre-configured collections are available in the [`postman/`](file:///postman) directory:
1. Open Postman -> Click **Import**.
2. Select `postman/Users.postman_collection.json` and `postman/CRUD.postman_collection.json`.
3. Test requests in order: Register -> Login -> Create Post -> Get Posts -> Update Post -> Delete Post.
