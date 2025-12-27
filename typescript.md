# TypeScript Interview Preparation Guide
*Essential TypeScript Concepts for JavaScript Developers*

**For Students:** This guide assumes you know JavaScript. Part 1 is in read-aloud interview format. Part 2 has quick-reference questions.

Link to Typescript Docs:  https://docs.google.com/document/d/1g9GhDW_WOgg8UqmqvTeESFR5oLLjHB5G/edit

## Table of Contents

### Part 1: Read-Aloud Interview Questions

#### TypeScript Basics
1. [What is TypeScript?](#q1-what-is-typescript)
2. [TypeScript vs JavaScript](#q2-typescript-vs-javascript)
3. [How to Set Up TypeScript](#q3-how-to-set-up-typescript)
4. [Basic Types](#q4-basic-types)
5. [Type Annotations vs Type Inference](#q5-type-annotations-vs-type-inference)
6. [Any vs Unknown vs Never](#q6-any-vs-unknown-vs-never)
7. [Union Types](#q7-union-types)
8. [Literal Types](#q8-literal-types)

#### Objects and Functions
9. [Object Types](#q9-object-types)
10. [Interfaces](#q10-interfaces)
11. [Type Aliases](#q11-type-aliases)
12. [Interface vs Type](#q12-interface-vs-type)
13. [Optional and Readonly Properties](#q13-optional-and-readonly-properties)
14. [Function Types](#q14-function-types)

#### Arrays and Complex Types
15. [Array Types](#q15-array-types)
16. [Tuples](#q16-tuples)
17. [Enums](#q17-enums)
18. [Intersection Types](#q18-intersection-types)

#### Advanced Concepts
19. [Type Guards and Narrowing](#q19-type-guards-and-narrowing)
20. [Generics Basics](#q20-generics-basics)
21. [Generic Constraints](#q21-gener
## Part 1: Read-Aloud Interview Questions

### Q1: What is TypeScript?

**How to Answer:**

"TypeScript is JavaScript with a type system added on top. It's a superset of JavaScript developed by Microsoft that helps catch errors before you run your code.

**Key points:**

- TypeScript compiles to JavaScript - it's not a different language
- All valid JavaScript is valid TypeScript
- Adds optional static typing to JavaScript
- Provides better IDE support and autocomplete
- Helps catch bugs during development, not at runtime

**Basic example:**

```javascript
// JavaScript - no type checking
function add(a, b) {
    return a + b;
}

add(5, '10');  // Returns '510' - string concatenation (bug!)
```

```typescript
// TypeScript - with types
function add(a: number, b: number): number {
    return a + b;
}

add(5, '10');  // Error! '10' is not a number
```

**Why use TypeScript:**

1. **Catch errors early** - Before running code
2. **Better IDE support** - Autocomplete and IntelliSense
3. **Self-documenting code** - Types serve as documentation
4. **Easier refactoring** - Rename variables/functions safely
5. **Team collaboration** - Clear contracts between code

**TypeScript workflow:**

```
Write TypeScript (.ts) → Compile → JavaScript (.js) → Run in browser/Node
```

**Interview tip:** TypeScript is JavaScript with types. It compiles to regular JavaScript. Main benefit: catch errors during development instead of at runtime. If you know JavaScript, you already know 90% of TypeScript."

---

### Q2: TypeScript vs JavaScript

**How to Answer:**

"TypeScript is a superset of JavaScript that adds optional static typing. Here's how they differ:

**Key differences:**

| Feature | JavaScript | TypeScript |
|---------|-----------|------------|
| Type system | Dynamic (runtime) | Static (compile-time) |
| Error detection | At runtime | During development |
| File extension | .js | .ts |
| Compilation | Not needed | Compiles to JS |
| IDE support | Basic | Advanced (autocomplete) |
| Learning curve | Easier | Slightly steeper |

**Examples:**

**Variables:**

```javascript
// JavaScript
let name = 'John';
let age = 30;
name = 123;  // OK in JS (but probably a bug)
```

```typescript
// TypeScript
let name: string = 'John';
let age: number = 30;
name = 123;  // Error! Type 'number' is not assignable to type 'string'
```

**Functions:**

```javascript
// JavaScript
function greet(name) {
    return 'Hello ' + name;
}

greet(123);  // Returns 'Hello 123' - no error
```

```typescript
// TypeScript
function greet(name: string): string {
    return 'Hello ' + name;
}

greet(123);  // Error! Argument of type 'number' is not assignable to 'string'
```

**Objects:**

```javascript
// JavaScript - no shape enforcement
const user = {
    name: 'Alice',
    age: 25
};

user.email = 'alice@email.com';  // OK
user.age = 'twenty-five';  // OK (but probably wrong)
```

```typescript
// TypeScript - defined shape
interface User {
    name: string;
    age: number;
}

const user: User = {
    name: 'Alice',
    age: 25
};

user.email = 'alice@email.com';  // Error! Property doesn't exist
user.age = 'twenty-five';  // Error! Type mismatch
```

**Advantages of TypeScript:**

- Catches bugs before running code
- Better refactoring tools
- Improved documentation
- Scales better for large projects
- Better team collaboration

**Advantages of JavaScript:**

- Simpler to learn
- No compilation step
- Faster to prototype
- No setup required
- Smaller bundle size

**Interview tip:** TypeScript adds types to JavaScript. Main difference: errors caught at compile-time vs runtime. All JavaScript code is valid TypeScript. TypeScript compiles to JavaScript, so it works everywhere JS works."

---

### Q3: How to Set Up TypeScript

**How to Answer:**

"Setting up TypeScript is straightforward. You need Node.js installed, then install TypeScript globally or per project.

**Installation:**

```bash
# Install TypeScript globally
npm install -g typescript

# Check version
tsc --version

# Or install in project
npm init -y
npm install typescript --save-dev
```

**Initialize TypeScript:**

```bash
# Create tsconfig.json
tsc --init
```

**Basic tsconfig.json:**

```json
{
  "compilerOptions": {
    "target": "ES2020",           // JavaScript version to compile to
    "module": "commonjs",          // Module system (commonjs for Node)
    "outDir": "./dist",            // Output folder for compiled JS
    "rootDir": "./src",            // Source folder for TS files
    "strict": true,                // Enable all strict type checks
    "esModuleInterop": true,       // Better ES6 import support
    "skipLibCheck": true           // Skip type checking of library files
  },
  "include": ["src/**/*"],         // Files to compile
  "exclude": ["node_modules"]      // Files to exclude
}
```

**Project structure:**

```
my-project/
├── src/
│   ├── index.ts      # TypeScript source files
│   └── utils.ts
├── dist/             # Compiled JavaScript (auto-generated)
│   ├── index.js
│   └── utils.js
├── tsconfig.json     # TypeScript configuration
├── package.json
└── node_modules/
```

**Write TypeScript code:**

**src/index.ts:**
```typescript
function greet(name: string): string {
    return `Hello, ${name}!`;
}

const message = greet('Alice');
console.log(message);
```

**Compile TypeScript:**

```bash
# Compile once
tsc

# Watch mode (auto-compile on save)
tsc --watch

# Compile specific file
tsc src/index.ts
```

**Run compiled JavaScript:**

```bash
node dist/index.js
```

**Using ts-node (run TypeScript directly):**

```bash
# Install ts-node
npm install -g ts-node

# Run TypeScript file directly (no compilation needed)
ts-node src/index.ts
```

**Package.json scripts:**

```json
{
  "scripts": {
    "build": "tsc",
    "start": "node dist/index.js",
    "dev": "ts-node src/index.ts",
    "watch": "tsc --watch"
  }
}
```

```bash
npm run build   # Compile TypeScript
npm start       # Run compiled JavaScript
npm run dev     # Run TypeScript directly
npm run watch   # Auto-compile on changes
```

**Important tsconfig.json options:**

- **strict: true** - Enables all strict type checking (recommended)
- **target** - JavaScript version (ES2020, ES2021, ESNext)
- **module** - Module system (commonjs for Node, es2015 for browsers)
- **outDir** - Where compiled JS goes
- **rootDir** - Where TS source files are
- **noImplicitAny** - Error on variables with implied 'any' type

**Interview tip:** Install with npm install typescript. Create tsconfig.json with tsc --init. Write .ts files, compile with tsc, run with node. Use ts-node to run TypeScript directly without compiling. Enable strict mode for best type checking."

---

### Q4: Basic Types

**How to Answer:**

"TypeScript has all JavaScript types plus a few extras for better type safety.

**Primitive types:**

```typescript
// string - Text values
let name: string = 'Alice';
let message: string = 'Hello';

// number - All numbers (integers and decimals)
let age: number = 25;
let price: number = 99.99;
let negative: number = -10;

// boolean - true or false
let isActive: boolean = true;
let hasAccess: boolean = false;

// null and undefined
let nothing: null = null;
let notDefined: undefined = undefined;
```

**Special TypeScript types:**

```typescript
// any - Turns off type checking (avoid when possible)
let anything: any = 'hello';
anything = 42;        // OK
anything = true;      // OK
anything = {};        // OK - any accepts everything

// unknown - Safer version of any (must check type before use)
let mystery: unknown = 'hello';

// mystery.toUpperCase();  // Error! Must check type first

if (typeof mystery === 'string') {
    mystery.toUpperCase();  // OK now
}

// void - For functions that don't return anything
function logMessage(msg: string): void {
    console.log(msg);
    // No return statement
}

// never - For functions that never return
function throwError(message: string): never {
    throw new Error(message);
    // Never reaches end
}

function infiniteLoop(): never {
    while (true) {
        // Never exits
    }
}
```

**Complete example:**

```typescript
// String
let username: string = 'john_doe';
let email: string = 'john@email.com';

// Number
let userId: number = 12345;
let temperature: number = 98.6;
let score: number = -5;

// Boolean
let isLoggedIn: boolean = true;
let hasPermission: boolean = false;

// Void (functions with no return)
function sayHello(name: string): void {
    console.log(`Hello, ${name}`);
}

// Any (use sparingly!)
let flexible: any = 'start as string';
flexible = 42;  // Can change to number
flexible = true;  // Can change to boolean

// Unknown (safer than any)
let userInput: unknown = getUserInput();

// Must check type before using
if (typeof userInput === 'string') {
    console.log(userInput.toUpperCase());
}
```

**Type annotations vs values:**

```typescript
// Type annotation          Value
let name: string         = 'Alice';
     ↑                      ↑
   Type                   Value
```

**When to use each:**

| Type | When to Use |
|------|-------------|
| string | Text, messages, names |
| number | Numbers, IDs, prices |
| boolean | true/false flags |
| any | Avoid! Use only when migrating JS |
| unknown | When type is truly unknown |
| void | Functions with no return |
| never | Functions that throw or never end |

**Interview tip:** Main types: string, number, boolean (same as JavaScript). Special TypeScript types: any (avoid), unknown (safer than any), void (no return), never (never returns). Use unknown instead of any when type is truly unknown - it's safer."

---

### Q5: Type Annotations vs Type Inference

**How to Answer:**

"TypeScript can automatically figure out types (inference) or you can explicitly specify them (annotations). Both are valid approaches.

**Type Annotations (explicit):**

You explicitly tell TypeScript the type:

```typescript
// With type annotations
let name: string = 'Alice';
let age: number = 25;
let isStudent: boolean = true;
```

**Type Inference (automatic):**

TypeScript figures out the type from the value:

```typescript
// TypeScript infers types automatically
let name = 'Alice';       // Inferred as string
let age = 25;             // Inferred as number
let isStudent = true;     // Inferred as boolean

// Hover over these in VS Code and you'll see the types!
```

**When TypeScript infers types:**

```typescript
// Variable initialization
let message = 'Hello';  // string

// Function returns
function add(a: number, b: number) {
    return a + b;  // Return type inferred as number
}

// Arrays
let numbers = [1, 2, 3];  // number[]
let names = ['Alice', 'Bob'];  // string[]

// Objects
let user = {
    name: 'Alice',  // string
    age: 25         // number
};
```

**When to use annotations:**

```typescript
// 1. Function parameters (must annotate)
function greet(name: string) {  // Must annotate parameter
    return `Hello, ${name}`;
}

// 2. When declaring without initializing
let age: number;
age = 25;  // Assigned later

// 3. When you want to be explicit
let userId: string | number = '123';  // Can be string or number

// 4. Return types (optional but recommended)
function getUser(): User {  // Explicit return type
    return { id: 1, name: 'Alice' };
}
```

**Comparison:**

```typescript
// Type annotation - explicit
function add1(a: number, b: number): number {
    return a + b;
}

// Type inference - implicit (TypeScript figures it out)
function add2(a: number, b: number) {
    return a + b;  // Return type inferred as number
}

// Both are equivalent!
```

**Best practices:**

```typescript
// ✅ Good - Let inference work
let name = 'Alice';
let age = 25;

// ❌ Redundant - TypeScript already knows
let name: string = 'Alice';
let age: number = 25;

// ✅ Good - Annotate function parameters
function greet(name: string) {
    return `Hello, ${name}`;
}

// ✅ Good - Annotate return type for clarity
function getTotal(items: number[]): number {
    return items.reduce((sum, item) => sum + item, 0);
}

// ✅ Good - Annotate when initializing later
let userId: string;
// ... some code ...
userId = 'abc123';
```

**Hover to see inferred types:**

```typescript
let message = 'Hello';
//  ↑ Hover in VS Code shows: let message: string

let numbers = [1, 2, 3];
//  ↑ Hover shows: let numbers: number[]
```

**Interview tip:** Type inference means TypeScript automatically figures out types. Type annotations mean you explicitly specify types. Use inference when possible (cleaner code). Always annotate function parameters. Optionally annotate return types for clarity. Let TypeScript do the work - don't over-annotate!"

---

### Q6: Any vs Unknown vs Never

**How to Answer:**

"These are three special TypeScript types that handle different situations. Each has specific use cases.

**Any - Opt out of type checking:**

```typescript
let anything: any = 'hello';
anything = 42;        // OK
anything = true;      // OK
anything = {};        // OK
anything.foo.bar();   // OK (but might crash at runtime!)

// any turns off type checking completely
```

**Problems with any:**

```typescript
function processData(data: any) {
    return data.toUpperCase();  // No error, but crashes if data is number
}

processData(42);  // Runtime error! Numbers don't have toUpperCase
```

**Unknown - Safer version of any:**

```typescript
let mystery: unknown = 'hello';

// Must check type before using
// mystery.toUpperCase();  // Error! Type is unknown

// Type guard required
if (typeof mystery === 'string') {
    mystery.toUpperCase();  // OK now!
}
```

**Unknown forces type checking:**

```typescript
function processData(data: unknown) {
    // Must check type first
    if (typeof data === 'string') {
        return data.toUpperCase();  // Safe!
    }
    
    if (typeof data === 'number') {
        return data.toFixed(2);  // Safe!
    }
    
    throw new Error('Unsupported type');
}
```

**Never - For functions that never return:**

```typescript
// Function that throws error
function throwError(message: string): never {
    throw new Error(message);
    // Never reaches end of function
}

// Function with infinite loop
function infiniteLoop(): never {
    while (true) {
        console.log('Running forever');
    }
    // Never exits
}

// Exhaustive checking
type Shape = 'circle' | 'square';

function getArea(shape: Shape): number {
    switch (shape) {
        case 'circle':
            return 3.14;
        case 'square':
            return 4;
        default:
            const exhaustive: never = shape;  // Ensures all cases covered
            throw new Error('Unhandled case');
    }
}
```

**Comparison:**

| Type | Purpose | Can be assigned to | Type checking |
|------|---------|-------------------|---------------|
| any | Opt out | Anything | None |
| unknown | Unknown type | Unknown only | Required |
| never | Never returns | Nothing | Strict |

**When to use:**

**Use any:**
```typescript
// ❌ Avoid in new code
// ✅ OK when migrating from JavaScript gradually
// ✅ OK for truly dynamic data (rare)

let legacyData: any = getLegacyAPI();
```

**Use unknown:**
```typescript
// ✅ When type is genuinely unknown
// ✅ When receiving data from external source

async function fetchData(url: string): Promise<unknown> {
    const response = await fetch(url);
    return response.json();  // Don't know what API returns
}

const data = await fetchData('/api/data');

// Must validate before using
if (isUser(data)) {
    console.log(data.name);
}
```

**Use never:**
```typescript
// ✅ Functions that always throw
// ✅ Functions that never return
// ✅ Exhaustive type checking

function fail(message: string): never {
    throw new Error(message);
}
```

**Real-world example:**

```typescript
// API response with unknown data
interface ApiResponse {
    data: unknown;  // Could be anything
    status: number;
}

function handleResponse(response: ApiResponse) {
    // Must validate data
    if (typeof response.data === 'object' && response.data !== null) {
        const data = response.data as { name: string };
        console.log(data.name);
    }
}

// Error handling with never
function assertNever(value: never): never {
    throw new Error(`Unexpected value: ${value}`);
}

type Status = 'pending' | 'approved';

function handleStatus(status: Status) {
    switch (status) {
        case 'pending':
            return 'Waiting';
        case 'approved':
            return 'Done';
        default:
            return assertNever(status);  // Catches missing cases
    }
}
```

**Interview tip:** any disables type checking (avoid!). unknown is safer - requires type checking before use. never is for functions that don't return (throw errors or infinite loops). Use unknown instead of any when type is truly unknown. never ensures exhaustive checking in switch statements."

---

### Q7: Union Types

**How to Answer:**

"Union types let a variable be one of several types. It's like saying 'this OR that'.

**Basic union:**

```typescript
// Variable can be string OR number
let id: string | number;

id = 101;        // OK
id = 'ABC123';   // OK
// id = true;    // Error! boolean not in union
```

**Function with union parameter:**

```typescript
function printId(id: string | number) {
    console.log(`Your ID is: ${id}`);
}

printId(101);        // OK
printId('ABC123');   // OK
```

**Working with unions - Type narrowing:**

```typescript
function formatId(id: string | number): string {
    // Must check type before using type-specific methods
    if (typeof id === 'string') {
        return id.toUpperCase();  // OK - TypeScript knows it's string
    } else {
        return id.toFixed(0);  // OK - TypeScript knows it's number
    }
}

console.log(formatId('abc123'));  // 'ABC123'
console.log(formatId(42.7));      // '43'
```

**Common use case - Literal types:**

```typescript
// Union of specific string values
type Status = 'pending' | 'approved' | 'rejected';
type Direction = 'up' | 'down' | 'left' | 'right';

let orderStatus: Status = 'pending';  // OK
// orderStatus = 'invalid';  // Error! Not a valid Status

function move(direction: Direction) {
    console.log(`Moving ${direction}`);
}

move('up');     // OK
// move('diagonal');  // Error!
```

**Array with union:**

```typescript
// Array can contain numbers OR strings
let mixed: (number | string)[] = [1, 'two', 3, 'four'];

// OR using union with Array
let mixed2: Array<number | string> = [1, 'two', 3, 'four'];
```

**Object with union property:**

```typescript
interface User {
    id: number;
    name: string;
    age: number | null;  // Age can be number or null
}

const user1: User = { id: 1, name: 'Alice', age: 25 };
const user2: User = { id: 2, name: 'Bob', age: null };
```

**Multiple unions:**

```typescript
type ID = string | number;
type Result = 'success' | 'error' | 'pending';

function processRequest(id: ID, result: Result) {
    console.log(`Request ${id}: ${result}`);
}

processRequest(123, 'success');
processRequest('ABC', 'pending');
```

**Union with null and undefined:**

```typescript
// Function can return string or null
function getUser(id: number): string | null {
    if (id === 1) {
        return 'Alice';
    }
    return null;  // User not found
}

const user = getUser(1);

// Must check for null before using
if (user !== null) {
    console.log(user.toUpperCase());
}

// Or use optional chaining
console.log(user?.toUpperCase());
```

**Discriminated unions (pattern matching):**

```typescript
interface Success {
    status: 'success';
    data: string;
}

interface Error {
    status: 'error';
    message: string;
}

type Response = Success | Error;

function handleResponse(response: Response) {
    if (response.status === 'success') {
        console.log(response.data);  // TypeScript knows it's Success
    } else {
        console.log(response.message);  // TypeScript knows it's Error
    }
}
```

**Real-world examples:**

```typescript
// API response that can be different types
type ApiResponse = 
    | { success: true; data: User[] }
    | { success: false; error: string };

function handleApiResponse(response: ApiResponse) {
    if (response.success) {
        response.data.forEach(user => console.log(user.name));
    } else {
        console.error(response.error);
    }
}

// Event handlers
type MouseEvent = 'click' | 'mousedown' | 'mouseup';
type KeyboardEvent = 'keydown' | 'keyup' | 'keypress';
type Event = MouseEvent | KeyboardEvent;

function handleEvent(event: Event) {
    console.log(`Handling ${event}`);
}
```

**Interview tip:** Union types use | (pipe) to say 'this OR that'. Common pattern: string | number for flexible IDs. Literal unions like 'pending' | 'approved' limit values to specific strings. Must narrow type with typeof or checks before using type-specific methods. Great for API responses and status values."

---

### Q8: Literal Types

**How to Answer:**

"Literal types let you specify exact values a variable can have, not just the type. They're very useful for status values, directions, or any fixed set of options.

**String literals:**

```typescript
// Instead of accepting any string
let direction: 'up' | 'down' | 'left' | 'right';

direction = 'up';     // OK
direction = 'left';   // OK
// direction = 'diagonal';  // Error! Not a valid direction
```

**Number literals:**

```typescript
// Only specific numbers allowed
let diceRoll: 1 | 2 | 3 | 4 | 5 | 6;

diceRoll = 3;   // OK
// diceRoll = 7;   // Error!
```

**Boolean literals:**

```typescript
// Fixed boolean value
let alwaysTrue: true = true;
// alwaysTrue = false;  // Error!
```

**Type alias with literals:**

```typescript
type Status = 'pending' | 'approved' | 'rejected';
type HTTPMethod = 'GET' | 'POST' | 'PUT' | 'DELETE';
type Size = 'small' | 'medium' | 'large';

let orderStatus: Status = 'pending';
let requestMethod: HTTPMethod = 'GET';
let shirtSize: Size = 'medium';
```

**Function with literal parameters:**

```typescript
function setAlignment(align: 'left' | 'center' | 'right') {
    console.log(`Aligning ${align}`);
}

setAlignment('left');    // OK
setAlignment('center');  // OK
// setAlignment('top');     // Error! Not a valid alignment
```

**Combining with other types:**

```typescript
// Literal + other types
type SuccessCode = 200 | 201 | 204;
type ErrorCode = 400 | 401 | 403 | 404 | 500;
type StatusCode = SuccessCode | ErrorCode | string;

// Literal + null/undefined
type Theme = 'light' | 'dark' | null;
```

**Object with literal properties:**

```typescript
interface Button {
    label: string;
    size: 'small' | 'medium' | 'large';
    variant: 'primary' | 'secondary' | 'danger';
}

const submitButton: Button = {
    label: 'Submit',
    size: 'large',
    variant: 'primary'
};

// submitButton.size = 'extra-large';  // Error!
```

**Function overloads with literals:**

```typescript
function createElement(tag: 'div'): HTMLDivElement;
function createElement(tag: 'span'): HTMLSpanElement;
function createElement(tag: 'button'): HTMLButtonElement;

function createElement(tag: string): HTMLElement {
    return document.createElement(tag);
}

const div = createElement('div');  // Type is HTMLDivElement
```

**Template literal types (advanced):**

```typescript
type EmailStatus = `${string}@${string}.${string}`;

let email: EmailStatus = 'user@example.com';  // OK
// let invalidEmail: EmailStatus = 'not-an-email';  // Error!
```

**Real-world examples:**

```typescript
// API endpoints
type ApiEndpoint = '/users' | '/posts' | '/comments';

function fetchData(endpoint: ApiEndpoint) {
    return fetch(`https://api.example.com${endpoint}`);
}

// User roles
type UserRole = 'admin' | 'moderator' | 'user' | 'guest';

interface User {
    id: number;
    name: string;
    role: UserRole;
}

function hasPermission(user: User, action: 'read' | 'write' | 'delete'): boolean {
    if (user.role === 'admin') return true;
    if (user.role === 'moderator' && action !== 'delete') return true;
    if (user.role === 'user' && action === 'read') return true;
    return false;
}

// HTTP response
interface ApiResponse {
    status: 200 | 400 | 401 | 404 | 500;
    method: 'GET' | 'POST' | 'PUT' | 'DELETE';
    data?: any;
}
```

**Switch statement with literals:**

```typescript
type TrafficLight = 'red' | 'yellow' | 'green';

function handleLight(light: TrafficLight) {
    switch (light) {
        case 'red':
            console.log('Stop');
            break;
        case 'yellow':
            console.log('Slow down');
            break;
        case 'green':
            console.log('Go');
            break;
        // TypeScript ensures all cases are handled!
    }
}
```

**Interview tip:** Literal types restrict values to exact strings, numbers, or booleans. Very useful for status values ('pending' | 'approved'), directions, sizes, etc. Provides autocomplete and prevents typos. Type alias makes them reusable. TypeScript ensures all possible values are handled in switch statements."

---

### Q9: Object Types

**How to Answer:**

"In TypeScript, you can define the shape of objects - what properties they have and their types.

**Inline object type:**

```typescript
const user: {
    name: string;
    age: number;
    email: string;
} = {
    name: 'Alice',
    age: 25,
    email: 'alice@email.com'
};
```

**Function with object parameter:**

```typescript
function printUser(user: { name: string; age: number }) {
    console.log(`${user.name} is ${user.age} years old`);
}

printUser({ name: 'Bob', age: 30 });
```

**Optional properties:**

```typescript
const user: {
    name: string;
    age: number;
    email?: string;  // Optional (may not exist)
} = {
    name: 'Alice',
    age: 25
    // email is optional, can be omitted
};
```

**Readonly properties:**

```typescript
const user: {
    readonly id: number;
    name: string;
} = {
    id: 1,
    name: 'Alice'
};

// user.id = 2;  // Error! id is readonly
user.name = 'Bob';  // OK
```

**Nested objects:**

```typescript
const user: {
    name: string;
    address: {
        street: string;
        city: string;
        zip: number;
    };
} = {
    name: 'Alice',
    address: {
        street: '123 Main St',
        city: 'Boston',
        zip: 02101
    }
};

console.log(user.address.city);  // 'Boston'
```

**Index signatures (dynamic keys):**

```typescript
const scores: {
    [subject: string]: number;  // Any string key, number value
} = {
    math: 95,
    science: 88,
    history: 92
};

scores.english = 90;  // OK
// scores.math = '95';  // Error! Must be number
```

**Methods in objects:**

```typescript
const calculator: {
    add: (a: number, b: number) => number;
    subtract: (a: number, b: number) => number;
} = {
    add: (a, b) => a + b,
    subtract: (a, b) => a - b
};

console.log(calculator.add(5, 3));  // 8
```

**Type alias for objects (better approach):**

```typescript
// Define once, reuse everywhere
type User = {
    id: number;
    name: string;
    email: string;
    age?: number;
};

const user1: User = {
    id: 1,
    name: 'Alice',
    email: 'alice@email.com'
};

const user2: User = {
    id: 2,
    name: 'Bob',
    email: 'bob@email.com',
    age: 30
};

function printUser(user: User) {
    console.log(user.name);
}
```

**Combining object types:**

```typescript
type Person = {
    name: string;
    age: number;
};

type Employee = {
    employeeId: number;
    department: string;
};

// Intersection - has all properties
type EmployeePerson = Person & Employee;

const emp: EmployeePerson = {
    name: 'Alice',
    age: 30,
    employeeId: 12345,
    department: 'Engineering'
};
```

**Interview tip:** Object types define structure with property names and types. Use ? for optional properties. Use readonly to prevent changes. Can use inline types or type aliases for reusability. Index signatures allow dynamic keys. Methods are typed like: (params) => returnType."

---

### Q10: Interfaces

**How to Answer:**

"Interfaces define the shape of objects. They're like contracts that objects must follow - similar to blueprints.

**Basic interface:**

```typescript
interface User {
    id: number;
    name: string;
    email: string;
}

const user: User = {
    id: 1,
    name: 'Alice',
    email: 'alice@email.com'
};

// Must have all required properties
// const user2: User = { id: 2 };  // Error! Missing name and email
```

**Optional properties:**

```typescript
interface User {
    id: number;
    name: string;
    email: string;
    age?: number;  // Optional
    phone?: string;  // Optional
}

const user1: User = {
    id: 1,
    name: 'Alice',
    email: 'alice@email.com'
    // age and phone can be omitted
};

const user2: User = {
    id: 2,
    name: 'Bob',
    email: 'bob@email.com',
    age: 30  // age is provided
};
```

**Readonly properties:**

```typescript
interface User {
    readonly id: number;  // Can't be changed after creation
    name: string;
}

const user: User = {
    id: 1,
    name: 'Alice'
};

// user.id = 2;  // Error! id is readonly
user.name = 'Bob';  // OK
```

**Methods in interfaces:**

```typescript
interface Calculator {
    add(a: number, b: number): number;
    subtract(a: number, b: number): number;
}

const calc: Calculator = {
    add(a, b) {
        return a + b;
    },
    subtract(a, b) {
        return a - b;
    }
};

console.log(calc.add(5, 3));  // 8
```

**Function type interface:**

```typescript
interface GreetFunction {
    (name: string): string;
}

const greet: GreetFunction = (name) => {
    return `Hello, ${name}`;
};

console.log(greet('Alice'));  // 'Hello, Alice'
```

**Extending interfaces:**

```typescript
interface Person {
    name: string;
    age: number;
}

// Employee extends Person (inherits all properties)
interface Employee extends Person {
    employeeId: number;
    department: string;
}

const emp: Employee = {
    name: 'Alice',
    age: 30,
    employeeId: 12345,
    department: 'Engineering'
};
```

**Multiple extends:**

```typescript
interface Named {
    name: string;
}

interface Aged {
    age: number;
}

// Inherits from both
interface Person extends Named, Aged {
    email: string;
}

const person: Person = {
    name: 'Alice',
    age: 25,
    email: 'alice@email.com'
};
```

**Index signatures:**

```typescript
interface StringDictionary {
    [key: string]: string;
}

const colors: StringDictionary = {
    primary: 'blue',
    secondary: 'green',
    accent: 'red'
};

colors.background = 'white';  // OK
// colors.opacity = 0.5;  // Error! Must be string
```

**Class implementing interface:**

```typescript
interface Animal {
    name: string;
    makeSound(): void;
}

class Dog implements Animal {
    name: string;
    
    constructor(name: string) {
        this.name = name;
    }
    
    makeSound() {
        console.log('Woof!');
    }
}

const dog = new Dog('Buddy');
dog.makeSound();  // 'Woof!'
```

**Real-world examples:**

```typescript
// API Response
interface ApiResponse<T> {
    data: T;
    status: number;
    message: string;
}

interface User {
    id: number;
    name: string;
    email: string;
}

const response: ApiResponse<User> = {
    data: { id: 1, name: 'Alice', email: 'alice@email.com' },
    status: 200,
    message: 'Success'
};

// Form data
interface LoginForm {
    email: string;
    password: string;
    rememberMe?: boolean;
}

function handleLogin(form: LoginForm) {
    console.log(`Logging in: ${form.email}`);
}

// Configuration
interface AppConfig {
    apiUrl: string;
    timeout: number;
    retries?: number;
    debug?: boolean;
}

const config: AppConfig = {
    apiUrl: 'https://api.example.com',
    timeout: 5000,
    debug: true
};
```

**Declaration merging:**

```typescript
// First declaration
interface User {
    name: string;
}

// Second declaration - merged with first
interface User {
    age: number;
}

// User now has both name and age
const user: User = {
    name: 'Alice',
    age: 25
};
```

**Interview tip:** Interfaces define object shapes/contracts. Use interface keyword. Properties can be optional (?) or readonly. Can extend other interfaces for inheritance. Classes can implement interfaces. Interfaces are great for defining API responses, form data, and configuration objects."

---

### Q11: Type Aliases

**How to Answer:**

"Type aliases let you create custom names for types. They're similar to interfaces but more flexible.

**Basic type alias:**

```typescript
type UserID = string | number;
type Status = 'pending' | 'approved' | 'rejected';

let id: UserID = 123;
let orderStatus: Status = 'pending';
```

**Object type alias:**

```typescript
type User = {
    id: number;
    name: string;
    email: string;
    age?: number;
};

const user: User = {
    id: 1,
    name: 'Alice',
    email: 'alice@email.com'
};
```

**Function type alias:**

```typescript
type MathOperation = (a: number, b: number) => number;

const add: MathOperation = (a, b) => a + b;
const multiply: MathOperation = (a, b) => a * b;
```

**Union types:**

```typescript
type ID = string | number;
type Result = 'success' | 'error' | 'pending';

function processRequest(id: ID, result: Result) {
    console.log(`Request ${id}: ${result}`);
}
```

**Intersection types:**

```typescript
type Person = {
    name: string;
    age: number;
};

type Employee = {
    employeeId: number;
    department: string;
};

type EmployeePerson = Person & Employee;

const emp: EmployeePerson = {
    name: 'Alice',
    age: 30,
    employeeId: 12345,
    department: 'Engineering'
};
```

**Interview tip:** Type aliases use 'type' keyword. Can alias primitives, objects, unions, intersections. More flexible than interfaces. Use for unions ('pending' | 'approved'), primitive aliases (type ID = number), and complex types."

---

### Q12: Interface vs Type

**How to Answer:**

"Interfaces and types are similar but have key differences in how they can be used and extended.

**Similarities - both can:**

```typescript
// Define object shapes
interface UserInterface {
    name: string;
    age: number;
}

type UserType = {
    name: string;
    age: number;
};

// Both work the same way
const user1: UserInterface = { name: 'Alice', age: 25 };
const user2: UserType = { name: 'Bob', age: 30 };
```

**Key differences:**

**1. Extending:**

```typescript
// Interface - use extends
interface Person {
    name: string;
}

interface Employee extends Person {
    employeeId: number;
}

// Type - use intersection
type Person = {
    name: string;
};

type Employee = Person & {
    employeeId: number;
};
```

**2. Declaration merging (interface only):**

```typescript
// Interfaces can be declared multiple times and merge
interface User {
    name: string;
}

interface User {
    age: number;
}

// User now has both name and age
const user: User = {
    name: 'Alice',
    age: 25
};

// Types cannot be declared multiple times
// type User = { name: string };
// type User = { age: number };  // Error! Duplicate identifier
```

**3. Type can do more:**

```typescript
// Type can alias primitives
type ID = string | number;  // ✅ OK
// interface ID = string | number;  // ❌ Error

// Type can use unions
type Status = 'active' | 'inactive';  // ✅ OK
// interface Status = 'active' | 'inactive';  // ❌ Error

// Type can use mapped types
type Readonly<T> = {
    readonly [P in keyof T]: T[P];
};  // ✅ OK with type
```

**When to use Interface:**

```typescript
// ✅ Defining object shapes
interface User {
    id: number;
    name: string;
}

// ✅ When you might extend later
interface Person {
    name: string;
}

interface Employee extends Person {
    employeeId: number;
}

// ✅ For classes to implement
interface Animal {
    makeSound(): void;
}

class Dog implements Animal {
    makeSound() {
        console.log('Woof!');
    }
}

// ✅ Library/API contracts (can be extended by users)
```

**When to use Type:**

```typescript
// ✅ Union types
type ID = string | number;
type Status = 'pending' | 'approved' | 'rejected';

// ✅ Intersection types
type EmployeePerson = Person & Employee;

// ✅ Utility types and mapped types
type Partial<T> = {
    [P in keyof T]?: T[P];
};

// ✅ Aliasing primitives
type Age = number;
type Email = string;

// ✅ Tuple types
type Point = [number, number];

// ✅ Function types
type MathOp = (a: number, b: number) => number;
```

**Comparison table:**

| Feature | Interface | Type |
|---------|-----------|------|
| Objects | ✅ | ✅ |
| Extends/Intersects | extends | & |
| Declaration merging | ✅ | ❌ |
| Unions | ❌ | ✅ |
| Primitives | ❌ | ✅ |
| Tuples | ❌ | ✅ |
| Mapped types | ❌ | ✅ |
| Class implements | ✅ | ✅ |

**Interview tip:** Use interfaces for objects by default, types for everything else. Interfaces can be extended and merged. Types are more flexible (unions, mapped types, primitives). In practice, both work for objects - choose based on team preference. For unions and intersections, must use type."

---

### Q13: Optional and Readonly Properties

**How to Answer:**

"TypeScript lets you make properties optional with ? or prevent changes with readonly.

**Optional properties (?):**

```typescript
interface User {
    id: number;
    name: string;
    email: string;
    age?: number;  // Optional - may not exist
    phone?: string;  // Optional
}

// age and phone can be omitted
const user1: User = {
    id: 1,
    name: 'Alice',
    email: 'alice@email.com'
};

// Or included
const user2: User = {
    id: 2,
    name: 'Bob',
    email: 'bob@email.com',
    age: 30,
    phone: '555-1234'
};
```

**Checking optional properties:**

```typescript
function printAge(user: User) {
    // Must check if age exists
    if (user.age !== undefined) {
        console.log(`Age: ${user.age}`);
    }
    
    // Or use optional chaining
    console.log(user.age?.toFixed());
    
    // Or provide default
    const age = user.age ?? 0;
}
```

**Readonly properties:**

```typescript
interface User {
    readonly id: number;  // Can't be changed
    name: string;
}

const user: User = {
    id: 1,
    name: 'Alice'
};

user.name = 'Bob';  // OK
// user.id = 2;  // Error! id is readonly
```

**Readonly arrays:**

```typescript
const numbers: readonly number[] = [1, 2, 3];

// numbers.push(4);  // Error! Can't modify
// numbers[0] = 10;  // Error! Can't modify
console.log(numbers[0]);  // OK to read
```

**Readonly vs const:**

```typescript
// const - variable can't be reassigned
const user = { name: 'Alice' };
user.name = 'Bob';  // OK - property can change
// user = { name: 'Charlie' };  // Error - can't reassign

// readonly - property can't be changed
interface User {
    readonly name: string;
}
const user: User = { name: 'Alice' };
// user.name = 'Bob';  // Error - property is readonly
```

**Combining optional and readonly:**

```typescript
interface Config {
    readonly apiUrl: string;  // Required and can't change
    readonly apiKey: string;  // Required and can't change
    timeout?: number;  // Optional
    retries?: number;  // Optional
}

const config: Config = {
    apiUrl: 'https://api.example.com',
    apiKey: 'secret123'
};

// config.apiUrl = 'https://other.com';  // Error! readonly
config.timeout = 5000;  // OK - optional property can be added
```

**Interview tip:** Optional properties use ? and may not exist. Check with if or optional chaining (?.). Readonly properties can't be changed after creation. const prevents reassignment, readonly prevents property modification. Can combine optional and readonly."

---

### Q14: Function Types

**How to Answer:**

"TypeScript lets you type function parameters, return values, and the function itself.

**Function declaration:**

```typescript
function add(a: number, b: number): number {
    return a + b;
}

// Parameter types: a: number, b: number
// Return type: : number
```

**Arrow functions:**

```typescript
const multiply = (a: number, b: number): number => {
    return a * b;
};

// Shorthand
const divide = (a: number, b: number): number => a / b;
```

**Optional parameters:**

```typescript
function greet(name: string, greeting?: string): string {
    if (greeting) {
        return `${greeting}, ${name}`;
    }
    return `Hello, ${name}`;
}

greet('Alice');  // 'Hello, Alice'
greet('Alice', 'Hi');  // 'Hi, Alice'
```

**Default parameters:**

```typescript
function greet(name: string, greeting: string = 'Hello'): string {
    return `${greeting}, ${name}`;
}

greet('Alice');  // 'Hello, Alice'
greet('Alice', 'Hi');  // 'Hi, Alice'
```

**Rest parameters:**

```typescript
function sum(...numbers: number[]): number {
    return numbers.reduce((total, n) => total + n, 0);
}

sum(1, 2, 3);  // 6
sum(10, 20, 30, 40);  // 100
```

**Function type:**

```typescript
// Type for a function
type MathOperation = (a: number, b: number) => number;

const add: MathOperation = (a, b) => a + b;
const subtract: MathOperation = (a, b) => a - b;
```

**Void return type:**

```typescript
function logMessage(message: string): void {
    console.log(message);
    // No return statement
}
```

**Never return type:**

```typescript
function throwError(message: string): never {
    throw new Error(message);
    // Never returns
}
```

**Callback functions:**

```typescript
function processArray(
    arr: number[],
    callback: (item: number) => number
): number[] {
    return arr.map(callback);
}

const doubled = processArray([1, 2, 3], (n) => n * 2);
// [2, 4, 6]
```

**Interview tip:** Annotate parameter types and return type. Optional parameters use ?. Default parameters have = value. Rest parameters use ...param: type[]. void for no return, never for functions that don't return. Function types: (params) => returnType."

---

### Q15: Array Types

**How to Answer:**

"TypeScript provides two ways to type arrays: Type[] or Array<Type>.

**Basic arrays:**

```typescript
// number array
let numbers: number[] = [1, 2, 3, 4, 5];

// string array
let names: string[] = ['Alice', 'Bob', 'Charlie'];

// boolean array
let flags: boolean[] = [true, false, true];
```

**Alternative syntax:**

```typescript
// Generic syntax - same as above
let numbers: Array<number> = [1, 2, 3];
let names: Array<string> = ['Alice', 'Bob'];
```

**Mixed type arrays (union):**

```typescript
// Array can contain numbers OR strings
let mixed: (number | string)[] = [1, 'two', 3, 'four'];

// Alternative syntax
let mixed2: Array<number | string> = [1, 'two', 3];
```

**Array of objects:**

```typescript
interface User {
    id: number;
    name: string;
}

let users: User[] = [
    { id: 1, name: 'Alice' },
    { id: 2, name: 'Bob' }
];
```

**Readonly arrays:**

```typescript
const numbers: readonly number[] = [1, 2, 3];

// numbers.push(4);  // Error! Can't modify
// numbers[0] = 10;  // Error! Can't modify
```

**Array methods remain typed:**

```typescript
let numbers: number[] = [1, 2, 3, 4, 5];

// map - returns new array
let doubled: number[] = numbers.map(n => n * 2);

// filter - returns filtered array
let evens: number[] = numbers.filter(n => n % 2 === 0);

// find - returns single item or undefined
let found: number | undefined = numbers.find(n => n > 3);
```

**Interview tip:** Two syntaxes: Type[] or Array<Type>. Use union for multiple types: (number | string)[]. readonly prevents modifications. Array methods preserve types."

---

### Q16: Tuples

**How to Answer:**

"Tuples are arrays with fixed length and specific types for each position.

**Basic tuple:**

```typescript
// Tuple: [string, number]
let user: [string, number] = ['Alice', 25];

console.log(user[0]);  // 'Alice' (string)
console.log(user[1]);  // 25 (number)
```

**Accessing tuple elements:**

```typescript
let point: [number, number] = [10, 20];

let x = point[0];  // number
let y = point[1];  // number
```

**Tuple vs Array:**

```typescript
// Array - same type, any length
let numbers: number[] = [1, 2, 3, 4, 5];

// Tuple - specific types, fixed length
let tuple: [string, number, boolean] = ['Alice', 25, true];
```

**Optional tuple elements:**

```typescript
let user: [string, number?] = ['Alice'];
// Second element is optional

user = ['Bob', 30];  // OK
```

**Readonly tuples:**

```typescript
let point: readonly [number, number] = [10, 20];

// point[0] = 5;  // Error! readonly
```

**Destructuring tuples:**

```typescript
let user: [string, number] = ['Alice', 25];

let [name, age] = user;
console.log(name);  // 'Alice'
console.log(age);   // 25
```

**Function returning tuple:**

```typescript
function getUserInfo(): [string, number] {
    return ['Alice', 25];
}

let [name, age] = getUserInfo();
```

**Interview tip:** Tuples have fixed length and specific types per position. Access with index: tuple[0], tuple[1]. Different from arrays (same type, any length). Good for returning multiple values from functions."

---

### Q17: Enums

**How to Answer:**

"Enums define a set of named constants. They're great for status values, directions, or any fixed set of options.

**Numeric enums:**

```typescript
enum Status {
    Pending,    // 0
    Approved,   // 1
    Rejected    // 2
}

let orderStatus: Status = Status.Pending;
console.log(orderStatus);  // 0

if (orderStatus === Status.Pending) {
    console.log('Order is pending');
}
```

**Custom numeric values:**

```typescript
enum Status {
    Pending = 1,
    Approved = 2,
    Rejected = 3
}

let status: Status = Status.Approved;
console.log(status);  // 2
```

**String enums (better for debugging):**

```typescript
enum Direction {
    Up = 'UP',
    Down = 'DOWN',
    Left = 'LEFT',
    Right = 'RIGHT'
}

function move(direction: Direction) {
    console.log(`Moving ${direction}`);
}

move(Direction.Up);  // 'Moving UP'
```

**Enum vs Literal types:**

```typescript
// Enum
enum Status {
    Pending = 'PENDING',
    Approved = 'APPROVED'
}

// Literal type (often preferred)
type Status = 'PENDING' | 'APPROVED';
```

**Interview tip:** Enums create named constants. Numeric enums start at 0 by default. String enums are better for debugging. Consider using literal types ('pending' | 'approved') instead - they're simpler and tree-shakeable."

---

### Q18: Intersection Types

**How to Answer:**

"Intersection types combine multiple types into one. It's like saying 'this AND that'.

**Basic intersection:**

```typescript
type Person = {
    name: string;
    age: number;
};

type Employee = {
    employeeId: number;
    department: string;
};

// Has ALL properties from both types
type EmployeePerson = Person & Employee;

const emp: EmployeePerson = {
    name: 'Alice',
    age: 30,
    employeeId: 12345,
    department: 'Engineering'
};
```

**Multiple intersections:**

```typescript
type Contact = {
    email: string;
    phone: string;
};

type User = Person & Employee & Contact;

const user: User = {
    name: 'Alice',
    age: 30,
    employeeId: 12345,
    department: 'Engineering',
    email: 'alice@email.com',
    phone: '555-1234'
};
```

**Interview tip:** Intersection types use & to combine types. Result has ALL properties from all types. Different from union (| = OR). Use when object needs properties from multiple sources."

---

### Q19: Type Guards and Narrowing

**How to Answer:**

"Type guards help TypeScript understand what type a variable is at runtime, enabling safe operations.

**typeof type guard:**

```typescript
function printValue(value: string | number) {
    if (typeof value === 'string') {
        console.log(value.toUpperCase());  // TypeScript knows it's string
    } else {
        console.log(value.toFixed(2));  // TypeScript knows it's number
    }
}
```

**instanceof type guard:**

```typescript
class Dog {
    bark() {
        console.log('Woof!');
    }
}

class Cat {
    meow() {
        console.log('Meow!');
    }
}

function makeSound(animal: Dog | Cat) {
    if (animal instanceof Dog) {
        animal.bark();  // TypeScript knows it's Dog
    } else {
        animal.meow();  // TypeScript knows it's Cat
    }
}
```

**in operator:**

```typescript
interface Fish {
    swim: () => void;
}

interface Bird {
    fly: () => void;
}

function move(animal: Fish | Bird) {
    if ('swim' in animal) {
        animal.swim();  // TypeScript knows it's Fish
    } else {
        animal.fly();  // TypeScript knows it's Bird
    }
}
```

**Custom type guard:**

```typescript
interface Fish {
    swim: () => void;
}

interface Bird {
    fly: () => void;
}

// Custom type guard function
function isFish(animal: Fish | Bird): animal is Fish {
    return (animal as Fish).swim !== undefined;
}

function move(animal: Fish | Bird) {
    if (isFish(animal)) {
        animal.swim();  // TypeScript knows it's Fish
    } else {
        animal.fly();  // TypeScript knows it's Bird
    }
}
```

**Interview tip:** Type guards narrow types using typeof, instanceof, in operator, or custom functions. After checking, TypeScript knows the specific type. Custom guards use 'parameterName is Type' return type. Essential for working with union types."

---

### Q20: Generics Basics

**How to Answer:**

"Generics let you write reusable code that works with multiple types. Think of <T> as a placeholder for a type.

**The problem generics solve:**

```typescript
// Without generics - need separate functions
function getFirstString(arr: string[]): string {
    return arr[0];
}

function getFirstNumber(arr: number[]): number {
    return arr[0];
}

// With generics - one function for all types
function getFirst<T>(arr: T[]): T {
    return arr[0];
}

getFirst(['a', 'b', 'c']);  // T is string
getFirst([1, 2, 3]);        // T is number
getFirst([true, false]);    // T is boolean
```

**Generic function:**

```typescript
function identity<T>(value: T): T {
    return value;
}

let str = identity<string>('hello');  // Explicit type
let num = identity(42);  // Type inferred as number
```

**Generic interface:**

```typescript
interface Box<T> {
    value: T;
}

const stringBox: Box<string> = { value: 'hello' };
const numberBox: Box<number> = { value: 42 };
```

**Generic array function:**

```typescript
function reverseArray<T>(arr: T[]): T[] {
    return arr.reverse();
}

reverseArray([1, 2, 3]);  // [3, 2, 1]
reverseArray(['a', 'b']);  // ['b', 'a']
```

**Real-world example - API response:**

```typescript
interface ApiResponse<T> {
    data: T;
    status: number;
    message: string;
}

interface User {
    id: number;
    name: string;
}

const response: ApiResponse<User> = {
    data: { id: 1, name: 'Alice' },
    status: 200,
    message: 'Success'
};
```

**Interview tip:** Generics use <T> as type placeholder. T becomes actual type when function is called. Makes code reusable for multiple types. Common in arrays, promises, API responses. TypeScript can often infer T automatically."

---

### Q21: Generic Constraints

**How to Answer:**

"Generic constraints limit what types can be used with generics using the extends keyword.

**Basic constraint:**

```typescript
// T must have a length property
function logLength<T extends { length: number }>(item: T): void {
    console.log(item.length);
}

logLength('hello');  // OK - string has length
logLength([1, 2, 3]);  // OK - array has length
// logLength(42);  // Error! number doesn't have length
```

**Constraining to specific types:**

```typescript
function merge<T extends object, U extends object>(obj1: T, obj2: U) {
    return { ...obj1, ...obj2 };
}

merge({ name: 'Alice' }, { age: 25 });  // OK
// merge('hello', { age: 25 });  // Error! string is not object
```

**keyof constraint:**

```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K) {
    return obj[key];
}

const user = { name: 'Alice', age: 25 };
getProperty(user, 'name');  // OK
// getProperty(user, 'email');  // Error! 'email' is not a key of user
```

**Interview tip:** Constraints use extends to limit what types are allowed. extends { length: number } means type must have length. extends object means must be object. keyof T means must be a key of T. Makes generics safer and more specific."

---

### Q22: Utility Types

**How to Answer:**

"TypeScript includes built-in utility types that transform existing types.

**Partial<T> - Makes all properties optional:**

```typescript
interface User {
    id: number;
    name: string;
    email: string;
}

function updateUser(id: number, updates: Partial<User>) {
    // updates can have any combination of User properties
}

updateUser(1, { name: 'Alice' });  // OK
updateUser(1, { email: 'alice@email.com' });  // OK
```

**Required<T> - Makes all properties required:**

```typescript
interface Config {
    host?: string;
    port?: number;
}

const config: Required<Config> = {
    host: 'localhost',
    port: 3000  // Both required now
};
```

**Pick<T, Keys> - Pick specific properties:**

```typescript
interface User {
    id: number;
    name: string;
    email: string;
    password: string;
}

type PublicUser = Pick<User, 'id' | 'name' | 'email'>;
// Only has id, name, email (no password)
```

**Omit<T, Keys> - Remove specific properties:**

```typescript
type UserWithoutPassword = Omit<User, 'password'>;
// Has everything except password
```

**Record<Keys, Type> - Create object type:**

```typescript
type PageScores = Record<string, number>;

const scores: PageScores = {
    home: 95,
    about: 88,
    contact: 92
};
```

**Interview tip:** Utility types transform existing types. Partial makes optional. Required makes all required. Pick selects properties. Omit removes properties. Record creates object with specific key/value types. Very useful for API responses and forms."

---

### Q23: Classes in TypeScript

**How to Answer:**

"TypeScript enhances JavaScript classes with access modifiers and type safety.

**Basic class:**

```typescript
class Person {
    name: string;
    age: number;
    
    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
    
    greet(): string {
        return `Hi, I'm ${this.name}`;
    }
}

const person = new Person('Alice', 25);
console.log(person.greet());  // 'Hi, I'm Alice'
```

**Access modifiers:**

```typescript
class Person {
    public name: string;      // Accessible everywhere (default)
    private age: number;       // Only inside class
    protected email: string;   // Inside class and subclasses
    
    constructor(name: string, age: number, email: string) {
        this.name = name;
        this.age = age;
        this.email = email;
    }
}

const person = new Person('Alice', 25, 'alice@email.com');
console.log(person.name);  // OK
// console.log(person.age);  // Error! private
```

**Shorthand constructor:**

```typescript
// Instead of this:
class Person {
    private name: string;
    public age: number;
    
    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
}

// Do this:
class Person {
    constructor(private name: string, public age: number) {}
}
```

**Readonly properties:**

```typescript
class Person {
    readonly id: number;
    name: string;
    
    constructor(id: number, name: string) {
        this.id = id;
        this.name = name;
    }
}

const person = new Person(1, 'Alice');
// person.id = 2;  // Error! readonly
person.name = 'Bob';  // OK
```

**Interview tip:** Classes get access modifiers: public (default), private (class only), protected (class + subclasses). Shorthand: constructor(private name: string) auto-creates property. readonly prevents changes after initialization."

---

### Q24: Async/Await with Types

**How to Answer:**

"TypeScript works seamlessly with async/await. Type the resolved value, not the Promise itself.

**Basic async function:**

```typescript
async function fetchUser(id: number): Promise<User> {
    const response = await fetch(`/api/users/${id}`);
    return response.json();
}

// Return type is Promise<User>, not User
```

**Using async function:**

```typescript
interface User {
    id: number;
    name: string;
}

async function getUser(id: number): Promise<User> {
    const response = await fetch(`/api/users/${id}`);
    const user: User = await response.json();
    return user;
}

// Call it
const user = await getUser(1);
console.log(user.name);
```

**Promise types:**

```typescript
// Promise that resolves to string
function fetchData(): Promise<string> {
    return fetch('/api/data').then(r => r.text());
}

// Promise that resolves to void
async function logData(): Promise<void> {
    console.log('Data logged');
}
```

**Interview tip:** Async functions return Promise<T>. Type the resolved value: Promise<User>, not just User. Use await to unwrap promises. TypeScript ensures type safety through the entire async flow."

---

### Q25: Common TypeScript Patterns

**How to Answer:**

"TypeScript has some common patterns that make code safer and cleaner.

**Optional chaining (?.):**

```typescript
interface User {
    name: string;
    address?: {
        street: string;
        city: string;
    };
}

const user: User = { name: 'Alice' };

// Safe access to nested optional properties
const city = user.address?.city;  // undefined (no error)
```

**Nullish coalescing (??):**

```typescript
const displayCity = user.address?.city ?? 'Unknown';
// If city is null or undefined, use 'Unknown'
```

**Non-null assertion (!):**

```typescript
const element = document.getElementById('myButton')!;
element.addEventListener('click', () => {});

// ! tells TypeScript: "I know this isn't null"
// Use carefully - can cause runtime errors!
```

**Type assertions (as):**

```typescript
const input = document.getElementById('myInput') as HTMLInputElement;
console.log(input.value);  // TypeScript knows it has value
```

**Interview tip:** Optional chaining (?.) safely accesses nested properties. Nullish coalescing (??) provides defaults. Non-null assertion (!) tells TypeScript value isn't null (use carefully). Type assertions (as) explicitly set type."

---

## Part 2: Quick Reference Questions

### 50 Quick TypeScript Interview Questions

**Basic Types:**

1. What are the primitive types in TypeScript?
   - Answer: string, number, boolean, null, undefined, symbol, bigint

2. What's the difference between any and unknown?
   - Answer: any disables type checking. unknown requires type checking before use.

3. What does never type represent?
   - Answer: Functions that never return (throw errors or infinite loops)

4. What's the difference between void and never?
   - Answer: void returns undefined/nothing. never never returns at all.

5. What are literal types?
   - Answer: Types for exact values like 'pending' | 'approved'

**Functions:**

6. How do you type function parameters?
   - Answer: functionName(param: type): returnType

7. What's an optional parameter?
   - Answer: Parameter with ?: paramName?: type

8. How do you type rest parameters?
   - Answer: ...param: type[]

9. What's a function type alias?
   - Answer: type FnType = (params) => returnType

10. Can TypeScript infer return types?
    - Answer: Yes, but explicit is better for clarity

**Objects & Interfaces:**

11. What's an interface?
    - Answer: Blueprint for object shape

12. Difference between interface and type?
    - Answer: Interface for objects, can extend. Type more flexible, can do unions.

13. What's an optional property?
    - Answer: Property with ?: propertyName?: type

14. What's a readonly property?
    - Answer: readonly propertyName: type (can't be changed)

15. Can interfaces extend other interfaces?
    - Answer: Yes, using extends keyword

16. What's declaration merging?
    - Answer: Multiple interface declarations merge into one (interfaces only)

**Arrays & Tuples:**

17. How do you type an array?
    - Answer: type[] or Array<type>

18. What's a tuple?
    - Answer: Fixed-length array with specific types per position

19. How do you make array readonly?
    - Answer: readonly type[]

20. Tuple vs Array difference?
    - Answer: Tuple has fixed length & types, array has same type, any length

**Union & Intersection:**

21. What's a union type?
    - Answer: Type that can be one of several types: type1 | type2

22. What's an intersection type?
    - Answer: Type that combines multiple types: type1 & type2

23. When to use union vs intersection?
    - Answer: Union for OR (either), intersection for AND (both)

**Generics:**

24. What are generics?
    - Answer: Type placeholders that make code reusable for multiple types

25. What does <T> mean?
    - Answer: Generic type parameter (placeholder)

26. Can TypeScript infer generic types?
    - Answer: Yes, often automatically

27. What's a generic constraint?
    - Answer: Limits generic type using extends: <T extends Type>

28. Why use generics instead of any?
    - Answer: Maintains type safety while being flexible

**Utility Types:**

29. What does Partial<T> do?
    - Answer: Makes all properties optional

30. What does Pick<T, Keys> do?
    - Answer: Selects specific properties from type

31. What does Omit<T, Keys> do?
    - Answer: Removes specific properties from type

32. What does Required<T> do?
    - Answer: Makes all properties required

33. What does Record<K, T> do?
    - Answer: Creates object type with specific keys and values

**Classes:**

34. What are access modifiers?
    - Answer: public, private, protected

35. What's the default access modifier?
    - Answer: public

36. What does private mean?
    - Answer: Only accessible inside the class

37. What does protected mean?
    - Answer: Accessible in class and subclasses

38. What's readonly in classes?
    - Answer: Property that can't be changed after initialization

39. What's shorthand constructor syntax?
    - Answer: constructor(public name: string) - auto-creates property

**Type Guards:**

40. What's a type guard?
    - Answer: Code that narrows type (typeof, instanceof, in)

41. What's typeof guard?
    - Answer: Checks primitive types: typeof x === 'string'

42. What's instanceof guard?
    - Answer: Checks class instances: x instanceof ClassName

43. What's in operator?
    - Answer: Checks if property exists: 'prop' in obj

44. What's a custom type guard?
    - Answer: Function with return type: param is Type

**Advanced:**

45. What's type assertion?
    - Answer: Explicitly tell TypeScript the type: value as Type

46. What's non-null assertion?
    - Answer: ! operator: value! (tells TS value isn't null)

47. What's optional chaining?
    - Answer: ?. operator: obj?.prop?.nested

48. What's nullish coalescing?
    - Answer: ?? operator: value ?? default

49. What's keyof operator?
    - Answer: Gets union of object keys: keyof Type

50. When to use enum vs literal types?
    - Answer: Literal types preferred (simpler, tree-shakeable)

---

## Summary

**You've covered:**
- ✅ TypeScript basics and setup
- ✅ All type systems (primitives, objects, arrays, tuples)
- ✅ Functions, interfaces, and type aliases
- ✅ Union, intersection, and literal types
- ✅ Generics and utility types
- ✅ Classes with access modifiers
- ✅ Type guards and narrowing
- ✅ Async/await with types
- ✅ Common patterns and best practices

**Key takeaways:**
1. TypeScript = JavaScript + Types
2. Catches errors at compile-time, not runtime
3. Use interfaces for objects, types for everything else
4. Let TypeScript infer when possible
5. Use strict mode for best type checking
6. Generics make code reusable and type-safe

**You're ready for TypeScript interviews!** 🚀

Good luck! 🎯
keSound() {
        console.log('Woof!');
    }
}

const dog = new Dog('Buddy');
dog.makeSound();  // 'Woof!'
```

**Real-world examples:**

```typescript
// API Response
interface ApiResponse<T> {
    data: T;
    status: number;
    message: string;
}

interface User {
    id: number;
    name: string;
    email: string;
}

const response: ApiResponse<User> = {
    data: { id: 1, name: 'Alice', email: 'alice@email.com' },
    status: 200,
    message: 'Success'
};

// Form data
interface LoginForm {
    email: string;
    password: string;
    rememberMe?: boolean;
}

function handleLogin(form: LoginForm) {
    console.log(`Logging in: ${form.email}`);
}

// Configuration
interface AppConfig {
    apiUrl: string;
    timeout: number;
    retries?: number;
    debug?: boolean;
}

const config: AppConfig = {
    apiUrl: 'https://api.example.com',
    timeout: 5000,
    debug: true
};
```

**Declaration merging:**

```typescript
// First declaration
interface User {
    name: string;
}

// Second declaration - merged with first
interface User {
    age: number;
}

// User now has both name and age
const user: User = {
    name: 'Alice',
    age: 25
};
```

**Interview tip:** Interfaces define object shapes/contracts. Use interface keyword. Properties can be optional (?) or readonly. Can extend other interfaces for inheritance. Classes can implement interfaces. Interfaces are great for defining API responses, form data, and configuration objects."

