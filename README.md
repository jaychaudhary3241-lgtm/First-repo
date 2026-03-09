# 🏙️ CivicReport — Community Issue Reporting Platform

> Empowering citizens to report, track, and resolve local civic issues in real time.

---

## 📌 Overview

**CivicReport** is a full-stack web application that allows citizens to report civic problems (potholes, broken streetlights, water leaks, garbage overflow, etc.) to local authorities. Residents can submit reports with location details and images, while administrators can manage, prioritize, and resolve tickets efficiently.

---

## ✨ Features

- 📝 **Submit Issue Reports** — Citizens can report civic problems with title, description, category, and location
- 📍 **Location Tagging** — Attach a specific address or map coordinates to each report
- 🖼️ **Image Upload** — Attach photo evidence to issue reports
- 🔄 **Status Tracking** — Track issue progress: `Pending → In Review → In Progress → Resolved`
- 🔐 **User Authentication** — Secure login and registration for citizens and admins
- 🛠️ **Admin Dashboard** — Authorities can view, filter, assign, and update issue statuses
- 📊 **Report Analytics** — Visual summary of issue categories and resolution rates
- 🔍 **Search & Filter** — Filter issues by category, status, date, or location
- 📱 **Responsive Design** — Works seamlessly across desktop and mobile devices

---

## 🛠️ Tech Stack

| Layer       | Technology              |
|-------------|-------------------------|
| **Frontend**  | HTML5, CSS3, JavaScript (Vanilla) |
| **Backend**   | Java (Spring Boot / Jakarta EE)   |
| **Database**  | PostgreSQL               |
| **Auth**      | JWT / Session-based Auth |
| **Build Tool**| Maven / Gradle           |

---

## 📁 Project Structure

```
civic-report/
│
├── frontend/
│   ├── index.html
│   ├── css/
│   │   └── style.css
│   ├── js/
│   │   ├── main.js
│   │   ├── auth.js
│   │   └── api.js
│   └── pages/
│       ├── dashboard.html
│       ├── report.html
│       └── admin.html
│
├── backend/
│   └── src/
│       └── main/
│           └── java/
│               └── com/civicreport/
│                   ├── controller/
│                   │   ├── IssueController.java
│                   │   └── UserController.java
│                   ├── service/
│                   │   ├── IssueService.java
│                   │   └── UserService.java
│                   ├── repository/
│                   │   ├── IssueRepository.java
│                   │   └── UserRepository.java
│                   ├── model/
│                   │   ├── Issue.java
│                   │   └── User.java
│                   └── CivicReportApplication.java
│
├── database/
│   └── schema.sql
│
└── README.md
```

---

## 🗄️ Database Schema (PostgreSQL)

```sql
-- Users table
CREATE TABLE users (
    id         SERIAL PRIMARY KEY,
    name       VARCHAR(100) NOT NULL,
    email      VARCHAR(150) UNIQUE NOT NULL,
    password   VARCHAR(255) NOT NULL,
    role       VARCHAR(20) DEFAULT 'CITIZEN',
    created_at TIMESTAMP DEFAULT NOW()
);

-- Issues table
CREATE TABLE issues (
    id          SERIAL PRIMARY KEY,
    title       VARCHAR(200) NOT NULL,
    description TEXT,
    category    VARCHAR(100),
    status      VARCHAR(50) DEFAULT 'PENDING',
    location    VARCHAR(255),
    image_url   VARCHAR(500),
    reported_by INT REFERENCES users(id),
    created_at  TIMESTAMP DEFAULT NOW(),
    updated_at  TIMESTAMP DEFAULT NOW()
);
```

---

## ⚙️ Getting Started

### Prerequisites

- Java 17+
- PostgreSQL 14+
- Maven or Gradle
- A modern web browser

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/civic-report.git
cd civic-report
```

### 2. Configure the Database

```bash
psql -U postgres -c "CREATE DATABASE civicreport;"
psql -U postgres -d civicreport -f database/schema.sql
```

### 3. Configure Backend

Update `backend/src/main/resources/application.properties`:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/civicreport
spring.datasource.username=your_db_username
spring.datasource.password=your_db_password
spring.jpa.hibernate.ddl-auto=update
```

### 4. Run the Backend

```bash
cd backend
mvn spring-boot:run
```

API available at `http://localhost:8080`

### 5. Open the Frontend

```bash
python -m http.server 3000 --directory frontend
```

---

## 🔗 API Endpoints

| Method | Endpoint                    | Description                        |
|--------|-----------------------------|------------------------------------|
| POST   | `/api/auth/register`        | Register a new user                |
| POST   | `/api/auth/login`           | Login and receive a token          |
| GET    | `/api/issues`               | Get all reported issues            |
| POST   | `/api/issues`               | Submit a new issue report          |
| GET    | `/api/issues/{id}`          | Get a specific issue by ID         |
| PUT    | `/api/issues/{id}/status`   | Update issue status (Admin only)   |
| DELETE | `/api/issues/{id}`          | Delete an issue (Admin only)       |
| GET    | `/api/issues/my`            | Get issues reported by current user|

---

## 📸 Screenshots

> *(Add screenshots of your app here)*

| Citizen Dashboard | Report Submission | Admin Panel |
|---|---|---|
| ![dashboard](#) | ![report](#) | ![admin](#) |

---

## 🚀 Future Improvements

- [ ] Email/SMS notifications on status updates
- [ ] Google Maps API integration for live location pinning
- [ ] Upvoting system so citizens can support existing issues
- [ ] Export reports to PDF/CSV for authorities
- [ ] Multi-language support

---

## 🤝 Contributing

1. Fork the project
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

## 👤 Author

**Your Name**  
GitHub: [@yourusername](https://github.com/yourusername)  
Email: youremail@example.com

---

> *"Good cities are built by engaged citizens."*
