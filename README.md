# Personal Contact Manager

A full-stack web application for managing personal and professional contacts with user authentication. Built with Node.js, Express, MongoDB, and vanilla HTML/CSS/JavaScript.

---

## Tech Stack

| Layer          | Technology                  |
|----------------|-----------------------------|
| Backend        | Node.js + Express 5         |
| Database       | MongoDB + Mongoose           |
| Authentication | JSON Web Tokens + bcryptjs  |
| Frontend       | HTML, CSS, JavaScript       |
| Hosting        | Render.com                  |
| Database Host  | MongoDB Atlas               |
| API Testing    | Postman                     |

---

## Features

- User registration and login with JWT authentication
- Password hashing with bcrypt before database storage
- User-scoped contacts — each user only sees their own data
- Create, read, update, and delete contacts
- Mark contacts as favorites with instant toggle
- Add personal notes to any contact
- Real-time search across name, email, and phone number
- Filter contacts by type (Personal or Professional)
- Clickable dashboard counters for quick filtering
- Persistent login via localStorage token storage
- Fully deployed and accessible from any browser

---

## API Endpoints

### Authentication

| Method | Endpoint              | Description                                          | Auth Required |
|--------|-----------------------|------------------------------------------------------|---------------|
| POST   | `/api/auth/register`  | Create a new account. Returns a JWT token.           | No            |
| POST   | `/api/auth/login`     | Log in with email and password. Returns a JWT token. | No            |
| GET    | `/api/auth/me`        | Get the currently logged-in user's info.             | Yes           |

### Contacts

All contact endpoints require a valid JWT token in the Authorization header as a Bearer token.

| Method | Endpoint                        | Description                                      |
|--------|---------------------------------|--------------------------------------------------|
| GET    | `/api/contacts`                 | Get all contacts for the logged-in user          |
| GET    | `/api/contacts/:id`             | Get a single contact by ID                       |
| POST   | `/api/contacts`                 | Create a new contact                             |
| PUT    | `/api/contacts/:id`             | Update an existing contact                       |
| DELETE | `/api/contacts/:id`             | Delete a contact                                 |
| PATCH  | `/api/contacts/:id/favorite`    | Toggle the favorite field on a contact           |

### Query Parameters for GET /api/contacts

| Parameter  | Example                   | Description                        |
|------------|---------------------------|------------------------------------|
| `search`   | `?search=jane`            | Search by name, email, or phone    |
| `type`     | `?type=Personal`          | Filter by Personal or Professional |
| `favorite` | `?favorite=true`          | Return only favorited contacts     |

---

## Database Schema

### Users Collection

```json
{
  "_id": "ObjectId (auto-generated)",
  "name": "String (required)",
  "email": "String (required, unique, validated format)",
  "password": "String (required, bcrypt hashed)",
  "createdAt": "Date (auto-generated)",
  "updatedAt": "Date (auto-generated)"
}
```

### Contacts Collection

```json
{
  "_id": "ObjectId (auto-generated)",
  "user": "ObjectId (reference to User — required)",
  "name": "String (required)",
  "email": "String (required, validated format)",
  "phone": "String (required)",
  "type": "String (enum: Personal | Professional, default: Personal)",
  "notes": "String (optional)",
  "favorite": "Boolean (default: false)",
  "createdAt": "Date (auto-generated)",
  "updatedAt": "Date (auto-generated)"
}
```

---

## Local Development

### Prerequisites

- Node.js v18 or later
- A MongoDB Atlas account or a local MongoDB installation

### Setup

```bash
# Clone the repository
git clone https://github.com/SamFredrick/Project_WebAPI_Fredrick.git
cd Project_WebAPI_Fredrick/backend

# Install dependencies
npm install

# Create your environment file
cp .env.example .env
```

Edit the `.env` file and fill in your values:

```
PORT=5000
MONGO_URI=mongodb+srv://<username>:<password>@cluster0.xxxxx.mongodb.net/contactmanager
JWT_SECRET=your_secret_key_here
```

```bash
# Start the server
node server.js
```

The API will be available at `http://localhost:5000`. Open `frontend/index.html` in your browser to use the application.

---

## Deployment on Render

1. Push your code to GitHub
2. Go to render.com and create a new Web Service
3. Connect your GitHub repository
4. Configure the service:
   - Root Directory: `backend`
   - Build Command: `npm install`
   - Start Command: `node server.js`
5. Add the following environment variables in the Render dashboard:
   - `MONGO_URI` — your MongoDB Atlas connection string
   - `JWT_SECRET` — a secure random string used to sign tokens
6. Click Deploy

Render will automatically redeploy the service on every push to the main branch.

---

## Postman Examples

### Register a new user

```
POST /api/auth/register
Content-Type: application/json

{
  "name": "Jane Smith",
  "email": "jane@example.com",
  "password": "mypassword123"
}
```

### Log in

```
POST /api/auth/login
Content-Type: application/json

{
  "email": "jane@example.com",
  "password": "mypassword123"
}
```

### Create a contact (authenticated)

```
POST /api/contacts
Authorization: Bearer <your_jwt_token>
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "phone": "303-555-0123",
  "type": "Professional",
  "notes": "Met at the Denver tech conference",
  "favorite": false
}
```

### Search contacts

```
GET /api/contacts?search=john&type=Professional
Authorization: Bearer <your_jwt_token>
```

---

## Project Structure

```
Project_WebAPI_Fredrick/
├── backend/
│   ├── middleware/
│   │   └── auth.js          # JWT verification middleware
│   ├── models/
│   │   ├── User.js          # User schema with bcrypt hashing
│   │   └── Contact.js       # Contact schema with user reference
│   ├── routes/
│   │   ├── auth.js          # Register and login routes
│   │   └── contacts.js      # CRUD and favorite routes
│   ├── .env.example         # Environment variable template
│   ├── package.json
│   └── server.js            # Express entry point
└── frontend/
    └── index.html           # Single-page application
```

---

## Links

- Live Application: https://contact-manager-api-5hvl.onrender.com
- GitHub Repository: https://github.com/SamFredrick/Project_WebAPI_Fredrick
