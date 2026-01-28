# RoehCare Project Plan (newPlan.md)

This document outlines the vision, strategy, and development roadmap for the RoehCare platform, incorporating your feedback and the technical foundation from existing documents.

---

## 1. Project Vision & Core Purpose

RoehCare is a **member care and church management platform**. Its primary purpose is to empower church leaders to care for their members effectively by facilitating communication, tracking spiritual growth, and fostering a sense of community.

The platform is designed to be flexible and relationship-focused, not a rigid, metric-driven tool.

## 2. MVP (Minimum Viable Product) Scope

The MVP will focus on the most critical features to achieve the core purpose. Other features will follow in later phases.

**MVP Priority List:**
1.  **Member Onboarding & Management:** The highest priority is to get members registered in the system to capture their information for communication and follow-up. This includes both a public registration page and an invitation-only flow.
2.  **Discipleship & Mentoring ("Growth Paths"):** Provide tools for leaders to track and support a member's spiritual journey. This involves managing member statuses and logging key interactions or milestones.
3.  **Basic Group Management:** Allow admins to create and assign members to groups (e.g., small groups, ministry teams).
4.  **Encouragement & Community (The "Tree"):** While the full interactive tree visualization is a post-MVP feature, the MVP will include the foundational APIs to support a simple, read-only view of the church's structure to give members a sense of belonging.

---

## 3. Core Concepts Explained

### User Roles (Access Control)
These roles are built-in and determine what a user can *do* in the system.

*   **Admin:** Has full control. Manages church-wide settings, configures "Growth Paths" (see below), and can manage all user data.
*   **Pastor:** Has high-level visibility. Can view all member profiles and their progress, manage groups, and assign leaders. Cannot change system-level configurations.
*   **Member:** The standard user. Can view and edit their own profile, see their assigned group, and view the overall church tree.

### Growth Paths (Configurable Member Status)
This is the name for the configurable "status" or "progress" tracking system you described. It's designed to be flexible to fit any church's discipleship model.

*   **Concept:** A "Growth Path" is a sequence of statuses that a member can progress through. It's a way to visualize and track a member's journey.
*   **Admin-Configurable:** The `Admin` defines the statuses for their church (e.g., `Visitor`, `New Believer`, `Baptized Member`, `Leader in Training`). They can create, name, and order these statuses.
*   **Progression:** Pastors or designated leaders can update a member's status on their profile, often after certain "Achievements" are met.
*   **Achievements:** These are significant events or milestones in a member's journey (e.g., "Completed Welcome Seminar," "Joined a Small Group," "Water Baptism"). An `Admin` can define a list of possible achievements. While the MVP won't automate status changes based on achievements, leaders can use them as a guide for manual updates.

---

## 4. Feature Breakdown & Technical Plan

### Authentication (JWT)
*   **Technology:** Spring Security with JSON Web Tokens (JWT).
*   **Flows:**
    1.  **Public Registration:** A user can navigate to a registration page and sign up.
    2.  **Invitation:** An existing member (e.g., Pastor, Leader) can send an invitation link to a new person. When the person clicks the link, they are taken to a registration page with the "invited by" field pre-filled.
*   **Security:**
    *   Access tokens will be short-lived.
    *   Secure refresh tokens will be used to maintain sessions.
    *   Passwords will be securely hashed using BCrypt.

### Backend (Spring Boot, Java 17)
*   **Architecture:** Follow a standard layered architecture: `Controller` -> `Service` -> `Repository`.
*   **Guardrails/Best Practices:**
    *   **Service Layer:** All business logic (e.g., how a member is created, how a status is updated) belongs in the service layer. Controllers should be thin and only handle HTTP requests/responses.
    *   **DTOs (Data Transfer Objects):** Use DTOs to transfer data between the client and the server. This prevents exposing your internal database models directly via the API.
    *   **Configuration:** Store sensitive information (database credentials, JWT secret key) in environment variables or a `.properties`/`.yml` file, not hardcoded in the source code.
    *   **Database:** Use H2 for local development for ease of use and PostgreSQL in production for robustness.

### Frontend (React, Tailwind CSS)
*   **Setup:** Use `create-react-app` with the TypeScript template.
*   **Styling:** Use Tailwind CSS for a utility-first styling approach.
*   **Responsiveness:** Design with a mobile-first mindset. Use Tailwind's responsive prefixes (`sm:`, `md:`, `lg:`) to adapt the layout for different screen sizes.
*   **State Management:** For the MVP, React's built-in `Context` API will be sufficient for managing global state like the logged-in user.

### Database Schema (In Sentences)
Here is a high-level description of the main database tables:

*   **Church:** A table will hold information about each church organization, allowing the platform to support multiple churches in the future.
*   **Person:** This central table will store all users, including their name, contact information, and their assigned `Role` (Admin, Pastor, Member) and `Status` (from the Growth Path). It will also link to their `Church`. A `supervisor_id` field will link a person to their mentor or leader, creating the tree structure.
*   **Group:** This table will define the various groups within a church, like "Youth Ministry" or "Sunday Welcome Team," and will have a designated leader.
*   **GrowthStatus:** An admin-managed table that will store the possible statuses a member can have (e.g., 'Visitor', 'Member'), including their order of progression.
*   **Achievement:** An admin-managed table that lists the potential milestones a person can achieve (e.g., 'Attended Welcome Seminar').
*   **PersonAchievement:** A join table that connects a `Person` to an `Achievement` they have completed, storing the date and any relevant notes.

---

## 5. Post-MVP / Future Enhancements
*   **Interactive Tree Visualization:** A dynamic, explorable view of the church's discipleship tree.
*   **Automated Workflows:** Automatically suggest or update a member's status based on completed achievements.
*   **Dashboard & Analytics:** Provide high-level, care-focused insights for leaders (e.g., "Members not contacted in the last month").
*   **AI Chatbot:** An encouraging guide for new visitors.
*   **Editable Landing Page:** Allow admins to customize a public-facing page for their church.
