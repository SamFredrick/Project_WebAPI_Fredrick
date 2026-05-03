# 📇 Personal Contact Manager

A full-stack web application for managing personal and professional contacts. Built with **Node.js/Express**, **MongoDB (Mongoose)**, and vanilla **HTML/CSS/JavaScript**.

## Tech Stack

| Layer      | Technology              |
|------------|-------------------------|
| Backend    | Node.js + Express       |
| Database   | MongoDB + Mongoose      |
| Frontend   | HTML, CSS, JavaScript   |
| Hosting    | Render.com              |
| API Client | Postman                 |

---

## API Endpoints

| Method | Endpoint               | Description                    |
|--------|------------------------|--------------------------------|
| GET    | `/api/contacts`        | Get all contacts (+ search/filter) |
| GET    | `/api/contacts/:id`    | Get single contact by ID       |
| POST   | `/api/contacts`        | Create a new contact           |
| PUT    | `/api/contacts/:id`    | Update an existing contact     |
| DELETE | `/api/contacts/:id`    | Delete a contact               |

### Query Parameters for GET /api/contacts
- `?search=john` — search by name, email, or phone
- `?type=Personal` or `?type=Professional` — filter by type
- Combined: `?search=john&type=Personal`

---

## Setup Instructions

### Prerequisites
- Node.js (v18+)
- MongoDB Atlas account (or local MongoDB)

### Local Development

```bash
# 1. Clone the repo
git clone https://github.com/YOUR_USERNAME/contact-manager.git
cd contact-manager/backend

# 2. Install dependencies
npm install

# 3. Configure environment
cp .env.example .env
# Edit .env with your MongoDB URI

# 4. Start the server
node server.js

# 5. Open frontend
# Open frontend/index.html in your browser
# Or serve with: npx serve frontend/
```

### Deploy to Render.com

1. Push your code to GitHub
2. Go to [render.com](https://render.com) and click **New Web Service**
3. Connect your GitHub repo
4. Set:
   - **Root Directory**: `backend`
   - **Build Command**: `npm install`
   - **Start Command**: `node server.js`
5. Add Environment Variables:
   - `MONGO_URI` = your MongoDB Atlas connection string
   - `PORT` = 5000
6. Click **Deploy**

---

## Database Schema

### Contacts Collection

```json
{
  "_id": "ObjectId (auto-generated)",
  "name": "String (required)",
  "email": "String (required, validated format)",
  "phone": "String (required)",
  "type": "String (enum: Personal | Professional)",
  "createdAt": "Date (auto)",
  "updatedAt": "Date (auto)"
}
```

---

## Postman Collection

Test the API with these sample requests:

### Create Contact
```
POST /api/contacts
Body: {
  "name": "Jane Smith",
  "email": "jane@example.com",
  "phone": "303-555-0123",
  "type": "Professional"
}
```

### Search Contacts
```
GET /api/contacts?search=jane&type=Professional
```

---

## Project Structure

```
contact-manager/
├── backend/
│   ├── models/
│   │   └── Contact.js       # Mongoose schema
│   ├── routes/
│   │   └── contacts.js      # CRUD route handlers
│   ├── .env.example         # Environment template
│   ├── package.json
│   └── server.js            # Express entry point
└── frontend/
    └── index.html           # Single-page UI
```
