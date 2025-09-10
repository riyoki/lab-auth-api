### Lab Auth API

### Project Overview
An authentication API built with Node.js, Express, MySQL, and JWT. 
This project demonstrates signup, login, logout, and profile retrieval using a MySQL database.

---

### Setup Steps

1.  Clone & Install
```bash
git clone https://github.com/riyoki/lab-auth-api.git
cd lab-auth-api

2. Install dependencies
```bash
npm install

3. Configure environment variables
   Copy .env.example to .env
   
  Fill in your MySQL details:
    DB_HOST=yourhost
    DB_USER=yourusername
    DB_PASS=yourpassword
    DB_NAME=yourdbname
    DB_PORT=yourport
    SERVER_PORT=3000
  
    JWT_SECRET=replace_with_a_long_random_string
    JWT_EXPIRES=1h

4. Setup Database
   - Open phpMyAdmin
     Usually at http://localhost/phpmyadmin (if you’re using XAMPP).
  - Create a new database
    - On the left sidebar, click New.
    - Enter your database name.
    - Choose utf8mb4_general_ci as collation.
    - Click Create.

    Go to the database you created, open the SQL tab and run:
     ```
    CREATE TABLE IF NOT EXISTS users (
      id INT AUTO_INCREMENT PRIMARY KEY,
      email VARCHAR(100) NOT NULL UNIQUE,
      password_hash VARCHAR(255) NOT NULL,
      full_name VARCHAR(120),
      role VARCHAR(30) DEFAULT 'student',
      created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

    CREATE TABLE IF NOT EXISTS revoked_tokens (
      id INT AUTO_INCREMENT PRIMARY KEY,
      jti VARCHAR(64) NOT NULL UNIQUE,
      expires_at DATETIME NOT NULL,
      revoked_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;



### How to Run

 1. Run the server  
 ```bash
 npm run dev

 2. Check if it’s working:
     - GET http://localhost:3000/api/health (Run through postman/browser)
     - You should get a JSON response similar to:
       {
         "status": "ok",
         "db": "connected",
         "time": "2025-09-04T07:59:08.035Z"
       }

---

### List of Endpoints

Base URL: http://localhost:3000/api

Auth
- POST /auth/signup -> Create new user
- POST /auth/login -> Login & get token
- POST /auth/logout -> Revoke token (requires Bearer token)

User
- GET /profile -> Get logged-in user profile (requires Bearer token)

Health
- GET /health -> Check API & DB status


