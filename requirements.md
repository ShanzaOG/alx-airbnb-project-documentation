# **ALX Airbnb Backend Project Documentation**

This repository contains the documentation for the backend of an Airbnb Clone. Below are the detailed technical and functional requirements for three core features: **User Authentication**, **Property Management**, and **Booking System**.

---

## **Features**

### **1. User Authentication**
#### **Functional Requirements**
- Users can register with an email, username, and password.
- Users can log in using valid credentials.
- Token-based authentication (e.g., JWT) is used for user sessions.
- Passwords are securely hashed (e.g., bcrypt).
- Email verification is required to activate accounts.

#### **API Endpoints**
- **`POST /api/auth/register`**
  - **Input**:
    ```json
    {
      "username": "string",
      "email": "string",
      "password": "string"
    }
    ```
  - **Output**:
    - **On Success**:
      ```json
      {
        "message": "User registered successfully. Please verify your email."
      }
      ```
    - **On Failure**:
      ```json
      {
        "error": "Invalid input or email already exists."
      }
      ```

- **`POST /api/auth/login`**
  - **Input**:
    ```json
    {
      "email": "string",
      "password": "string"
    }
    ```
  - **Output**:
    - **On Success**:
      ```json
      {
        "token": "string"
      }
      ```
    - **On Failure**:
      ```json
      {
        "error": "Invalid credentials."
      }
      ```

#### **Validation Rules**
- Email must follow a valid format and not exceed 100 characters.
- Password must be at least 8 characters and include a mix of uppercase, lowercase, and numbers.
- Username must be alphanumeric and 3-50 characters long.

#### **Performance Criteria**
- Registration and login responses must process within 300ms under normal load.

---

### **2. Property Management**
#### **Functional Requirements**
- Hosts can list properties with details like name, description, price, and images.
- Guests can search and filter properties by location, price, and amenities.
- Properties are categorized as available or unavailable based on booking status.

#### **API Endpoints**
- **`POST /api/properties`**
  - **Input**:
    ```json
    {
      "hostId": "string",
      "name": "string",
      "description": "string",
      "price": "number",
      "images": ["string"]
    }
    ```
  - **Output**:
    ```json
    {
      "message": "Property listed successfully."
    }
    ```

- **`GET /api/properties?location={location}&price={range}`**
  - **Output**:
    ```json
    [
      {
        "id": "string",
        "name": "string",
        "price": "number",
        "images": ["string"],
        "available": true
      }
    ]
    ```

#### **Validation Rules**
- Property names must be unique for each host and not exceed 100 characters.
- Price must be a positive number.
- At least one image URL must be provided.

#### **Performance Criteria**
- Search results must be returned within 500ms under normal load.

---

### **3. Booking System**
#### **Functional Requirements**
- Guests can book properties for specific dates if available.
- Hosts are notified of bookings on their properties.
- Bookings can be canceled or modified up to 24 hours before check-in.

#### **API Endpoints**
- **`POST /api/bookings`**
  - **Input**:
    ```json
    {
      "propertyId": "string",
      "guestId": "string",
      "checkInDate": "string",
      "checkOutDate": "string"
    }
    ```
  - **Output**:
    ```json
    {
      "message": "Booking successful.",
      "bookingId": "string"
    }
    ```

- **`GET /api/bookings/{guestId}`**
  - **Output**:
    ```json
    [
      {
        "bookingId": "string",
        "propertyId": "string",
        "checkInDate": "string",
        "checkOutDate": "string",
        "status": "string"
      }
    ]
    ```

#### **Validation Rules**
- Check-in date must be later than the current date.
- Check-out date must be at least 1 day after the check-in date.
- Property must be available for the selected dates.

#### **Performance Criteria**
- Booking confirmations must process within 300ms under normal conditions.

---

## **How to Use**
1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/alx-airbnb-project-documentation.git
