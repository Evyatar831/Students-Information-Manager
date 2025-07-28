# Students Information Manager

A Spring Boot REST API application for managing student information with CRUD operations. The application persists student data to a PostgreSQL database and can be deployed using Docker.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technologies](#technologies)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Configuration](#configuration)
- [API Endpoints](#api-endpoints)
- [Running the Application](#running-the-application)
- [Docker Deployment](#docker-deployment)
- [Testing](#testing)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

The Students Information Manager is a REST API built with Spring Boot that allows CRUD (Create, Read, Update, Delete) operations on student information. The application uses JPA Hibernate for database operations and PostgreSQL for data persistence.

## ✨ Features

- **Complete CRUD Operations**: Create, read, update, and delete student records
- **RESTful API**: Well-structured REST endpoints for student management
- **Database Persistence**: PostgreSQL database integration using JPA Hibernate
- **Data Validation**: Input validation and error handling
- **Docker Support**: Containerized deployment with Docker
- **Exception Handling**: Centralized error handling with custom exceptions
- **Clean Architecture**: Follows Spring Boot best practices and layered architecture

## 🛠️ Technologies

- **Spring Boot** - Application framework and auto-configuration
- **JPA Hibernate** - Object-relational mapping and database operations
- **PostgreSQL** - Relational database for data persistence
- **Docker** - Containerization and deployment
- **REST API** - RESTful web services architecture
- **Maven** - Dependency management and build tool

## 🔧 Prerequisites

Before running this application, make sure you have the following installed:

- **Java 17** or higher
- **Maven 3.6+**
- **PostgreSQL 12+**
- **Docker** (optional, for containerized deployment)
- **Git**
- **IDE** (IntelliJ IDEA, Eclipse, or VS Code recommended)

## 🚀 Getting Started

### Clone the Repository

```bash
git clone https://github.com/Evyatar831/basicspring.git
cd basicspring
```

### Build the Project

#### Using Maven
```bash
mvn clean install
```

## 📁 Project Structure

```
src/
├── main/
│   ├── java/
│   │   └── com/
│   │       └── example/
│   │           └── studentmanager/
│   │               ├── StudentManagerApplication.java   # Main application class
│   │               ├── config/                          # Configuration classes
│   │               │   └── DatabaseConfig.java
│   │               ├── controller/                      # REST controllers
│   │               │   └── StudentController.java
│   │               ├── service/                         # Business logic layer
│   │               │   └── StudentService.java
│   │               ├── repository/                      # Data access layer
│   │               │   └── StudentRepository.java
│   │               ├── model/                          # Entity classes
│   │               │   └── Student.java
│   │               ├── dto/                            # Data Transfer Objects
│   │               │   └── StudentDTO.java
│   │               └── exception/                      # Custom exceptions
│   │                   ├── StudentNotFoundException.java
│   │                   └── GlobalExceptionHandler.java
│   └── resources/
│       ├── application.properties                      # Application configuration
│       ├── application-docker.properties               # Docker configuration
│       └── docker/
│           └── docker-compose.yml                      # Docker compose file
└── test/
    └── java/
        └── com/
            └── example/
                └── studentmanager/                     # Test classes
                    ├── controller/
                    │   └── StudentControllerTest.java
                    ├── service/
                    │   └── StudentServiceTest.java
                    └── repository/
                        └── StudentRepositoryTest.java
```

### Key Components

- **Controllers**: Handle HTTP requests and responses
- **Services**: Contain business logic and processing
- **Repositories**: Manage data persistence and retrieval
- **Models/Entities**: Represent data structures
- **DTOs**: Transfer data between layers
- **Configuration**: Application and component configuration

## ⚙️ Configuration

### Application Properties

The application can be configured using `application.properties`:

```properties
# Server configuration
server.port=8080

# PostgreSQL Database configuration
spring.datasource.url=jdbc:postgresql://localhost:5432/studentdb
spring.datasource.username=postgres
spring.datasource.password=yourpassword
spring.datasource.driver-class-name=org.postgresql.Driver

# JPA Hibernate configuration
spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true

# Logging
logging.level.com.example.studentmanager=DEBUG
```

### Docker Configuration (`application-docker.properties`)

```properties
# Server configuration
server.port=8080

# PostgreSQL Database configuration for Docker
spring.datasource.url=jdbc:postgresql://postgres-db:5432/studentdb
spring.datasource.username=postgres
spring.datasource.password=postgres
spring.datasource.driver-class-name=org.postgresql.Driver

# JPA Hibernate configuration
spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.hibernate.ddl-auto=create-drop
spring.jpa.show-sql=true
```

## 🌐 API Endpoints

### Base URL
```
http://localhost:8080/api
```

### Student CRUD Operations

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET    | `/students` | Get all students |
| GET    | `/students/{id}` | Get student by ID |
| POST   | `/students` | Create new student |
| PUT    | `/students/{id}` | Update existing student |
| DELETE | `/students/{id}` | Delete student |

### Example Request/Response

**GET** `/api/students/1`

Response:
```json
{
  "id": 1,
  "firstName": "John",
  "lastName": "Doe",
  "email": "john.doe@student.edu",
  "studentId": "STU001",
  "phoneNumber": "+1234567890",
  "address": "123 Main St, City, State",
  "dateOfBirth": "2000-05-15",
  "enrollmentDate": "2024-01-15",
  "major": "Computer Science"
}
```

**POST** `/api/students`

Request:
```json
{
  "firstName": "Jane",
  "lastName": "Smith",
  "email": "jane.smith@student.edu",
  "studentId": "STU002",
  "phoneNumber": "+1234567891",
  "address": "456 Oak Ave, City, State",
  "dateOfBirth": "1999-08-22",
  "major": "Mathematics"
}
```

**PUT** `/api/students/1`

Request:
```json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john.doe.updated@student.edu",
  "phoneNumber": "+1234567892",
  "address": "789 Pine St, City, State",
  "major": "Computer Engineering"
}
```

**DELETE** `/api/students/1`

Response: `204 No Content`

## 🏃‍♂️ Running the Application

### 1. Setup PostgreSQL Database
```sql
-- Create database
CREATE DATABASE studentdb;

-- Create user (optional)
CREATE USER studentuser WITH PASSWORD 'password';
GRANT ALL PRIVILEGES ON DATABASE studentdb TO studentuser;
```

### 2. Run the Application

#### Using Maven
```bash
mvn spring-boot:run
```

#### Using JAR file
```bash
# Build the JAR first
mvn clean package
# Run the JAR
java -jar target/studentmanager-0.0.1-SNAPSHOT.jar
```

#### Using IDE
Run the `StudentManagerApplication.java` class directly from your IDE.

The application will start on `http://localhost:8080`

## 🐳 Docker Deployment

### Using Docker Compose (Recommended)

1. **Create docker-compose.yml**:
```yaml
version: '3.8'
services:
  postgres-db:
    image: postgres:15
    container_name: student-postgres
    environment:
      POSTGRES_DB: studentdb
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

  student-app:
    build: .
    container_name: student-manager-app
    depends_on:
      - postgres-db
    ports:
      - "8080:8080"
    environment:
      SPRING_PROFILES_ACTIVE: docker
    volumes:
      - ./logs:/app/logs

volumes:
  postgres_data:
```

2. **Create Dockerfile**:
```dockerfile
FROM openjdk:17-jdk-slim

WORKDIR /app

COPY target/studentmanager-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
```

3. **Build and Run**:
```bash
# Build the application
mvn clean package

# Run with Docker Compose
docker-compose up --build
```

### Using Docker Only

```bash
# Build the application
mvn clean package

# Build Docker image
docker build -t student-manager .

# Run PostgreSQL container
docker run --name postgres-db -e POSTGRES_DB=studentdb -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres:15

# Run application container
docker run --name student-app --link postgres-db:postgres-db -p 8080:8080 -e SPRING_PROFILES_ACTIVE=docker student-manager
```

## 🧪 Testing

### Run All Tests
```bash
mvn test
```

### Test Categories
- **Unit Tests**: Test individual components in isolation
- **Integration Tests**: Test database operations and component interactions
- **Web Layer Tests**: Test REST controllers using `@WebMvcTest`

### Example Test Structure
```java
@SpringBootTest
class StudentManagerApplicationTests {
    
    @Test
    void contextLoads() {
        // Test application context loads successfully
    }
}

@WebMvcTest(StudentController.class)
class StudentControllerTest {
    
    @Autowired
    private MockMvc mockMvc;
    
    @MockBean
    private StudentService studentService;
    
    @Test
    void shouldReturnAllStudents() throws Exception {
        mockMvc.perform(get("/api/students"))
               .andExpect(status().isOk());
    }
}

@DataJpaTest
class StudentRepositoryTest {
    
    @Autowired
    private TestEntityManager entityManager;
    
    @Autowired
    private StudentRepository studentRepository;
    
    @Test
    void shouldFindStudentById() {
        // Test repository operations
    }
}
```

## 🛠️ Built With

- **[Spring Boot](https://spring.io/projects/spring-boot)** - Application framework and auto-configuration
- **[JPA Hibernate](https://hibernate.org/)** - Object-relational mapping and database operations
- **[PostgreSQL](https://www.postgresql.org/)** - Relational database for data persistence
- **[Docker](https://www.docker.com/)** - Containerization and deployment
- **[Maven](https://maven.apache.org/)** - Dependency management and build tool
- **[JUnit 5](https://junit.org/junit5/)** - Testing framework

## 📈 Development

### Adding New Features

1. **Extend Student Entity**: Add new fields to `Student.java` entity
2. **Update Repository**: Add custom query methods to `StudentRepository.java`
3. **Enhance Service**: Add business logic in `StudentService.java`
4. **Update Controller**: Add new REST endpoints in `StudentController.java`
5. **Create/Update DTO**: Modify `StudentDTO.java` for API communication
6. **Add Tests**: Create corresponding test classes

### Common Development Tasks
- **Add student search**: Implement search by name, email, or student ID
- **Add pagination**: Implement paginated results for large datasets
- **Add validation**: Enhance input validation for student data
- **Export functionality**: Add endpoints to export student data (CSV, PDF)
- **Bulk operations**: Implement bulk insert/update operations

### Database Migration
- Use Flyway or Liquibase for database schema versioning
- Add migration scripts in `src/main/resources/db/migration/`

### Code Style
- Follow Java naming conventions
- Use meaningful variable and method names
- Add appropriate comments and documentation
- Maintain consistent indentation and formatting

## 🤝 Contributing

1. Fork the project
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📞 Contact

**Evyatar** - [@Evyatar831](https://github.com/Evyatar831)

Project Link: [https://github.com/Evyatar831/basicspring](https://github.com/Evyatar831/basicspring)

---

## 🔗 Additional Resources

- [Spring Boot Documentation](https://spring.io/projects/spring-boot)
- [Spring Data JPA Reference](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/)
- [Hibernate ORM Documentation](https://hibernate.org/orm/documentation/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [Docker Documentation](https://docs.docker.com/)
- [Building REST services with Spring](https://spring.io/guides/tutorials/rest/)
- [Spring Boot with PostgreSQL](https://spring.io/guides/gs/accessing-data-postgresql/)

---
*Happy Coding! 🚀*
