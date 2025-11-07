# Airbnb Clone Backend - Features and Functionalities

This document outlines the core features, technical requirements, and non-functional requirements of the Airbnb Clone backend. 

## Core Functionalities
- **User Management**: Registration, login, profile management for guests and hosts.
- **Property Listings**: Create, edit, delete property listings with detailed attributes.
- **Search & Filtering**: Search properties by location, price, number of guests, and amenities.
- **Booking Management**: Create, cancel, and track booking statuses.
- **Payment Integration**: Secure payments with Stripe/PayPal and multi-currency support.
- **Reviews & Ratings**: Guests leave reviews, hosts respond, linked to bookings.
- **Notifications**: Email and in-app notifications for booking and payment events.
- **Admin Dashboard**: Monitor and manage users, listings, bookings, and payments.

## Technical Requirements
- Relational database (PostgreSQL/MySQL)
- RESTful APIs with proper HTTP methods and status codes
- JWT authentication and role-based access control
- File storage (AWS S3 or Cloudinary)
- Third-party email services for notifications
- Global error handling and logging

## Non-Functional Requirements
- Scalability: Modular architecture, horizontal scaling
- Security: Encryption for sensitive data, firewalls, rate limiting
- Performance: Caching (Redis), query optimization
- Testing: Unit, integration, and automated API tests

The diagram `airbnb_features.png` visualizes all features and their relationships.
