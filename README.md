# 🔐 Vaultify — AI-Powered Personal Vault for Students

> One secure place for all your documents, notes, certificates, and ideas.  
> Built with **HTML + CSS + JavaScript** frontend and **Spring Boot 3** backend.

---

## 🎨 Color Palette

| Role | Color | Hex |
|------|-------|-----|
| Brand Blue | Primary | `#5e9ef4` |
| Brand Indigo | Secondary | `#7b6cf6` |
| Brand Teal | Accent | `#38c9b3` |
| Background | Base | `#0f1117` |
| Surface | Cards | `#1c2233` |
| Text Primary | — | `#edf0f7` |

Balanced mid-tone palette — not too dark, not too light.

---

## 📁 Project Structure

```
vaultify-project/
├── frontend/
│   └── index.html          ← Complete SPA (HTML + CSS + JS)
│
└── backend/
    ├── pom.xml
    └── src/main/
        ├── java/com/vaultify/
        │   ├── VaultifyApplication.java
        │   ├── config/
        │   │   ├── SecurityConfig.java     ← JWT filter + CORS + BCrypt
        │   │   └── AppConfig.java          ← UserDetailsService + GlobalExceptionHandler
        │   ├── controller/
        │   │   └── Controllers.java        ← All REST controllers
        │   ├── dto/
        │   │   ├── DTOs.java               ← Auth, File, Message, Reminder, Search DTOs
        │   │   ├── UserDTO.java
        │   │   └── UserUpdateRequest.java
        │   ├── model/
        │   │   ├── User.java
        │   │   ├── VaultFile.java
        │   │   ├── Message.java
        │   │   └── Reminder.java
        │   ├── repository/
        │   │   └── Repositories.java       ← All JPA repos
        │   ├── service/
        │   │   ├── AuthService.java
        │   │   ├── UserService.java
        │   │   ├── FileService.java
        │   │   └── MessageService.java     ← also has ReminderService + SearchService
        │   └── util/
        │       ├── JwtUtil.java
        │       ├── FileStorageUtil.java
        │       └── AppContextHolder.java
        └── resources/
            └── application.properties
```

---

## 🚀 Quick Start

### Prerequisites
- Java 17+
- Maven 3.8+
- MySQL 8+
- A modern browser (for the frontend)

---

### 1. Database Setup

```sql
CREATE DATABASE vaultify_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'vaultify'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON vaultify_db.* TO 'vaultify'@'localhost';
FLUSH PRIVILEGES;
```

---

### 2. Configure Backend

Edit `src/main/resources/application.properties`:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/vaultify_db?...
spring.datasource.username=vaultify
spring.datasource.password=your_password
vaultify.upload.dir=./uploads
vaultify.jwt.secret=YourSuperLongSecretKeyHere
```

---

### 3. Run Backend

```bash
cd backend
mvn clean install -DskipTests
mvn spring-boot:run
```

Backend starts at: **http://localhost:8080**

---

### 4. Open Frontend

Simply open `frontend/index.html` in your browser — no build step required!

> In demo mode the frontend works completely offline with mock data.  
> To connect to the real backend, update `API_BASE` in `index.html`:
> ```js
> const API_BASE = 'http://localhost:8080/api';
> ```

---

## 📡 API Reference

### Auth
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | Create account |
| POST | `/api/auth/login` | Get JWT token |
| GET  | `/api/auth/me` | Current user info |

### Files
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET  | `/api/files?category=&page=&size=` | List files |
| GET  | `/api/files/recent` | 6 most recent |
| POST | `/api/files` | Upload file (multipart) |
| GET  | `/api/files/{id}/download` | Download file |
| PATCH| `/api/files/{id}` | Update metadata |
| POST | `/api/files/{id}/favorite` | Toggle favorite |
| DELETE | `/api/files/{id}` | Delete file |
| GET  | `/api/files/storage-stats` | Storage usage |

### Messages
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET  | `/api/messages?page=&size=` | List messages |
| POST | `/api/messages/text` | Send text |
| POST | `/api/messages/file` | Send file message |
| GET  | `/api/messages/pinned` | Pinned messages |
| POST | `/api/messages/{id}/pin` | Toggle pin |
| DELETE | `/api/messages/{id}` | Delete message |

### Reminders
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET  | `/api/reminders?pendingOnly=` | List reminders |
| POST | `/api/reminders` | Create reminder |
| POST | `/api/reminders/{id}/toggle` | Mark done |
| DELETE | `/api/reminders/{id}` | Delete |

### Search
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET  | `/api/search?q=` | Smart search |

### Dashboard
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET  | `/api/dashboard/stats` | All stats in one call |

---

## 🔐 Authentication

All protected endpoints require:
```
Authorization: Bearer <your_jwt_token>
```

---

## ✨ Frontend Pages

| Page | Description |
|------|-------------|
| 🏠 Landing | Hero, features, stats, testimonials, CTA |
| 🔐 Login | JWT login with validation |
| ✨ Register | Signup with password strength meter |
| ⚡ Dashboard | Stats, quick actions, recent files, activity, reminders |
| 💬 Chat | Self-chat with text/file messages, emoji picker, drag-drop |
| 📁 Files | Grid/list view, drag-drop upload, categories, favorites |
| 🔍 Search | AI smart search with file + message results |
| 🔔 Reminders | Create, toggle done, delete, urgency indicators |
| 👤 Profile | Edit info, security settings, storage breakdown, preferences |

---

## 🛡️ Security Features
- BCrypt password hashing (strength 12)
- JWT stateless authentication (24h expiry)
- Per-user file isolation
- File size validation (50 MB max)
- Storage quota enforcement (5 GB free)
- CORS whitelist configuration
- Input validation on all endpoints

---

## 📦 Tech Stack

**Frontend**
- Pure HTML5, CSS3, Vanilla JavaScript
- Syne + DM Sans fonts (Google Fonts)
- No build tools required

**Backend**
- Spring Boot 3.2
- Spring Security (JWT)
- Spring Data JPA
- MySQL 8
- Apache Tika (MIME + OCR)
- Lombok

---

*Built with ☕ and 💙 · Vaultify © 2024*
