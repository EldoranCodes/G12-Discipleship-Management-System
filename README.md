# RoehCare

### Shepherding & Pastoral Care Management Platform

RoehCare is a **free and open-source web application** designed to help churches **care for people, manage relationships, and support discipleship**—without enforcing a single church growth model.

The platform is intentionally **flexible**, focusing on relationships over hierarchy and care over metrics.

> “Remain in me, as I also remain in you.” – John 15:4

---

## 💖 Purpose

Churches disciple people in many forms: cell groups, pastoral mentoring, ministry teams, and other hybrid models. Instead, it provides flexible tools to support the relationships already present in a church.

## 🚀 MVP Scope

The MVP will focus on the most critical features for member care and management.

1.  **Member Onboarding & Management:** Register members via a public page or invitation to capture information for communication and follow-up.
2.  **Discipleship & Mentoring ("Growth Paths"):** Provide tools for leaders to track and support a member's spiritual journey using configurable statuses.
3.  **Basic Group Management:** Allow admins to create and assign members to groups (e.g., small groups, ministry teams).
4.  **Encouragement & Community (The "Tree"):** Foundational APIs to support a simple, read-only view of the church's member structure.

---

## 🧱 Key Concepts

### User Roles (Access Control)
These built-in roles determine what a user can *do* in the system.

*   **Admin:** Has full control. Manages church-wide settings and configures "Growth Paths."
*   **Pastor:** Has high-level visibility. Can view all member profiles and progress, manage groups, and assign leaders.
*   **Member:** The standard user. Can view/edit their own profile and see their assigned group.

### Growth Paths (Configurable Member Status)
This is a flexible system for tracking a member's journey, adaptable to any church's model.

*   **Concept:** A "Growth Path" is a sequence of statuses defined by the church (e.g., `Visitor` -> `New Believer` -> `Baptized Member`).
*   **Admin-Configurable:** The `Admin` creates, names, and orders these statuses.
*   **Progression:** Leaders can update a member's status on their profile as they grow and meet milestones ("Achievements").

---

## 🧠 Core Design Principles

*   **Model-Agnostic:** No discipleship model is hard-coded. The system adapts to the church.
*   **Care-Centered:** Tracking exists to encourage follow-ups and support leaders, not to pressure members.
*   **Church-Defined:** Administrators have the power to configure roles, statuses, and structures to fit their unique context.

---

## 🛠️ Technical Stack

### Backend
*   Java 17+
*   Spring Boot 3+
*   Spring Security (JWT)
*   Spring Data JPA / Hibernate
*   PostgreSQL (Production)
*   H2 (Development)

### Frontend (MVP)
*   React (with TypeScript)
*   Tailwind CSS
*   Mobile-first responsive design

---

## 🏗️ Architecture

A simple, maintainable, monolithic architecture:
```
React Client (Web)
        ↓
     REST API
        ↓
  Spring Boot Backend
        ↓
      Database
```

---

## 🌱 Open Source & Ministry First

RoehCare is built for churches and for developers learning together. Contributions are welcome from developers, designers, writers, and church practitioners.

## 📦 Project Status

🚧 **MVP – Active Development**

Current focus is on building the core features outlined in the MVP scope.

## 🤝 Contributing

1.  Fork the repository.
2.  Create a feature branch for your change.
3.  Commit clear, readable changes.
4.  Open a pull request.

Beginner-friendly issues will be labeled to help new contributors get started.

---

## ❤️ Final Note

RoehCare exists to **serve the Church**, not define it. If technology can help leaders love people better, then it has done its job.
