# Student Management System

A comprehensive Spring Boot application for managing student information, grades, and related operations with JWT authentication, AWS S3 integration, and SMS capabilities.

## Features

### Core Functionality
- **Student Management**: CRUD operations for student records
- **Grade Management**: Track and manage student grades across different courses
- **User Authentication**: JWT-based authentication system
- **File Upload**: Profile picture upload to AWS S3 with presigned URLs
- **SMS Integration**: Bulk SMS notifications to students
- **Advanced Search**: Flexible search with pagination and sorting
- **REST API**: Complete RESTful API with Swagger documentation

### Technical Features
- Spring Boot 2.5.2 with Java 11
- PostgreSQL database with JPA/Hibernate
- JWT token-based authentication
- AWS S3 integration for file storage
- SMS service integration (SMS4Free)
- Comprehensive testing with JUnit
- Docker containerization
- Swagger API documentation

## Technology Stack

- **Backend**: Spring Boot, Spring Security, Spring Data JPA
- **Database**: PostgreSQL (production), H2 (testing)
- **Authentication**: JWT (JSON Web Tokens)
- **Cloud Storage**: AWS S3
- **SMS Service**: SMS4Free API
- **Documentation**: Swagger/OpenAPI
- **Testing**: JUnit, Mockito
- **Containerization**: Docker, Docker Compose
- **Build Tool**: Maven

## Project Structure

```
src/
├── main/
│   ├── java/com/handson/basic/
│   │   ├── controller/          # REST controllers
│   │   ├── model/              # Entity and DTO classes
│   │   ├── repo/               # Repository interfaces and services
│   │   ├── jwt/                # JWT authentication components
│   │   ├── util/               # Utility classes
│   │   └── config/             # Configuration classes
│   └── resources/
│       └── application.properties
└── test/
    ├── java/                   # Test classes
    └── resources/              # Test resources
```

## Getting Started

### Prerequisites

- Java 11 or higher
- Maven 3.6+
- PostgreSQL 12+
- Docker (optional)
- AWS Account (for S3 integration)
- SMS4Free account (for SMS functionality)

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd student-management-system
   ```

2. **Configure the database**
   
   Update `src/main/resources/application.properties`:
   ```properties
   spring.datasource.url=jdbc:postgresql://localhost:5432/your_database
   spring.datasource.username=your_username
   spring.datasource.password=your_password
   ```

3. **Configure AWS S3**
   ```properties
   amazon.aws.accesskey=your_access_key
   amazon.aws.secretkey=your_secret_key
   bucket.url=your_bucket_name
   ```

4. **Configure SMS Service**
   ```properties
   sms4free.key=your_sms_key
   sms4free.user=your_sms_user
   sms4free.password=your_sms_password
   ```

5. **Build and run**
   ```bash
   mvn clean install
   mvn spring-boot:run
   ```

### Using Docker

1. **Start with Docker Compose**
   ```bash
   docker-compose up -d
   ```

   This will start:
   - PostgreSQL database on port 5432
   - Application server on port 8080

2. **For CI/CD environment**
   ```bash
   docker-compose -f docker-compose-ci.yml up
   ```

## API Documentation

Once the application is running, access the Swagger UI at:
```
http://localhost:8080/swagger-ui.html
```

### Authentication

1. **Create a user**
   ```bash
   POST /user
   {
     "username": "testuser",
     "password": "password123"
   }
   ```

2. **Authenticate**
   ```bash
   POST /authenticate
   {
     "username": "testuser",
     "password": "password123"
   }
   ```

3. **Use the returned JWT token**
   Add to request headers:
   ```
   Authorization: Bearer <your-jwt-token>
   ```

### Key Endpoints

#### Student Management
- `GET /api/students` - Search students with filters
- `POST /api/students` - Create new student
- `GET /api/students/{id}` - Get student by ID
- `PUT /api/students/{id}` - Update student
- `DELETE /api/students/{id}` - Delete student
- `PUT /api/students/{id}/image` - Upload profile picture

#### Grade Management
- `POST /api/students/{studentId}/grades` - Add grade
- `PUT /api/students/{studentId}/grades/{id}` - Update grade
- `DELETE /api/students/{studentId}/grades/{id}` - Delete grade

#### Other Features
- `GET /api/students/highSat?sat=600` - Get students with high SAT scores
- `POST /api/students/sms/all?text=message` - Send SMS to all students

## Data Models

### Student
```json
{
  "fullname": "John Doe",
  "birthDate": "1995-05-15",
  "satScore": 750,
  "graduationScore": 85.5,
  "phone": "052-123-4567"
}
```

### Grade
```json
{
  "courseName": "Mathematics",
  "courseScore": 95
}
```

## Search and Filtering

The student search endpoint supports various filters:
- `fullName` - Filter by student name
- `fromBirthDate` / `toBirthDate` - Filter by birth date range
- `fromSatScore` / `toSatScore` - Filter by SAT score range
- `fromAvgScore` - Filter by average grade
- `page` / `count` - Pagination
- `sort` / `sortDirection` - Sorting options

Example:
```
GET /api/students?fullName=John&fromSatScore=600&page=1&count=10&sort=fullName&sortDirection=asc
```

## Testing

Run the test suite:
```bash
mvn test
```

The project includes:
- Unit tests for controllers and services
- Integration tests with H2 database
- Mock objects for external services (AWS S3, SMS)

## Configuration

### Environment Variables

For production deployment, use environment variables:
- `SPRING_DATASOURCE_URL`
- `SPRING_DATASOURCE_USERNAME`
- `SPRING_DATASOURCE_PASSWORD`
- `AMAZON_AWS_ACCESSKEY`
- `AMAZON_AWS_SECRETKEY`
- `BUCKET_URL`
- `SMS4FREE_KEY`
- `SMS4FREE_USER`
- `SMS4FREE_PASSWORD`

### Security

- JWT tokens expire after 5 hours
- Passwords are encrypted using BCrypt
- CORS is configured for cross-origin requests
- All endpoints (except authentication) require valid JWT token

## Deployment

### Production Deployment

1. **Build the JAR file**
   ```bash
   mvn clean package
   ```

2. **Run with production profile**
   ```bash
   java -jar target/basic-*.jar --spring.profiles.active=production
   ```

### Docker Deployment

Build and deploy using Docker:
```bash
docker build -t student-management-system .
docker run -p 8080:8080 student-management-system
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Ensure all tests pass
6. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For support and questions:
- Email: admin@handson-academy.com
- Website: https://handson-academy.com

## Changelog

### Version 0.0.1-SNAPSHOT
- Initial release
- Student and grade management
- JWT authentication
- AWS S3 integration
- SMS functionality
- Swagger documentation
