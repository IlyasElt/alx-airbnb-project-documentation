# Backend Feature Requirements – Airbnb Clone

This document describes the technical and functional requirements for three key backend features of the Airbnb Clone project:

1. **User Authentication**
2. **Property Management**
3. **Booking System**

Each section includes:
- Feature overview
- API endpoints
- Input & output specifications
- Validation rules
- Performance considerations

---

## ✅ 1. User Authentication

### **Feature Overview**
Handles user registration, login, and authentication using secure best practices. Ensures only authorized users can access protected endpoints.

---

### **API Endpoints**

#### **POST /api/auth/register**
Registers a new user.

**Request Body:**
```json
{
  "first_name": "John",
  "last_name": "Doe",
  "email": "john@example.com",
  "password": "Secret123!"
}
```

**Response:**
```json
{
  "message": "User registered successfully",
  "user_id": "<uuid>"
}
```

---

#### **POST /api/auth/login**
Authenticates a user and returns a JWT token.

**Request Body:**
```json
{
  "email": "john@example.com",
  "password": "Secret123!"
}
```

**Response:**
```json
{
  "message": "Login successful",
  "token": "<jwt_token>"
}
```

---

### **Validation Rules**

- `email` must be unique and valid.
- `password` must be at least 8 characters (letters + numbers).
- All required fields must be present.
- Password must be hashed before saving.
- Email comparison must be case-insensitive.

---

### **Performance Requirements**

- Frequent authentication requests should be fast (token-based).
- Should scale using stateless JWT tokens.
- Avoid database lookups on every protected request (verify JWT first).

---

## ✅ 2. Property Management

### **Feature Overview**

Allows hosts to create, update, delete, and manage property listings.

---

### **API Endpoints**

#### **POST /api/properties**

Create a new property (Host only).

**Request Body:**
```json
{
  "name": "Beach House",
  "description": "A beautiful ocean view home.",
  "location": "California",
  "price_per_night": 120,
  "amenities": ["wifi", "pool", "parking"]
}
```

**Response:**
```json
{
  "message": "Property created",
  "property_id": "uuid-value"
}
```

---

#### **GET /api/properties**

Fetch all properties with filters (search).

**Query Params (optional):**
- `location`
- `min_price`
- `max_price`

**Response:**
```json
[
  {
    "property_id": "123",
    "name": "Cozy Apartment",
    "location": "New York",
    "price_per_night": 80
  }
]
```

---

#### **PUT /api/properties/:id**

Host updates their property.

---

#### **DELETE /api/properties/:id**

Host deletes their property.

---

### **Validation Rules**

- Only a Host can create or modify properties.
- `name`, `description`, and `location` cannot be empty.
- `price_per_night` must be a positive number.
- Property must belong to the authenticated host to be editable.

---

### **Performance Requirements**

- Add indexes on:
  - `location`
  - `price_per_night`
- Pagination required for large property lists.
- Avoid returning large payloads (limit fields).

---

## ✅ 3. Booking System

### **Feature Overview**

Allows guests to book properties, validates availability, and prevents double bookings.

---

### **API Endpoints**

#### **POST /api/bookings**

Creates a booking.

**Request Body:**
```json
{
  "property_id": "uuid",
  "start_date": "2025-06-10",
  "end_date": "2025-06-14"
}
```

**Response:**
```json
{
  "message": "Booking created",
  "booking_id": "uuid"
}
```

---

#### **GET /api/bookings/me**

List bookings for the authenticated user.

---

### **Validation Rules**

- `start_date` must be before `end_date`.
- Property must exist.
- Property must not already be booked for those dates.
- Only guests can book.
- A booking cannot overlap with an existing booking in the database.

---

### **Performance Requirements**

- Use database-level constraints or SQL queries to detect overlapping dates.
- Use indexing on:
  - `property_id`
  - `start_date`
  - `end_date`
- Cache property availability checks if needed.

---

