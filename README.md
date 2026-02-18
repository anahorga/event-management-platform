# 🎟️ EventHub — Spring Boot Event Management Platform

A full-stack web application built with **Spring Boot**, featuring secure user authentication, role-based access control, and a complete event management system.

---

## 🚀 Features

- **User Authentication & Authorization** — Custom Spring Security implementation with BCrypt password hashing
- **Role-Based Access Control** — Granular permissions for `ADMIN`, `DEVELOPER`, and `USER` roles
- **Event Management** — Create, view, and delete events with categories and tags
- **User Registration** — Self-service account creation with persistent storage
- **Thymeleaf Templates** — Server-side rendered UI with Bootstrap 5 styling
- **Audit Events** — Login success/failure event listeners for security monitoring

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Backend | Java 17+, Spring Boot 3 |
| Security | Spring Security 6, BCrypt |
| Persistence | Spring Data JPA, Hibernate |
| Database | MySQL 8 |
| Frontend | Thymeleaf, Bootstrap 5 |
| Build Tool | Maven |
| Utilities | Lombok |

---

## 📁 Project Structure

```
src/
├── main/
│   ├── java/com/example/demo/
│   │   ├── config/          # Security config, custom UserDetails
│   │   ├── controller/      # MVC controllers (Events, Users, Roles, Tags)
│   │   ├── dto/             # Data Transfer Objects
│   │   ├── mapper/          # Entity ↔ DTO mappers
│   │   ├── model/           # JPA entities (User, Event, Role, Tag...)
│   │   ├── repository/      # Spring Data JPA repositories
│   │   └── service/         # Business logic layer
│   └── resources/
│       ├── templates/       # Thymeleaf HTML templates
│       └── static/          # CSS stylesheets
```

---

## ⚙️ Getting Started

### Prerequisites

- Java 17+
- Maven 3.8+
- MySQL 8+

### 1. Clone the repository

```bash
git clone https://github.com/your-username/eventhub.git
cd eventhub
```

### 2. Configure the database

Edit `src/main/resources/application.properties`:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/eventhub
spring.datasource.username=your_username
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update
```

### 3. Run the application

```bash
mvn spring-boot:run
```

The app will start at `http://localhost:8080`

---

## 🔐 Security Overview

The application uses a fully custom Spring Security configuration:

- **`MyUserDetailsService`** — Loads users from the database with their roles
- **`MySecurityUser`** — Extends Spring's `User` class with extra profile fields
- **`MySecurityAuthentication`** — Custom `Authentication` implementation with factory methods for authenticated/unauthenticated states
- **`SecurityFilterChain`** — Endpoint-level authorization rules

| Endpoint | Access |
|---|---|
| `/`, `/login`, `/register` | Public |
| `/admin`, `/user` | `ADMIN` only |
| `/developer` | `DEVELOPER` only |
| `/users`, `/authorities` | `ADMIN` or `DEVELOPER` |
| All others | Authenticated |

---

## 📊 Data Model

```
User ──< users_roles >── Role
Event >── EventCategory
Event ──< event_tags >── Tag
Event ── EventDetails
```

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
