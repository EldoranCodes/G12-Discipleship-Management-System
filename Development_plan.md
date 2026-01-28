# Development Plan – G12 Discipleship Management System

This document outlines the **step-by-step development roadmap** for building the MVP and beyond.

---

## Phase 0 – Foundations

### Goals

* Stable project base
* Clear domain model

### Tasks

* Initialize Spring Boot project
* Configure JPA & H2
* Create base packages:

  * domain
  * repository
  * service
  * controller
  * security
* Add UUID support

---

## Phase 1 – Core Domain

### Goals

* Represent G12 structure in code

### Tasks

* Implement entities:

  * Church
  * Member
  * CellGroup
* Leader → disciple relationship
* Enforce 12-member rule in service layer
* Basic CRUD APIs

---

## Phase 2 – Authentication & Authorization

### Goals

* Secure role-based access

### Tasks

* Spring Security + JWT
* Member login & password setup
* Role-based method security
* Admin vs Leader vs Member permissions

---

## Phase 3 – Promotion Workflow

### Goals

* Controlled leadership growth

### Tasks

* PromotionRequest entity
* Approval flow
* Notifications (initially in-app)
* Status updates

---

## Phase 4 – Tree Visualization API

### Goals

* Visual discipleship structure

### Tasks

* Tree-building service (recursive)
* Church-wide tree endpoint
* Leader subtree endpoint
* JSON tree response

---

## Phase 5 – Milestones & Follow-ups

### Goals

* Track spiritual progress

### Tasks

* Milestone & MemberMilestone entities
* Assign milestones
* Add pastoral notes

---

## Phase 6 – Frontend MVP

### Goals

* Usable web interface

### Tasks

* Login & dashboard
* Member management UI
* Tree visualization (basic)
* Mobile-responsive layout

---

## Phase 7 – Open Source Polish

### Goals

* Contributor-friendly project

### Tasks

* Improve README
* Add CONTRIBUTING.md
* Add issue templates
* Label beginner issues

---

## Phase 8 – Future Enhancements

* Attendance tracking
* Training modules
* Mobile app
* Multi-language support
* Analytics (non-pressure-based)

---

## Development Principles

* Keep logic in service layer
* Avoid overengineering
* Prioritize clarity over features
* Respect church culture & people

---

This plan is intentionally incremental. Each phase delivers usable value while keeping the system maintainable and welcoming to contributors.
