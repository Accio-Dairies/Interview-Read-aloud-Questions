# Node.js & Express Interview Preparation Guide
*Essential Backend Concepts for Freshers*

**Note for Students:** This guide is written exactly how you should answer in interviews. Practice reading these answers out loud to make them natural when speaking. Focus is on theoretical understanding with practical code examples.

---

## Table of Contents

### Node.js Fundamentals
1. [What is Node.js? Why use it?](#q1-what-is-nodejs-why-use-it)
2. [Node.js Architecture](#q2-nodejs-architecture-event-loop-single-threaded)
3. [Blocking vs Non-blocking I/O](#q3-blocking-vs-non-blocking-io)
4. [Modules in Node.js](#q4-modules-in-nodejs)
5. [require() vs import](#q5-require-vs-import)
6. [NPM - Node Package Manager](#q6-npm---node-package-manager)
7. [package.json and package-lock.json](#q7-packagejson-and-package-lockjson)
8. [Global Objects](#q8-global-objects-process-__dirname-__filename)
9. [Built-in Modules](#q9-built-in-modules-fs-path-http-os)
10. [Asynchronous Patterns](#q10-asynchronous-patterns-callbacks-promises-asyncawait)

### Express.js Basics
11. [What is Express.js?](#q11-what-is-expressjs)
12. [Setting up Express Server](#q12-setting-up-express-server)
13. [Routing](#q13-routing-get-post-put-delete)
14. [Route Parameters and Query Strings](#q14-route-parameters-and-query-strings)
15. [Request and Response Objects](#q15-request-and-response-objects)
16. [Middleware - What and Why](#q16-middleware---what-and-why)
17. [Built-in Middleware](#q17-built-in-middleware)
18. [Custom Middleware](#q18-custom-middleware)
19. [Error Handling Middleware](#q19-error-handling-middleware)
20. [express.Router()](#q20-expressrouter)

### REST API Development
21. [What is REST API?](#q21-what-is-rest-api)
22. [HTTP Methods](#q22-http-methods-get-post-put-patch-delete)
23. [Status Codes](#q23-status-codes)
24. [Request Data](#q24-request-data-body-params-query)
25. [CORS](#q25-cors---cross-origin-resource-sharing)
26. [API Versioning](#q26-api-versioning)
27. [Request Validation](#q27-request-validation)
28. [Response Formatting](#q28-response-formatting-json)

### Database Integration
29. [Connecting MongoDB with Mongoose](#q29-connecting-mongodb-with-mongoose)
30. [Mongoose Schema and Models](#q30-mongoose-schema-and-models)
31. [CRUD with Mongoose](#q31-crud-operations-with-mongoose)
32. [Connecting SQL Databases](#q32-connecting-sql-databases-mysqlpostgresql)
33. [Using ORM - Sequelize](#q33-using-orm---sequelize-basics)
34. [Connection Pooling](#q34-connection-pooling)

### Authentication & Security
35. [Authentication vs Authorization](#q35-authentication-vs-authorization)
36. [JWT - JSON Web Tokens](#q36-jwt---json-web-tokens)
37. [Password Hashing](#q37-password-hashing-bcrypt)
38. [Sessions and Cookies](#q38-sessions-and-cookies)
39. [Environment Variables](#q39-environment-variables-env)
40. [Security Best Practices](#q40-security-best-practices)

### File Handling & Advanced
41. [File Upload](#q41-file-upload-multer)
42. [File Operations](#q42-file-operations-fs-module)
43. [Streaming](#q43-streaming-in-nodejs)
44. [Template Engines](#q44-template-engines-ejs-pug)
45. [Logging](#q45-logging)
46. [Error Handling Patterns](#q46-error-handling-patterns)
47. [Debugging](#q47-debugging-nodejs-applications)
48. [Deployment Basics](#q48-deployment-basics)

### Practical Patterns
49. [Folder Structure](#q49-folder-structure--project-organization)
50. [MVC Pattern](#q50-mvc-pattern-in-express)
51. [API Documentation](#q51-api-documentation)
52. [Common Interview Questions](#q52-common-interview-coding-questions)

---

## Node.js Fundamentals

### Q1: What is Node.js? Why use it?

**How to Answer:**

"Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. It allows you to run JavaScript on the server side, outside of the browser.

**What is Node.js?**

Node.js is NOT a language or a framework - it's a runtime environment that executes JavaScript code outside the browser.

**Key features:**

1. **JavaScript everywhere** - Same language for frontend and backend
2. **Non-blocking I/O** - Handles many connections simultaneously
3. **Event-driven** - Uses events and callbacks
4. **Single-threaded** - Uses one thread with event loop
5. **Fast** - Built on V8 engine (compiles JS to machine code)

**Before Node.js:**

```
Browser only:
- JavaScript runs only in browser
- Backend needs PHP, Java, Python, etc.
- Different languages for frontend/backend
```

**With Node.js:**

```
Full-stack JavaScript:
- Frontend: JavaScript (React, Vue, Angular)
- Backend: JavaScript (Node.js)
- Same language, shared code possible
```

**Why use Node.js?**

✅ **Single language** - JavaScript for both frontend and backend
✅ **Fast** - Non-blocking I/O, event-driven
✅ **Scalable** - Handles many concurrent connections
✅ **Large ecosystem** - NPM has millions of packages
✅ **Real-time** - Great for chat apps, live updates, streaming
✅ **Microservices** - Perfect for building APIs

**When to use Node.js:**

✅ Good for:
- REST APIs
- Real-time applications (chat, notifications)
- Microservices
- Streaming applications
- Single-page applications (SPAs)
- I/O intensive operations

❌ Not ideal for:
- CPU-intensive tasks (video encoding, complex calculations)
- Heavy computation (use Python, Java, C++)

**Simple example:**

```javascript
// server.js - Simple Node.js server
const http = require('http');

const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('Hello from Node.js!');
});

server.listen(3000, () => {
  console.log('Server running on port 3000');
});
```

**Real-world usage:**

Companies using Node.js:
- Netflix - Reduced startup time by 70%
- PayPal - 2x faster with fewer developers
- LinkedIn - 2-10x faster performance
- Uber - Processes 2 billion requests daily

**Interview tip:** Node.js is a JavaScript runtime for server-side development. It's fast, event-driven, and uses non-blocking I/O. Great for APIs and real-time applications. Single language for full-stack development is a major advantage."

---

### Q2: Node.js Architecture (Event Loop, Single-threaded)

**How to Answer:**

"Node.js uses a single-threaded, event-driven architecture with a non-blocking I/O model. This makes it efficient and scalable.

**Single-threaded architecture:**

Node.js runs on a single thread but handles multiple requests using the event loop.

```
Traditional server (multi-threaded):
Request 1 → Thread 1 → Response
Request 2 → Thread 2 → Response
Request 3 → Thread 3 → Response
(Each request needs a new thread)

Node.js (single-threaded + event loop):
Request 1 ─┐
Request 2 ─┼→ Single Thread + Event Loop → Responses
Request 3 ─┘
(One thread handles all requests)
```

**Event Loop:**

The event loop is the heart of Node.js. It continuously checks for events and executes callbacks.

```javascript
// How event loop works
console.log('1: Start');

setTimeout(() => {
  console.log('2: Inside setTimeout');
}, 0);

console.log('3: End');

// Output:
// 1: Start
// 3: End
// 2: Inside setTimeout

// Why? Event loop executes sync code first, then callbacks
```

**Event Loop phases:**

```
   ┌───────────────────────────┐
┌─→│           timers          │ (setTimeout, setInterval)
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │     pending callbacks     │ (I/O callbacks)
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │       idle, prepare       │ (internal use)
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │           poll            │ (retrieve I/O events)
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │           check           │ (setImmediate)
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
└──│      close callbacks      │
   └───────────────────────────┘
```

**Simple explanation:**

1. **Synchronous code** executes immediately
2. **Asynchronous operations** (file read, DB query) are sent to worker threads
3. **Event loop** waits for operations to complete
4. **Callbacks** execute when operations finish

**Example:**

```javascript
const fs = require('fs');

console.log('Start');

// Async operation - goes to worker thread
fs.readFile('file.txt', 'utf8', (err, data) => {
  console.log('File read complete');
});

console.log('End');

// Output:
// Start
// End
// File read complete
```

**Why single-threaded is powerful:**

Traditional (multi-threaded):
- Each thread uses ~2MB memory
- 1000 connections = 2GB memory
- Context switching overhead
- Complex synchronization

Node.js (single-threaded + event loop):
- One thread handles thousands of connections
- Minimal memory overhead
- No context switching
- No thread synchronization issues

**Non-blocking I/O:**

```javascript
// Blocking (BAD - freezes server)
const data = fs.readFileSync('file.txt'); // Wait here
console.log('After file read');

// Non-blocking (GOOD - doesn't freeze)
fs.readFile('file.txt', (err, data) => {
  // Executes when file is read
});
console.log('After initiating file read'); // Executes immediately
```

**libuv:**

Node.js uses libuv library to handle:
- Event loop
- Thread pool (for file system operations)
- Async I/O
- Timers

**Interview tip:** Node.js is single-threaded but handles multiple requests efficiently using the event loop and non-blocking I/O. The event loop continuously checks for events and executes callbacks. This makes Node.js lightweight and scalable without creating multiple threads."

---

### Q3: Blocking vs Non-blocking I/O

**How to Answer:**

"Blocking and non-blocking refer to how Node.js handles I/O operations like reading files, database queries, or network requests.

**Blocking I/O (Synchronous):**

Execution stops and waits for the operation to complete before moving to the next line.

```javascript
const fs = require('fs');

console.log('Before reading file');

// Blocking - waits here until file is read
const data = fs.readFileSync('file.txt', 'utf8');
console.log(data);

console.log('After reading file');

// Output (in order):
// Before reading file
// [file contents]
// After reading file
```

**Flow:**
```
Start → Read File (WAIT) → Process File → Continue
         ↑ Execution pauses here
```

**Non-blocking I/O (Asynchronous):**

Execution continues immediately. When operation completes, a callback is invoked.

```javascript
const fs = require('fs');

console.log('Before reading file');

// Non-blocking - doesn't wait
fs.readFile('file.txt', 'utf8', (err, data) => {
  console.log(data); // Executes later
});

console.log('After reading file');

// Output:
// Before reading file
// After reading file
// [file contents]
```

**Flow:**
```
Start → Initiate Read File → Continue → Do other work
                   ↓
              (File reading in background)
                   ↓
              Callback when done
```

**Real-world comparison:**

**Blocking (like standing in line):**
```javascript
// Server handles ONE request at a time
const data1 = readFileSync('file1.txt'); // User 1 waits
const data2 = readFileSync('file2.txt'); // User 2 waits for User 1
const data3 = readFileSync('file3.txt'); // User 3 waits for User 2

// If each file takes 2 seconds:
// User 1: waits 2 seconds
// User 2: waits 4 seconds
// User 3: waits 6 seconds
```

**Non-blocking (like ordering at McDonald's):**
```javascript
// Server initiates ALL requests immediately
readFile('file1.txt', callback1); // User 1 order placed
readFile('file2.txt', callback2); // User 2 order placed
readFile('file3.txt', callback3); // User 3 order placed

// All callbacks execute when their operations complete
// If each file takes 2 seconds:
// All users wait ~2 seconds (processed in parallel)
```

**Performance impact:**

```javascript
// Blocking - handles 1 request/second
function handleRequest(req, res) {
  const data = fs.readFileSync('data.txt'); // 1 second
  res.send(data);
}
// 1 user → 1 second
// 10 users → 10 seconds
// Server is BLOCKED

// Non-blocking - handles many requests/second
function handleRequest(req, res) {
  fs.readFile('data.txt', (err, data) => { // 1 second
    res.send(data);
  });
}
// 1 user → 1 second
// 10 users → ~1 second (all processed together)
// Server continues accepting requests
```

**When to use blocking:**

```javascript
// Startup configuration - OK to block
const config = fs.readFileSync('config.json');
const server = createServer(config);

// During request handling - NEVER block
app.get('/data', (req, res) => {
  // BAD - blocks server
  const data = fs.readFileSync('data.txt');
  
  // GOOD - non-blocking
  fs.readFile('data.txt', (err, data) => {
    res.send(data);
  });
});
```

**All async patterns:**

```javascript
// 1. Callbacks (traditional)
fs.readFile('file.txt', (err, data) => {
  console.log(data);
});

// 2. Promises
const readFilePromise = util.promisify(fs.readFile);
readFilePromise('file.txt')
  .then(data => console.log(data));

// 3. Async/Await (modern)
async function readFileAsync() {
  const data = await fs.promises.readFile('file.txt');
  console.log(data);
}
```

**Interview tip:** Blocking I/O waits for operation to complete (synchronous), freezes the server. Non-blocking I/O continues execution immediately (asynchronous), uses callbacks. Node.js is designed for non-blocking operations - use async methods during request handling for better performance and scalability."

---

### Q4: Modules in Node.js

**How to Answer:**

"Modules are reusable pieces of code in Node.js. They allow you to organize code into separate files and packages.

**What are modules?**

A module is a JavaScript file that exports code (functions, objects, variables) that can be used in other files.

**Why modules?**

- **Organize code** - Split large applications into smaller files
- **Reusability** - Use same code in multiple places
- **Maintainability** - Easier to debug and update
- **Avoid naming conflicts** - Each module has its own scope

**Types of modules:**

1. **Core/Built-in modules** - Come with Node.js (fs, http, path)
2. **Local/Custom modules** - Created by you
3. **Third-party modules** - Installed via NPM (express, mongoose)

**1. Built-in modules:**

```javascript
// No installation needed
const fs = require('fs');
const http = require('http');
const path = require('path');
const os = require('os');
```

**2. Custom modules:**

**Creating a module (math.js):**
```javascript
// math.js - Export functions
function add(a, b) {
  return a + b;
}

function subtract(a, b) {
  return a - b;
}

// Export single function
module.exports = add;

// Or export multiple
module.exports = {
  add: add,
  subtract: subtract
};

// Or shorthand
module.exports = { add, subtract };
```

**Using the module:**
```javascript
// app.js - Import the module
const math = require('./math'); // ./ for local file

console.log(math.add(5, 3)); // 8
console.log(math.subtract(10, 4)); // 6
```

**3. Third-party modules:**

```javascript
// Install first: npm install express
const express = require('express');
const app = express();
```

**Different export patterns:**

**Export single item:**
```javascript
// utils.js
function greet(name) {
  return `Hello, ${name}!`;
}

module.exports = greet;

// app.js
const greet = require('./utils');
greet('John'); // Hello, John!
```

**Export multiple items:**
```javascript
// utils.js
module.exports = {
  greet: function(name) {
    return `Hello, ${name}!`;
  },
  bye: function(name) {
    return `Goodbye, ${name}!`;
  }
};

// app.js
const utils = require('./utils');
utils.greet('John'); // Hello, John!
utils.bye('John');   // Goodbye, John!

// Or destructure
const { greet, bye } = require('./utils');
greet('John'); // Hello, John!
```

**Export as you go:**
```javascript
// utils.js
exports.greet = function(name) {
  return `Hello, ${name}!`;
};

exports.bye = function(name) {
  return `Goodbye, ${name}!`;
};
```

**module.exports vs exports:**

```javascript
// These are the SAME
exports.name = 'John';
module.exports.name = 'John';

// BUT this OVERWRITES exports
module.exports = { name: 'John' }; // Use this for single export

// This WON'T work (exports is reassigned, loses reference)
exports = { name: 'John' }; // DON'T DO THIS
```

**Module caching:**

```javascript
// counter.js
let count = 0;
module.exports = {
  increment: () => ++count,
  getCount: () => count
};

// app.js
const counter1 = require('./counter');
const counter2 = require('./counter');

counter1.increment(); // 1
console.log(counter2.getCount()); // 1 (same instance!)

// Modules are cached - loaded only once
```

**Module wrapper:**

Node.js wraps every module in a function:

```javascript
// Your code
const name = 'John';

// Actually wrapped by Node.js
(function(exports, require, module, __filename, __dirname) {
  const name = 'John';
  // Your code here
});

// This is why we have access to:
// - exports, require, module
// - __filename, __dirname
```

**Interview tip:** Modules organize code into reusable files. Three types: built-in (fs, http), custom (your files), third-party (npm packages). Use module.exports to export and require() to import. Modules are cached - loaded once and reused."

---

### Q5: require() vs import

**How to Answer:**

"require() and import are two ways to include modules in JavaScript, but they work differently and come from different module systems.

**require() - CommonJS (Node.js default):**

Traditional Node.js way to import modules.

```javascript
// Importing
const express = require('express');
const { readFile } = require('fs');

// Exporting
module.exports = function() {
  console.log('Hello');
};

// Or
module.exports = {
  greet: function() {},
  bye: function() {}
};
```

**import - ES6 Modules (Modern JavaScript):**

Modern JavaScript standard for modules.

```javascript
// Importing
import express from 'express';
import { readFile } from 'fs';

// Exporting
export default function() {
  console.log('Hello');
}

// Or named exports
export function greet() {}
export function bye() {}
```

**Key differences:**

| Feature | require() | import |
|---------|-----------|--------|
| Standard | CommonJS | ES6 (ESM) |
| Loading | Runtime (dynamic) | Compile-time (static) |
| Syntax | `const x = require('x')` | `import x from 'x'` |
| Node.js default | Yes | No (needs setup) |
| Browser support | No | Yes |
| Can be conditional | Yes | No |
| Top-level only | No | Yes |

**Loading time difference:**

```javascript
// require - RUNTIME (loads when code executes)
if (condition) {
  const module = require('./module'); // Loads only if condition true
}

// import - COMPILE-TIME (loads before execution)
if (condition) {
  import module from './module'; // ERROR! Can't use import conditionally
}
```

**Using require():**

```javascript
// math.js
module.exports = {
  add: (a, b) => a + b,
  subtract: (a, b) => a - b
};

// app.js
const math = require('./math');
console.log(math.add(5, 3));

// Or destructure
const { add, subtract } = require('./math');
console.log(add(5, 3));
```

**Using import:**

```javascript
// math.js
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// Or default export
export default {
  add: (a, b) => a + b,
  subtract: (a, b) => a - b
};

// app.js
import { add, subtract } from './math.js'; // Note: .js extension
console.log(add(5, 3));

// Or default import
import math from './math.js';
console.log(math.add(5, 3));
```

**Using ES6 modules in Node.js:**

**Method 1: Add "type": "module" in package.json**

```json
{
  "name": "my-app",
  "type": "module"
}
```

```javascript
// Now you can use import
import express from 'express';
```

**Method 2: Use .mjs extension**

```javascript
// app.mjs
import express from 'express';
```

**Dynamic import (ES6):**

```javascript
// Can import conditionally using dynamic import
if (condition) {
  const module = await import('./module.js');
  module.doSomething();
}

// In async function
async function loadModule() {
  const module = await import('./module.js');
  return module;
}
```

**Mixed usage (in transition):**

```javascript
// Using both in same project

// Old files - CommonJS
// users.js
module.exports = { getUsers };

// New files - ES6
// products.js
export { getProducts };

// Main file can require CommonJS
const users = require('./users');

// But import needs "type": "module"
import { getProducts } from './products.js';
```

**Which to use?**

**Use require() when:**
- Working with older Node.js projects
- Need dynamic imports (conditional loading)
- Working with CommonJS packages
- Default Node.js (no configuration needed)

**Use import when:**
- Starting new project (modern standard)
- Want better tree-shaking (unused code removal)
- Working with frontend frameworks
- Want static analysis benefits

**Current industry practice:**

Most Node.js projects still use `require()` for backend, but `import` is gaining popularity.

**Interview tip:** require() is CommonJS (Node.js traditional), import is ES6 (modern JavaScript standard). require() loads at runtime (dynamic), import loads at compile-time (static). Node.js uses require() by default, but can use import with configuration. Import is the future but require() is still widely used."

---

### Q6: NPM - Node Package Manager

**How to Answer:**

"NPM is the default package manager for Node.js. It allows you to install, share, and manage packages (libraries/modules) in your project.

**What is NPM?**

NPM is two things:
1. **Registry** - Online database of public packages (over 2 million packages)
2. **CLI tool** - Command-line tool to install and manage packages

**Why NPM?**

- Don't reinvent the wheel - use existing solutions
- Install dependencies easily
- Manage project versions
- Share your own packages

**Basic NPM commands:**

**1. Initialize a project:**

```bash
npm init
# Creates package.json with interactive prompts

npm init -y
# Creates package.json with defaults (faster)
```

**2. Install packages:**

```bash
# Install and save to dependencies
npm install express
npm install mongoose
npm i express  # shorthand

# Install multiple
npm install express mongoose cors

# Install as dev dependency (only for development)
npm install --save-dev nodemon
npm install -D nodemon  # shorthand

# Install specific version
npm install express@4.17.1

# Install globally (available system-wide)
npm install -g nodemon
npm install -g create-react-app
```

**3. Uninstall packages:**

```bash
npm uninstall express
npm un express  # shorthand

# Remove dev dependency
npm uninstall --save-dev nodemon
```

**4. Update packages:**

```bash
# Update specific package
npm update express

# Update all packages
npm update

# Check outdated packages
npm outdated
```

**5. List packages:**

```bash
# List installed packages
npm list
npm ls

# List only top-level
npm list --depth=0

# List globally installed
npm list -g --depth=0
```

**6. Run scripts:**

```bash
# package.json scripts
npm run start
npm run dev
npm test
```

**Dependencies vs DevDependencies:**

**package.json:**
```json
{
  "dependencies": {
    "express": "^4.18.0",      // Needed in production
    "mongoose": "^6.0.0"
  },
  "devDependencies": {
    "nodemon": "^2.0.0",       // Only for development
    "jest": "^27.0.0"
  }
}
```

**Dependencies (--save or default):**
- Required to RUN the application
- Installed in production
- Examples: express, mongoose, cors, jwt

```bash
npm install express
# Goes to "dependencies"
```

**DevDependencies (--save-dev):**
- Only needed for DEVELOPMENT
- NOT installed in production
- Examples: nodemon, jest, eslint

```bash
npm install --save-dev nodemon
# Goes to "devDependencies"
```

**Installing from package.json:**

```bash
# Install all dependencies
npm install

# Install only production dependencies
npm install --production
# Skips devDependencies (for production servers)
```

**Version numbers:**

```json
{
  "dependencies": {
    "express": "4.18.2",     // Exact version
    "mongoose": "^6.0.0",    // Compatible with 6.x.x
    "cors": "~2.8.5"         // Compatible with 2.8.x
  }
}
```

**Versioning explained:**

```
Version: MAJOR.MINOR.PATCH
         4.18.2

^4.18.2  // Caret - compatible updates
         // Allows: 4.18.3, 4.19.0
         // Blocks: 5.0.0

~4.18.2  // Tilde - patch updates only
         // Allows: 4.18.3, 4.18.4
         // Blocks: 4.19.0

4.18.2   // Exact - no updates
         // Only: 4.18.2
```

**node_modules folder:**

```
my-project/
├── node_modules/      ← All installed packages (large!)
│   ├── express/
│   ├── mongoose/
│   └── ...
├── package.json
└── app.js
```

**NEVER commit node_modules to git!**

**.gitignore:**
```
node_modules/
.env
```

**Recreating node_modules:**
```bash
# On new machine or after git clone
npm install
# Reads package.json and downloads all dependencies
```

**package-lock.json:**

```json
// Locks exact versions of all dependencies
{
  "express": {
    "version": "4.18.2",
    "resolved": "https://...",
    "integrity": "sha512-..."
  }
}
```

- Ensures everyone gets same versions
- Commit to git (unlike node_modules)
- Auto-generated, don't edit manually

**NPM scripts:**

**package.json:**
```json
{
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js",
    "test": "jest"
  }
}
```

**Running scripts:**
```bash
npm start        # node app.js
npm run dev      # nodemon app.js
npm test         # jest

# "start" and "test" don't need "run"
```

**Popular packages to know:**

```bash
# Web framework
npm install express

# MongoDB ORM
npm install mongoose

# Environment variables
npm install dotenv

# CORS handling
npm install cors

# Authentication
npm install jsonwebtoken bcrypt

# Validation
npm install joi express-validator

# File upload
npm install multer

# Dev tools
npm install --save-dev nodemon
```

**npx vs npm:**

```bash
# npm - installs package
npm install create-react-app

# npx - executes package without installing
npx create-react-app my-app

# Use npx for one-time commands
npx nodemon app.js
```

**Interview tip:** NPM manages packages in Node.js projects. Use npm install to add packages, package.json tracks dependencies, node_modules stores installed packages. Dependencies are for production, devDependencies for development only. package-lock.json locks exact versions. Always add node_modules to .gitignore."

---

### Q7: package.json and package-lock.json

**How to Answer:**

"package.json and package-lock.json are configuration files that manage dependencies in a Node.js project.

**package.json:**

The main configuration file for your Node.js project. Contains metadata and dependencies.

**Creating package.json:**
```bash
npm init
# Or
npm init -y  # Skip questions, use defaults
```

**Basic structure:**

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "description": "My Node.js application",
  "main": "app.js",
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js",
    "test": "jest"
  },
  "keywords": ["express", "api"],
  "author": "Your Name",
  "license": "MIT",
  "dependencies": {
    "express": "^4.18.0",
    "mongoose": "^6.0.0"
  },
  "devDependencies": {
    "nodemon": "^2.0.0",
    "jest": "^27.0.0"
  }
}
```

**Important fields:**

**name:**
```json
"name": "my-app"
```
- Project name
- Must be lowercase, no spaces
- Used if you publish to NPM

**version:**
```json
"version": "1.0.0"
```
- Follows semantic versioning (MAJOR.MINOR.PATCH)
- 1.0.0 → 1.0.1 (bug fix)
- 1.0.0 → 1.1.0 (new feature)
- 1.0.0 → 2.0.0 (breaking change)

**main:**
```json
"main": "app.js"
```
- Entry point of application
- File that runs when package is required

**scripts:**
```json
"scripts": {
  "start": "node app.js",
  "dev": "nodemon app.js",
  "test": "jest",
  "build": "webpack"
}
```

**Running scripts:**
```bash
npm start        # Runs "node app.js"
npm run dev      # Runs "nodemon app.js"
npm test         # Runs "jest"
```

**dependencies:**
```json
"dependencies": {
  "express": "^4.18.0",
  "mongoose": "^6.0.0",
  "cors": "^2.8.5"
}
```
- Packages needed to RUN the app
- Installed in production
- Added with: `npm install express`

**devDependencies:**
```json
"devDependencies": {
  "nodemon": "^2.0.0",
  "jest": "^27.0.0",
  "eslint": "^8.0.0"
}
```
- Packages needed only for DEVELOPMENT
- NOT installed in production
- Added with: `npm install --save-dev nodemon`

**Why separate dev and production dependencies?**

```bash
# Development - installs all
npm install

# Production - skips devDependencies
npm install --production

# Smaller deployment, faster install
```

**package-lock.json:**

Automatically generated file that locks exact versions of all dependencies and their dependencies.

**Why package-lock.json?**

**Problem without lock file:**

```json
// package.json
{
  "dependencies": {
    "express": "^4.18.0"  // ^ allows updates
  }
}

// Developer A installs on Jan 1
// Gets: express 4.18.0

// Developer B installs on Feb 1
// Gets: express 4.18.2 (newer version)

// Different versions = potential bugs!
```

**Solution with lock file:**

```json
// package-lock.json
{
  "express": {
    "version": "4.18.0",    // Exact version locked
    "resolved": "https://registry.npmjs.org/express/-/express-4.18.0.tgz",
    "integrity": "sha512-...",
    "requires": {
      "body-parser": "1.19.0",
      "cookie": "0.4.1"
    }
  },
  "body-parser": {
    "version": "1.19.0",
    // ... locks this too
  }
}

// Everyone gets EXACT same versions
```

**Key differences:**

| Feature | package.json | package-lock.json |
|---------|-------------|-------------------|
| Created by | You (npm init) | NPM automatically |
| Edit manually | Yes | No |
| Commit to git | Yes | Yes |
| Contains | Your direct dependencies | All dependencies + sub-dependencies |
| Version format | Range (^4.18.0) | Exact (4.18.0) |

**What gets committed to Git:**

```
✅ package.json          // YES - always commit
✅ package-lock.json     // YES - commit this too
❌ node_modules/         // NO - never commit (too large)
```

**.gitignore:**
```
node_modules/
.env
```

**Workflow:**

**Developer A (creates project):**
```bash
npm init -y
npm install express mongoose

# Creates:
# - package.json
# - package-lock.json
# - node_modules/

# Commits to Git:
git add package.json package-lock.json
git commit -m "Initial setup"
```

**Developer B (clones project):**
```bash
git clone <repo>
cd project

npm install
# Reads package-lock.json
# Installs EXACT same versions as Developer A
```

**Updating dependencies:**

```bash
# Update specific package
npm update express

# Updates both:
# - package.json (if needed)
# - package-lock.json (exact versions)
```

**Fixing lock file issues:**

```bash
# If lock file is corrupted or out of sync
rm package-lock.json
rm -rf node_modules
npm install

# Generates new lock file
```

**Interview tip:** package.json is the main configuration file with project metadata and dependencies. package-lock.json locks exact versions for consistency across environments. Always commit both to Git, but never commit node_modules. Use npm install to recreate node_modules from package files."

---

### Q8: Global Objects (process, __dirname, __filename)

**How to Answer:**

"Node.js provides several global objects that are available in all modules without requiring them. The most important are process, __dirname, and __filename.

**1. process object:**

The process object provides information about and control over the current Node.js process.

**Common properties:**

```javascript
// Current working directory
console.log(process.cwd());
// /Users/john/projects/my-app

// Node.js version
console.log(process.version);
// v18.12.0

// Platform
console.log(process.platform);
// 'darwin' (Mac), 'win32' (Windows), 'linux'

// Process ID
console.log(process.pid);
// 12345

// Memory usage
console.log(process.memoryUsage());
// { rss: 25600000, heapTotal: 4534272, heapUsed: 2857056 }

// Uptime (how long process has been running)
console.log(process.uptime());
// 45.123 (seconds)
```

**process.env - Environment variables:**

```javascript
// Access environment variables
console.log(process.env.NODE_ENV);  // 'development' or 'production'
console.log(process.env.PORT);       // '3000'
console.log(process.env.DB_URL);     // 'mongodb://localhost/mydb'

// Usage in code
const port = process.env.PORT || 3000;
const isDev = process.env.NODE_ENV === 'development';

if (isDev) {
  console.log('Running in development mode');
}
```

**Setting environment variables:**

```bash
# Command line (temporary)
PORT=3000 NODE_ENV=production node app.js

# .env file (with dotenv package)
npm install dotenv
```

**.env file:**
```
PORT=3000
DB_URL=mongodb://localhost/mydb
JWT_SECRET=mysecret123
```

**app.js:**
```javascript
require('dotenv').config();

console.log(process.env.PORT);      // '3000'
console.log(process.env.DB_URL);    // 'mongodb://localhost/mydb'
```

**process.argv - Command line arguments:**

```javascript
// app.js
console.log(process.argv);

// Run: node app.js hello world
// Output:
[
  '/usr/local/bin/node',    // Node executable
  '/path/to/app.js',        // Script file
  'hello',                  // First argument
  'world'                   // Second argument
]

// Accessing arguments
const args = process.argv.slice(2); // Skip first 2
console.log(args); // ['hello', 'world']
```

**process methods:**

```javascript
// Exit process
process.exit(0);  // Success
process.exit(1);  // Error

// Change directory
process.chdir('/path/to/dir');

// Kill process
process.kill(process.pid);
```

**process.on() - Event listeners:**

```javascript
// Listen for uncaught exceptions
process.on('uncaughtException', (err) => {
  console.error('Uncaught Exception:', err);
  process.exit(1);
});

// Listen for unhandled promise rejections
process.on('unhandledRejection', (reason, promise) => {
  console.error('Unhandled Rejection:', reason);
});

// Before process exits
process.on('exit', (code) => {
  console.log(`Process exiting with code: ${code}`);
});

// SIGINT - Ctrl+C
process.on('SIGINT', () => {
  console.log('Received SIGINT. Cleaning up...');
  // Close database connections, etc.
  process.exit(0);
});
```

**2. __dirname:**

Gives the absolute path of the directory containing the current file.

```javascript
// File: /Users/john/projects/my-app/routes/users.js

console.log(__dirname);
// /Users/john/projects/my-app/routes

// Use for file paths
const path = require('path');
const configPath = path.join(__dirname, 'config.json');
// /Users/john/projects/my-app/routes/config.json
```

**3. __filename:**

Gives the absolute path of the current file.

```javascript
// File: /Users/john/projects/my-app/routes/users.js

console.log(__filename);
// /Users/john/projects/my-app/routes/users.js

// Get just the filename
const path = require('path');
console.log(path.basename(__filename));
// users.js
```

**Practical examples:**

**Serving static files:**
```javascript
const express = require('express');
const path = require('path');
const app = express();

// Serve files from 'public' folder
app.use(express.static(path.join(__dirname, 'public')));
```

**Reading config file:**
```javascript
const fs = require('fs');
const path = require('path');

const configPath = path.join(__dirname, 'config.json');
const config = JSON.parse(fs.readFileSync(configPath, 'utf8'));
```

**Environment-based config:**
```javascript
const port = process.env.PORT || 3000;
const dbUrl = process.env.NODE_ENV === 'production'
  ? process.env.PROD_DB_URL
  : process.env.DEV_DB_URL;

app.listen(port, () => {
  console.log(`Server on port ${port}`);
});
```

**Graceful shutdown:**
```javascript
const server = app.listen(3000);

process.on('SIGTERM', () => {
  console.log('SIGTERM received. Closing server...');
  server.close(() => {
    console.log('Server closed');
    process.exit(0);
  });
});
```

**Other global objects:**

```javascript
// console - logging
console.log('Message');
console.error('Error');

// setTimeout, setInterval
setTimeout(() => {}, 1000);
setInterval(() => {}, 1000);

// Buffer - for binary data
const buf = Buffer.from('hello');

// global - like window in browser
global.myVar = 'value';
```

**__dirname vs process.cwd():**

```javascript
// Structure:
// /Users/john/projects/my-app/
//   ├── app.js
//   └── routes/
//       └── users.js

// Running: node app.js from /Users/john/projects/my-app/

// In app.js:
console.log(__dirname);     // /Users/john/projects/my-app
console.log(process.cwd()); // /Users/john/projects/my-app

// In routes/users.js:
console.log(__dirname);     // /Users/john/projects/my-app/routes
console.log(process.cwd()); // /Users/john/projects/my-app (same!)

// __dirname = directory of current file
// process.cwd() = directory where command was run
```

**Interview tip:** process object provides info about Node.js process (env variables, args, platform). __dirname is absolute path of current file's directory. __filename is absolute path of current file. Use process.env for environment variables (with dotenv). Use __dirname for file paths to avoid hardcoding."

---

(Content continues...)


### Q9: Built-in Modules (fs, path, http, os)

**How to Answer:**

"Node.js comes with many built-in modules that provide essential functionality without needing to install external packages.

**1. fs (File System) module:**

Read and write files.

```javascript
const fs = require('fs');

// Read file (async)
fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(data);
});

// Read file (sync) - blocks execution
const data = fs.readFileSync('file.txt', 'utf8');

// Write file
fs.writeFile('output.txt', 'Hello World', (err) => {
  if (err) throw err;
  console.log('File written');
});

// Append to file
fs.appendFile('log.txt', 'New log entry\n', (err) => {
  if (err) throw err;
});

// Delete file
fs.unlink('file.txt', (err) => {
  if (err) throw err;
});

// Check if file exists
fs.existsSync('file.txt'); // true or false

// Create directory
fs.mkdir('new-folder', (err) => {
  if (err) throw err;
});

// Read directory
fs.readdir('./', (err, files) => {
  console.log(files); // Array of filenames
});
```

**2. path module:**

Handle file and directory paths.

```javascript
const path = require('path');

// Join paths
const filePath = path.join(__dirname, 'uploads', 'image.jpg');
// /Users/john/project/uploads/image.jpg

// Resolve to absolute path
path.resolve('folder', 'file.txt');
// /current/working/directory/folder/file.txt

// Get file extension
path.extname('image.jpg'); // '.jpg'

// Get filename
path.basename('/path/to/file.txt'); // 'file.txt'

// Get directory
path.dirname('/path/to/file.txt'); // '/path/to'

// Parse path
path.parse('/path/to/file.txt');
// {
//   root: '/',
//   dir: '/path/to',
//   base: 'file.txt',
//   ext: '.txt',
//   name: 'file'
// }
```

**3. http module:**

Create HTTP servers.

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  // Set response header
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  
  // Send response
  res.end('Hello World');
});

server.listen(3000, () => {
  console.log('Server running on port 3000');
});
```

**4. os module:**

Get operating system information.

```javascript
const os = require('os');

// Platform
os.platform(); // 'darwin', 'win32', 'linux'

// CPU architecture
os.arch(); // 'x64', 'arm'

// CPU info
os.cpus(); // Array of CPU cores

// Free memory
os.freemem(); // Bytes of free memory

// Total memory
os.totalmem(); // Total memory in bytes

// Home directory
os.homedir(); // '/Users/john'

// Hostname
os.hostname(); // 'Johns-MacBook'

// Uptime
os.uptime(); // System uptime in seconds
```

**Other useful built-in modules:**

```javascript
// url - Parse URLs
const url = require('url');
const myUrl = url.parse('http://example.com/path?name=john');

// querystring - Parse query strings
const qs = require('querystring');
const parsed = qs.parse('name=john&age=25');

// events - Event emitter
const EventEmitter = require('events');

// crypto - Encryption
const crypto = require('crypto');

// util - Utility functions
const util = require('util');
```

**Interview tip:** Node.js has many built-in modules. Most important for freshers: fs (file operations), path (file paths), http (create servers), os (system info). No installation needed, just require() them."

---

### Q10: Asynchronous Patterns (Callbacks, Promises, Async/Await)

**How to Answer:**

"Node.js uses three main patterns for handling asynchronous operations: Callbacks, Promises, and Async/Await.

**1. Callbacks (traditional):**

A function passed as an argument, executed when operation completes.

```javascript
// Callback pattern
fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(data);
});

// Convention: error-first callback
// First parameter is always error (null if no error)
// Second parameter is the result
```

**Callback hell (pyramid of doom):**

```javascript
// Multiple async operations - messy!
fs.readFile('file1.txt', (err, data1) => {
  if (err) return console.error(err);
  
  fs.readFile('file2.txt', (err, data2) => {
    if (err) return console.error(err);
    
    fs.readFile('file3.txt', (err, data3) => {
      if (err) return console.error(err);
      
      console.log(data1, data2, data3);
    });
  });
});
```

**2. Promises (ES6):**

Better way to handle async operations with chaining.

```javascript
// Creating a promise
const readFilePromise = (filename) => {
  return new Promise((resolve, reject) => {
    fs.readFile(filename, 'utf8', (err, data) => {
      if (err) reject(err);
      else resolve(data);
    });
  });
};

// Using promise
readFilePromise('file.txt')
  .then(data => {
    console.log(data);
    return readFilePromise('file2.txt'); // Chain
  })
  .then(data2 => {
    console.log(data2);
  })
  .catch(err => {
    console.error(err); // Single error handler
  });
```

**3. Async/Await (ES2017) - Modern approach:**

Cleaner syntax for promises.

```javascript
// Using async/await
async function readFiles() {
  try {
    const data1 = await readFilePromise('file1.txt');
    const data2 = await readFilePromise('file2.txt');
    const data3 = await readFilePromise('file3.txt');
    
    console.log(data1, data2, data3);
  } catch (err) {
    console.error(err);
  }
}

readFiles();
```

**Comparison of all three:**

**Callbacks:**
```javascript
getUser(1, (err, user) => {
  if (err) return console.error(err);
  
  getOrders(user.id, (err, orders) => {
    if (err) return console.error(err);
    
    console.log(orders);
  });
});
```

**Promises:**
```javascript
getUser(1)
  .then(user => getOrders(user.id))
  .then(orders => console.log(orders))
  .catch(err => console.error(err));
```

**Async/Await:**
```javascript
async function getUserOrders() {
  try {
    const user = await getUser(1);
    const orders = await getOrders(user.id);
    console.log(orders);
  } catch (err) {
    console.error(err);
  }
}
```

**util.promisify - Convert callback to promise:**

```javascript
const util = require('util');
const fs = require('fs');

// Convert fs.readFile to promise-based
const readFile = util.promisify(fs.readFile);

// Now use with async/await
async function read() {
  const data = await readFile('file.txt', 'utf8');
  console.log(data);
}
```

**Or use fs.promises (built-in):**

```javascript
const fs = require('fs').promises;

async function read() {
  const data = await fs.readFile('file.txt', 'utf8');
  console.log(data);
}
```

**Interview tip:** Three patterns: Callbacks (error-first, traditional), Promises (chainable, better error handling), Async/Await (cleanest, modern). Async/await is preferred in modern code. Use try/catch for error handling with async/await."

---

## Express.js Basics

### Q11: What is Express.js?

**How to Answer:**

"Express.js is a minimal and flexible Node.js web application framework. It simplifies building web servers and APIs.

**Why Express?**

**Without Express (raw Node.js):**
```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  if (req.url === '/' && req.method === 'GET') {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Home Page');
  } else if (req.url === '/about' && req.method === 'GET') {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('About Page');
  } else {
    res.writeHead(404);
    res.end('Not Found');
  }
});

server.listen(3000);
```

**With Express:**
```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Home Page');
});

app.get('/about', (req, res) => {
  res.send('About Page');
});

app.listen(3000);
```

**Key features:**

1. **Routing** - Easy URL handling
2. **Middleware** - Request/response processing
3. **Template engines** - Dynamic HTML rendering
4. **Static files** - Serve CSS, images, etc.
5. **Error handling** - Centralized error management
6. **HTTP utilities** - Simplified request/response

**Interview tip:** Express is a Node.js framework that simplifies web server and API development. It provides routing, middleware, and utilities that make code cleaner and faster to write than raw Node.js."

---

### Q12: Setting up Express Server

**How to Answer:**

"Setting up a basic Express server involves installing Express, creating an app instance, defining routes, and listening on a port.

**Step-by-step setup:**

**1. Initialize project:**
```bash
npm init -y
```

**2. Install Express:**
```bash
npm install express
```

**3. Create server (app.js):**
```javascript
const express = require('express');
const app = express();

// Define a route
app.get('/', (req, res) => {
  res.send('Hello World!');
});

// Start server
const PORT = 3000;
app.listen(PORT, () => {
  console.log(`Server running on http://localhost:${PORT}`);
});
```

**4. Run server:**
```bash
node app.js
```

**With environment variables:**

```javascript
require('dotenv').config();
const express = require('express');
const app = express();

const PORT = process.env.PORT || 3000;

app.get('/', (req, res) => {
  res.send('Hello World!');
});

app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

**.env file:**
```
PORT=5000
```

**With nodemon (auto-restart):**

```bash
npm install --save-dev nodemon
```

**package.json:**
```json
{
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js"
  }
}
```

**Run:**
```bash
npm run dev
```

**Interview tip:** Install express with npm, create app with express(), define routes with app.get/post/etc, and start server with app.listen(). Use environment variables for port and nodemon for development auto-restart."

---

### Q13: Routing (GET, POST, PUT, DELETE)

**How to Answer:**

"Routing defines how an application responds to client requests at different endpoints (URLs) and HTTP methods.

**Basic routes:**

```javascript
const express = require('express');
const app = express();

// GET route
app.get('/', (req, res) => {
  res.send('GET request to homepage');
});

// POST route
app.post('/users', (req, res) => {
  res.send('POST request to create user');
});

// PUT route
app.put('/users/:id', (req, res) => {
  res.send('PUT request to update user');
});

// DELETE route
app.delete('/users/:id', (req, res) => {
  res.send('DELETE request to delete user');
});

// PATCH route (partial update)
app.patch('/users/:id', (req, res) => {
  res.send('PATCH request to partially update user');
});
```

**Route parameters:**

```javascript
// Dynamic route with parameter
app.get('/users/:id', (req, res) => {
  const userId = req.params.id;
  res.send(`User ID: ${userId}`);
});

// Multiple parameters
app.get('/users/:userId/posts/:postId', (req, res) => {
  const { userId, postId } = req.params;
  res.send(`User ${userId}, Post ${postId}`);
});
```

**All routes for a resource:**

```javascript
const express = require('express');
const app = express();

// Middleware to parse JSON
app.use(express.json());

let users = [
  { id: 1, name: 'John' },
  { id: 2, name: 'Jane' }
];

// GET all users
app.get('/api/users', (req, res) => {
  res.json(users);
});

// GET single user
app.get('/api/users/:id', (req, res) => {
  const user = users.find(u => u.id === parseInt(req.params.id));
  if (!user) return res.status(404).send('User not found');
  res.json(user);
});

// POST create user
app.post('/api/users', (req, res) => {
  const user = {
    id: users.length + 1,
    name: req.body.name
  };
  users.push(user);
  res.status(201).json(user);
});

// PUT update user
app.put('/api/users/:id', (req, res) => {
  const user = users.find(u => u.id === parseInt(req.params.id));
  if (!user) return res.status(404).send('User not found');
  
  user.name = req.body.name;
  res.json(user);
});

// DELETE user
app.delete('/api/users/:id', (req, res) => {
  const index = users.findIndex(u => u.id === parseInt(req.params.id));
  if (index === -1) return res.status(404).send('User not found');
  
  users.splice(index, 1);
  res.status(204).send(); // No content
});

app.listen(3000);
```

**Testing routes with curl:**

```bash
# GET all users
curl http://localhost:3000/api/users

# GET single user
curl http://localhost:3000/api/users/1

# POST create user
curl -X POST http://localhost:3000/api/users \
  -H "Content-Type: application/json" \
  -d '{"name":"Bob"}'

# PUT update user
curl -X PUT http://localhost:3000/api/users/1 \
  -H "Content-Type: application/json" \
  -d '{"name":"John Updated"}'

# DELETE user
curl -X DELETE http://localhost:3000/api/users/1
```

**Interview tip:** Use app.get() for reading, app.post() for creating, app.put() for updating, app.delete() for deleting. Route parameters use :param syntax. Always use appropriate HTTP status codes (200, 201, 404, etc.)."

---

### Q14: Route Parameters and Query Strings

**How to Answer:**

"Route parameters and query strings are two ways to pass data in URLs.

**Route Parameters (req.params):**

Part of the URL path, defined with colon syntax.

```javascript
// Route with parameter
app.get('/users/:id', (req, res) => {
  const userId = req.params.id;
  res.send(`User ID: ${userId}`);
});

// Access: GET /users/123
// req.params.id = '123'

// Multiple parameters
app.get('/users/:userId/posts/:postId', (req, res) => {
  const { userId, postId } = req.params;
  res.send(`User ${userId}, Post ${postId}`);
});

// Access: GET /users/5/posts/10
// req.params = { userId: '5', postId: '10' }
```

**Query Strings (req.query):**

Key-value pairs after ? in URL, optional parameters.

```javascript
// Route with query strings
app.get('/search', (req, res) => {
  const { q, page, limit } = req.query;
  res.json({
    searchTerm: q,
    page: page,
    limit: limit
  });
});

// Access: GET /search?q=express&page=2&limit=10
// req.query = { q: 'express', page: '2', limit: '10' }
```

**Combining both:**

```javascript
// Parameters + Query strings
app.get('/users/:id/posts', (req, res) => {
  const userId = req.params.id;
  const { page, limit } = req.query;
  
  res.json({
    userId: userId,
    page: page || 1,
    limit: limit || 10
  });
});

// Access: GET /users/5/posts?page=2&limit=20
// req.params.id = '5'
// req.query = { page: '2', limit: '20' }
```

**Real-world example - Pagination & Filtering:**

```javascript
app.get('/api/products', (req, res) => {
  const {
    page = 1,
    limit = 10,
    category,
    minPrice,
    maxPrice,
    sort = 'name'
  } = req.query;

  // Convert to numbers
  const pageNum = parseInt(page);
  const limitNum = parseInt(limit);

  // Filter products (example)
  let products = allProducts;
  
  if (category) {
    products = products.filter(p => p.category === category);
  }
  
  if (minPrice) {
    products = products.filter(p => p.price >= parseFloat(minPrice));
  }
  
  if (maxPrice) {
    products = products.filter(p => p.price <= parseFloat(maxPrice));
  }

  // Sort
  products.sort((a, b) => a[sort].localeCompare(b[sort]));

  // Paginate
  const startIndex = (pageNum - 1) * limitNum;
  const endIndex = startIndex + limitNum;
  const paginatedProducts = products.slice(startIndex, endIndex);

  res.json({
    page: pageNum,
    limit: limitNum,
    total: products.length,
    products: paginatedProducts
  });
});

// Access: GET /api/products?category=electronics&minPrice=100&page=2&limit=5
```

**When to use which:**

**Use route parameters for:**
- Required data (user ID, post ID)
- Identifying a specific resource
- Part of the resource path

```javascript
GET /users/123         // Get user with ID 123
GET /posts/456         // Get post with ID 456
DELETE /users/123      // Delete user 123
```

**Use query strings for:**
- Optional data (filters, pagination)
- Searching and filtering
- Sorting and limits

```javascript
GET /users?age=25&city=NYC    // Filter users
GET /products?page=2&limit=10 // Pagination
GET /search?q=laptop          // Search
```

**Interview tip:** Route parameters (req.params) are part of the URL path, required for identifying resources. Query strings (req.query) come after ? in URL, used for optional filters, pagination, and search. Parameters with colon syntax (:id), query strings are key=value pairs."

---

(Content continues with Middleware, REST APIs, Database, Auth, and more...)


### Q16: Middleware - What and Why

**How to Answer:**

"Middleware functions are functions that have access to the request object (req), response object (res), and the next middleware function in the application's request-response cycle.

**What is Middleware?**

Middleware sits between the request and response. It can:
- Execute any code
- Make changes to req and res objects
- End the request-response cycle
- Call the next middleware in the stack

**Middleware flow:**

```
Request → Middleware 1 → Middleware 2 → Route Handler → Response
```

**Basic middleware:**

```javascript
const express = require('express');
const app = express();

// Simple middleware function
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next(); // Pass control to next middleware
});

app.get('/', (req, res) => {
  res.send('Home Page');
});
```

**Middleware with next():**

```javascript
// Middleware that adds timestamp
app.use((req, res, next) => {
  req.requestTime = new Date().toISOString();
  next(); // MUST call next() to continue
});

app.get('/', (req, res) => {
  res.send(`Request at: ${req.requestTime}`);
});
```

**Types of middleware:**

**1. Application-level middleware:**

```javascript
// Runs for all routes
app.use((req, res, next) => {
  console.log('Time:', Date.now());
  next();
});

// Runs for specific path
app.use('/api', (req, res, next) => {
  console.log('API request');
  next();
});
```

**2. Router-level middleware:**

```javascript
const router = express.Router();

router.use((req, res, next) => {
  console.log('Router middleware');
  next();
});

router.get('/users', (req, res) => {
  res.send('Users');
});

app.use('/api', router);
```

**3. Built-in middleware:**

```javascript
// Parse JSON bodies
app.use(express.json());

// Parse URL-encoded bodies
app.use(express.urlencoded({ extended: true }));

// Serve static files
app.use(express.static('public'));
```

**4. Third-party middleware:**

```javascript
const cors = require('cors');
const morgan = require('morgan');

app.use(cors()); // Enable CORS
app.use(morgan('dev')); // Logging
```

**5. Error-handling middleware:**

```javascript
// Has 4 parameters (err, req, res, next)
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});
```

**Practical examples:**

**Logging middleware:**

```javascript
const logger = (req, res, next) => {
  console.log(`${req.method} ${req.url} - ${new Date().toISOString()}`);
  next();
};

app.use(logger);
```

**Authentication middleware:**

```javascript
const requireAuth = (req, res, next) => {
  const token = req.headers['authorization'];
  
  if (!token) {
    return res.status(401).json({ error: 'No token provided' });
  }
  
  // Verify token (simplified)
  if (token === 'valid-token') {
    next(); // User authenticated
  } else {
    res.status(403).json({ error: 'Invalid token' });
  }
};

// Protected route
app.get('/api/protected', requireAuth, (req, res) => {
  res.json({ message: 'Protected data' });
});
```

**Multiple middleware:**

```javascript
const checkUser = (req, res, next) => {
  // Check user
  next();
};

const checkPermission = (req, res, next) => {
  // Check permission
  next();
};

const logAction = (req, res, next) => {
  // Log action
  next();
};

// Chain multiple middleware
app.get('/admin', checkUser, checkPermission, logAction, (req, res) => {
  res.send('Admin panel');
});
```

**Order matters:**

```javascript
// ❌ WRONG - static middleware after routes
app.get('/', (req, res) => {
  res.send('Home');
});
app.use(express.json()); // Too late!

// ✅ CORRECT - middleware before routes
app.use(express.json());
app.get('/', (req, res) => {
  res.send('Home');
});
```

**Interview tip:** Middleware functions execute in sequence between request and response. They can modify req/res, end response, or call next(). Must call next() to pass control to next middleware. Used for logging, authentication, parsing, error handling, etc. Order matters - define middleware before routes."

---

### Q17: Built-in Middleware

**How to Answer:**

"Express provides several built-in middleware functions for common tasks.

**1. express.json():**

Parses incoming JSON payloads.

```javascript
app.use(express.json());

app.post('/api/users', (req, res) => {
  console.log(req.body); // Access JSON data
  // req.body = { name: 'John', age: 25 }
  res.json(req.body);
});

// Test with:
// POST /api/users
// Body: { "name": "John", "age": 25 }
```

**2. express.urlencoded():**

Parses URL-encoded data (form submissions).

```javascript
app.use(express.urlencoded({ extended: true }));

app.post('/submit', (req, res) => {
  console.log(req.body); // Access form data
  // req.body = { name: 'John', email: 'john@email.com' }
  res.send('Form received');
});

// Test with:
// POST /submit
// Body: name=John&email=john@email.com
```

**3. express.static():**

Serves static files (CSS, images, JS).

```javascript
// Serve files from 'public' directory
app.use(express.static('public'));

// Now accessible:
// public/style.css → http://localhost:3000/style.css
// public/images/logo.png → http://localhost:3000/images/logo.png

// Custom path prefix
app.use('/static', express.static('public'));
// public/style.css → http://localhost:3000/static/style.css
```

**Complete setup:**

```javascript
const express = require('express');
const app = express();

// Parse JSON bodies
app.use(express.json());

// Parse URL-encoded bodies
app.use(express.urlencoded({ extended: true }));

// Serve static files
app.use(express.static('public'));

// Routes
app.post('/api/data', (req, res) => {
  res.json({ received: req.body });
});

app.listen(3000);
```

**Interview tip:** express.json() parses JSON, express.urlencoded() parses form data, express.static() serves static files. Always use express.json() for APIs that accept JSON data."

---

### Q18: Custom Middleware

**How to Answer:**

"Custom middleware are functions you create for specific application needs.

**Creating custom middleware:**

```javascript
// Logger middleware
const logger = (req, res, next) => {
  console.log(`${req.method} ${req.url} - ${new Date().toISOString()}`);
  next(); // Pass to next middleware
};

// Use it
app.use(logger);
```

**Middleware with parameters:**

```javascript
// Middleware factory function
const requireRole = (role) => {
  return (req, res, next) => {
    if (req.user && req.user.role === role) {
      next(); // User has required role
    } else {
      res.status(403).json({ error: 'Insufficient permissions' });
    }
  };
};

// Use with parameter
app.get('/admin', requireRole('admin'), (req, res) => {
  res.send('Admin panel');
});

app.get('/moderator', requireRole('moderator'), (req, res) => {
  res.send('Moderator panel');
});
```

**Practical examples:**

**Request validation:**

```javascript
const validateUser = (req, res, next) => {
  const { name, email } = req.body;
  
  if (!name || !email) {
    return res.status(400).json({ 
      error: 'Name and email are required' 
    });
  }
  
  if (!email.includes('@')) {
    return res.status(400).json({ 
      error: 'Invalid email format' 
    });
  }
  
  next(); // Validation passed
};

app.post('/api/users', validateUser, (req, res) => {
  // Validation already done
  res.json({ message: 'User created', user: req.body });
});
```

**Rate limiting:**

```javascript
const requestCounts = {};

const rateLimit = (req, res, next) => {
  const ip = req.ip;
  const currentTime = Date.now();
  const timeWindow = 60000; // 1 minute
  const maxRequests = 10;
  
  if (!requestCounts[ip]) {
    requestCounts[ip] = {
      count: 1,
      startTime: currentTime
    };
    return next();
  }
  
  const timePassed = currentTime - requestCounts[ip].startTime;
  
  if (timePassed > timeWindow) {
    requestCounts[ip] = {
      count: 1,
      startTime: currentTime
    };
    return next();
  }
  
  if (requestCounts[ip].count >= maxRequests) {
    return res.status(429).json({ 
      error: 'Too many requests' 
    });
  }
  
  requestCounts[ip].count++;
  next();
};

app.use(rateLimit);
```

**Async middleware:**

```javascript
// Wrap async functions to catch errors
const asyncHandler = (fn) => {
  return (req, res, next) => {
    Promise.resolve(fn(req, res, next)).catch(next);
  };
};

// Use with async route handlers
app.get('/users', asyncHandler(async (req, res) => {
  const users = await User.find();
  res.json(users);
}));
```

**Interview tip:** Custom middleware are functions with (req, res, next). Use them for validation, authentication, logging, rate limiting, etc. Always call next() unless ending the response. Can create middleware factories that return middleware functions with parameters."

---

### Q19: Error Handling Middleware

**How to Answer:**

"Error handling middleware catches errors in your application and sends appropriate responses to clients.

**Basic error handler:**

```javascript
// Error middleware has 4 parameters
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ 
    error: 'Something went wrong!' 
  });
});
```

**Complete error handling setup:**

```javascript
const express = require('express');
const app = express();

app.use(express.json());

// Routes
app.get('/error', (req, res) => {
  throw new Error('Intentional error');
});

// 404 handler (must be after all routes)
app.use((req, res, next) => {
  res.status(404).json({ 
    error: 'Route not found' 
  });
});

// Error handler (must be last)
app.use((err, req, res, next) => {
  console.error(err.stack);
  
  const statusCode = err.statusCode || 500;
  const message = err.message || 'Internal Server Error';
  
  res.status(statusCode).json({ 
    error: message,
    ...(process.env.NODE_ENV === 'development' && { stack: err.stack })
  });
});

app.listen(3000);
```

**Custom error class:**

```javascript
class AppError extends Error {
  constructor(message, statusCode) {
    super(message);
    this.statusCode = statusCode;
    this.isOperational = true;
    Error.captureStackTrace(this, this.constructor);
  }
}

// Usage
app.get('/users/:id', (req, res, next) => {
  const user = users.find(u => u.id === req.params.id);
  
  if (!user) {
    return next(new AppError('User not found', 404));
  }
  
  res.json(user);
});

// Error handler
app.use((err, req, res, next) => {
  const { statusCode = 500, message } = err;
  
  res.status(statusCode).json({
    status: 'error',
    statusCode,
    message
  });
});
```

**Async error handling:**

```javascript
// Wrapper for async routes
const catchAsync = (fn) => {
  return (req, res, next) => {
    fn(req, res, next).catch(next);
  };
};

// Use with async functions
app.get('/users', catchAsync(async (req, res, next) => {
  const users = await User.find();
  
  if (!users || users.length === 0) {
    throw new AppError('No users found', 404);
  }
  
  res.json(users);
}));
```

**Interview tip:** Error middleware has 4 parameters (err, req, res, next). Place it after all routes. Use custom error classes for better error handling. Wrap async functions to catch errors and pass to error middleware with next(err)."

---

## REST API Development

### Q21: What is REST API?

**How to Answer:**

"REST (Representational State Transfer) is an architectural style for designing networked applications. A REST API is an API that follows REST principles.

**REST Principles:**

1. **Client-Server** - Separation of concerns
2. **Stateless** - Each request contains all needed information
3. **Cacheable** - Responses can be cached
4. **Uniform Interface** - Consistent way to interact
5. **Layered System** - Client doesn't know if connected directly to server

**Key concepts:**

**Resources:**
Everything is a resource (users, posts, products).

```
/users          → Users resource
/users/123      → Specific user
/users/123/posts → User's posts
```

**HTTP Methods (CRUD operations):**

| Method | Operation | Example |
|--------|-----------|---------|
| GET | Read | Get users |
| POST | Create | Create user |
| PUT | Update (full) | Update entire user |
| PATCH | Update (partial) | Update user email |
| DELETE | Delete | Delete user |

**Example REST API:**

```javascript
const express = require('express');
const app = express();

app.use(express.json());

let users = [
  { id: 1, name: 'John', email: 'john@email.com' },
  { id: 2, name: 'Jane', email: 'jane@email.com' }
];

// GET /api/users - Get all users
app.get('/api/users', (req, res) => {
  res.json(users);
});

// GET /api/users/:id - Get single user
app.get('/api/users/:id', (req, res) => {
  const user = users.find(u => u.id === parseInt(req.params.id));
  
  if (!user) {
    return res.status(404).json({ error: 'User not found' });
  }
  
  res.json(user);
});

// POST /api/users - Create user
app.post('/api/users', (req, res) => {
  const newUser = {
    id: users.length + 1,
    name: req.body.name,
    email: req.body.email
  };
  
  users.push(newUser);
  res.status(201).json(newUser);
});

// PUT /api/users/:id - Update user (full)
app.put('/api/users/:id', (req, res) => {
  const user = users.find(u => u.id === parseInt(req.params.id));
  
  if (!user) {
    return res.status(404).json({ error: 'User not found' });
  }
  
  user.name = req.body.name;
  user.email = req.body.email;
  
  res.json(user);
});

// PATCH /api/users/:id - Update user (partial)
app.patch('/api/users/:id', (req, res) => {
  const user = users.find(u => u.id === parseInt(req.params.id));
  
  if (!user) {
    return res.status(404).json({ error: 'User not found' });
  }
  
  if (req.body.name) user.name = req.body.name;
  if (req.body.email) user.email = req.body.email;
  
  res.json(user);
});

// DELETE /api/users/:id - Delete user
app.delete('/api/users/:id', (req, res) => {
  const index = users.findIndex(u => u.id === parseInt(req.params.id));
  
  if (index === -1) {
    return res.status(404).json({ error: 'User not found' });
  }
  
  users.splice(index, 1);
  res.status(204).send(); // No content
});

app.listen(3000);
```

**REST best practices:**

1. **Use nouns, not verbs** in URLs
```
❌ /getUsers, /createUser
✅ /users (GET), /users (POST)
```

2. **Use plural nouns**
```
❌ /user/123
✅ /users/123
```

3. **Nested resources**
```
✅ /users/123/posts
✅ /posts/456/comments
```

4. **Versioning**
```
✅ /api/v1/users
✅ /api/v2/users
```

5. **Use HTTP status codes**
```
200 OK - Success
201 Created - Resource created
204 No Content - Success with no body
400 Bad Request - Invalid data
401 Unauthorized - Not authenticated
403 Forbidden - Not authorized
404 Not Found - Resource doesn't exist
500 Internal Server Error - Server error
```

**Interview tip:** REST API uses HTTP methods (GET, POST, PUT, DELETE) to perform CRUD operations on resources. URLs represent resources (nouns), not actions (verbs). Stateless - each request has all needed info. Use proper HTTP status codes."

---

### Q23: Status Codes

**How to Answer:**

"HTTP status codes indicate the result of a client's request. They're grouped into five classes.

**Status code ranges:**

- **1xx** - Informational (rarely used)
- **2xx** - Success
- **3xx** - Redirection
- **4xx** - Client errors
- **5xx** - Server errors

**Common status codes for APIs:**

**Success (2xx):**

```javascript
// 200 OK - Request succeeded
app.get('/users', (req, res) => {
  res.status(200).json(users);
  // or just: res.json(users)  // 200 is default
});

// 201 Created - Resource created
app.post('/users', (req, res) => {
  const newUser = createUser(req.body);
  res.status(201).json(newUser);
});

// 204 No Content - Success but no data to return
app.delete('/users/:id', (req, res) => {
  deleteUser(req.params.id);
  res.status(204).send();
});
```

**Client Errors (4xx):**

```javascript
// 400 Bad Request - Invalid request data
app.post('/users', (req, res) => {
  if (!req.body.email) {
    return res.status(400).json({ 
      error: 'Email is required' 
    });
  }
});

// 401 Unauthorized - Not authenticated
app.get('/profile', (req, res) => {
  if (!req.headers.authorization) {
    return res.status(401).json({ 
      error: 'Authentication required' 
    });
  }
});

// 403 Forbidden - Authenticated but not authorized
app.delete('/users/:id', (req, res) => {
  if (req.user.role !== 'admin') {
    return res.status(403).json({ 
      error: 'Insufficient permissions' 
    });
  }
});

// 404 Not Found - Resource doesn't exist
app.get('/users/:id', (req, res) => {
  const user = findUser(req.params.id);
  
  if (!user) {
    return res.status(404).json({ 
      error: 'User not found' 
    });
  }
  
  res.json(user);
});

// 409 Conflict - Request conflicts with server state
app.post('/users', (req, res) => {
  const exists = checkUserExists(req.body.email);
  
  if (exists) {
    return res.status(409).json({ 
      error: 'User already exists' 
    });
  }
});
```

**Server Errors (5xx):**

```javascript
// 500 Internal Server Error - Unexpected server error
app.get('/users', (req, res) => {
  try {
    const users = getAllUsers();
    res.json(users);
  } catch (error) {
    res.status(500).json({ 
      error: 'Internal server error' 
    });
  }
});

// 503 Service Unavailable - Server temporarily unavailable
app.get('/users', (req, res) => {
  if (!database.isConnected()) {
    return res.status(503).json({ 
      error: 'Service temporarily unavailable' 
    });
  }
});
```

**Quick reference:**

| Code | Meaning | When to Use |
|------|---------|-------------|
| 200 | OK | Successful GET, PUT, PATCH |
| 201 | Created | Successful POST (created resource) |
| 204 | No Content | Successful DELETE |
| 400 | Bad Request | Invalid input data |
| 401 | Unauthorized | Missing or invalid authentication |
| 403 | Forbidden | Valid auth but insufficient permissions |
| 404 | Not Found | Resource doesn't exist |
| 409 | Conflict | Duplicate resource |
| 500 | Server Error | Unexpected server error |

**Interview tip:** Use appropriate status codes: 200 for success, 201 for created, 204 for deleted, 400 for bad input, 401 for not authenticated, 403 for not authorized, 404 for not found, 500 for server errors. 2xx = success, 4xx = client error, 5xx = server error."

---



## Database Integration

### Q29: Connecting MongoDB with Mongoose

**How to Answer:**

"Mongoose is an ODM (Object Data Modeling) library for MongoDB and Node.js. It provides a schema-based solution to model application data.

**Installation:**

```bash
npm install mongoose
```

**Connecting to MongoDB:**

```javascript
const mongoose = require('mongoose');

// Connection string
const dbURL = 'mongodb://localhost:27017/myapp';

// Connect
mongoose.connect(dbURL, {
  useNewUrlParser: true,
  useUnifiedTopology: true
})
.then(() => console.log('MongoDB connected'))
.catch(err => console.error('Connection error:', err));
```

**With environment variables:**

**.env:**
```
MONGODB_URI=mongodb://localhost:27017/myapp
# Or MongoDB Atlas:
# MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/myapp
```

**app.js:**
```javascript
require('dotenv').config();
const mongoose = require('mongoose');

const connectDB = async () => {
  try {
    await mongoose.connect(process.env.MONGODB_URI);
    console.log('MongoDB connected successfully');
  } catch (error) {
    console.error('MongoDB connection error:', error);
    process.exit(1);
  }
};

connectDB();
```

**Connection events:**

```javascript
mongoose.connection.on('connected', () => {
  console.log('Mongoose connected to MongoDB');
});

mongoose.connection.on('error', (err) => {
  console.error('Mongoose connection error:', err);
});

mongoose.connection.on('disconnected', () => {
  console.log('Mongoose disconnected');
});

// Graceful shutdown
process.on('SIGINT', async () => {
  await mongoose.connection.close();
  process.exit(0);
});
```

**Interview tip:** Mongoose connects Node.js to MongoDB. Use mongoose.connect() with connection string. Store connection string in .env file. Handle connection events for better error tracking."

---

### Q30: Mongoose Schema and Models

**How to Answer:**

"In Mongoose, schemas define the structure of documents, and models provide an interface to interact with the database.

**Creating a Schema:**

```javascript
const mongoose = require('mongoose');

// Define schema
const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true,
    trim: true
  },
  email: {
    type: String,
    required: true,
    unique: true,
    lowercase: true
  },
  age: {
    type: Number,
    min: 0,
    max: 120
  },
  isActive: {
    type: Boolean,
    default: true
  },
  createdAt: {
    type: Date,
    default: Date.now
  }
});

// Create model
const User = mongoose.model('User', userSchema);

module.exports = User;
```

**Schema types:**

```javascript
const schema = new mongoose.Schema({
  name: String,              // String type
  age: Number,              // Number type
  isActive: Boolean,        // Boolean type
  birthDate: Date,          // Date type
  tags: [String],           // Array of strings
  profile: {                // Nested object
    bio: String,
    website: String
  },
  userId: mongoose.Schema.Types.ObjectId  // ObjectId reference
});
```

**Validation:**

```javascript
const userSchema = new mongoose.Schema({
  email: {
    type: String,
    required: [true, 'Email is required'],
    unique: true,
    validate: {
      validator: function(v) {
        return /\S+@\S+\.\S+/.test(v);
      },
      message: 'Invalid email format'
    }
  },
  age: {
    type: Number,
    min: [18, 'Must be at least 18'],
    max: [100, 'Must be at most 100']
  },
  role: {
    type: String,
    enum: ['user', 'admin', 'moderator'],
    default: 'user'
  }
});
```

**Schema methods:**

```javascript
// Instance method
userSchema.methods.getFullInfo = function() {
  return `${this.name} (${this.email})`;
};

// Static method
userSchema.statics.findByEmail = function(email) {
  return this.findOne({ email });
};

// Usage
const user = await User.findById(id);
console.log(user.getFullInfo()); // Instance method

const user2 = await User.findByEmail('john@email.com'); // Static method
```

**Virtual properties:**

```javascript
const userSchema = new mongoose.Schema({
  firstName: String,
  lastName: String
});

// Virtual property (not stored in DB)
userSchema.virtual('fullName').get(function() {
  return `${this.firstName} ${this.lastName}`;
});

// Usage
const user = new User({ firstName: 'John', lastName: 'Doe' });
console.log(user.fullName); // 'John Doe'
```

**Interview tip:** Schema defines document structure with types and validation. Model is created from schema and used to query database. Use validation for data integrity. Schema methods add custom functionality."

---

### Q31: CRUD Operations with Mongoose

**How to Answer:**

"Mongoose provides methods to Create, Read, Update, and Delete documents.

**CREATE:**

```javascript
const User = require('./models/User');

// Method 1: new + save()
const user = new User({
  name: 'John',
  email: 'john@email.com',
  age: 25
});

await user.save();

// Method 2: create()
const user = await User.create({
  name: 'Jane',
  email: 'jane@email.com',
  age: 30
});

// Create multiple
const users = await User.insertMany([
  { name: 'Bob', email: 'bob@email.com' },
  { name: 'Alice', email: 'alice@email.com' }
]);
```

**READ:**

```javascript
// Find all
const users = await User.find();

// Find with filter
const activeUsers = await User.find({ isActive: true });

// Find one
const user = await User.findOne({ email: 'john@email.com' });

// Find by ID
const user = await User.findById('507f1f77bcf86cd799439011');

// With specific fields (projection)
const users = await User.find().select('name email');
// Returns only name and email

// Sort
const users = await User.find().sort({ age: -1 }); // Descending
const users = await User.find().sort({ age: 1 });  // Ascending

// Limit and skip (pagination)
const users = await User.find()
  .limit(10)
  .skip(20);

// Count
const count = await User.countDocuments({ isActive: true });

// Exists
const exists = await User.exists({ email: 'john@email.com' });
```

**UPDATE:**

```javascript
// Update one
await User.updateOne(
  { email: 'john@email.com' },
  { age: 26 }
);

// Update many
await User.updateMany(
  { isActive: false },
  { isActive: true }
);

// Find and update (returns updated document)
const user = await User.findByIdAndUpdate(
  '507f1f77bcf86cd799439011',
  { age: 26 },
  { new: true } // Return updated document
);

// Find one and update
const user = await User.findOneAndUpdate(
  { email: 'john@email.com' },
  { age: 26 },
  { new: true }
);
```

**DELETE:**

```javascript
// Delete one
await User.deleteOne({ email: 'john@email.com' });

// Delete many
await User.deleteMany({ isActive: false });

// Find and delete (returns deleted document)
const user = await User.findByIdAndDelete('507f1f77bcf86cd799439011');

// Find one and delete
const user = await User.findOneAndDelete({ email: 'john@email.com' });
```

**Express API with Mongoose:**

```javascript
const express = require('express');
const User = require('./models/User');

const app = express();
app.use(express.json());

// GET all users
app.get('/api/users', async (req, res) => {
  try {
    const users = await User.find();
    res.json(users);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

// GET single user
app.get('/api/users/:id', async (req, res) => {
  try {
    const user = await User.findById(req.params.id);
    
    if (!user) {
      return res.status(404).json({ error: 'User not found' });
    }
    
    res.json(user);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

// POST create user
app.post('/api/users', async (req, res) => {
  try {
    const user = await User.create(req.body);
    res.status(201).json(user);
  } catch (error) {
    res.status(400).json({ error: error.message });
  }
});

// PUT update user
app.put('/api/users/:id', async (req, res) => {
  try {
    const user = await User.findByIdAndUpdate(
      req.params.id,
      req.body,
      { new: true, runValidators: true }
    );
    
    if (!user) {
      return res.status(404).json({ error: 'User not found' });
    }
    
    res.json(user);
  } catch (error) {
    res.status(400).json({ error: error.message });
  }
});

// DELETE user
app.delete('/api/users/:id', async (req, res) => {
  try {
    const user = await User.findByIdAndDelete(req.params.id);
    
    if (!user) {
      return res.status(404).json({ error: 'User not found' });
    }
    
    res.status(204).send();
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

app.listen(3000);
```

**Interview tip:** Mongoose CRUD: create() or new+save() for create, find()/findOne()/findById() for read, updateOne()/findByIdAndUpdate() for update, deleteOne()/findByIdAndDelete() for delete. Always use try/catch with async operations. Return appropriate status codes."

---

## Authentication & Security

### Q35: Authentication vs Authorization

**How to Answer:**

"Authentication and authorization are both security concepts but serve different purposes.

**Authentication:**
Verifying WHO the user is (identity).

```
Question: "Who are you?"
Answer: "I am John" (proves identity with password)
```

**Authorization:**
Determining WHAT the user can do (permissions).

```
Question: "What can you do?"
Answer: "I can view users but not delete them" (based on role/permissions)
```

**Comparison:**

| Authentication | Authorization |
|----------------|---------------|
| Who are you? | What can you do? |
| Logging in | Checking permissions |
| Username + Password | Roles and permissions |
| Happens first | Happens after authentication |
| Example: Login with email/password | Example: Only admins can delete users |

**Example flow:**

```javascript
// 1. Authentication - Login
app.post('/api/login', async (req, res) => {
  const { email, password } = req.body;
  
  // Find user
  const user = await User.findOne({ email });
  if (!user) {
    return res.status(401).json({ error: 'Invalid credentials' });
  }
  
  // Verify password
  const isMatch = await bcrypt.compare(password, user.password);
  if (!isMatch) {
    return res.status(401).json({ error: 'Invalid credentials' });
  }
  
  // User authenticated - generate token
  const token = jwt.sign({ userId: user._id }, 'secret');
  res.json({ token });
});

// 2. Authorization - Check if admin
const requireAdmin = (req, res, next) => {
  if (req.user.role !== 'admin') {
    return res.status(403).json({ error: 'Not authorized' });
  }
  next();
};

// Protected route - requires both
app.delete('/api/users/:id', authenticate, requireAdmin, async (req, res) => {
  // Only authenticated admins can delete users
  await User.findByIdAndDelete(req.params.id);
  res.status(204).send();
});
```

**Interview tip:** Authentication verifies identity (login), Authorization checks permissions (what you can do). Authentication uses username/password, Authorization uses roles/permissions. 401 for authentication failure, 403 for authorization failure."

---

### Q36: JWT - JSON Web Tokens

**How to Answer:**

"JWT is a secure way to transmit information between client and server as a JSON object. Commonly used for authentication.

**Installation:**

```bash
npm install jsonwebtoken
```

**JWT structure:**

```
header.payload.signature

eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOiIxMjMifQ.signature
```

- **Header:** Algorithm and token type
- **Payload:** Data (user info)
- **Signature:** Verifies token hasn't been tampered

**Creating JWT:**

```javascript
const jwt = require('jsonwebtoken');

// Sign token
const token = jwt.sign(
  { userId: user._id, email: user.email },  // Payload
  process.env.JWT_SECRET,                    // Secret key
  { expiresIn: '7d' }                       // Options
);
```

**Verifying JWT:**

```javascript
try {
  const decoded = jwt.verify(token, process.env.JWT_SECRET);
  console.log(decoded); // { userId: '...', email: '...', iat: ..., exp: ... }
} catch (error) {
  console.log('Invalid token');
}
```

**Complete authentication example:**

```javascript
const express = require('express');
const jwt = require('jsonwebtoken');
const bcrypt = require('bcrypt');
const User = require('./models/User');

const app = express();
app.use(express.json());

// Register
app.post('/api/register', async (req, res) => {
  try {
    const { name, email, password } = req.body;
    
    // Hash password
    const hashedPassword = await bcrypt.hash(password, 10);
    
    // Create user
    const user = await User.create({
      name,
      email,
      password: hashedPassword
    });
    
    // Generate token
    const token = jwt.sign(
      { userId: user._id },
      process.env.JWT_SECRET,
      { expiresIn: '7d' }
    );
    
    res.status(201).json({ token });
  } catch (error) {
    res.status(400).json({ error: error.message });
  }
});

// Login
app.post('/api/login', async (req, res) => {
  try {
    const { email, password } = req.body;
    
    // Find user
    const user = await User.findOne({ email });
    if (!user) {
      return res.status(401).json({ error: 'Invalid credentials' });
    }
    
    // Check password
    const isMatch = await bcrypt.compare(password, user.password);
    if (!isMatch) {
      return res.status(401).json({ error: 'Invalid credentials' });
    }
    
    // Generate token
    const token = jwt.sign(
      { userId: user._id },
      process.env.JWT_SECRET,
      { expiresIn: '7d' }
    );
    
    res.json({ token });
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

// Authentication middleware
const authenticate = async (req, res, next) => {
  try {
    // Get token from header
    const token = req.headers.authorization?.replace('Bearer ', '');
    
    if (!token) {
      return res.status(401).json({ error: 'No token provided' });
    }
    
    // Verify token
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    
    // Find user
    const user = await User.findById(decoded.userId);
    if (!user) {
      return res.status(401).json({ error: 'User not found' });
    }
    
    // Attach user to request
    req.user = user;
    next();
  } catch (error) {
    res.status(401).json({ error: 'Invalid token' });
  }
};

// Protected route
app.get('/api/profile', authenticate, (req, res) => {
  res.json(req.user);
});

app.listen(3000);
```

**Client-side usage:**

```javascript
// After login, store token
localStorage.setItem('token', token);

// Include token in requests
fetch('/api/profile', {
  headers: {
    'Authorization': `Bearer ${localStorage.getItem('token')}`
  }
});
```

**Interview tip:** JWT is a token-based authentication method. Sign tokens on login with jwt.sign(), verify on protected routes with jwt.verify(). Store JWT in localStorage on client, send in Authorization header. Use secret key from .env file."

---

### Q37: Password Hashing (bcrypt)

**How to Answer:**

"bcrypt is a library for hashing passwords. Never store passwords as plain text - always hash them.

**Installation:**

```bash
npm install bcrypt
```

**Why hash passwords?**

```javascript
// ❌ NEVER do this
const user = {
  email: 'john@email.com',
  password: 'mypassword123' // Plain text - VERY BAD!
};

// ✅ Always hash
const user = {
  email: 'john@email.com',
  password: '$2b$10$...' // Hashed - GOOD!
};
```

**Hashing password:**

```javascript
const bcrypt = require('bcrypt');

// Hash password
const password = 'mypassword123';
const saltRounds = 10;

const hashedPassword = await bcrypt.hash(password, saltRounds);
// $2b$10$N9qo8uLOickgx2ZMRZoMyeIjZAgcfl7p92ldGxad68LJZdL17lhWy
```

**Comparing password:**

```javascript
// When user logs in
const enteredPassword = 'mypassword123';
const hashedPasswordFromDB = '$2b$10$N9qo8uLOickgx2ZMRZoMyeIjZAgcfl7p92ldGxad68LJZdL17lhWy';

const isMatch = await bcrypt.compare(enteredPassword, hashedPasswordFromDB);
// true if passwords match
```

**Complete example:**

```javascript
const bcrypt = require('bcrypt');
const User = require('./models/User');

// Register - Hash password
app.post('/api/register', async (req, res) => {
  try {
    const { email, password } = req.body;
    
    // Check if user exists
    const exists = await User.findOne({ email });
    if (exists) {
      return res.status(409).json({ error: 'User already exists' });
    }
    
    // Hash password
    const hashedPassword = await bcrypt.hash(password, 10);
    
    // Create user with hashed password
    const user = await User.create({
      email,
      password: hashedPassword
    });
    
    res.status(201).json({ message: 'User created' });
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

// Login - Compare password
app.post('/api/login', async (req, res) => {
  try {
    const { email, password } = req.body;
    
    // Find user
    const user = await User.findOne({ email });
    if (!user) {
      return res.status(401).json({ error: 'Invalid credentials' });
    }
    
    // Compare passwords
    const isMatch = await bcrypt.compare(password, user.password);
    if (!isMatch) {
      return res.status(401).json({ error: 'Invalid credentials' });
    }
    
    // Generate token
    const token = jwt.sign({ userId: user._id }, process.env.JWT_SECRET);
    res.json({ token });
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});
```

**Using Mongoose pre-save hook:**

```javascript
const mongoose = require('mongoose');
const bcrypt = require('bcrypt');

const userSchema = new mongoose.Schema({
  email: String,
  password: String
});

// Hash password before saving
userSchema.pre('save', async function(next) {
  // Only hash if password is modified
  if (!this.isModified('password')) {
    return next();
  }
  
  // Hash password
  this.password = await bcrypt.hash(this.password, 10);
  next();
});

const User = mongoose.model('User', userSchema);
```

**Interview tip:** Use bcrypt to hash passwords before storing. bcrypt.hash() to hash, bcrypt.compare() to verify. Salt rounds (10) controls complexity. Never store plain text passwords. Use pre-save hooks in Mongoose for automatic hashing."

---

## Practical Patterns

### Q49: Folder Structure / Project Organization

**How to Answer:**

"A well-organized folder structure makes code maintainable and scalable.

**Basic structure:**

```
my-app/
├── node_modules/
├── src/
│   ├── config/
│   │   └── db.js
│   ├── models/
│   │   ├── User.js
│   │   └── Product.js
│   ├── routes/
│   │   ├── userRoutes.js
│   │   └── productRoutes.js
│   ├── controllers/
│   │   ├── userController.js
│   │   └── productController.js
│   ├── middleware/
│   │   ├── auth.js
│   │   └── errorHandler.js
│   └── app.js
├── .env
├── .gitignore
├── package.json
└── server.js
```

**Explanation:**

- **config/** - Configuration files (database, environment)
- **models/** - Database schemas/models
- **routes/** - Route definitions
- **controllers/** - Route handlers (business logic)
- **middleware/** - Custom middleware
- **app.js** - Express app setup
- **server.js** - Server startup

**Example implementation:**

**server.js** (Entry point):
```javascript
require('dotenv').config();
const app = require('./src/app');
const connectDB = require('./src/config/db');

const PORT = process.env.PORT || 3000;

connectDB().then(() => {
  app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
  });
});
```

**src/config/db.js** (Database):
```javascript
const mongoose = require('mongoose');

const connectDB = async () => {
  try {
    await mongoose.connect(process.env.MONGODB_URI);
    console.log('MongoDB connected');
  } catch (error) {
    console.error('MongoDB connection error:', error);
    process.exit(1);
  }
};

module.exports = connectDB;
```

**src/models/User.js** (Model):
```javascript
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true }
});

module.exports = mongoose.model('User', userSchema);
```

**src/controllers/userController.js** (Controller):
```javascript
const User = require('../models/User');

exports.getAllUsers = async (req, res) => {
  try {
    const users = await User.find();
    res.json(users);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
};

exports.createUser = async (req, res) => {
  try {
    const user = await User.create(req.body);
    res.status(201).json(user);
  } catch (error) {
    res.status(400).json({ error: error.message });
  }
};
```

**src/routes/userRoutes.js** (Routes):
```javascript
const express = require('express');
const router = express.Router();
const userController = require('../controllers/userController');

router.get('/', userController.getAllUsers);
router.post('/', userController.createUser);

module.exports = router;
```

**src/app.js** (App setup):
```javascript
const express = require('express');
const userRoutes = require('./routes/userRoutes');

const app = express();

app.use(express.json());
app.use('/api/users', userRoutes);

module.exports = app;
```

**Interview tip:** Separate concerns: models for database, routes for endpoints, controllers for logic, middleware for reusable functions. Keep server.js minimal - just start server. This structure is scalable and maintainable."

---

### Q50: MVC Pattern in Express

**How to Answer:**

"MVC (Model-View-Controller) is a design pattern that separates application into three components.

**Components:**

1. **Model** - Database schema and business logic
2. **View** - User interface (for APIs, this is JSON responses)
3. **Controller** - Handles requests, coordinates model and view

**MVC in Express:**

```
Request → Router → Controller → Model → Database
                      ↓
                   Response
```

**Complete example:**

**models/User.js** (Model):
```javascript
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  name: String,
  email: { type: String, unique: true },
  password: String
}, { timestamps: true });

module.exports = mongoose.model('User', userSchema);
```

**controllers/userController.js** (Controller):
```javascript
const User = require('../models/User');

// Get all users
exports.getUsers = async (req, res) => {
  try {
    const users = await User.find().select('-password');
    res.json(users);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
};

// Get single user
exports.getUser = async (req, res) => {
  try {
    const user = await User.findById(req.params.id).select('-password');
    if (!user) {
      return res.status(404).json({ error: 'User not found' });
    }
    res.json(user);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
};

// Create user
exports.createUser = async (req, res) => {
  try {
    const user = await User.create(req.body);
    res.status(201).json(user);
  } catch (error) {
    res.status(400).json({ error: error.message });
  }
};

// Update user
exports.updateUser = async (req, res) => {
  try {
    const user = await User.findByIdAndUpdate(
      req.params.id,
      req.body,
      { new: true }
    );
    if (!user) {
      return res.status(404).json({ error: 'User not found' });
    }
    res.json(user);
  } catch (error) {
    res.status(400).json({ error: error.message });
  }
};

// Delete user
exports.deleteUser = async (req, res) => {
  try {
    const user = await User.findByIdAndDelete(req.params.id);
    if (!user) {
      return res.status(404).json({ error: 'User not found' });
    }
    res.status(204).send();
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
};
```

**routes/userRoutes.js** (Routes):
```javascript
const express = require('express');
const router = express.Router();
const userController = require('../controllers/userController');

router.get('/', userController.getUsers);
router.get('/:id', userController.getUser);
router.post('/', userController.createUser);
router.put('/:id', userController.updateUser);
router.delete('/:id', userController.deleteUser);

module.exports = router;
```

**app.js**:
```javascript
const express = require('express');
const userRoutes = require('./routes/userRoutes');

const app = express();

app.use(express.json());
app.use('/api/users', userRoutes);

module.exports = app;
```

**Benefits of MVC:**

- **Separation of Concerns** - Each component has specific role
- **Maintainability** - Easy to update or fix
- **Reusability** - Controllers can be reused
- **Testability** - Easy to test each component
- **Scalability** - Add features without affecting others

**Interview tip:** MVC separates application into Model (database), View (response), Controller (logic). Models define schemas, Controllers handle business logic, Routes define endpoints. This makes code organized, maintainable, and scalable."

---

### Q52: Common Interview Coding Questions

**How to Answer:**

"Here are frequently asked Node.js/Express coding questions for freshers:

**1. Create a simple Express server:**

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello World');
});

app.listen(3000, () => {
  console.log('Server running on port 3000');
});
```

**2. Create a REST API with in-memory data:**

```javascript
const express = require('express');
const app = express();

app.use(express.json());

let users = [
  { id: 1, name: 'John' },
  { id: 2, name: 'Jane' }
];

app.get('/users', (req, res) => {
  res.json(users);
});

app.post('/users', (req, res) => {
  const user = { id: users.length + 1, ...req.body };
  users.push(user);
  res.status(201).json(user);
});

app.listen(3000);
```

**3. Authentication middleware:**

```javascript
const authenticate = (req, res, next) => {
  const token = req.headers.authorization;
  if (!token) {
    return res.status(401).json({ error: 'No token' });
  }
  // Verify token
  next();
};

app.get('/protected', authenticate, (req, res) => {
  res.json({ message: 'Protected data' });
});
```

**4. Error handling:**

```javascript
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: err.message });
});
```

**5. Read file and send as response:**

```javascript
const fs = require('fs').promises;

app.get('/file', async (req, res) => {
  try {
    const data = await fs.readFile('data.txt', 'utf8');
    res.send(data);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});
```

**Practice these patterns - they're commonly asked in fresher interviews!"**

---

## Summary for Interview Preparation

**Node.js Must-Know:**
1. What is Node.js (runtime, event-driven, non-blocking)
2. Event loop and single-threaded architecture
3. Modules (require, module.exports)
4. NPM and package.json
5. Async patterns (callbacks, promises, async/await)
6. Built-in modules (fs, path, http)

**Express Must-Know:**
1. Creating server with express()
2. Routing (GET, POST, PUT, DELETE)
3. Middleware concept and usage
4. Request/Response objects
5. Error handling
6. express.Router()

**REST API Must-Know:**
1. REST principles and HTTP methods
2. Status codes (200, 201, 400, 404, 500)
3. Route parameters vs query strings
4. JSON request/response
5. CRUD operations

**Database Must-Know:**
1. Mongoose connection
2. Schema and models
3. CRUD with Mongoose
4. Validation

**Authentication Must-Know:**
1. JWT token creation and verification
2. bcrypt for password hashing
3. Authentication vs Authorization
4. Protected routes

**Best Practices:**
1. MVC pattern for organization
2. Environment variables (.env)
3. Error handling middleware
4. Async/await with try/catch
5. Proper HTTP status codes
6. Input validation

**Interview Tips:**
- Write clean, readable code
- Explain your approach
- Handle errors properly
- Use async/await (modern)
- Follow REST conventions
- Organize code properly (MVC)

Good luck with your interviews! 🚀


---

## 📌 Note: This is Part 1

**Part 2 Available:** Additional topics covered in separate file including:
- Request/Response objects (detailed)
- express.Router()
- CORS & Validation  
- SQL databases (MySQL/PostgreSQL)
- Sessions & Cookies
- File uploads (Multer)
- Logging & Deployment
- And more...

See: **nodejs-express-interview-guide-part2.md**

---