# air-bnb-clone
# Airbnb Clone Project

## Project Overview

This project aims to build a Airbnb clone, focusing on developing a secure backend system that supports property listings, user management, booking functionalities, reviews, and payment processing. My goal is to create a scalable, secure, and efficient platform that mimics the core functionalities of Airbnb while implementing modern software development practices.

The tech stack has been carefully selected to ensure performance, scalability, and maintainability, featuring Django for the backend, SQL for database management, and GraphQL for flexible API queries.

## Team Roles

### Backend Developer
Responsible for designing and implementing the server-side logic, defining and maintaining the central database, and ensuring high performance and responsiveness to requests from the front-end.

### Database Administrator
Oversees the design, implementation, maintenance, and repair of the database. The Database Administrator ensures data integrity, optimizes database performance, implements backup and recovery strategies, and enforces data security measures.

### DevOps Engineer
Handles the CI/CD pipeline, infrastructure management, and deployment processes. The DevOps Engineer works on automating development workflows, monitoring system performance, and ensuring high availability and scalability of the application.

### API/Integration Specialist
Focuses on developing and maintaining APIs for internal services and external integrations. The API Specialist ensures seamless communication between different components of the application and third-party services, while implementing proper security measures for all API endpoints.

### Security Specialist
Identifies and fixes security vulnerabilities, implements authentication and authorization mechanisms, and ensures compliance with data protection regulations. The Security Specialist conducts security audits and penetration testing to maintain the highest security standards.

### Project Manager
Coordinates team efforts, tracks progress, manages resources, and ensures timely delivery of project milestones. The Project Manager facilitates communication between team members and stakeholders and resolves any issues that might impede project progress.

## Technology Stack

### Django
A high-level Python web framework that encourages rapid development and clean, pragmatic design. Django handles the core backend functionality, including request processing, view rendering, and business logic implementation.

### SQL
A powerful, open-source object-relational database system that provides robustness, performance, and tools for managing data.

### GraphQL
A query language for APIs and a runtime for executing those queries with existing data. GraphQL enables clients to request exactly the data they need, making API calls more efficient and flexible compared to traditional REST APIs.

### Redis
An in-memory data structure store used as a database, cache, and message broker. Redis enhances performance by caching frequently accessed data and managing session information.

### Docker
A platform for developing, shipping, and running applications in containers. Docker ensures consistent environments across development, testing, and production, simplifying deployment and scaling.

### Nginx
A web server that can also be used as a reverse proxy, load balancer, and HTTP cache. Nginx handles HTTP requests, routes them to the appropriate backend services, and serves static files efficiently.

### JWT (JSON Web Tokens)
A compact, URL-safe means of representing claims to be transferred between two parties. JWT provides secure authentication and authorization for API endpoints.

### Celery
An asynchronous task queue based on distributed message passing. Celery handles background tasks such as sending emails, processing payments, and generating reports.

## Database Design

### Users
- **user_id**: Unique identifier for each user
- **first_name**: User's first name
- **last_name**: User's last name
- **email**: User's email address (unique)
- **password**: Encrypted password
- **role**: can be admin, host or guest
- **created_at**: user's profile creation date
- **deleted_at**: user's deletion date
Users can have multiple properties (as hosts) and multiple bookings (as guests).

### Properties
- **property_id**: Unique identifier for each property
- **host_id**: Reference to the user who owns the property
- **title**: Property title
- **property_image**: image files to the property
- **property_type**: can be apartment, bedsitter, cottage
- **location**: property location
- **is_available**: boolean to check if property is available for booking or not
- **price_per_night**: Cost per night in Ksh

Each property belongs to one user (host) and can have multiple bookings and reviews.

### Bookings
- **booking_id**: Unique identifier for each booking
- **property_id**: Reference to the booked property
- **guest_id**: Reference to the user making the booking
- **num_of_guests**: Number of guests per night
- **total_price**: total price of bookings
- **check_in_date**: Date of check-in
- **check_out_date**: Date of check-out
- **cancelled_at**: Date of cancellation
- **status**: Pending or completed or cancelled

Each booking belongs to one property and one user (guest).

### Reviews
- **review_id**: Unique identifier for each review
- **booking_id**: Reference to the reviewed property. I'm usig booking_id to ensure only users who have stayed there can review
- **guest_id**: Reference to the user writing the review
- **rating**: Numerical rating (1-5)
- **review**: Text content of the review
- **date**: Date of review submission

Each review belongs to one property and is written by one user (guest).

### Payments
- **payment_id**: Unique identifier for each payment
- **booking_id**: Reference to the associated booking
- **amount**: Payment amount in USD
- **payment_method**: card, cash or mpesa
- **status**: Current status of payment (pending, completed, refunded)
- **payment_date**: Date and time of payment
- **refund_requested_at**: Date of refund request
- **refund_granted_at**: Date of refund grant
- **refund_reason**: Reason of refund

Each payment is associated with one booking.

## Feature Breakdown

### User Management
The User Management feature handles user registration, authentication, and profile management. It ensures secure user data storage and provides functionalities for users to update their profiles, manage notification preferences, and control account settings, enhancing the overall user experience and security.

### Property Management
The Property Management feature enables hosts to create, update, and manage their property listings. It includes functionalities for adding property details, uploading photos, setting pricing and availability, and managing booking requests, providing hosts with comprehensive control over their listings.

### Booking System
The Booking System facilitates the process of finding and reserving properties. It includes search functionality with filters, property availability calendars, booking request processing, and reservation management, creating a seamless booking experience for guests and efficient reservation management for hosts.

### Review and Rating System
The Review and Rating System allows guests to provide feedback on properties they've stayed at. It includes functionalities for submitting ratings and written reviews, displaying aggregate ratings, and managing review responses from hosts, promoting transparency and trust within the platform community.

### Payment Processing
The Payment Processing feature manages all financial transactions on the platform. It handles secure payment collection from guests, payout disbursement to hosts, refund processing, and financial reporting, ensuring smooth and secure monetary exchanges between users.

### Search and Filtering
The Search and Filtering feature enables users to efficiently find properties that match their preferences. It provides advanced search capabilities with multiple filters (location, price, amenities, etc.), sorting options, and saved search functionality, enhancing the property discovery experience.

### Messaging System
The Messaging System facilitates communication between hosts and guests. It includes direct messaging functionalities, automated notifications, message history, and inquiry management, ensuring clear and efficient communication throughout the booking process.

## API Security

### Authentication and Authorization
The system implements JWT-based authentication to verify user identities and role-based authorization to control access to resources. This is crucial for protecting user data, preventing unauthorized access to sensitive information, and ensuring that users can only perform actions they are permitted to do.

### Data Encryption
All sensitive data, including personal information and payment details, is encrypted both in transit and at rest. This protects against data breaches and unauthorized access, ensuring compliance with data protection regulations and maintaining user trust.

### Rate Limiting
API endpoints are protected with rate limiting to prevent abuse and denial-of-service attacks. This ensures fair usage of platform resources, protects against brute force attacks, and maintains service availability during high traffic periods.

### Input Validation and Sanitization
All user inputs are thoroughly validated and sanitized to prevent injection attacks and data corruption. This protects the database integrity, prevents cross-site scripting (XSS) attacks, and ensures that only valid data enters the system.

### Security Headers and CORS Policies
Proper security headers and Cross-Origin Resource Sharing (CORS) policies are implemented to protect against various web vulnerabilities. This prevents unauthorized websites from accessing API resources, protects against clickjacking attacks, and enhances overall browser security.

## CI/CD Pipeline

Continuous Integration/Continuous Deployment (CI/CD) pipelines automate the testing and deployment processes, ensuring code quality and enabling rapid, reliable software delivery. These automated workflows help detect bugs early, facilitate consistent deployments, and allow developers to focus on writing code rather than manual deployment tasks.

The CI/CD pipeline I chose uses GitHub Actions for automation, Docker for containerization, and deployment scripts for consistent environment setup. The pipeline includes:

1. **Code Linting and Style Checking**: Ensures code quality and consistency
2. **Automated Testing**: Runs unit and integration tests to catch bugs early
3. **Security Scanning**: Identifies potential vulnerabilities in the codebase
4. **Build Process**: Creates Docker images for deployment
5. **Staging Deployment**: Automatically deploys to a staging environment for testing
6. **Production Deployment**: Promotes verified builds to production after approval

This approach significantly reduces human error in the deployment process, enables rapid iteration, and maintains high standards of code quality throughout the development lifecycle.
