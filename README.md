# User Authentication API

A RESTful API for user authentication with JWT-based token authentication.

## Features

- User registration with password hashing
- JWT-based authentication
- Protected routes
- CORS enabled
- JSON-based communication

## Getting Started

### Prerequisites

- Node.js
- npm (Node Package Manager)

### Installation

1. Clone the repository
2. Install dependencies:
   ```bash
   npm install
   ```

### Environment Variables

Create a `.env` file with the following variables:

```
cp .env.example .env

PORT=your_port_number_here
JWT_SECRET=your_jwt_secret_key_here
```

## API Endpoints

### Register

- **Endpoint**: POST `/register`
- **Description**: Register a new user
- **Request Body**:
  ```json
  {
    "username": "string",
    "password": "string"
  }
  ```
- **Response**:
  ```json
  {
    "message": "User registered successfully"
  }
  ```

### Login

- **Endpoint**: POST `/login`
- **Description**: Authenticate user and get JWT token
- **Request Body**:
  ```json
  {
    "username": "string",
    "password": "string"
  }
  ```
- **Response**:
  ```json
  {
    "token": "jwt_token"
  }
  ```

### Profile

- **Endpoint**: GET `/profile`
- **Description**: Get user profile information
- **Authentication**: Requires JWT token in Authorization header
- **Response**:
  ```json
  {
    "id": "string",
    "username": "string"
  }
  ```

## Error Responses

The API returns appropriate HTTP status codes and error messages:

- 400: Bad Request (e.g., missing fields, invalid data)
- 401: Unauthorized (e.g., invalid credentials, missing token)
- 403: Forbidden (e.g., invalid token)
- 404: Not Found (e.g., user not found)
- 500: Internal Server Error

## Security

- Passwords are hashed using bcrypt
- JWT tokens have a 15-minute expiration
- CORS is enabled for cross-origin requests
- Input validation is implemented

## Running Tests

The API can be tested using tools like curl or Postman. Example curl commands:

```bash
# Register a new user
curl -X POST http://localhost:3000/register \
  -H "Content-Type: application/json" \
  -d '{"username":"testuser","password":"testpassword123"}'

# Login and get token
curl -X POST http://localhost:3000/login \
  -H "Content-Type: application/json" \
  -d '{"username":"testuser","password":"testpassword123"}'

# Access protected endpoint
curl -X GET http://localhost:3000/profile \
  -H "Authorization: Bearer your_jwt_token"
```
