# RoehCare - MVP README

This document provides a guide for setting up and running the Minimum Viable Product (MVP) of the RoehCare platform.

---

## 1. Project Goal (MVP)

The goal of the RoehCare MVP is to deliver a functional core application for **member care and church management**.

**Core MVP Features:**
*   **Member Onboarding:** Allow new members to register via a public page or by invitation.
*   **Member Profiles:** Store and manage essential member information.
*   **Configurable Growth Paths:** Allow church admins to define and track the spiritual journey of members through custom statuses.
*   **Role-Based Access:** A secure system with distinct permissions for `Admin`, `Pastor`, and `Member` roles.
*   **Tech Stack:** Spring Boot (Java 17) backend and a React (TypeScript) frontend with Tailwind CSS.

---

## 2. Getting Started: Backend (Spring Boot)

These instructions will guide you through setting up the backend server.

### Prerequisites
*   **Java Development Kit (JDK) 17:** Make sure you have JDK 17 installed.
*   **Maven or Gradle:** A Java build tool for managing dependencies.

### Setup Instructions
1.  **Generate the Project:**
    *   Go to [start.spring.io](https://start.spring.io).
    *   Set the following options:
        *   Project: `Maven` or `Gradle`
        *   Language: `Java`
        *   Spring Boot: `3.x.x` (any recent version)
        *   Java: `17`
        *   Packaging: `Jar`
    *   **Add Dependencies:** Click "Add Dependencies" and include:
        *   `Spring Web`: For building RESTful APIs.
        *   `Spring Data JPA`: For database interaction.
        *   `Spring Security`: For authentication and authorization.
        *   `PostgreSQL Driver`: For connecting to a PostgreSQL database.
        *   `H2 Database`: For in-memory testing during local development.
    *   Click "Generate" and unzip the downloaded project file.

2.  **Configuration (`application.properties`):**
    *   Locate the `src/main/resources/application.properties` file.
    *   For local development with H2, you don't need much configuration. Spring Boot will auto-configure an in-memory database.
    *   For production with PostgreSQL, you would add:
        ```properties
        # Use environment variables in a real project!
        spring.datasource.url=jdbc:postgresql://localhost:5432/roehcare_db
        spring.datasource.username=your_db_user
        spring.datasource.password=your_db_password
        spring.jpa.hibernate.ddl-auto=update
        ```

### Backend Development Guardrails
*   **Keep Logic in Services:** Controllers handle HTTP requests, repositories handle database access. All your business rules and logic should live in the **Service layer**.
*   **Use DTOs (Data Transfer Objects):** Never expose your database entities directly in your API. Create separate classes (DTOs) for API requests and responses to control what data is sent and received.
*   **Secure Your Secrets:** Do not hardcode passwords, API keys, or JWT secrets in your code. Use environment variables or Spring's configuration management to handle them safely.
*   **Organize Your Packages:** A clean structure helps maintainability.
    ```
    com.roehcare
    ├── config      // Spring Security, CORS settings
    ├── controller  // API endpoints
    ├── domain      // JPA Entities
    ├── dto         // Data Transfer Objects
    ├── repository  // JPA Repositories
    └── service     // Business logic
    ```

---

## 3. Getting Started: Frontend (React + Tailwind CSS)

These instructions will guide you through setting up the frontend application.

### Prerequisites
*   **Node.js and npm:** Make sure you have a recent version of Node.js installed (which includes npm).

### Setup Instructions
1.  **Create the React App:**
    *   Open your terminal and run the following command to create a new React project with TypeScript:
        ```sh
        npx create-react-app roehcare-front --template typescript
        ```
    *   Navigate into the new directory:
        ```sh
        cd roehcare-front
        ```

2.  **Install and Configure Tailwind CSS:**
    *   Install Tailwind CSS and its peer dependencies:
        ```sh
        npm install -D tailwindcss postcss autoprefixer
        ```
    *   Generate the Tailwind configuration files:
        ```sh
        npx tailwindcss init -p
        ```
        This creates `tailwind.config.js` and `postcss.config.js`.

3.  **Configure Tailwind's Template Paths:**
    *   Open `tailwind.config.js`.
    *   Modify the `content` array to include the paths to all of your component files so Tailwind can scan them for class names:
        ```javascript
        /** @type {import('tailwindcss').Config} */
        module.exports = {
          content: [
            "./src/**/*.{js,jsx,ts,tsx}", // Include all relevant file types
          ],
          theme: {
            extend: {},
          },
          plugins: [],
        }
        ```

4.  **Add Tailwind Directives to your CSS:**
    *   Open `src/index.css`.
    *   Add the following lines at the top of the file. This will inject Tailwind's base, components, and utility styles.
        ```css
        @tailwind base;
        @tailwind components;
        @tailwind utilities;
        ```

5.  **Start the Development Server:**
    *   You're all set! Run the app:
        ```sh
        npm start
        ```

### Tips for Basic Responsive Design
*   **Mobile-First:** Design your components for small screens first, then add styles for larger screens.
*   **Use Responsive Prefixes:** Tailwind uses prefixes like `sm:`, `md:`, `lg:`, and `xl:` to apply styles at specific breakpoints.
    *   `w-full md:w-1/2`: The element will be full-width on small screens and half-width on medium screens and up.
    *   `flex-col md:flex-row`: A flex container will be a column on small screens and a row on medium screens and up.
*   **Example of a responsive card:**
    ```jsx
    <div className="bg-white p-4 rounded-lg shadow-md md:flex">
      <img src="..." alt="" className="w-full h-32 object-cover rounded-t-lg md:w-48 md:h-auto md:rounded-l-lg md:rounded-t-none" />
      <div className="p-4">
        <h3 className="font-bold text-lg">Member Name</h3>
        <p className="text-gray-600">Status: Active</p>
      </div>
    </div>
    ```
