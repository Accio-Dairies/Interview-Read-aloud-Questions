# Node.js & Express Interview Preparation Guide - Part 2
*Additional Essential Topics for Freshers*

**Note:** This is Part 2. Make sure you've studied Part 1 first!

---

## Table of Contents - Part 2

### Request/Response & Routing
15. [Request and Response Objects (Detailed)](#q15-request-and-response-objects-detailed)
20. [express.Router()](#q20-expressrouter)
22. [HTTP Methods (Detailed)](#q22-http-methods-detailed)
24. [Request Data (Body, Params, Query)](#q24-request-data-body-params-query)

### Advanced API Concepts
25. [CORS - Cross-Origin Resource Sharing](#q25-cors---cross-origin-resource-sharing)
26. [API Versioning](#q26-api-versioning)
27. [Request Validation](#q27-request-validation)
28. [Response Formatting](#q28-response-formatting)

### SQL Databases
32. [Connecting SQL Databases (MySQL/PostgreSQL)](#q32-connecting-sql-databases-mysqlpostgresql)
33. [Using ORM - Sequelize Basics](#q33-using-orm---sequelize-basics)
34. [Connection Pooling](#q34-connection-pooling)

### Sessions & Security
38. [Sessions and Cookies](#q38-sessions-and-cookies)
39. [Environment Variables (.env)](#q39-environment-variables-env)
40. [Security Best Practices](#q40-security-best-practices)

### File Handling & Advanced
41. [File Upload (Multer)](#q41-file-upload-multer)
42. [File Operations (fs module)](#q42-file-operations-fs-module)
43. [Streaming in Node.js](#q43-streaming-in-nodejs)
44. [Template Engines (EJS, Pug)](#q44-template-engines-ejs-pug)
45. [Logging](#q45-logging)
46. [Error Handling Patterns](#q46-error-handling-patterns)
47. [Debugging Node.js Applications](#q47-debugging-nodejs-applications)
48. [Deployment Basics](#q48-deployment-basics)

### API Documentation
51. [API Documentation](#q51-api-documentation)

---

## Request/Response & Routing

### Q15: Request and Response Objects (Detailed)

**How to Answer:**

"Request (req) and Response (res) objects are the core of Express. They contain all information about the HTTP request and methods to send responses.

**Request Object (req):**

```javascript
app.get('/users/:id', (req, res) => {
  // Route parameters
  console.log(req.params);        // { id: '123' }
  
  // Query strings
  console.log(req.query);         // { page: '2', limit: '10' }
  
  // Request body (with express.json())
  console.log(req.body);          // { name: 'John', email: 'john@...' }
  
  // Headers
  console.log(req.headers);       // All headers
  console.log(req.get('Authorization'));  // Get specific header
  
  // HTTP method
  console.log(req.method);        // 'GET', 'POST', etc.
  
  // URL information
  console.log(req.url);           // '/users/123?page=2'
  console.log(req.path);          // '/users/123'
  console.log(req.originalUrl);   // Full URL
  console.log(req.hostname);      // 'localhost'
  console.log(req.protocol);      // 'http' or 'https'
  
  // IP address
  console.log(req.ip);            // Client IP
  
  // Check content type
  console.log(req.is('json'));    // true if JSON
  console.log(req.is('html'));    // true if HTML
});
```

**Response Object (res):**

```javascript
app.get('/api/data', (req, res) => {
  // Send JSON response
  res.json({ name: 'John', age: 25 });
  
  // Send plain text
  res.send('Hello World');
  
  // Set status code
  res.status(404).send('Not Found');
  res.status(201).json({ message: 'Created' });
  
  // Set headers
  res.set('Content-Type', 'application/json');
  res.set({
    'Content-Type': 'application/json',
    'X-Custom-Header': 'value'
  });
  
  // Redirect
  res.redirect('/login');
  res.redirect(301, 'https://example.com');
  
  // Send file
  res.sendFile('/path/to/file.pdf');
  
  // Download file
  res.download('/path/to/file.pdf');
  res.download('/path/to/file.pdf', 'custom-name.pdf');
  
  // Set cookie
  res.cookie('token', 'abc123', { maxAge: 900000, httpOnly: true });
  
  // Clear cookie
  res.clearCookie('token');
  
  // End response (no data)
  res.end();
  
  // Send status without message
  res.sendStatus(200);  // Sends 'OK'
  res.sendStatus(404);  // Sends 'Not Found'
});
```

**Common patterns:**

```javascript
// Success response
app.get('/users', async (req, res) => {
  const users = await User.find();
  res.status(200).json({
    success: true,
    count: users.length,
    data: users
  });
});

// Error response
app.get('/users/:id', async (req, res) => {
  const user = await User.findById(req.params.id);
  
  if (!user) {
    return res.status(404).json({
      success: false,
      error: 'User not found'
    });
  }
  
  res.json({ success: true, data: user });
});

// Multiple operations
app.post('/users', async (req, res) => {
  const user = await User.create(req.body);
  
  res
    .status(201)
    .set('X-User-Id', user._id.toString())
    .json({
      success: true,
      data: user
    });
});
```

**Interview tip:** req contains request data (params, query, body, headers). res sends responses (json, send, status, redirect). Always set appropriate status codes. Chain methods like res.status(200).json({})."

---

### Q20: express.Router()

**How to Answer:**

"express.Router() creates modular, mountable route handlers. It helps organize routes into separate files.

**Why use Router?**

Without Router (messy):
```javascript
// app.js - All routes in one file
app.get('/api/users', ...);
app.post('/api/users', ...);
app.get('/api/users/:id', ...);
app.get('/api/products', ...);
app.post('/api/products', ...);
// Becomes very large!
```

With Router (organized):
```javascript
// routes/userRoutes.js
const express = require('express');
const router = express.Router();

router.get('/', getAllUsers);
router.post('/', createUser);
router.get('/:id', getUser);

module.exports = router;

// app.js
app.use('/api/users', userRoutes);
```

**Complete example:**

**routes/userRoutes.js:**
```javascript
const express = require('express');
const router = express.Router();
const { 
  getUsers, 
  getUser, 
  createUser, 
  updateUser, 
  deleteUser 
} = require('../controllers/userController');

// All routes start with /api/users (defined in app.js)
router.get('/', getUsers);           // GET /api/users
router.post('/', createUser);        // POST /api/users
router.get('/:id', getUser);         // GET /api/users/:id
router.put('/:id', updateUser);      // PUT /api/users/:id
router.delete('/:id', deleteUser);   // DELETE /api/users/:id

// Can chain same path
router.route('/:id')
  .get(getUser)
  .put(updateUser)
  .delete(deleteUser);

module.exports = router;
```

**routes/productRoutes.js:**
```javascript
const express = require('express');
const router = express.Router();
const productController = require('../controllers/productController');

router.get('/', productController.getProducts);
router.post('/', productController.createProduct);

module.exports = router;
```

**app.js:**
```javascript
const express = require('express');
const userRoutes = require('./routes/userRoutes');
const productRoutes = require('./routes/productRoutes');

const app = express();

app.use(express.json());

// Mount routers
app.use('/api/users', userRoutes);
app.use('/api/products', productRoutes);

app.listen(3000);
```

**Router with middleware:**

```javascript
const router = express.Router();

// Middleware for this router only
router.use((req, res, next) => {
  console.log('User routes accessed');
  next();
});

// Authentication middleware for specific routes
const authenticate = require('../middleware/auth');

router.get('/', getUsers);                    // Public
router.post('/', authenticate, createUser);    // Protected
router.put('/:id', authenticate, updateUser);  // Protected

module.exports = router;
```

**Nested routers:**

```javascript
// routes/userRoutes.js
const router = express.Router();
const postRoutes = require('./postRoutes');

// User's posts
router.use('/:userId/posts', postRoutes);

router.get('/', getUsers);

module.exports = router;

// routes/postRoutes.js
const router = express.Router({ mergeParams: true });

// Can access req.params.userId from parent
router.get('/', getUserPosts);

module.exports = router;

// Results in: GET /api/users/:userId/posts
```

**Interview tip:** express.Router() creates mini-apps with their own routes and middleware. Helps organize code into separate files. Mount with app.use(). Use mergeParams: true for nested routers to access parent params."

---

### Q22: HTTP Methods (Detailed)

**How to Answer:**

"HTTP methods define the type of operation to perform on a resource. Each method has specific semantics and use cases.

**GET - Retrieve data:**

```javascript
// Get all resources
app.get('/api/users', (req, res) => {
  res.json(users);
});

// Get single resource
app.get('/api/users/:id', (req, res) => {
  const user = users.find(u => u.id === req.params.id);
  res.json(user);
});

// Characteristics:
// - Read-only (safe)
// - Idempotent (same result every time)
// - Can be cached
// - Should NOT have body
```

**POST - Create new resource:**

```javascript
app.post('/api/users', (req, res) => {
  const newUser = {
    id: users.length + 1,
    ...req.body
  };
  users.push(newUser);
  res.status(201).json(newUser);
});

// Characteristics:
// - NOT safe (creates data)
// - NOT idempotent (multiple calls create multiple resources)
// - Cannot be cached
// - Has request body
```

**PUT - Replace entire resource:**

```javascript
app.put('/api/users/:id', (req, res) => {
  const user = users.find(u => u.id === req.params.id);
  
  // Replace ALL fields
  user.name = req.body.name;
  user.email = req.body.email;
  user.age = req.body.age;
  // Must provide all fields
  
  res.json(user);
});

// Characteristics:
// - Updates entire resource
// - Idempotent (same call = same result)
// - Must send complete resource
```

**PATCH - Partial update:**

```javascript
app.patch('/api/users/:id', (req, res) => {
  const user = users.find(u => u.id === req.params.id);
  
  // Update only provided fields
  if (req.body.name) user.name = req.body.name;
  if (req.body.email) user.email = req.body.email;
  // Optional fields
  
  res.json(user);
});

// Characteristics:
// - Updates partial resource
// - Send only fields to update
// - More flexible than PUT
```

**DELETE - Remove resource:**

```javascript
app.delete('/api/users/:id', (req, res) => {
  const index = users.findIndex(u => u.id === req.params.id);
  users.splice(index, 1);
  res.status(204).send();  // No content
});

// Characteristics:
// - Removes resource
// - Idempotent
// - Returns 204 (no content)
```

**PUT vs PATCH example:**

```javascript
// Current user
const user = {
  id: 1,
  name: 'John',
  email: 'john@email.com',
  age: 25
};

// PUT - Must send ALL fields
app.put('/users/1', (req, res) => {
  // Body: { name: 'John Doe', email: 'john@email.com', age: 26 }
  // All fields required!
});

// PATCH - Send only changed fields
app.patch('/users/1', (req, res) => {
  // Body: { age: 26 }
  // Only updating age
});
```

**Method comparison table:**

| Method | Purpose | Idempotent | Safe | Has Body | Common Status |
|--------|---------|-----------|------|----------|---------------|
| GET | Read | Yes | Yes | No | 200 |
| POST | Create | No | No | Yes | 201 |
| PUT | Replace | Yes | No | Yes | 200 |
| PATCH | Update | No | No | Yes | 200 |
| DELETE | Remove | Yes | No | No | 204 |

**Idempotent explained:**

```javascript
// GET is idempotent
GET /users/1  // Returns user 1
GET /users/1  // Returns same user 1
GET /users/1  // Returns same user 1

// POST is NOT idempotent
POST /users { name: 'John' }  // Creates user 1
POST /users { name: 'John' }  // Creates user 2 (duplicate!)
POST /users { name: 'John' }  // Creates user 3

// PUT is idempotent
PUT /users/1 { name: 'John' }  // Updates user 1
PUT /users/1 { name: 'John' }  // Same result
PUT /users/1 { name: 'John' }  // Same result

// DELETE is idempotent
DELETE /users/1  // Deletes user 1
DELETE /users/1  // User already deleted (same result)
DELETE /users/1  // Still deleted
```

**Interview tip:** GET reads, POST creates, PUT replaces entire resource, PATCH updates partial, DELETE removes. GET and DELETE are idempotent (same result on repeat). POST is not idempotent (creates duplicates). Use 200 for success, 201 for created, 204 for deleted."

---

### Q24: Request Data (Body, Params, Query)

**How to Answer:**

"Express provides three main ways to access data from requests: params, query, and body.

**1. Route Parameters (req.params):**

Part of the URL path, required data.

```javascript
// Define route with parameters
app.get('/users/:userId/posts/:postId', (req, res) => {
  const { userId, postId } = req.params;
  console.log(userId);   // '123'
  console.log(postId);   // '456'
  res.json({ userId, postId });
});

// Access: GET /users/123/posts/456
```

**When to use params:**
- Identifying specific resources
- Required data
- Part of resource hierarchy

```javascript
GET /users/123              // User ID
GET /posts/456/comments/789 // Post ID + Comment ID
DELETE /products/999        // Product to delete
```

**2. Query Strings (req.query):**

Optional data after `?` in URL.

```javascript
app.get('/search', (req, res) => {
  const { q, category, page, limit, sort } = req.query;
  
  console.log(q);         // 'laptop'
  console.log(category);  // 'electronics'
  console.log(page);      // '2'
  console.log(limit);     // '10'
  
  res.json({ q, category, page, limit });
});

// Access: GET /search?q=laptop&category=electronics&page=2&limit=10
```

**When to use query:**
- Filtering data
- Pagination
- Sorting
- Search terms
- Optional parameters

```javascript
GET /products?category=electronics&minPrice=100&maxPrice=500
GET /users?page=2&limit=20&sort=name
GET /search?q=nodejs&type=article
```

**3. Request Body (req.body):**

Data sent in request body (requires middleware).

```javascript
// Enable JSON parsing
app.use(express.json());

app.post('/users', (req, res) => {
  const { name, email, age } = req.body;
  
  console.log(req.body);  // { name: 'John', email: '...', age: 25 }
  
  res.status(201).json({ name, email, age });
});

// Client sends: POST /users
// Body: { "name": "John", "email": "john@email.com", "age": 25 }
```

**When to use body:**
- Creating resources (POST)
- Updating resources (PUT/PATCH)
- Sending complex data
- Sensitive data (passwords)

```javascript
POST /users
Body: { "name": "John", "email": "john@email.com", "password": "secret" }

PUT /products/123
Body: { "name": "Updated Product", "price": 99.99, "stock": 50 }
```

**Combining all three:**

```javascript
app.put('/users/:id/posts/:postId', (req, res) => {
  // Route parameters
  const { id, postId } = req.params;
  
  // Query strings
  const { notify } = req.query;
  
  // Request body
  const { title, content } = req.body;
  
  res.json({
    userId: id,
    postId: postId,
    notify: notify,
    title: title,
    content: content
  });
});

// Access: PUT /users/123/posts/456?notify=true
// Body: { "title": "Updated", "content": "New content" }
```

**Type conversion:**

```javascript
app.get('/users/:id', (req, res) => {
  // ALL values are strings!
  console.log(typeof req.params.id);     // 'string'
  console.log(typeof req.query.page);    // 'string'
  
  // Convert to number
  const id = parseInt(req.params.id);
  const page = parseInt(req.query.page);
  
  // Or use + operator
  const id2 = +req.params.id;
});
```

**Validation example:**

```javascript
app.post('/users', (req, res) => {
  // Validate body
  const { name, email, age } = req.body;
  
  if (!name || !email) {
    return res.status(400).json({ 
      error: 'Name and email are required' 
    });
  }
  
  if (age && (age < 0 || age > 120)) {
    return res.status(400).json({ 
      error: 'Invalid age' 
    });
  }
  
  // Create user
  const user = { name, email, age };
  res.status(201).json(user);
});
```

**Real-world example - Product API:**

```javascript
// GET /api/products?category=electronics&minPrice=100&page=2&limit=10
app.get('/api/products', (req, res) => {
  const {
    category,
    minPrice,
    maxPrice,
    page = 1,
    limit = 10,
    sort = 'name'
  } = req.query;
  
  let products = allProducts;
  
  // Filter by category
  if (category) {
    products = products.filter(p => p.category === category);
  }
  
  // Filter by price
  if (minPrice) {
    products = products.filter(p => p.price >= parseFloat(minPrice));
  }
  
  if (maxPrice) {
    products = products.filter(p => p.price <= parseFloat(maxPrice));
  }
  
  // Sort
  products.sort((a, b) => a[sort] > b[sort] ? 1 : -1);
  
  // Paginate
  const startIndex = (parseInt(page) - 1) * parseInt(limit);
  const endIndex = startIndex + parseInt(limit);
  const paginatedProducts = products.slice(startIndex, endIndex);
  
  res.json({
    page: parseInt(page),
    limit: parseInt(limit),
    total: products.length,
    products: paginatedProducts
  });
});

// PUT /api/products/123
app.put('/api/products/:id', (req, res) => {
  const productId = req.params.id;
  const { name, price, stock } = req.body;
  
  const product = products.find(p => p.id === productId);
  
  if (!product) {
    return res.status(404).json({ error: 'Product not found' });
  }
  
  product.name = name;
  product.price = price;
  product.stock = stock;
  
  res.json(product);
});
```

**Comparison table:**

| Feature | Params | Query | Body |
|---------|--------|-------|------|
| Location | URL path | URL after ? | Request payload |
| Required | Usually yes | No | Depends |
| Type | Always string | Always string | Any (JSON) |
| Use case | IDs, resources | Filters, options | Create/Update data |
| Example | /users/:id | ?page=2 | { name: 'John' } |
| Visible in URL | Yes | Yes | No |

**Interview tip:** Params for resource IDs (required), query for filters/pagination (optional), body for create/update data. All params and query values are strings - convert if needed. Body requires express.json() middleware. Validate all input data."

---

## Advanced API Concepts

### Q25: CORS - Cross-Origin Resource Sharing

**How to Answer:**

"CORS is a security feature that controls which domains can access your API. By default, browsers block requests from different origins.

**What is CORS?**

```
Same origin:
http://example.com/api → http://example.com/page  ✅ Allowed

Different origin (blocked without CORS):
http://example.com/api → http://another.com/page  ❌ Blocked
```

**Why CORS exists:**

Security - prevents malicious sites from accessing your API.

**CORS error:**

```
Access to fetch at 'http://localhost:3000/api/users' from origin 
'http://localhost:5173' has been blocked by CORS policy
```

**Solution - Enable CORS:**

**Install:**
```bash
npm install cors
```

**Basic usage:**

```javascript
const express = require('express');
const cors = require('cors');

const app = express();

// Enable CORS for all routes
app.use(cors());

app.get('/api/users', (req, res) => {
  res.json(users);
});

app.listen(3000);
```

**CORS with options:**

```javascript
// Allow specific origin
app.use(cors({
  origin: 'http://localhost:5173'  // Only this origin allowed
}));

// Allow multiple origins
const allowedOrigins = [
  'http://localhost:5173',
  'http://localhost:3001',
  'https://myapp.com'
];

app.use(cors({
  origin: function(origin, callback) {
    if (!origin || allowedOrigins.includes(origin)) {
      callback(null, true);
    } else {
      callback(new Error('Not allowed by CORS'));
    }
  }
}));

// With credentials (cookies)
app.use(cors({
  origin: 'http://localhost:5173',
  credentials: true  // Allow cookies
}));

// Allowed methods
app.use(cors({
  origin: 'http://localhost:5173',
  methods: ['GET', 'POST', 'PUT', 'DELETE']
}));
```

**Environment-based CORS:**

```javascript
const corsOptions = {
  origin: process.env.NODE_ENV === 'production'
    ? 'https://myapp.com'
    : 'http://localhost:5173',
  credentials: true
};

app.use(cors(corsOptions));
```

**Manual CORS (without package):**

```javascript
app.use((req, res, next) => {
  res.header('Access-Control-Allow-Origin', '*');
  res.header('Access-Control-Allow-Methods', 'GET, POST, PUT, DELETE');
  res.header('Access-Control-Allow-Headers', 'Content-Type, Authorization');
  
  // Handle preflight
  if (req.method === 'OPTIONS') {
    return res.sendStatus(200);
  }
  
  next();
});
```

**CORS for specific routes:**

```javascript
// CORS only for API routes
app.use('/api', cors());

app.get('/api/users', (req, res) => {
  res.json(users);  // CORS enabled
});

app.get('/admin', (req, res) => {
  res.send('Admin');  // CORS not enabled
});
```

**Interview tip:** CORS controls cross-origin requests for security. Use cors package with app.use(cors()). Configure origin to allow specific domains. Enable credentials for cookies. Browsers automatically handle CORS - it's server-side configuration."

---

### Q27: Request Validation

**How to Answer:**

"Request validation ensures incoming data meets requirements before processing. It prevents bad data from entering your system.

**Manual validation:**

```javascript
app.post('/api/users', (req, res) => {
  const { name, email, age } = req.body;
  
  // Check required fields
  if (!name || !email) {
    return res.status(400).json({
      error: 'Name and email are required'
    });
  }
  
  // Email format
  if (!/\S+@\S+\.\S+/.test(email)) {
    return res.status(400).json({
      error: 'Invalid email format'
    });
  }
  
  // Age range
  if (age && (age < 18 || age > 100)) {
    return res.status(400).json({
      error: 'Age must be between 18 and 100'
    });
  }
  
  // Validation passed
  const user = { name, email, age };
  res.status(201).json(user);
});
```

**Using Joi (popular validation library):**

**Install:**
```bash
npm install joi
```

**Usage:**

```javascript
const Joi = require('joi');

// Define schema
const userSchema = Joi.object({
  name: Joi.string().min(3).max(30).required(),
  email: Joi.string().email().required(),
  age: Joi.number().integer().min(18).max(100),
  password: Joi.string().min(8).required()
});

app.post('/api/users', (req, res) => {
  // Validate
  const { error, value } = userSchema.validate(req.body);
  
  if (error) {
    return res.status(400).json({
      error: error.details[0].message
    });
  }
  
  // Use validated data
  const user = value;
  res.status(201).json(user);
});
```

**Validation middleware:**

```javascript
const validate = (schema) => {
  return (req, res, next) => {
    const { error } = schema.validate(req.body);
    
    if (error) {
      return res.status(400).json({
        error: error.details[0].message
      });
    }
    
    next();
  };
};

// Use middleware
app.post('/api/users', validate(userSchema), (req, res) => {
  // Body is already validated
  const user = req.body;
  res.status(201).json(user);
});
```

**Complex validation:**

```javascript
const productSchema = Joi.object({
  name: Joi.string().required(),
  price: Joi.number().positive().required(),
  category: Joi.string().valid('electronics', 'clothing', 'food').required(),
  tags: Joi.array().items(Joi.string()),
  inStock: Joi.boolean(),
  specifications: Joi.object({
    weight: Joi.number(),
    dimensions: Joi.object({
      length: Joi.number(),
      width: Joi.number(),
      height: Joi.number()
    })
  })
});
```

**Using express-validator:**

**Install:**
```bash
npm install express-validator
```

**Usage:**

```javascript
const { body, validationResult } = require('express-validator');

app.post('/api/users',
  // Validation rules
  body('name').notEmpty().withMessage('Name is required')
    .isLength({ min: 3 }).withMessage('Name must be at least 3 characters'),
  body('email').isEmail().withMessage('Invalid email'),
  body('age').optional().isInt({ min: 18, max: 100 })
    .withMessage('Age must be between 18 and 100'),
  body('password').isLength({ min: 8 })
    .withMessage('Password must be at least 8 characters'),
  
  // Handler
  (req, res) => {
    const errors = validationResult(req);
    
    if (!errors.isEmpty()) {
      return res.status(400).json({ errors: errors.array() });
    }
    
    const user = req.body;
    res.status(201).json(user);
  }
);
```

**Validation middleware (express-validator):**

```javascript
const { body, validationResult } = require('express-validator');

const validateUser = [
  body('name').notEmpty().isLength({ min: 3 }),
  body('email').isEmail(),
  body('password').isLength({ min: 8 }),
  
  (req, res, next) => {
    const errors = validationResult(req);
    
    if (!errors.isEmpty()) {
      return res.status(400).json({ errors: errors.array() });
    }
    
    next();
  }
];

app.post('/api/users', validateUser, (req, res) => {
  // Body is validated
  res.status(201).json(req.body);
});
```

**Interview tip:** Always validate user input. Use validation libraries like Joi or express-validator for cleaner code. Return 400 status for validation errors. Create reusable validation middleware. Never trust client-side validation alone."

---

## Sessions & Security

### Q38: Sessions and Cookies

**How to Answer:**

"Sessions and cookies store user state across requests. Cookies store data on client, sessions store data on server.

**Cookies:**

Small pieces of data stored in browser.

```javascript
// Set cookie
app.get('/set-cookie', (req, res) => {
  res.cookie('username', 'john', {
    maxAge: 24 * 60 * 60 * 1000,  // 1 day
    httpOnly: true,                 // Not accessible via JS
    secure: false                   // true for HTTPS only
  });
  res.send('Cookie set');
});

// Read cookie (needs cookie-parser)
npm install cookie-parser

const cookieParser = require('cookie-parser');
app.use(cookieParser());

app.get('/get-cookie', (req, res) => {
  const username = req.cookies.username;
  res.send(`Username: ${username}`);
});

// Clear cookie
app.get('/clear-cookie', (req, res) => {
  res.clearCookie('username');
  res.send('Cookie cleared');
});
```

**Sessions:**

Store user data on server, only session ID in cookie.

**Install:**
```bash
npm install express-session
```

**Usage:**

```javascript
const session = require('express-session');

app.use(session({
  secret: 'your-secret-key',      // Used to sign session ID
  resave: false,                   // Don't save session if not modified
  saveUninitialized: false,        // Don't create session until stored
  cookie: {
    maxAge: 24 * 60 * 60 * 1000   // 1 day
  }
}));

// Set session data
app.post('/login', (req, res) => {
  const { username, password } = req.body;
  
  // Verify credentials (simplified)
  if (username === 'john' && password === 'password') {
    req.session.user = {
      id: 1,
      username: username
    };
    res.json({ message: 'Logged in' });
  } else {
    res.status(401).json({ error: 'Invalid credentials' });
  }
});

// Read session data
app.get('/profile', (req, res) => {
  if (!req.session.user) {
    return res.status(401).json({ error: 'Not logged in' });
  }
  
  res.json({ user: req.session.user });
});

// Destroy session (logout)
app.post('/logout', (req, res) => {
  req.session.destroy((err) => {
    if (err) {
      return res.status(500).json({ error: 'Logout failed' });
    }
    res.json({ message: 'Logged out' });
  });
});
```

**Session authentication example:**

```javascript
// Middleware to check if logged in
const requireLogin = (req, res, next) => {
  if (!req.session.user) {
    return res.status(401).json({ error: 'Login required' });
  }
  next();
};

// Protected route
app.get('/dashboard', requireLogin, (req, res) => {
  res.json({
    message: 'Dashboard',
    user: req.session.user
  });
});
```

**Cookies vs Sessions:**

| Feature | Cookies | Sessions |
|---------|---------|----------|
| Storage | Client (browser) | Server |
| Size limit | 4KB | No limit |
| Security | Less secure | More secure |
| Data type | String only | Any type |
| Speed | Faster | Slower (server lookup) |

**When to use:**

**Cookies:**
- Simple data (theme, language)
- Don't need security
- Persistent across sessions

**Sessions:**
- Sensitive data (user info)
- Authentication
- Shopping cart
- Need security

**Interview tip:** Cookies store data on client (browser), sessions store on server. Use sessions for sensitive data. Session ID stored in cookie. express-session package for sessions. Always use httpOnly and secure flags for security."

---

### Q39: Environment Variables (.env)

**How to Answer:**

"Environment variables store configuration separate from code. They keep sensitive data (API keys, passwords) out of version control.

**Why use .env?**

❌ Bad - Hardcoded secrets:
```javascript
const dbUrl = 'mongodb://username:password@localhost/mydb';
const jwtSecret = 'mysecretkey123';
// Exposed in GitHub!
```

✅ Good - Environment variables:
```javascript
const dbUrl = process.env.DB_URL;
const jwtSecret = process.env.JWT_SECRET;
// Secrets not in code!
```

**Using dotenv:**

**Install:**
```bash
npm install dotenv
```

**Create .env file:**
```
# .env file
PORT=3000
NODE_ENV=development

# Database
DB_URL=mongodb://localhost:27017/myapp
DB_NAME=myapp

# JWT
JWT_SECRET=your_super_secret_key_here
JWT_EXPIRE=7d

# Email
EMAIL_USER=your@email.com
EMAIL_PASS=your_email_password

# API Keys
STRIPE_API_KEY=sk_test_xyz123
AWS_ACCESS_KEY=AKIAIOSFODNN7EXAMPLE
```

**Usage in code:**

```javascript
// Load at the very top of entry file
require('dotenv').config();

const express = require('express');
const mongoose = require('mongoose');

const app = express();

// Access env variables
const PORT = process.env.PORT || 3000;
const DB_URL = process.env.DB_URL;
const JWT_SECRET = process.env.JWT_SECRET;

// Connect database
mongoose.connect(DB_URL);

// Use in routes
app.post('/login', async (req, res) => {
  const token = jwt.sign(
    { userId: user._id },
    process.env.JWT_SECRET,  // From .env
    { expiresIn: process.env.JWT_EXPIRE }
  );
  res.json({ token });
});

app.listen(PORT, () => {
  console.log(`Server on port ${PORT}`);
});
```

**Different environments:**

**.env.development:**
```
PORT=3000
DB_URL=mongodb://localhost:27017/myapp-dev
NODE_ENV=development
```

**.env.production:**
```
PORT=5000
DB_URL=mongodb://prod-server:27017/myapp
NODE_ENV=production
```

**Load based on environment:**

```javascript
const env = process.env.NODE_ENV || 'development';
require('dotenv').config({ path: `.env.${env}` });
```

**.gitignore (CRITICAL!):**

```
# .gitignore
node_modules/
.env
.env.development
.env.production
```

**.env.example (commit this):**

```
# .env.example - Template for .env file
PORT=3000
NODE_ENV=development

DB_URL=your_database_url_here
DB_NAME=your_database_name

JWT_SECRET=your_jwt_secret_here
JWT_EXPIRE=7d

EMAIL_USER=your_email
EMAIL_PASS=your_password
```

**Validation:**

```javascript
// Ensure required env variables exist
const requiredEnv = [
  'PORT',
  'DB_URL',
  'JWT_SECRET'
];

requiredEnv.forEach((key) => {
  if (!process.env[key]) {
    console.error(`Missing required environment variable: ${key}`);
    process.exit(1);
  }
});
```

**Best practices:**

```javascript
// ✅ Good - Use env variables
const secret = process.env.JWT_SECRET;

// ❌ Bad - Hardcode sensitive data
const secret = 'mysecretkey123';

// ✅ Good - Provide defaults for non-sensitive
const port = process.env.PORT || 3000;

// ✅ Good - Descriptive names
DB_URL, JWT_SECRET, API_KEY

// ❌ Bad - Generic names
URL, SECRET, KEY
```

**Interview tip:** Use .env files for configuration and secrets. Load with dotenv package at app start. Never commit .env to Git - add to .gitignore. Provide .env.example template. Access with process.env.VARIABLE_NAME. Different .env files for dev/prod."

---

### Q40: Security Best Practices

**How to Answer:**

"Security is critical for production applications. Follow these practices to protect your API.

**1. Use Helmet (Security headers):**

```bash
npm install helmet
```

```javascript
const helmet = require('helmet');
app.use(helmet());

// Sets multiple security headers:
// - X-Content-Type-Options
// - X-Frame-Options
// - Strict-Transport-Security
// - etc.
```

**2. Rate Limiting:**

```bash
npm install express-rate-limit
```

```javascript
const rateLimit = require('express-rate-limit');

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100, // 100 requests per window
  message: 'Too many requests, please try again later'
});

// Apply to all routes
app.use(limiter);

// Or specific routes
app.use('/api/', limiter);

// Stricter for auth routes
const authLimiter = rateLimit({
  windowMs: 15 * 60 * 1000,
  max: 5
});

app.post('/api/login', authLimiter, loginController);
```

**3. Input Validation & Sanitization:**

```bash
npm install express-validator
```

```javascript
const { body, validationResult } = require('express-validator');

app.post('/api/users',
  body('email').isEmail().normalizeEmail(),
  body('name').trim().escape(),
  (req, res) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
      return res.status(400).json({ errors: errors.array() });
    }
    // Process sanitized data
  }
);
```

**4. Password Hashing (NEVER store plain text):**

```javascript
const bcrypt = require('bcrypt');

// Hash password
const hashedPassword = await bcrypt.hash(password, 10);

// ❌ NEVER do this
const user = { password: 'plaintext123' };

// ✅ ALWAYS hash
const user = { password: hashedPassword };
```

**5. JWT Best Practices:**

```javascript
// Use strong secret
const token = jwt.sign(
  { userId: user._id },
  process.env.JWT_SECRET,  // Strong, random secret
  { expiresIn: '7d' }      // Set expiration
);

// Verify token
const authMiddleware = (req, res, next) => {
  try {
    const token = req.headers.authorization?.replace('Bearer ', '');
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.user = decoded;
    next();
  } catch (error) {
    res.status(401).json({ error: 'Invalid token' });
  }
};
```

**6. HTTPS Only (in production):**

```javascript
// Redirect HTTP to HTTPS
if (process.env.NODE_ENV === 'production') {
  app.use((req, res, next) => {
    if (req.header('x-forwarded-proto') !== 'https') {
      res.redirect(`https://${req.header('host')}${req.url}`);
    } else {
      next();
    }
  });
}
```

**7. CORS Configuration:**

```javascript
const corsOptions = {
  origin: process.env.FRONTEND_URL, // Specific origin
  credentials: true,
  optionsSuccessStatus: 200
};

app.use(cors(corsOptions));
```

**8. SQL/NoSQL Injection Prevention:**

```javascript
// ✅ Good - Use parameterized queries
User.findOne({ email: req.body.email });

// ❌ Bad - String concatenation
User.findOne({ $where: `this.email == '${req.body.email}'` });
```

**9. Environment Variables:**

```javascript
// ❌ Bad - Hardcoded secrets
const secret = 'mysecret123';

// ✅ Good - Use .env
const secret = process.env.JWT_SECRET;
```

**10. Error Handling (Don't expose details):**

```javascript
app.use((err, req, res, next) => {
  console.error(err.stack);
  
  // ❌ Bad - Exposes details
  res.status(500).json({ error: err.stack });
  
  // ✅ Good - Generic message
  res.status(500).json({ 
    error: process.env.NODE_ENV === 'production' 
      ? 'Internal server error'
      : err.message
  });
});
```

**11. MongoDB Security:**

```javascript
// Create user with limited permissions
// In mongo shell:
use myapp
db.createUser({
  user: "appUser",
  pwd: "securePassword",
  roles: [{ role: "readWrite", db: "myapp" }]
})

// Don't use admin credentials in app
```

**12. Dependencies Security:**

```bash
# Check for vulnerabilities
npm audit

# Fix vulnerabilities
npm audit fix

# Update packages
npm update
```

**Security checklist:**

```javascript
const express = require('express');
const helmet = require('helmet');
const cors = require('cors');
const rateLimit = require('express-rate-limit');
const mongoSanitize = require('express-mongo-sanitize');

const app = express();

// Security middleware
app.use(helmet());                    // Security headers
app.use(cors(corsOptions));           // CORS
app.use(express.json({ limit: '10kb' })); // Limit body size
app.use(mongoSanitize());            // Prevent NoSQL injection
app.use(rateLimit({
  windowMs: 15 * 60 * 1000,
  max: 100
}));

// HTTPS only in production
if (process.env.NODE_ENV === 'production') {
  app.set('trust proxy', 1);
}

// Routes with authentication
app.use('/api', requireAuth, routes);

// Error handler (no details in production)
app.use((err, req, res, next) => {
  const message = process.env.NODE_ENV === 'production'
    ? 'Something went wrong'
    : err.message;
  
  res.status(err.statusCode || 500).json({ error: message });
});
```

**Interview tip:** Use helmet for security headers, rate limiting to prevent abuse, always hash passwords, validate/sanitize input, use JWT with expiration, enable HTTPS in production, configure CORS properly, don't expose error details, use environment variables for secrets, keep dependencies updated."

---

## File Handling & Advanced

### Q41: File Upload (Multer)

**How to Answer:**

"Multer is middleware for handling file uploads in Express.

**Install:**
```bash
npm install multer
```

**Basic file upload:**

```javascript
const express = require('express');
const multer = require('multer');
const path = require('path');

const app = express();

// Configure storage
const storage = multer.diskStorage({
  destination: function(req, file, cb) {
    cb(null, 'uploads/');  // Save to uploads folder
  },
  filename: function(req, file, cb) {
    // Create unique filename
    const uniqueSuffix = Date.now() + '-' + Math.round(Math.random() * 1E9);
    cb(null, file.fieldname + '-' + uniqueSuffix + path.extname(file.originalname));
  }
});

const upload = multer({ storage: storage });

// Single file upload
app.post('/upload', upload.single('avatar'), (req, res) => {
  if (!req.file) {
    return res.status(400).json({ error: 'No file uploaded' });
  }
  
  res.json({
    message: 'File uploaded',
    filename: req.file.filename,
    path: req.file.path,
    size: req.file.size
  });
});

// Multiple files
app.post('/upload-multiple', upload.array('photos', 5), (req, res) => {
  if (!req.files || req.files.length === 0) {
    return res.status(400).json({ error: 'No files uploaded' });
  }
  
  const files = req.files.map(file => ({
    filename: file.filename,
    size: file.size
  }));
  
  res.json({ message: 'Files uploaded', files });
});
```

**File validation:**

```javascript
const upload = multer({
  storage: storage,
  limits: {
    fileSize: 5 * 1024 * 1024  // 5MB limit
  },
  fileFilter: function(req, file, cb) {
    // Allow only images
    const filetypes = /jpeg|jpg|png|gif/;
    const mimetype = filetypes.test(file.mimetype);
    const extname = filetypes.test(path.extname(file.originalname).toLowerCase());
    
    if (mimetype && extname) {
      return cb(null, true);
    }
    
    cb(new Error('Only image files are allowed'));
  }
});
```

**Complete example with user profile:**

```javascript
// Upload profile picture
app.post('/api/users/profile-picture', 
  authenticate,  // Check if logged in
  upload.single('profilePicture'),
  async (req, res) => {
    try {
      if (!req.file) {
        return res.status(400).json({ error: 'No file uploaded' });
      }
      
      // Update user with image path
      const user = await User.findById(req.user.id);
      user.profilePicture = req.file.filename;
      await user.save();
      
      res.json({
        message: 'Profile picture updated',
        filename: req.file.filename
      });
    } catch (error) {
      res.status(500).json({ error: error.message });
    }
  }
);

// Serve uploaded files
app.use('/uploads', express.static('uploads'));
```

**Interview tip:** Multer handles file uploads. Configure storage (destination and filename). Use upload.single() for one file, upload.array() for multiple. Validate file type and size. Store file path in database. Serve files with express.static()."

---

### Q45: Logging

**How to Answer:**

"Logging helps track application behavior, debug issues, and monitor production.

**Console logging (basic):**

```javascript
// Development
console.log('Server started');
console.error('Error occurred');
console.warn('Warning message');

// Problems:
// - No timestamps
// - No log levels
// - Hard to filter
// - Lost when server restarts
```

**Morgan (HTTP request logging):**

```bash
npm install morgan
```

```javascript
const morgan = require('morgan');

// Development - detailed
app.use(morgan('dev'));
// GET /api/users 200 15.123 ms - 1234

// Production - minimal
app.use(morgan('combined'));

// Custom format
app.use(morgan(':method :url :status :response-time ms'));
```

**Winston (Advanced logging):**

```bash
npm install winston
```

```javascript
const winston = require('winston');

// Create logger
const logger = winston.createLogger({
  level: 'info',
  format: winston.format.json(),
  transports: [
    // Write to files
    new winston.transports.File({ 
      filename: 'logs/error.log', 
      level: 'error' 
    }),
    new winston.transports.File({ 
      filename: 'logs/combined.log' 
    })
  ]
});

// Console in development
if (process.env.NODE_ENV !== 'production') {
  logger.add(new winston.transports.Console({
    format: winston.format.simple()
  }));
}

// Use logger
logger.info('Server started on port 3000');
logger.error('Database connection failed', { error: err });
logger.warn('Deprecated API used');
```

**Usage in Express:**

```javascript
// Log requests
app.use((req, res, next) => {
  logger.info(`${req.method} ${req.url}`);
  next();
});

// Log errors
app.use((err, req, res, next) => {
  logger.error('Error occurred', {
    error: err.message,
    stack: err.stack,
    url: req.url,
    method: req.method
  });
  
  res.status(500).json({ error: 'Internal server error' });
});
```

**Interview tip:** Use Morgan for HTTP logging, Winston for application logging. Log to files in production. Include timestamps and log levels. Never log sensitive data (passwords, tokens)."

---

### Q48: Deployment Basics

**How to Answer:**

"Deploying Node.js apps involves preparing code for production and hosting on a server.

**Preparation checklist:**

**1. Environment variables:**

```javascript
// Use .env for production
DB_URL=production_db_url
JWT_SECRET=strong_random_secret
NODE_ENV=production
PORT=5000
```

**2. package.json scripts:**

```json
{
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js",
    "production": "NODE_ENV=production node app.js"
  }
}
```

**3. Error handling:**

```javascript
// Global error handler
process.on('uncaughtException', (err) => {
  console.error('Uncaught Exception:', err);
  process.exit(1);
});

process.on('unhandledRejection', (reason, promise) => {
  console.error('Unhandled Rejection:', reason);
  process.exit(1);
});
```

**4. Security:**

```javascript
// Enable in production
if (process.env.NODE_ENV === 'production') {
  app.use(helmet());
  app.set('trust proxy', 1);
}
```

**5. Process manager (PM2):**

```bash
# Install PM2 globally
npm install -g pm2

# Start app
pm2 start app.js --name myapp

# Start with env
pm2 start app.js --env production

# Auto-restart on crash
pm2 restart myapp

# View logs
pm2 logs myapp

# Monitor
pm2 monit

# Startup script (auto-start on server reboot)
pm2 startup
pm2 save
```

**Deployment platforms:**

**Heroku:**
```bash
# Install Heroku CLI
# Login
heroku login

# Create app
heroku create myapp

# Set env variables
heroku config:set DB_URL=mongodb://...
heroku config:set JWT_SECRET=secret

# Deploy
git push heroku main

# View logs
heroku logs --tail
```

**Render/Railway:**
- Connect GitHub repo
- Set environment variables in dashboard
- Auto-deploy on push

**VPS (DigitalOcean, AWS EC2):**
```bash
# SSH into server
ssh user@server-ip

# Install Node.js
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# Clone repo
git clone https://github.com/user/repo
cd repo

# Install dependencies
npm install --production

# Setup PM2
pm2 start app.js
pm2 startup
pm2 save

# Setup Nginx (reverse proxy)
sudo apt install nginx
# Configure Nginx to proxy to Node app
```

**Interview tip:** Use PM2 for process management in production. Set NODE_ENV=production. Store secrets in environment variables. Use platforms like Heroku, Render, or VPS. Setup error handling and logging. Enable security middleware."

---

### Q51: API Documentation

**How to Answer:**

"API documentation describes endpoints, parameters, and responses. It helps other developers use your API.

**Manual documentation (README):**

```markdown
## API Documentation

### Base URL
`http://localhost:3000/api`

### Authentication
Include JWT token in Authorization header:
```
Authorization: Bearer <token>
```

### Endpoints

#### Get All Users
- **URL:** `/users`
- **Method:** `GET`
- **Auth required:** Yes
- **Query Parameters:**
  - `page` (optional): Page number
  - `limit` (optional): Items per page
- **Success Response:**
  - **Code:** 200
  - **Content:** 
    ```json
    {
      "users": [
        { "id": 1, "name": "John", "email": "john@email.com" }
      ]
    }
    ```

#### Create User
- **URL:** `/users`
- **Method:** `POST`
- **Auth required:** No
- **Body:**
  ```json
  {
    "name": "John",
    "email": "john@email.com",
    "password": "password123"
  }
  ```
- **Success Response:**
  - **Code:** 201
  - **Content:** `{ "id": 1, "name": "John", "email": "john@email.com" }`
```

**Postman:**

- Create collection
- Add all endpoints
- Add examples
- Export and share

**Swagger/OpenAPI:**

```bash
npm install swagger-ui-express swagger-jsdoc
```

```javascript
const swaggerUi = require('swagger-ui-express');
const swaggerJsdoc = require('swagger-jsdoc');

const options = {
  definition: {
    openapi: '3.0.0',
    info: {
      title: 'My API',
      version: '1.0.0',
      description: 'API documentation'
    },
    servers: [
      { url: 'http://localhost:3000' }
    ]
  },
  apis: ['./routes/*.js']
};

const specs = swaggerJsdoc(options);
app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(specs));

// In route files, add JSDoc comments:
/**
 * @swagger
 * /api/users:
 *   get:
 *     summary: Get all users
 *     responses:
 *       200:
 *         description: List of users
 */
app.get('/api/users', getUsers);
```

**Interview tip:** Document all endpoints with URL, method, parameters, and responses. Use tools like Postman, Swagger, or README. Include authentication requirements and example requests/responses."

---

## Summary - Part 2

**Key Topics Covered:**

**Request/Response:**
- Detailed req/res objects
- express.Router()
- HTTP methods (GET, POST, PUT, PATCH, DELETE)
- Request data (params, query, body)

**Advanced API:**
- CORS configuration
- Request validation (Joi, express-validator)

**Sessions & Security:**
- Sessions and cookies
- Environment variables
- Security best practices (helmet, rate limiting)

**File Handling:**
- File uploads with Multer
- File operations

**Production:**
- Logging (Morgan, Winston)
- Deployment (PM2, Heroku, VPS)
- API documentation

**Remember:** This is Part 2 - combine with Part 1 for complete preparation!

Good luck with your interviews! 