

---

## 🔥 Node.js Interview Notes – Master Level 🔧

---

### **1. What is Node.js?**

* **Node.js** is an **open-source**, **cross-platform** runtime environment that allows JavaScript to run **outside the browser**, typically on servers.
* Built on **Chrome’s V8 JavaScript engine**.
* Uses a **single-threaded**, **non-blocking**, **event-driven** architecture.
* Runs on **Windows, macOS, and Linux**.
* Commonly used to build scalable **network applications**, **REST APIs**, and **real-time apps** like chats or streaming platforms.

🧠 *"It’s the bridge that brought JavaScript from the browser to the server."*

---

### **2. Node.js vs JavaScript**

| Feature          | JavaScript (JS)            | Node.js                               |
| ---------------- | -------------------------- | ------------------------------------- |
| Environment      | Runs in browser            | Runs on server                        |
| Use Case         | Frontend UI interactions   | Backend services, APIs, file handling |
| Access to DOM    | Yes                        | No                                    |
| Access to OS, FS | No                         | Yes                                   |
| Modules          | ES Modules (import/export) | CommonJS or ES6 modules               |

👉 Node.js **extends JavaScript** by giving it **server-side capabilities**.

---

### **3. How Node.js Works – Internal Architecture**

Imagine 2 clients sending requests (client1 and client2). Here’s what happens:

**Types of tasks**:

* 🛑 **Blocking I/O** – e.g., querying database, large computation
* ✅ **Non-blocking I/O** – e.g., reading files, HTTP requests

**Flow**:

1. Requests come in.
2. Event Loop checks the type of request.
3. If **non-blocking** – it handles it directly.
4. If **blocking** – it delegates it to the **libuv thread pool**.
5. Once results are ready, the **callback queue** sends them back to the event loop.
6. Event loop picks and sends the response to the correct client.

🌀 *This is how Node handles 1000s of requests without crashing – by not waiting!*

---

### **4. Why is Node.js Popular?**

* One language (JavaScript) across **frontend and backend**.
* **Non-blocking**, **event-driven** model = great for high I/O tasks.
* Ideal for **real-time apps**: chats, live updates, streaming.
* Massive ecosystem (npm) and used by top companies like **Netflix, Uber, LinkedIn, PayPal**.

---

### **5. Synchronous vs Asynchronous**

* **Synchronous**: One task at a time. Blocks execution.

```js
const data = fs.readFileSync("file.txt"); // Blocks here
console.log(data);
```

* **Asynchronous**: Doesn't block. Execution continues.

```js
fs.readFile("file.txt", (err, data) => {
  console.log(data);
});
console.log("Runs while file is being read.");
```

---

### **6. How Node.js Handles Asynchronous Code**

Node achieves async behavior through:

* ✅ **Callbacks** – Functions passed as arguments:

```js
fs.readFile('file.txt', callback);
```

* ✅ **Promises** – Clean alternative to callbacks:

```js
readFile('file.txt').then(data => {}).catch(err => {});
```

* ✅ **Async/Await** – Makes async code look synchronous:

```js
async function readFileAsync() {
  const data = await fs.promises.readFile("file.txt");
  console.log(data);
}
```

---

### **7. What is package.json?**

The **heart of every Node.js project**:

* Contains metadata: name, version, description, main file, scripts, dependencies.
* Run `npm init` to generate it.
* Helps npm manage the project and its dependencies.

```json
{
  "name": "myapp",
  "version": "1.0.0",
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "express": "^4.17.1"
  }
}
```

---

### **8. Top 5 Built-in Modules in Node.js**

| Module   | Purpose                                               |
| -------- | ----------------------------------------------------- |
| `http`   | Create web servers and handle HTTP requests/responses |
| `fs`     | File system operations (read/write/delete files)      |
| `path`   | Handle and transform file paths                       |
| `os`     | Info about system, memory, CPU, etc.                  |
| `events` | Handle custom events in applications                  |

Bonus: `express` is **not built-in**, it’s a 3rd-party module from npm.

---

### **9. Node.js vs Express.js**

| Feature  | Node.js                                  | Express.js                               |
| -------- | ---------------------------------------- | ---------------------------------------- |
| Type     | Runtime Environment                      | Web Framework for Node.js                |
| Purpose  | Run JS server-side                       | Simplify API and server logic            |
| Features | Non-blocking, Event Loop, FS, HTTP, etc. | Routing, Middleware, Templating, etc.    |
| Usage    | Raw, more control, more boilerplate      | Opinionated, less setup, easier to scale |

---

### **10. What is Event-Driven Programming?**

* Programming paradigm where **actions are triggered by events** (user click, API call, data received).
* In Node.js:

  * The **event loop** listens for events (HTTP requests, file read).
  * **Callbacks** or **event listeners** are triggered when an event occurs.

Example:

```js
const EventEmitter = require("events");
const emitter = new EventEmitter();

emitter.on("greet", () => console.log("Hello World!"));
emitter.emit("greet");
```

---
## 📦 MODULES & PACKAGE MANAGEMENT — Node.js Interview Notes

---

### ✅ **What is the difference between `require()` and `import`?**

| Feature      | `require()`                             | `import` (ES6)                                              |
| ------------ | --------------------------------------- | ----------------------------------------------------------- |
| Type         | CommonJS module system                  | ES6 module system                                           |
| Syntax       | `const x = require('module')`           | `import x from 'module'`                                    |
| Sync/Async   | Synchronous (blocks until module loads) | Asynchronous (non-blocking)                                 |
| Usage        | Default in Node.js before ES6           | Modern JS apps, supported with `.mjs` or `"type": "module"` |
| Export Style | `module.exports`                        | `export` / `export default`                                 |
| When to Use  | Most common in existing Node projects   | Used when working with frontend or latest Node.js apps      |

🧠 Extra:

* Node.js supports both now, but **mixing them in the same file = ❌ chaos**.
* Use `require()` for older/common modules, `import` when using Babel/Webpack or latest `Node >= 14+`.

---

### 🔄 **CommonJS vs ES6 Modules**

| Feature           | CommonJS                 | ES6 Modules                                  |
| ----------------- | ------------------------ | -------------------------------------------- |
| File Extension    | `.js`                    | `.mjs` or `"type": "module"` in package.json |
| Load Type         | Synchronous              | Asynchronous                                 |
| Export            | `module.exports = value` | `export const x = ...` / `export default`    |
| Import            | `const x = require(...)` | `import x from '...'`                        |
| Top-Level `await` | ❌ Not allowed            | ✅ Allowed                                    |
| Tree Shaking      | ❌ Not Supported          | ✅ Supported by bundlers                      |

💡 **Interview Nugget**:

> ES Modules are better for performance (like tree shaking) and will become the standard long term.

---

### 🛠️ **How does `require()` work under the hood?**

Here’s a breakdown of what happens when you call:

```js
const fs = require('fs');
```

🔍 Internally:

1. **Resolve**: Node checks if the module exists in core modules, `node_modules`, or a relative path.
2. **Cache Check**: If it's already loaded, return from **module cache** to avoid reloading.
3. **Load**: Loads the file and wraps it like this:

```js
(function(exports, require, module, __filename, __dirname) {
  // Module code goes here
});
```

4. **Execute**: Executes the code inside that function.
5. **Export**: Returns `module.exports` back to your variable.

📦 Bonus:

* Node uses **CommonJS module wrapper** function for isolation.

---

### 📁 **What is `package.json` and what does it contain?**

It's the **manifest file** for every Node.js project. Created using:

```bash
npm init
```

It contains:

```json
{
  "name": "myapp",
  "version": "1.0.0",
  "description": "A sample app",
  "main": "index.js",           // Entry file
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "express": "^4.17.1"
  },
  "devDependencies": {
    "nodemon": "^2.0.0"
  }
}
```

🧠 Other important fields:

* `license`, `author`, `engines`, `keywords`

---

### 🔍 **Difference between `dependencies` and `devDependencies`**

| Aspect                | `dependencies`                | `devDependencies`                                          |
| --------------------- | ----------------------------- | ---------------------------------------------------------- |
| Used in Production?   | ✅ Yes                         | ❌ No                                                       |
| Example Packages      | `express`, `mongoose`, `cors` | `nodemon`, `eslint`, `jest`                                |
| Installed by default  | Yes (`npm install`)           | Only with `npm install --dev` or `npm install` in dev mode |
| Field in package.json | `"dependencies"`              | `"devDependencies"`                                        |

🧪 Think of devDependencies as **“build tools / helpers”** and dependencies as **“your actual app logic.”**

---

### 📦 **How does npm work internally?**

Let’s demystify what happens when you run:

```bash
npm install express
```

Internally:

1. **Checks package.json** for version compatibility.
2. **Connects to npm registry** and fetches the metadata.
3. **Resolves dependencies recursively**.
4. **Downloads the packages** to `node_modules`.
5. **Creates package-lock.json** (for version locking).
6. **Saves the dependency** in `package.json`.

📌 `npm` = Node Package Manager
It manages **installation**, **versioning**, **scripts**, and **dependency trees**.

---

### 🧨 **What is `npx` and how is it different from `npm`?**

| Feature         | `npm`                          | `npx`                                    |
| --------------- | ------------------------------ | ---------------------------------------- |
| Purpose         | Install and manage packages    | Execute a package without installing it  |
| Installs?       | Yes, adds to `node_modules`    | No (temporary execution)                 |
| Usage           | `npm install create-react-app` | `npx create-react-app my-app`            |
| Global Install? | Often required                 | No need (works without polluting system) |

🧠 Example:

* **npm**: You install `eslint` globally and run it.
* **npx**: You just run `npx eslint .` — it fetches and runs latest version on the fly.

---

## ✅ Quick Summary (1-liners for interview flashback):

* `require()` = CommonJS, sync, used mostly in Node.
* `import` = ES6 modules, async, future of JavaScript.
* CommonJS is older, ES6 is modern + supports tree-shaking.
* `package.json` is your project’s heart and brain.
* `dependencies` run in production, `devDependencies` don’t.
* `npm` installs & manages packages. `npx` just runs them temporarily.

---


