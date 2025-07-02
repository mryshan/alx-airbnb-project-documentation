# 📋 Backend Requirements – Airbnb Clone

This document outlines the technical and functional requirements for three key backend features: **User Authentication**, **Property Management**, and **Booking System**.

---

## 1️⃣ User Authentication

### 🔧 API Endpoints

| Method | Endpoint             | Description                              |
|--------|----------------------|------------------------------------------|
| POST   | `/api/register`      | Register a new user                      |
| POST   | `/api/login`         | Authenticate user and return JWT         |
| GET    | `/api/user/profile`  | Retrieve logged-in user profile          |
| PUT    | `/api/user/profile`  | Update user profile info                 |

### 📥 Input / Output Specifications

**Register**

**Input**
```json
{
  "name": "Jane Doe",
  "email": "jane@example.com",
  "password": "SecurePassword123"
}
```

**Output**
```json
{
  "message": "User created successfully",
  "token": "JWT_TOKEN_HERE"
}
```

**Login**

**Input**
```json
{
  "email": "jane@example.com",
  "password": "SecurePassword123"
}
```

**Output**
```json
{
  "token": "JWT_TOKEN_HERE",
  "user": {
    "id": 1,
    "name": "Jane Doe",
    "email": "jane@example.com"
  }
}
```

### ✅ Validation Rules

- Email must be unique and in valid format  
- Password must be at least 8 characters, with letters and numbers  
- All fields are required  
- Passwords should be securely hashed using bcrypt  

### ⚙️ Performance Criteria

- JWT token generation and login response should be under 1 second  
- Token expiration should be secure (e.g., 24 hours)  

---

## 2️⃣ Property Management

### 🔧 API Endpoints

| Method | Endpoint                 | Description                          |
|--------|--------------------------|--------------------------------------|
| POST   | `/api/properties`        | Create a new property listing        |
| GET    | `/api/properties`        | Retrieve all or filtered listings    |
| GET    | `/api/properties/:id`    | View single property details         |
| PUT    | `/api/properties/:id`    | Update property info                 |
| DELETE | `/api/properties/:id`    | Remove a property listing            |

### 📥 Input / Output Specifications

**Add Property**

**Input**
```json
{
  "title": "Cozy Apartment in Nairobi",
  "description": "2-bedroom near city center",
  "location": "Nairobi, Kenya",
  "price_per_night": 50,
  "availability": true,
  "amenities": ["WiFi", "Kitchen", "Parking"]
}
```

**Output**
```json
{
  "message": "Property added successfully",
  "property_id": 201
}
```

### ✅ Validation Rules

- Title, location, price, and description are required  
- Price must be a positive number  
- Only users with host role can create, edit, or delete properties  

### ⚙️ Performance Criteria

- Listings query with filters must respond in under 2 seconds  
- Property creation/editing should respond in under 1.5 seconds  

---

## 3️⃣ Booking System

### 🔧 API Endpoints

| Method | Endpoint                | Description                           |
|--------|-------------------------|---------------------------------------|
| POST   | `/api/bookings`         | Guest books a property                |
| GET    | `/api/bookings`         | View guest's booking history          |
| DELETE | `/api/bookings/:id`     | Cancel a booking                      |

### 📥 Input / Output Specifications

**Create Booking**

**Input**
```json
{
  "property_id": 201,
  "check_in": "2025-08-01",
  "check_out": "2025-08-05",
  "guests": 2
}
```

**Output**
```json
{
  "message": "Booking successful",
  "booking_id": 501
}
```

### ✅ Validation Rules

- Check-in and check-out must be valid future dates  
- Property must be available on selected dates  
- Guests must be a positive number  
- Double bookings should be prevented by date overlap check  

### ⚙️ Performance Criteria

- Availability validation should complete in under 1 second  
- Booking creation should respond in under 1.5 seconds  
- Cancellations must update database and notify both guest and host  

---
