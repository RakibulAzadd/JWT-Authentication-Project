JWT Authentication Project with Golang

This is a secure JWT-based authentication backend built with Golang, providing RESTful APIs for user signup and login. It features password hashing, token management, and modular design for easy integration. This README includes setup instructions, API endpoints, and Swagger documentation.

## Features

- **User Authentication**:
  - User signup and login.
  - JWT-based authentication.
  - Password hashing with bcrypt.
  - Token-based session management.
- **Error Handling**:
  - Structured JSON error responses.
  - Input validation using validator.
- **Database**:
  - PostgreSQL for user data storage.
  - Database migrations with Golang-migrate.

## Tech Stack

- **Language**: Golang
- **Database**: PostgreSQL
- **Authentication**: JWT (JSON Web Token)
- **API Testing**: Postman
- **Environment Variables**: Managed via `.env` with godotenv
- **API Documentation**: Swagger (OpenAPI 3.0)
- **Database Migration**: Golang-migrate
- **Logging**: Zerolog

## Folder Structure

```
jwt-auth-golang/
│
├── main.go                # Entry point of the application
├── go.mod                 # Go module file
├── go.sum                 # Go dependencies checksum
├── config/                # Configuration files
│   └── config.go          # Database and environment setup
├── controllers/           # HTTP request handlers
│   └── auth.go
├── models/                # Database models
│   └── user.go
├── routes/                # API routes
│   └── routes.go
├── middleware/            # Authentication & error handling
│   ├── auth.go
│   └── error.go
├── utils/                 # Helper functions
│   ├── jwt.go
│   └── validator.go
```

## Entity-Relationship (ER) Diagram

```
[Users]
+----+
| id | <--- PK
+----+
| username |
| email    |
| password |
| created_at |
| updated_at |
+----+
```

- **Users**: Stores user information (id, username, email, password).

## Installation & Setup

1. **Clone the Repository**:

   ```bash
   git clone https://github.com/RakibulAzadd/jwt-auth-golang.git
   cd jwt-auth-golang
   ```

2. **Set Up PostgreSQL**: Run the following SQL commands:

   ```sql
   CREATE DATABASE jwt_auth_db;
   CREATE USER jwt_auth_user WITH PASSWORD 'yourpassword';
   GRANT ALL PRIVILEGES ON DATABASE jwt_auth_db TO jwt_auth_user;
   ```

3. **Configure Environment Variables**: Create a `.env` file in the project root:

   ```
   VERSION=1.0.0
   SERVICE_NAME=JWT_AUTH
   HTTP_PORT=4000
   DB_HOST=127.0.0.1
   DB_PORT=5432
   DB_USER=postgres
   DB_PASSWORD=12345
   DB_NAME=jwt_auth_db
   JWT_SECRET=your_jwt_secret_key
   ```

4. **Install Dependencies**:

   ```bash
   go mod tidy
   ```

5. **Run Database Migrations**:

   ```bash
   migrate -path migrations -database "postgres://jwt_auth_user:yourpassword@localhost:5432/jwt_auth_db?sslmode=disable" up
   ```

6. **Run the Server**:

   ```bash
   go run main.go
   ```

   The server will run at `http://localhost:4000`.

## API Endpoints

### Authentication

| Method | Endpoint | Description |
| --- | --- | --- |
| POST | `/api/v1/signup` | Register a new user |
| POST | `/api/v1/login` | Login user and get JWT token |

## Swagger Documentation

Access Swagger UI at:

```
http://localhost:4000/docs
```

Swagger YAML file: `docs/swagger.yaml`.

## Postman Instructions

1. Import `postman_collection.json` (in project root) into Postman.
2. Set up Postman environment variables:
   - `BASE_URL`: `http://localhost:4000`
   - `JWT_TOKEN`: (Set after `/api/v1/login`)
3. Test endpoints:
   - **Signup**:

     ```json
     POST http://localhost:4000/api/v1/signup
     Content-Type: application/json
     {
       "username": "testuser",
       "email": "test@example.com",
       "password": "12345678"
     }
     ```
   - **Login**:

     ```json
     POST http://localhost:4000/api/v1/login
     Content-Type: application/json
     {
       "email": "test@example.com",
       "password": "12345678"
     }
     ```

## Contributing

1. Fork the repository.
2. Create a branch (`git checkout -b feature/feature-name`).
3. Commit changes (`git commit -m 'Add feature'`).
4. Push to branch (`git push origin feature/feature-name`).
5. Open a Pull Request.

## License

MIT License

## Contact

Rakibul Azad\
Email: rakibulazad4049@example.com\
Phone: +8801611580264

## Future Improvements

- Add refresh token support.
- Implement role-based access control.
- Add unit tests with Go’s testing package.
- Integrate Redis for token blacklisting.
- Add rate limiting for APIs.
