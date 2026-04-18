# 📋 Task Manager API

A production-ready RESTful API built with **Spring Boot**, secured with **JWT Authentication**, documented with **Swagger/OpenAPI**, containerized with **Docker**, and deployed on **AWS Elastic Beanstalk**.

---

## 🚀 Tech Stack

| Technology | Purpose |
|------------|---------|
| Java 21 | Core language |
| Spring Boot 3.x | Application framework |
| Spring Security | Authentication & Authorization |
| JWT (jjwt) | Token-based auth |
| Spring Data JPA | Database ORM |
| H2 Database | In-memory database |
| Swagger/OpenAPI 3 | API documentation |
| Docker | Containerization |
| Maven | Build tool |
| AWS Elastic Beanstalk | Cloud deployment |

---

## 📁 Project Structure

```
src/main/java/com/kaushik/taskmanager/
├── config/          # Swagger configuration
│   └── SwaggerConfig.java
├── controller/      # REST controllers
│   ├── AuthController.java
│   └── TaskController.java
├── model/           # JPA entities
│   ├── Task.java
│   └── User.java
├── repository/      # Spring Data repositories
│   ├── TaskRepository.java
│   └── UserRepository.java
├── security/        # JWT & Spring Security
│   ├── JwtUtil.java
│   ├── JwtFilter.java
│   └── SecurityConfig.java
└── service/         # Business logic
    ├── TaskService.java
    └── UserDetailsServiceImpl.java
```

---

## 🔐 Authentication

This API uses **JWT (JSON Web Token)** authentication.

### Register
```http
POST /api/auth/register
Content-Type: application/json

{
  "username": "kaushik",
  "password": "secret123"
}
```

### Login
```http
POST /api/auth/login
Content-Type: application/json

{
  "username": "kaushik",
  "password": "secret123"
}
```

Returns a JWT token. Use it in all subsequent requests:
```
Authorization: Bearer <your-token>
```

---

## 📌 API Endpoints

### Tasks
| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| GET | `/api/tasks` | Get all tasks | ✅ |
| GET | `/api/tasks/{id}` | Get task by ID | ✅ |
| POST | `/api/tasks` | Create new task | ✅ |
| PUT | `/api/tasks/{id}` | Update task | ✅ |
| DELETE | `/api/tasks/{id}` | Delete task | ✅ |

### Auth
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | Register user |
| POST | `/api/auth/login` | Login & get token |

---

## 🛠️ Running Locally

### Prerequisites
- Java 21+
- Maven 3.9+
- Docker (optional)

### Without Docker
```bash
./mvnw spring-boot:run
```

### With Docker
```bash
# Build image
docker build -t taskmanager .

# Run container
docker run -p 8080:8080 taskmanager
```

### With Docker Compose
```bash
docker-compose up --build
```

App runs at: `http://localhost:8080`

---

## 📖 API Documentation

Swagger UI available at:
```
http://localhost:8080/swagger-ui/index.html
```

---

## 🧪 Testing the API

### PowerShell
```powershell
# Register
Invoke-RestMethod -Uri "http://localhost:8080/api/auth/register" `
  -Method POST -ContentType "application/json" `
  -Body '{"username":"kaushik","password":"secret123"}'

# Login
Invoke-RestMethod -Uri "http://localhost:8080/api/auth/login" `
  -Method POST -ContentType "application/json" `
  -Body '{"username":"kaushik","password":"secret123"}'

# Get all tasks (use token from login)
Invoke-RestMethod -Uri "http://localhost:8080/api/tasks" `
  -Headers @{Authorization="Bearer <TOKEN>"}

# Create a task
Invoke-RestMethod -Uri "http://localhost:8080/api/tasks" `
  -Method POST -ContentType "application/json" `
  -Headers @{Authorization="Bearer <TOKEN>"} `
  -Body '{"title":"Buy groceries","description":"Milk, eggs, bread","priority":"HIGH","completed":false}'

# Update a task
Invoke-RestMethod -Uri "http://localhost:8080/api/tasks/1" `
  -Method PUT -ContentType "application/json" `
  -Headers @{Authorization="Bearer <TOKEN>"} `
  -Body '{"title":"Buy groceries","description":"Milk, eggs, bread","priority":"HIGH","completed":true}'

# Delete a task
Invoke-RestMethod -Uri "http://localhost:8080/api/tasks/1" `
  -Method DELETE `
  -Headers @{Authorization="Bearer <TOKEN>"}
```

### Using Swagger UI
1. Open `http://localhost:8080/swagger-ui/index.html`
2. Use `POST /api/auth/register` to create a user
3. Use `POST /api/auth/login` to get your JWT token
4. Click **Authorize 🔒** and paste your token
5. Test any endpoint directly from the browser

---

## ☁️ AWS Deployment

This app is deployed on **AWS Elastic Beanstalk** (Free Tier).

### Live URL
```
http://<your-eb-url>/swagger-ui/index.html
```

### Deploy Steps
1. Build the JAR:
```bash
./mvnw clean package -DskipTests
```
2. Go to [AWS Elastic Beanstalk Console](https://console.aws.amazon.com/elasticbeanstalk)
3. Create application → Platform: **Java / Corretto 21**
4. Upload `target/taskmanager-0.0.1-SNAPSHOT.jar`
5. Set environment variables:
    - `SERVER_PORT` = `5000`
    - `JWT_SECRET` = your secret key
    - `JWT_EXPIRATION` = `86400000`

---

## 👨‍💻 Author

**Kaushik** — [GitHub](https://github.com/kaushikuk10-cpu)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
