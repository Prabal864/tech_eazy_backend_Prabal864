# Tech Eazy Backend

## Getting Started

### Prerequisites:
1. Java SDK 21 or higher.
2. Spring dependencies.
3. A database instance (H2 In-Memory Database).
4. Postman (optional, for testing API).

### Installation:
1. Clone the repository:
   ```bash
   git clone https://github.com/Prabal864/tech_eazy_backend_Prabal864.git
   cd tech_eazy_backend_Prabal864
   git checkout feature/delivery-orders
   ```

2. Configure application properties for database connectivity (update `application.properties`).

3. Build the project:
   ```bash
   ./mvnw clean install
   ```

4. Run the project:
   ```bash
   ./mvnw spring-boot:run
   ```

### Testing APIs:
- Import the `postman_collection.json` file into Postman to access pre-configured requests for all API endpoints.
- **Server Port:** The application runs on port `80`.

## 🔐 Authentication APIs
🔗 **Base URL:** `http://localhost:80`
- These are used to create and authenticate users. Use the JWT token returned by login APIs to access protected endpoints.

| API Name           | Method | URL                         | Role Assigned / Behavior                      |
|--------------------|--------|------------------------------|-----------------------------------------------|
| **User - Register** | POST   | `/api/auth/register`         | Registers a new user with default role: `ROLE_VENDOR` |
| **User - Login**    | POST   | `/api/auth/login`            | Login for **registered VENDOR users**         |
| **Admin - Login**   | POST   | `/api/auth/login`            | Login for **hardcoded ADMIN user** |

> ✅ Both logins return a **JWT token** containing the user's role (`ROLE_VENDOR` or `ROLE_ADMIN`).  
> 🔐 Use this token in your requests as a **Bearer Token** in Authorization headers to access protected APIs.

> ⚠️ **Important:**  
> Use the **Vendor token** (returned after VENDOR login) exclusively for VENDOR-only APIs, and the **Admin token** (returned after ADMIN login) exclusively for ADMIN-only APIs.  
> Tokens are role-specific—attempting to use a VENDOR token for ADMIN-only endpoints (or vice versa) will result in an authorization error.

## 🔐 VENDOR-Only APIs

| API Name              | Method | URL                                 | Description                   |
|------------------------|--------|--------------------------------------|-------------------------------|
| **Vendor - File Upload** | POST   | `/api/delivery-orders/upload`        | Upload delivery order file    |

> 🔐 Requires **VENDOR token only**  
> ❌ Admin is **not allowed** to access this API.

---

## 🔐 ADMIN-Only APIs

| API Name               | Method | URL                        | Description         |
|-------------------------|--------|-----------------------------|---------------------|
| **Admin - All Parcels** | GET    | `/api/parcels/all`          | Get all parcel data |

> 🔐 Requires **ADMIN token only**

---

## 🔐 Shared Access: ADMIN + VENDOR

| API Name                  | Method | URL                                                                 | Description                         |
|---------------------------|--------|----------------------------------------------------------------------|-------------------------------------|
| **admin/vendor - Today**  | GET    | `/api/delivery-orders/today?page=0&size=5`                           | Get today's delivery orders         |
| **Vendors By Name & Date**| GET    | `/api/delivery-orders/today?vendorName=Meesho&date=YYYY-MM-DD`      | Filter orders by vendor and date    |

> 🔐 Requires **either ADMIN or VENDOR token**

---

## 🌐 Public APIs (No Auth Required)

| API Name             | Method | URL                            | Description                    |
|----------------------|--------|----------------------------------|--------------------------------|
| **Public - Track ID**| GET    | `/api/parcels/track/{id}`       | Track a parcel by its ID       |

> 🟢 No authentication token required.

---

## 🛠️ How to Use JWT Token in Postman

1. Login using `User - Login` or `Admin - Login` API
2. Copy the returned `token` from the JSON response
3. For any secured API:
   - Open the request in Postman
   - Go to the `Authorization` tab
   - Set:
      - **Type**: Bearer Token
      - **Token**: *Paste the token here*

---

## 📝 Notes

- Only one role per user (`ROLE_VENDOR` or `ROLE_ADMIN`)
- Default registered users are assigned the role: `ROLE_VENDOR`
- Admin user exists with predefined credentials

