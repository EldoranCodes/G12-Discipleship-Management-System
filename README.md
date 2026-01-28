# G12 Discipleship Management System

A **free and open-source web application** designed to help churches manage discipleship using the **G12 growth model**.

This project focuses on clarity, structure, and pastoral care — not metrics pressure. It exists to serve churches and equip leaders.

---

## ✝️ Vision

To provide churches with a simple, structured system that:

* Reflects real G12 discipleship relationships
* Encourages spiritual growth
* Helps leaders care for people effectively
* Is accessible to churches of all sizes

---

## 🚀 Core Features

* Multi-church support
* Role-based access (Admin, Pastor, Leader, Member)
* G12 discipleship tree visualization
* Leader → disciple relationships (1 to 12)
* Cell group management
* Invitation tracking
* Promotion & approval workflow
* Spiritual milestones & follow-ups
* Web-first, mobile-friendly design

---

## 🧱 Tech Stack

### Backend

* Java 17+
* Spring Boot
* Spring Security (JWT)
* JPA / Hibernate
* H2 (development)
* PostgreSQL / MySQL (production)

### Frontend (Initial MVP)

* HTML / CSS / JavaScript
* Bootstrap or Tailwind

### Planned Frontend (Future)

* React or Vue
* Tree visualization (D3 / React Flow)

---

## 🏗️ Architecture

```
Frontend (Web)
   ↓ REST API
Spring Boot Backend
   ↓ JPA
Database
```

Monolithic, simple, and maintainable.

---

## 🔐 Roles & Permissions

| Role   | Access Scope             |
| ------ | ------------------------ |
| Admin  | Entire church            |
| Pastor | Full tree                |
| Leader | Own disciples & cell     |
| Member | Personal info & progress |

---

## 🌱 Spiritual Design Philosophy

This system is **not** about performance.

Milestones, notes, and follow-ups exist to:

* Encourage growth
* Support pastoral care
* Understand needs

Never to shame, rank, or pressure people.

---

## 📦 Project Status

🚧 **Early development (MVP phase)**

Planned initial release:

* Member management
* G12 enforcement
* Tree visualization
* Promotion workflow

---

## 🤝 Contributing

We welcome contributors of all levels.

Especially needed:

* Frontend developers
* UI/UX designers
* Java/Spring contributors
* Documentation writers

### How to Contribute

1. Fork the repository
2. Create a feature branch
3. Commit clean, readable changes
4. Open a pull request

Good first issues will be labeled.

---

## ❤️ Why Open Source?

This project is built:

* For churches
* For developers learning together
* For ministry, not profit

If you believe technology can serve people and faith communities — you belong here.

---

**"Go and make disciples." – Matthew 28:19**
