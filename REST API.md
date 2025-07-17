---

# 🚀 What is a RESTful API?

---

### ✅ **Definition:**

A **RESTful API** (REpresentational State Transfer) is an **architectural style** for designing networked applications (usually web services).
It uses **HTTP methods** (GET, POST, PUT, DELETE) to **perform operations on resources** (like users, products, posts) identified by **URLs**.

---

### 📦 Think of it Like This:

Imagine you're ordering food through **Swiggy** or **Zomato**.
You:

* **View restaurants** → `GET /restaurants`
* **Place an order** → `POST /orders`
* **Update your delivery address** → `PUT /user/address`
* **Cancel the order** → `DELETE /orders/:id`

That's REST in real life. You're interacting with "resources" via specific actions.

---

### 🔥 REST API Basics (The 6 Principles)

1. **Stateless**

   * Every request is independent.
   * Server doesn't store client state between requests.
   * Each request must contain all the necessary info (like a token).

2. **Client-Server**

   * Client (frontend) and server (backend) are separate and independent.
   * They only communicate through requests/responses.

3. **Cacheable**

   * Responses must define if they can be cached.
   * Helps with performance.

4. **Uniform Interface**

   * Use standard methods: `GET`, `POST`, `PUT`, `DELETE`
   * Resources are identified via URIs like `/users/1`

5. **Layered System**

   * You can have multiple layers (proxies, load balancers, etc.) and client doesn’t need to care.

6. **Code on Demand (optional)**

   * Server can send executable code (like JavaScript), but rarely used.

---

### ⚙️ Example of RESTful API

```http
GET /users            --> Get all users  
GET /users/5          --> Get user with ID 5  
POST /users           --> Create a new user  
PUT /users/5          --> Update user 5  
DELETE /users/5       --> Delete user 5
```

Each URL (called a **resource endpoint**) represents a specific **thing**, and the **HTTP method** defines **what you want to do** with it.

---

### 🧠 Why RESTful APIs Are Loved by Devs:

* Simple and predictable
* Works over HTTP — no need for fancy protocols
* Easily consumed by frontend (React, Angular) or mobile apps
* Scalable and stateless

---

### ⚠️ REST ≠ RESTful

* Just using HTTP doesn’t make your API RESTful.
* You need to follow the rules (like statelessness, resource URIs, proper status codes, etc.).

---

### 🚀 Real Interview Answer

**"A RESTful API is an architectural style for designing APIs that use standard HTTP methods to perform operations on resources. Each resource is identified via a URI, and the operations follow stateless, client-server communication principles. It ensures scalability, simplicity, and separation between frontend and backend systems."**

---
