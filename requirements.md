
# 📘 Backend Feature Specifications – Airbnb Clone

This document outlines the detailed requirements and technical specifications for core backend features of an Airbnb-style rental platform.

---

## ✅ 1. User Authentication

### 🔗 API Endpoints

| Method | Endpoint           | Description                 |
|--------|--------------------|-----------------------------|
| POST   | `/api/auth/register` | Register a new user        |
| POST   | `/api/auth/login`    | Authenticate and return JWT |
| GET    | `/api/user/profile`  | Fetch user profile (auth required) |
| PUT    | `/api/user/profile`  | Update user profile         |

### 🔐 Input (Registration)
```json
{
  "first_name": "John",
  "last_name": "Dam",
  "email": "john@example.com",
  "password": "StrongPass123!",
  "role": "guest"
}
```

### ✅ Validation Rules
- Email must be unique and valid.
- Password must have at least 8 characters, including uppercase and number.
- Role must be either `guest` or `host`.

### ✅ Output
```json
{
  "message": "Registration successful",
  "token": "<JWT_TOKEN>"
}
```

---

## 🏘️ 2. Property Management

### 🔗 API Endpoints

| Method | Endpoint              | Description                |
|--------|-----------------------|----------------------------|
| POST   | `/api/properties`     | Create a new property      |
| GET    | `/api/properties`     | List all properties        |
| GET    | `/api/properties/:id` | View a specific property   |
| PUT    | `/api/properties/:id` | Edit a property            |
| DELETE | `/api/properties/:id` | Delete a property          |

### 🧾 Input
```json
{
  "name": "Seaside Villa",
  "description": "A beautiful home near the beach.",
  "location": "California, USA",
  "pricepernight": 250.00
}
```

### ✅ Validation Rules
- Fields required: `name`, `description`, `location`, `pricepernight`.
- `pricepernight` must be a positive decimal.
- Only hosts can create/edit/delete listings.

---

## 📅 3. Booking System

### 🔗 API Endpoints

| Method | Endpoint                  | Description                      |
|--------|---------------------------|----------------------------------|
| POST   | `/api/bookings`           | Create a new booking             |
| GET    | `/api/bookings`           | List bookings for current user   |
| PUT    | `/api/bookings/:id/cancel`| Cancel a booking                 |

### 🧾 Input
```json
{
  "property_id": "uuid",
  "start_date": "2025-07-01",
  "end_date": "2025-07-05"
}
```

### ✅ Validation Rules
- Dates must not overlap existing bookings.
- `start_date` must be before `end_date`.
- `property_id` must exist and be active.

### ✅ Output
```json
{
  "message": "Booking confirmed",
  "booking_id": "uuid",
  "status": "pending",
  "total_price": 1000.00
}
```

---

## 💳 4. Payment Integration

### 🔗 API Endpoints

| Method | Endpoint               | Description                         |
|--------|------------------------|-------------------------------------|
| POST   | `/api/payments`        | Process a payment for a booking     |
| GET    | `/api/payments/:id`    | View a specific payment             |

### 🧾 Input
```json
{
  "booking_id": "uuid",
  "payment_method": "stripe"
}
```

### ✅ Validation Rules
- `booking_id` must refer to a valid and uncompleted booking.
- `payment_method` must be one of: `stripe`, `paypal`, `credit_card`.

### ✅ Output
```json
{
  "message": "Payment successful",
  "amount": 1000.00,
  "payment_method": "stripe",
  "payment_date": "2025-05-11T12:34:00Z"
}
```

### ⚙️ Performance Notes
- Stripe/PayPal integration with retries on failure.
- Payment records linked to booking and user.
- Host payouts triggered after booking completion.

---

## 🌟 5. Reviews and Ratings

### 🔗 API Endpoints

| Method | Endpoint              | Description                     |
|--------|-----------------------|---------------------------------|
| POST   | `/api/reviews`        | Submit a review for a property  |
| GET    | `/api/reviews/:id`    | Get all reviews for a property  |

### 🧾 Input
```json
{
  "property_id": "uuid",
  "rating": 5,
  "comment": "Fantastic place to stay!"
}
```

### ✅ Validation Rules
- `rating` must be between 1 and 5.
- `comment` cannot be empty.
- Each booking can generate only one review by the guest.

### ✅ Output
```json
{
  "message": "Review submitted",
  "review_id": "uuid"
}
```

---

## 📈 Performance Criteria Summary

- **User Auth**: Response under 300ms; secure password hashing (bcrypt).
- **Property Listing**: Paginated (default 10/page); support filtering.
- **Booking**: Availability checks ≤ 100ms; booking status lifecycle managed.
- **Payments**: Secure via Stripe/PayPal; logging of failures/successes.
- **Reviews**: Review integrity ensured via booking linkage.
