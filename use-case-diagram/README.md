
# 🎯 Use Case Diagram - Property Rental System

This document describes the use case diagram representing the main interactions between users and the backend system of a property management platform. The diagram highlights the essential features for user authentication, property management, booking, and payment.

---

## 👥 Actors

- **Guest**: A user who hasn't registered yet but can browse and register.
- **User**: A general logged-in user who can search, book, and make payments.
- **Host**: A user who can list properties and manage bookings.

---

## 🔄 Use Cases

1. **Register**
   - Performed by: Guest
   - Description: Sign up using email/password or social login (Google, Facebook).

2. **Log In**
   - Performed by: User, Host
   - Description: Authenticate using credentials or OAuth.

3. **Search Properties**
   - Performed by: User, Host
   - Description: Filter and search listings by location, price, and amenities.

4. **Book Property**
   - Performed by: User
   - Description: Book available dates for a property, triggering validation logic.

5. **Make Payment** 
   - Performed by: User, Host
   - Description: Secure transaction with cerely.

---

