
---

# 🚀 Express.js Interview Guide — Core + Advanced Breakdown

---

## 🎯 CORE CONCEPTS

---

### ✅ **1. What is Express.js? Why do we use it with Node.js?**

**Express.js** is a **minimal, flexible web framework** built on top of **Node.js** that simplifies the process of:

* Routing
* Handling HTTP requests/responses
* Middleware support
* Error handling

**Why use it with Node.js?**

* Node.js is low-level (you’d have to manually create a server using `http.createServer()`).
* Express abstracts away all the boilerplate.
* Lets you create **REST APIs** with just a few lines of code.

```js
const express = require('express');
const app = express();

app.get('/', (req, res) => res.send('Hello World!'));
app.listen(3000);
```

---

### ✅ **2. What are middleware functions in Express? Real-world examples?**

**Middleware** functions are functions that execute **in sequence** during the **request-response cycle**. They can:

* Modify request (`req`) or response (`res`)
* End request cycle
* Call the next middleware

**Types**:

* Built-in (`express.json()`, `express.static()`)
* Application-level (`custom middleware`)
* Error-handling middleware
* Third-party (`cors`, `morgan`, `helmet`)

**Real-world example:**

```js
app.use((req, res, next) => {
  console.log(`[${new Date()}] ${req.method} ${req.url}`);
  next(); // pass to next middleware or route handler
});
```

---

### ✅ **3. Explain the Request-Response Cycle in Express**

Here’s what happens:

1. A **client sends a request** to the server.
2. **Express middleware** stack is processed (logging, body parsing, auth).
3. **Route handler** is matched (`app.get('/users')`).
4. Controller logic executes, possibly talks to a DB.
5. **Response is sent** using `res.send()` / `res.json()` / `res.render()`.

Diagram:

```
Client → Middleware 1 → Middleware 2 → Route Handler → Response
```

---

### ✅ **4. How do you set up routing in Express?**

Routes are how you **handle different URLs and HTTP methods**.

```js
app.get('/', (req, res) => res.send('Home Page'));
app.post('/login', (req, res) => res.send('Logging in'));
app.put('/user/:id', (req, res) => res.send(`Updating ${req.params.id}`));
```

You can also modularize using **`express.Router()`**:

```js
const router = express.Router();

router.get('/profile', profileHandler);
app.use('/user', router);
```

---

### ✅ **5. Difference Between `app.use()` vs `app.get()` / `app.post()`**

| Function     | Purpose                                                            |
| ------------ | ------------------------------------------------------------------ |
| `app.use()`  | Mounts middleware for **all methods** (GET, POST) or path prefixes |
| `app.get()`  | Handles only **GET** requests                                      |
| `app.post()` | Handles only **POST** requests                                     |

```js
app.use('/api', middleware);  // All requests to /api/*
app.get('/api/user', handler); // Only GET
```

---

### ✅ **6. How to Handle Query Parameters and Route Parameters in Express?**

**Query Parameters**: `?name=abdur&age=22`

```js
app.get('/user', (req, res) => {
  res.send(req.query); // { name: 'abdur', age: '22' }
});
```

**Route Parameters**: `/user/:id`

```js
app.get('/user/:id', (req, res) => {
  res.send(req.params); // { id: '123' }
});
```

---

### ✅ **7. Difference: `req.query` vs `req.params` vs `req.body`**

| Property     | Where it comes from   | Example                                         |
| ------------ | --------------------- | ----------------------------------------------- |
| `req.query`  | URL query string      | `/user?name=abdur` → `{name: 'abdur'}`          |
| `req.params` | URL route parameters  | `/user/:id` `/user/123` → `{id: '123'}`         |
| `req.body`   | POST/PUT request body | `{ "email": "abdur@gmail.com" }` from JSON body |

**Don't forget to use** `express.json()` to parse JSON body!

---

### ✅ **8. How to Serve Static Files in Express?**

Use `express.static()` middleware:

```js
app.use(express.static('public'));
```

Now, `http://localhost:3000/image.png` will serve `public/image.png`.

---

### ✅ **9. Error Handling Middleware**

Use a middleware with **4 parameters**:

```js
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});
```

💡 Use `next(err)` in any middleware to forward to this handler.

---

### ✅ **10. Handle 404 Responses**

Add this **after all routes**:

```js
app.use((req, res) => {
  res.status(404).send("Page Not Found!");
});
```

---

## 🧰 ADVANCED EXPRESS USAGE

---

### ✅ **11. Organizing Large Express Applications**

**Recommended structure:**

```
/controllers
/routes
/models
/middleware
/app.js
```

Example:

```js
app.use('/api/users', require('./routes/userRoutes'));
```

Keeps your code **modular**, **clean**, and **scalable**.

---

### ✅ **12. How to Secure Express Applications**

* ✅ Use **Helmet** – sets security headers
* ✅ Enable **CORS** carefully
* ✅ Sanitize user input (prevent XSS/NoSQL injection)
* ✅ Use **Rate Limiting** (e.g. `express-rate-limit`)
* ✅ HTTPS only
* ✅ Validate input with libraries like `Joi` or `express-validator`
* ✅ Disable `x-powered-by` header

```js
app.use(helmet());
app.disable('x-powered-by');
```

---

### ✅ **13. Implement JWT-based Authentication**

Steps:

1. User logs in → server sends JWT token
2. Client stores token (localStorage)
3. On protected routes, client sends token in headers
4. Server verifies using middleware

```js
const jwt = require('jsonwebtoken');

const auth = (req, res, next) => {
  const token = req.header('Authorization');
  try {
    const decoded = jwt.verify(token, 'secretKey');
    req.user = decoded;
    next();
  } catch {
    res.status(401).send('Unauthorized');
  }
};
```

---

### ✅ **14. Connect Express with MongoDB**

Install `mongoose`:

```bash
npm install mongoose
```

Connect:

```js
const mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/mydb', { useNewUrlParser: true });
```

Use inside route:

```js
const User = mongoose.model('User', new mongoose.Schema({ name: String }));
```

---

### ✅ **15. Implement Session Management**

Install and use:

```bash
npm install express-session
```

```js
const session = require('express-session');
app.use(session({
  secret: 'yourSecret',
  resave: false,
  saveUninitialized: true
}));
```

Store user data in `req.session`:

```js
req.session.user = { id: 123, name: "Abdur" };
```

---

### ✅ **16. Cookie-based vs Token-based Authentication**

| Feature          | Cookie-based (Sessions)                  | Token-based (JWT)                  |
| ---------------- | ---------------------------------------- | ---------------------------------- |
| Storage          | Server (session) + Client (cookie)       | Only Client (localStorage/headers) |
| Stateless?       | ❌ Server must track sessions             | ✅ Server doesn’t store any session |
| CSRF vulnerable? | ✅ Needs CSRF protection                  | ❌ Less vulnerable                  |
| Scalability      | ❌ Requires sticky sessions/load balancer | ✅ Easily scalable (stateless)      |
| Use-case         | Traditional web apps                     | Mobile + APIs                      |

💡 **Token-based = Better for APIs**, **Cookie-based = Simpler for server-rendered apps**

---
