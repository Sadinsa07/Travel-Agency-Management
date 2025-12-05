# 🌍 Travel Agency Management System

A comprehensive, enterprise-grade microservices-based Travel Agency Management System built with Spring Boot. This system provides a robust platform for managing travel packages, customer bookings, feedback, and customer information through independent, scalable microservices.

[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4.2-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![Java](https://img.shields.io/badge/Java-17%2B-orange.svg)](https://www.oracle.com/java/)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-blue.svg)](https://www.mysql.com/)
[![Maven](https://img.shields.io/badge/Maven-3.6%2B-red.svg)](https://maven.apache.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 📋 Table of Contents

- [Overview](#-overview)
- [System Architecture](#-system-architecture)
- [Key Features](#-key-features)
- [Microservices](#-microservices)
- [Technology Stack](#-technology-stack)
- [Prerequisites](#-prerequisites)
- [Installation & Setup](#-installation--setup)
- [Database Configuration](#-database-configuration)
- [API Documentation](#-api-documentation)
- [Project Structure](#-project-structure)
- [Usage Examples](#-usage-examples)
- [Testing](#-testing)
- [Contributing](#-contributing)
- [Troubleshooting](#-troubleshooting)
- [Future Enhancements](#-future-enhancements)
- [License](#-license)
- [Contact](#-contact)

---

## 🎯 Overview

The **Travel Agency Management System** is a modern, microservices-based application designed to streamline travel agency operations. Built using Spring Boot and following industry best practices, this system offers independent, scalable services for managing different aspects of a travel business.

### Why This System?

- **Microservices Architecture**: Each service can be developed, deployed, and scaled independently
- **RESTful APIs**: Clean, well-documented API endpoints for all operations
- **Persistent Storage**: MySQL database integration with JPA/Hibernate
- **Production Ready**: Built with Spring Boot best practices and enterprise patterns
- **API Documentation**: Integrated Swagger/OpenAPI for interactive API documentation

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    Travel Agency System                      │
├─────────────────────────────────────────────────────────────┤
│                                                               │
│  ┌─────────────────┐  ┌─────────────────┐                   │
│  │   Booking       │  │   Customer      │                   │
│  │   Service       │  │   Service       │                   │
│  │   Port: 8080    │  │   Port: 8080    │                   │
│  └────────┬────────┘  └────────┬────────┘                   │
│           │                    │                             │
│           └────────┬───────────┘                             │
│                    │                                         │
│  ┌─────────────────┴─────┐  ┌─────────────────┐            │
│  │   Packages Service    │  │   Feedback      │            │
│  │   Port: 8090          │  │   Service       │            │
│  └───────────────────────┘  │   Port: 8080    │            │
│                              └─────────────────┘            │
│                                                               │
├─────────────────────────────────────────────────────────────┤
│                   MySQL Database Layer                       │
│   travel_management_db  │  travel_agency                    │
└─────────────────────────────────────────────────────────────┘
```

---

## ✨ Key Features

### 🎫 Booking Management
- Create, update, and manage travel bookings
- Track booking dates and travel dates
- Calculate and manage pricing
- Customer association with bookings

### 👥 Customer Management
- Complete customer profile management (CRUD operations)
- Store customer details (name, email, phone, address, NIC)
- Role-based customer classification
- Secure password management

### 📦 Package Management
- Create and manage travel packages
- Define destinations, durations, and pricing
- Track available slots for each package
- Detailed package descriptions

### 💬 Feedback System
- Collect customer feedback and ratings
- Link feedback to bookings and customers
- Time-stamped feedback entries
- Rating system (1-5 stars)

### 🔧 Technical Features
- **RESTful APIs** with standard HTTP methods
- **OpenAPI/Swagger Documentation** for interactive API testing
- **JPA/Hibernate** for ORM and database operations
- **Lombok** for reduced boilerplate code
- **MySQL** for reliable data persistence
- **Exception Handling** for robust error management
- **Auto-DDL** database schema generation

---

## 🎛️ Microservices

### 1. 📅 Booking Service
**Port**: Default (8080) | **Package**: `com.travelAgent.booking_service`

Manages all booking-related operations for the travel agency.

**Endpoints**:
- `POST /api/bookings` - Create new booking
- `GET /api/bookings` - Get all bookings
- `GET /api/bookings/{id}` - Get booking by ID
- `PUT /api/bookings/{id}` - Update booking
- `DELETE /api/bookings/{id}` - Delete booking

**Data Model**:
```java
{
  "id": Long,
  "customerName": String,
  "packageId": String,
  "bookingDate": LocalDate,
  "travelDate": LocalDate,
  "totalPrice": BigDecimal
}
```

---

### 2. 👤 Customer Service
**Port**: Default (8080) | **Package**: `com.example.CustomerMicroservice`

Handles customer registration, profile management, and authentication.

**Endpoints**:
- `POST /api/Customer` - Create new customer
- `GET /api/Customer` - Get all customers
- `GET /api/Customer/{id}` - Get customer by ID
- `PUT /api/Customer/{id}` - Update customer
- `DELETE /api/Customer/{id}` - Delete customer

**Data Model**:
```java
{
  "userId": Integer,
  "firstName": String,
  "lastName": String,
  "email": String,
  "password": String,
  "phoneNumber": String,
  "gender": String,
  "address": String,
  "NIC": String,
  "role": String
}
```

---

### 3. 🎁 Packages Service
**Port**: 8090 | **Package**: `com.example.Packages.Microservice`

Manages travel package offerings with detailed information about destinations and pricing.

**Endpoints**:
- `POST /api/packages` - Create new package (201 Created)
- `GET /api/packages` - Get all packages
- `GET /api/packages/{id}` - Get package by ID
- `PUT /api/packages/{id}` - Update package
- `DELETE /api/packages/{id}` - Delete package (204 No Content)

**Data Model**:
```java
{
  "packageId": Long,
  "packageName": String,
  "description": String,
  "destination": String,
  "durationDays": Integer,
  "price": BigDecimal,
  "availableSlots": Integer
}
```

---

### 4. ⭐ Feedback Service
**Port**: Default (8080) | **Package**: `com.travelAgent.feedback`

Collects and manages customer feedback and ratings for completed trips.

**Endpoints**:
- `POST /api/feedbacks` - Create new feedback
- `GET /api/feedbacks` - Get all feedbacks
- `GET /api/feedbacks/{id}` - Get feedback by ID
- `PUT /api/feedbacks/{id}` - Update feedback
- `DELETE /api/feedbacks/{id}` - Delete feedback

**Data Model**:
```java
{
  "id": Long,
  "customerId": String,
  "bookingId": String,
  "rating": Integer (1-5),
  "comment": String,
  "feedbackDate": LocalDate
}
```

---

## 🛠️ Technology Stack

### Backend Framework
- **Spring Boot 3.4.2** - Core framework
- **Spring Web** - RESTful web services
- **Spring Data JPA** - Database abstraction and ORM
- **Hibernate** - ORM implementation

### Database
- **MySQL 8.0+** - Primary relational database
- **MySQL Connector/J 8.0.33** - JDBC driver

### Documentation & Tools
- **SpringFox 3.0.0** - Swagger UI integration (Booking Service)
- **SpringDoc OpenAPI 2.3.0** - OpenAPI 3.0 documentation (Other Services)
- **Lombok** - Reduce boilerplate code

### Build & Development
- **Maven 3.6+** - Dependency management and build tool
- **Java 17+** - Programming language (Java 23 for Packages Service)

### Additional Libraries
- **JWT (JSON Web Tokens) 0.9.1** - Authentication (Customer Service)
- **Spring Boot DevTools** - Development productivity

---

## 📋 Prerequisites

Before running this application, ensure you have the following installed:

1. **Java Development Kit (JDK) 17 or higher**
   ```bash
   java -version
   ```

2. **Apache Maven 3.6+**
   ```bash
   mvn -version
   ```

3. **MySQL 8.0+**
   ```bash
   mysql --version
   ```

4. **Git** (for cloning the repository)
   ```bash
   git --version
   ```

5. **IDE** (Optional but recommended)
   - IntelliJ IDEA
   - Eclipse
   - VS Code with Java extensions

---

## 🚀 Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/travel-agency-management.git
cd travel-agency-management
```

### 2. Database Setup

#### Create Databases

```sql
-- Connect to MySQL
mysql -u root -p

-- Create databases
CREATE DATABASE travel_management_db;
CREATE DATABASE travel_agency;

-- Create user (optional)
CREATE USER 'travelapp'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON travel_management_db.* TO 'travelapp'@'localhost';
GRANT ALL PRIVILEGES ON travel_agency.* TO 'travelapp'@'localhost';
FLUSH PRIVILEGES;
```

### 3. Configure Application Properties

Update the database credentials in each service's `application.properties`:

#### Booking Service
```properties
# Location: booking-service/src/main/resources/application.properties
spring.datasource.url=jdbc:mysql://localhost:3306/travel_management_db
spring.datasource.username=your_username
spring.datasource.password=your_password
```

#### Customer Service
```properties
# Location: CustomerMicroService/CustomerMicroService/src/main/resources/application.properties
spring.datasource.url=jdbc:mysql://localhost:3306/travel_management_db
spring.datasource.username=your_username
spring.datasource.password=your_password
```

#### Feedback Service
```properties
# Location: feedback/src/main/resources/application.properties
spring.datasource.url=jdbc:mysql://localhost:3306/travel_management_db
spring.datasource.username=your_username
spring.datasource.password=your_password
```

#### Packages Service
```properties
# Location: Packages-Microservice/Packages-Microservice/src/main/resources/application.properties
spring.datasource.url=jdbc:mysql://localhost:3306/travel_agency?createDatabaseIfNotExist=true
spring.datasource.username=your_username
spring.datasource.password=your_password
server.port=8090
```

### 4. Build the Services

Navigate to each service directory and build:

```bash
# Booking Service
cd "Travel Agency Management/booking-service"
mvn clean install

# Customer Service
cd "../CustomerMicroService/CustomerMicroService"
mvn clean install

# Feedback Service
cd "../../feedback"
mvn clean install

# Packages Service
cd "../Packages-Microservice/Packages-Microservice"
mvn clean install
```

### 5. Run the Services

Start each service in a separate terminal:

```bash
# Terminal 1: Booking Service
cd "Travel Agency Management/booking-service"
mvn spring-boot:run

# Terminal 2: Customer Service
cd "Travel Agency Management/CustomerMicroService/CustomerMicroService"
mvn spring-boot:run

# Terminal 3: Feedback Service
cd "Travel Agency Management/feedback"
mvn spring-boot:run

# Terminal 4: Packages Service
cd "Travel Agency Management/Packages-Microservice/Packages-Microservice"
mvn spring-boot:run
```

**Note**: Ensure each service runs on a different port. The Packages Service is configured for port 8090, while others use default 8080. You may need to configure different ports for other services.

---

## 🗄️ Database Configuration

### Connection Properties

Each microservice uses the following Hibernate configuration:

```properties
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

### DDL Auto Options

- `update` - Update schema without dropping data
- `create` - Create schema, destroying existing data
- `create-drop` - Create schema, drop on SessionFactory close
- `validate` - Validate schema, no changes
- `none` - Disable DDL handling

**Production Recommendation**: Use `validate` or `none` and manage schema with migration tools like Flyway or Liquibase.

---

## 📚 API Documentation

### Swagger/OpenAPI Access

Once the services are running, access the interactive API documentation:

#### Customer Service
```
http://localhost:8080/swagger-ui/index.html
```

#### Feedback Service
```
http://localhost:8080/swagger-ui/index.html
```

#### Packages Service
```
http://localhost:8090/swagger-ui/index.html
```

#### Booking Service (SpringFox)
```
http://localhost:8080/swagger-ui/
```

### API Testing with cURL

#### Create a Package
```bash
curl -X POST http://localhost:8090/api/packages \
  -H "Content-Type: application/json" \
  -d '{
    "packageName": "Bali Paradise",
    "description": "7-day tropical getaway",
    "destination": "Bali, Indonesia",
    "durationDays": 7,
    "price": 1299.99,
    "availableSlots": 20
  }'
```

#### Get All Packages
```bash
curl http://localhost:8090/api/packages
```

#### Create a Booking
```bash
curl -X POST http://localhost:8080/api/bookings \
  -H "Content-Type: application/json" \
  -d '{
    "customerName": "John Doe",
    "packageId": "1",
    "bookingDate": "2025-01-15",
    "travelDate": "2025-03-20",
    "totalPrice": 1299.99
  }'
```

---

## 📁 Project Structure

```
Travel-Agency-Management-main/
├── README.md
└── Travel Agency Management/
    ├── booking-service/
    │   ├── src/
    │   │   ├── main/
    │   │   │   ├── java/com/travelAgent/booking_service/
    │   │   │   │   ├── controller/
    │   │   │   │   │   └── BookingController.java
    │   │   │   │   ├── model/
    │   │   │   │   │   └── Booking.java
    │   │   │   │   ├── repository/
    │   │   │   │   │   └── BookingRepository.java
    │   │   │   │   ├── service/
    │   │   │   │   │   └── BookingService.java
    │   │   │   │   └── BookingServiceApplication.java
    │   │   │   └── resources/
    │   │   │       └── application.properties
    │   │   └── test/
    │   ├── pom.xml
    │   ├── mvnw
    │   └── mvnw.cmd
    │
    ├── CustomerMicroService/
    │   └── CustomerMicroService/
    │       ├── src/
    │       │   ├── main/
    │       │   │   ├── java/com/example/CustomerMicroservice/
    │       │   │   │   ├── controller/
    │       │   │   │   │   └── CustomerController.java
    │       │   │   │   ├── data/
    │       │   │   │   │   └── Customer.java
    │       │   │   │   ├── dto/
    │       │   │   │   │   └── LoginRequest.java
    │       │   │   │   ├── repository/
    │       │   │   │   │   └── CustomerRepository.java
    │       │   │   │   ├── service/
    │       │   │   │   │   └── CustomerService.java
    │       │   │   │   └── CustomerMicroserviceApplication.java
    │       │   │   └── resources/
    │       │   │       ├── application.properties
    │       │   │       └── application.yml
    │       │   └── test/
    │       └── pom.xml
    │
    ├── feedback/
    │   ├── src/
    │   │   ├── main/
    │   │   │   ├── java/com/travelAgent/feedback/
    │   │   │   │   ├── controller/
    │   │   │   │   │   └── FeedbackController.java
    │   │   │   │   ├── model/
    │   │   │   │   │   └── Feedback.java
    │   │   │   │   ├── repository/
    │   │   │   │   │   └── FeedbackRepository.java
    │   │   │   │   ├── service/
    │   │   │   │   │   └── FeedbackService.java
    │   │   │   │   └── FeedbackApplication.java
    │   │   │   └── resources/
    │   │   │       └── application.properties
    │   │   └── test/
    │   └── pom.xml
    │
    └── Packages-Microservice/
        └── Packages-Microservice/
            ├── src/
            │   ├── main/
            │   │   ├── java/com/example/Packages/Microservice/
            │   │   │   ├── controller/
            │   │   │   │   └── PackageController.java
            │   │   │   ├── model/
            │   │   │   │   └── TravelPackage.java
            │   │   │   ├── repository/
            │   │   │   │   └── PackageRepository.java
            │   │   │   ├── service/
            │   │   │   │   ├── PackageService.java
            │   │   │   │   └── PackageServiceImpl.java
            │   │   │   └── PackagesMicroserviceApplication.java
            │   │   └── resources/
            │   │       └── application.properties
            │   └── test/
            └── pom.xml
```

---

## 💡 Usage Examples

### Complete Booking Workflow

#### Step 1: Create a Customer
```bash
curl -X POST http://localhost:8080/api/Customer \
  -H "Content-Type: application/json" \
  -d '{
    "firstName": "Jane",
    "lastName": "Smith",
    "email": "jane.smith@example.com",
    "password": "SecurePass123",
    "phoneNumber": "+1234567890",
    "gender": "Female",
    "address": "123 Main St, City",
    "NIC": "123456789V",
    "role": "customer"
  }'
```

#### Step 2: Browse Available Packages
```bash
curl http://localhost:8090/api/packages
```

#### Step 3: Create a Booking
```bash
curl -X POST http://localhost:8080/api/bookings \
  -H "Content-Type: application/json" \
  -d '{
    "customerName": "Jane Smith",
    "packageId": "1",
    "bookingDate": "2025-01-20",
    "travelDate": "2025-04-15",
    "totalPrice": 1299.99
  }'
```

#### Step 4: Submit Feedback (After Travel)
```bash
curl -X POST http://localhost:8080/api/feedbacks \
  -H "Content-Type: application/json" \
  -d '{
    "customerId": "1",
    "bookingId": "1",
    "rating": 5,
    "comment": "Excellent service and amazing destination!",
    "feedbackDate": "2025-04-25"
  }'
```

---

## 🧪 Testing

### Run Unit Tests

```bash
# Test Booking Service
cd "Travel Agency Management/booking-service"
mvn test

# Test Customer Service
cd "../CustomerMicroService/CustomerMicroService"
mvn test

# Test Feedback Service
cd "../../feedback"
mvn test

# Test Packages Service
cd "../Packages-Microservice/Packages-Microservice"
mvn test
```

### Integration Testing

Use Postman or Thunder Client to test API endpoints:

1. Import the Swagger/OpenAPI specification
2. Test each CRUD operation
3. Verify database persistence
4. Check error handling

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. **Fork the Repository**
   ```bash
   git fork https://github.com/yourusername/travel-agency-management.git
   ```

2. **Create a Feature Branch**
   ```bash
   git checkout -b feature/AmazingFeature
   ```

3. **Commit Your Changes**
   ```bash
   git commit -m 'Add some AmazingFeature'
   ```

4. **Push to the Branch**
   ```bash
   git push origin feature/AmazingFeature
   ```

5. **Open a Pull Request**

### Coding Standards

- Follow Java naming conventions
- Write meaningful commit messages
- Add unit tests for new features
- Update documentation as needed
- Use Lombok annotations consistently

---

## 🔧 Troubleshooting

### Common Issues

#### Port Already in Use
```bash
# Find process using port 8080
netstat -ano | findstr :8080

# Kill the process
taskkill /PID <process_id> /F
```

#### Database Connection Refused
- Verify MySQL is running
- Check database credentials in `application.properties`
- Ensure databases exist

#### Maven Build Failures
```bash
# Clear Maven cache
mvn dependency:purge-local-repository

# Rebuild
mvn clean install -U
```

#### Swagger UI Not Loading
- Verify service is running
- Check console for errors
- Access the correct port for each service

---

## 🚀 Future Enhancements

### Planned Features

- [ ] **Authentication & Authorization**
  - JWT token-based authentication
  - Role-based access control (RBAC)
  - OAuth2 integration

- [ ] **Service Discovery**
  - Spring Cloud Eureka integration
  - API Gateway with Spring Cloud Gateway
  - Load balancing

- [ ] **Payment Integration**
  - Stripe/PayPal integration
  - Payment processing service
  - Invoice generation

- [ ] **Notification Service**
  - Email notifications (booking confirmation, reminders)
  - SMS integration
  - Push notifications

- [ ] **Advanced Features**
  - Real-time availability checking
  - Dynamic pricing engine
  - Analytics dashboard
  - Multi-language support
  - Mobile app integration

- [ ] **DevOps & Deployment**
  - Docker containerization
  - Kubernetes orchestration
  - CI/CD pipelines
  - Monitoring with Prometheus/Grafana

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2025 Travel Agency Management System

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.
```

---

## 📞 Contact

**Project Maintainer**: Your Name

- 📧 Email: your.email@example.com
- 💼 LinkedIn: (https://linkedin.com/in/sadinsa07)
- 🐙 GitHub: (https://github.com/sadinsa07)

---

## 🙏 Acknowledgments

- Spring Boot Team for the excellent framework
- MySQL for the reliable database system
- OpenAPI/Swagger for API documentation tools
- The open-source community for continuous support

---

<div align="center">


[Report Bug](https://github.com/yourusername/travel-agency-management/issues) · 
[Request Feature](https://github.com/yourusername/travel-agency-management/issues) · 
[Documentation](https://github.com/yourusername/travel-agency-management/wiki)

</div>
