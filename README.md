# airbnb-clone-project

**Status**: In Development

Welcome to the **Airbnb Clone Project** - a web app that mirrors the core functionalities of the Airbnb platform.

## Project Goals

- Recreate essential features of Airbnb such as property listings, user profiles, bookings, and reviews.
- Build a scalable and maintainable backend using industry-standard tools and practices.
- Implement a robust API that supports both REST and GraphQL queries.
- Employ asynchronous processing and caching for performance optimization.
- Ensure smooth deployments and code quality with modern DevOps practices.

## Team Roles

- **Project Manager**: Oversees the planning, execution, and delivery of the project. Ensures deadlines are met, manages the team’s workflow, coordinates meetings, and acts as the bridge between stakeholders and developers.
- **Backend Developer**: Designs and implements the server-side logic, database interactions, and core application functionality.
- **Frontend Developer**: Handles the user interface and experience (UI/UX), integrating with the APIs provided by the backend.
- **Database Administrator**: Responsible for designing, implementing, and maintaining the PostgreSQL database schema. Ensures data integrity, performance tuning, and backup management.
- **DevOps Engineer**: Implements and manages CI/CD pipelines, containerization with Docker, and deployment workflows. Ensures that the code moves smoothly from development to production environments.
- **QA Engineer**: Develops and executes test plans to ensure software quality. Responsible for identifying bugs, ensuring functionality aligns with requirements, and maintaining high standards of performance.
- **Systems Architect**: Defines the overall system structure, including technology stack decisions, integration patterns, and scalability strategies. Ensures the system is robust and maintainable.
- **Asynchronous Task Manager**: Manages background tasks using **Celery** and **Redis**. This role ensures smooth handling of non-blocking operations such as sending emails, notifications, and scheduled tasks.

## Technology Stack

- **Django**: Web framework for rapid development and clean, pragmatic design.
- **Django REST Framework (DRF)**: For building RESTful APIs.
- **PostgreSQL**: Reliable and powerful open-source relational database.
- **GraphQL**: For flexible and efficient data querying.
- **Celery**: Handles asynchronous tasks like sending emails or notifications.
- **Redis**: Used for caching and managing session data.
- **Docker**: Containerization for consistent development and production environments.
- **CI/CD Pipelines**: Ensures continuous integration and deployment.

## Database Design

### Users

Represents hosts and guests

**Fields:**

- `id`: Unique identifier
- `full_name`: Full name of the user
- `email`: User’s email address (unique)
- `password`: Hashed password
- `role`: Host or Guest

**Relationships**

- A user can list multiple properties.
- A user can make multiple bookings and write multiple reviews.

### Properties

Represents listings available for rent.

**Fields:**

- `id`: Unique identifier
- `title`: Title of the listing
- `description`: Detailed description of the property
- `location`: City or address of the property
- `price_per_night`: Cost per night

**Relationships:**

- A property belongs to one user (host).
- A property can have multiple bookings and reviews.

### Bookings

Represents a reservation made by a guest.

**Fields:**

- `id`: Unique identifier
- `user_id`: References the guest who made the booking
- `property_id`: References the property being booked
- `check_in_date`: Start of stay
- `check_out_date`: End of stay

**Relationships:**

- A booking is linked to one user (guest) and one property.

### Reviews

Represents feedback left by guests

**Fields:**

- `id`: Unique identifier
- `user_id`: Guest who wrote the review
- `property_id`: Property being reviewed
- `rating`: Numerical score (e.g., 1–5)
- `comment`: Text feedback

**Relationships:**

- A review is linked to one user and one property.

### Payments

Represents payment transactions for bookings.

**Fields:**

- `id`: Unique identifier
- `booking_id`: Reference to the related booking
- `amount`: Payment amount
- `status`: e.g., pending, completed, failed
- `payment_method`: e.g., credit card, PayPal

**Relationships:**

- A payment is tied to one booking.

### Entity Relationships Summary

- One **User** can own many **Properties**.
- One **User** can make many **Bookings**.
- One **Property** can receive many **Bookings** and **Reviews**.
- One **Booking** is associated with one **Payment**.
- One **User** can write many **Reviews**.

## Feature Breakdown

- **User Management**: Handles user registration, login, profile management, and role distinction between hosts and guests. This feature ensures secure access to the platform and tailored functionality based on the user type.
- **Property Management**: Enables hosts to create, update, and delete property listings, including details like title, description, price, and location. This allows hosts to manage their rentals and ensures accurate information for potential guests.
- **Booking System**: Allows guests to book available properties for specific dates. This feature manages check-in and check-out dates, availability conflicts, and booking confirmations, forming the backbone of the rental process.
- **Review System**: Permits guests to leave reviews and ratings for properties they’ve booked. This builds trust among users and helps maintain quality standards across listings.
- **Payment Integration**: Supports secure payment processing for completed bookings. Payments are linked to individual bookings and tracked for status, ensuring a smooth transaction flow between guests and hosts.
- **Notifications & Background Tasks**: Utilizes Celery and Redis to send email confirmations, booking reminders, or status updates. This improves communication and user engagement through timely, automated notifications.
- **Search & Filtering**: Provides functionality to search listings based on parameters like location, price range, and availability. This helps guests find suitable properties quickly and efficiently.
- **Containerization & CI/CD**: The entire project is containerized using Docker and integrated with CI/CD pipelines for streamlined development and deployment. This ensures consistent environments and faster iteration cycles.

## API Security

### Authentication

- Secure user authentication using token-based methods such as JWT (JSON Web Tokens) or session-based authentication. This ensures that only registered users can access protected endpoints and prevents unauthorized access to sensitive data.
- **Importance**: Maintains platform performance and availability by blocking suspicious activity and malicious requests.

### Data Encryption

- Encryption of sensitive data, such as passwords and payment information
- **Importance**: Protects user credentials and payment data from interception or theft

### Input Validation & Sanitization

- All user input is validated and sanitized to prevent SQL injection, XSS (Cross-site Scripting), and other injection attacks.
- **Importance**: Maintains database integrity and prevents attackers from injecting malicious scripts or commands into the system.
