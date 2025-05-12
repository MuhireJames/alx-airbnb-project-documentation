
# 🧠 Backend Features - Property management app

This document outlines the backend architecture and features for a property management web application. The system supports user authentication, property listing management, booking coordination, and secure payment processing.

---

## 📌 Core Modules

### 1. 👥 User Authentication

- **User Registration**: Allows users to register as either guests or hosts with email and password.
- **Authentication**:
  - JWT-based secure login session management.
  - OAuth login using Google and Facebook.
- **User Profile**:
  - Users can update their profile, upload profile photos, and manage their contact information.

---

### 2. 🏠 Property Management

- **Add Property (Host-only)**:
  - Hosts can list properties with detailed information such as title, description, price per night, location, availability, and amenities.
- **Edit/Delete Property**:
  - Hosts can update property information or perform a soft delete to archive listings.

---

### 3. 📅 Booking Management

- **Create Booking**:
  - Guests can book properties for selected dates.
  - The system validates availability and calculates the total price.
- **View Bookings**:
  - Guests can see their booking history.
  - Hosts can track bookings by status: upcoming, past, or canceled.

---

### 4. 💳 Payment System

- **Handle Payments**:
  - Secure payment processing via integrated platforms like Stripe or PayPal.
  - Guests pay upfront; hosts are paid out after the booking is completed.
- **Multi-Currency Support**:
  - Prices are displayed in the user's preferred currency using real-time exchange rates.

---

## 🔐 Security Features

- Passwords are hashed (e.g., bcrypt).
- JWT tokens secure APIs.
- Role-based access control for host/admin actions.
---
This system ensures a scalable and secure backend for a complete rental experience across users, hosts, and admins.
