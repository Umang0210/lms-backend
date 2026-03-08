# LMS Backend

A simple Node.js + Express backend for user authentication and user management.

## Tech Stack

- Node.js
- Express
- MongoDB + Mongoose
- bcrypt (password hashing)
- JSON Web Token (`jsonwebtoken`)
- dotenv
- cors

## Project Structure

```text
lms-backend-main/
  config/
    db.js
  controllers/
    userController.js
  models/
    userModel.js
  routers/
    userRoute.js
  index.js
  package.json
```

## API Base URL

```text
http://localhost:8080/api/users
```

## Prerequisites

- Node.js (v18+ recommended)
- MongoDB connection string

## Environment Variables

Create a `.env` file in the root of the project:

```env
MONGO_URI=your_mongodb_connection_string
```

## Installation and Run

```bash
npm install
node index.js
```

For auto-restart during development:

```bash
npx nodemon index.js
```

The server starts on:

```text
http://localhost:8080
```

## User Schema

`users` collection fields:

- `name` (String, required)
- `email` (String, required, unique)
- `password` (String, required, hashed before save)
- `role` (String, default: `user`)

## API Endpoints

### 1. Signup

- Method: `POST`
- URL: `/signup`

Request body:

```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "123456",
  "role": "user"
}
```

Success response:

```json
{
  "message": "User Created"
}
```

### 2. Login

- Method: `POST`
- URL: `/login`

Request body:

```json
{
  "email": "john@example.com",
  "password": "123456"
}
```

Expected success response:

```json
{
  "message": "Login Success",
  "token": "<jwt_token>"
}
```

### 3. Get All Users

- Method: `GET`
- URL: `/`

Success response:

```json
[
  {
    "_id": "...",
    "name": "John Doe",
    "email": "john@example.com",
    "password": "<hashed_password>",
    "role": "user"
  }
]
```

### 4. Delete User

- Method: `DELETE`
- URL: `/:id`

Example:

```text
DELETE /api/users/65f1a2b3c4d5e6f7a8b9c0d1
```

Success response:

```json
{
  "message": "User Deleted"
}
```

## Notes

- Passwords are hashed using `bcrypt` before storing in MongoDB.
- JWT is generated during login with a 1-hour expiry.
- CORS and JSON body parsing are enabled globally.
