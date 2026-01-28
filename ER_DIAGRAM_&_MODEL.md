# ER Diagram & Domain Model (G12-Based)

This document explains the **core data model** for the G12 Discipleship Management System. The goal is to reflect real G12 church structure while keeping the system flexible, maintainable, and scalable.

---

## High-Level ER Diagram (Conceptual)

```
Church
  |
  | 1
  |———< Member >———|
          ^           |
          |           |
      leader_id       |
          |           |
          |           v
       Member      PromotionRequest
          |
          | 1
          |———1
       CellGroup

Member ——< Invitation
Member ——< MemberMilestone >—— Milestone
```

---

## Core Entities Explained

### 1. Church

Represents a single church organization.

```
Church
------
id (UUID)
name
status
created_at
```

Notes:

* All other entities are **scoped by church_id**
* Enables multi-church (SaaS-style) support

---

### 2. Member (Unified User Model)

Represents **all people** in the system: invited, members, leaders, pastors.

```
Member
------
id (UUID)
church_id (FK)
full_name
email
phone
status ENUM:
  INVITED | MEMBER | LEADER | PASTOR
leader_id (FK -> Member.id)
active BOOLEAN
created_at
```

Key G12 Rules:

* One member has **only one leader**
* One leader can have **up to 12 direct disciples** (enforced in service layer)
* `leader_id` is what creates the **discipleship tree**

---

### 3. CellGroup

In G12, a cell group belongs to a leader.

```
CellGroup
---------
id (UUID)
church_id
leader_id (FK -> Member.id)
name
active
```

Notes:

* Members of a cell group are those whose `leader_id` = leader
* No join table required (simpler + clearer)

---

### 4. Invitation

Tracks people who are invited but not yet members.

```
Invitation
----------
id (UUID)
church_id
invited_name
invited_by (FK -> Member.id)
status ENUM:
  INVITED | ACCEPTED | DECLINED
notes
created_at
```

Flow:

* ACCEPTED → creates a `Member` with status `INVITED`

---

### 5. PromotionRequest

Handles rank changes with leader approval.

```
PromotionRequest
----------------
id (UUID)
member_id
requested_status (LEADER | PASTOR)
requested_by
approved_by
status ENUM:
  PENDING | APPROVED | REJECTED
created_at
```

Rules:

* Approval must come from **leader above**
* On approval, `Member.status` is updated

---

### 6. Milestones (Spiritual Growth Tracking)

```
Milestone
---------
id
church_id
name
description
order_index
```

```
MemberMilestone
---------------
member_id
milestone_id
completed_at
notes
```

Purpose:

* Track spiritual progress
* Encouragement-focused (not performance-based)

---

## Why This Model Works for G12

* Natural **tree structure** using `leader_id`
* Supports promotion & multiplication
* Enforces G12 limits in business logic
* Simple queries, powerful visualization
* Easy to extend (attendance, training, notes)

---

This ER model is the foundation of the system. All APIs, security rules, and UI views are built on top of this structure.
