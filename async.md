# Async JavaScript Interview Preparation Guide
*How to Answer Async JavaScript Questions Confidently*

**Note for Students:** This guide is written exactly how you should answer in interviews. Practice reading these answers out loud to make them natural when speaking.

---

## Table of Contents
1. [Introduction to Async JavaScript](#introduction-to-async-javascript)
2. [Call Stack & Synchronous Execution](#call-stack--synchronous-execution)
3. [setTimeout & setInterval](#settimeout--setinterval)
4. [Callbacks & Callback Hell](#callbacks--callback-hell)
5. [Promises](#promises)
6. [Promise Methods (all, race, allSettled, any)](#promise-methods)
7. [Promise Chaining](#promise-chaining)
8. [async/await](#asyncawait)
9. [Error Handling in Async Code](#error-handling-in-async-code)
10. [fetch API](#fetch-api)
11. [Event Loop](#event-loop)
12. [Microtasks vs Macrotasks](#microtasks-vs-macrotasks)
13. [Global Execution Context](#global-execution-context)
14. [Closures in Async Context](#closures-in-async-context)
15. [this Keyword with Callbacks](#this-keyword-with-callbacks)
16. [Modules (import/export)](#modules-importexport)
17. [NPM & NPX Basics](#npm--npx-basics)
18. [Throttling & Debouncing](#throttling--debouncing)
19. [AbortController](#abortcontroller)
20. [Common Patterns & Best Practices](#common-patterns--best-practices)

---

## Introduction to Async JavaScript

### Q1: What is Asynchronous JavaScript and why do we need it?

**How to Answer:**

"JavaScript is a single-threaded language, which means it can only execute one thing at a time. But if we had to wait for every operation to complete before moving to the next one - like waiting for a file to load or an API call to finish - our applications would freeze and become unusable.

That's where asynchronous JavaScript comes in. It allows us to start long-running operations and continue executing other code while waiting for those operations to complete.

For example, imagine you're making a request to fetch user data from a server. Without async code, your entire application would freeze until the server responds. With async code, you can make the request and continue doing other things - like handling user clicks or updating the UI - while waiting for the response.

The main scenarios where we use async JavaScript are:
- Making API calls with fetch or AJAX
- Reading or writing files
- Setting timers with setTimeout or setInterval
- Database operations
- Any operation that takes time and we don't want to block the main thread

JavaScript achieves this using mechanisms like callbacks, promises, and async/await, all working together with the event loop."

**Key Point:** "Even though JavaScript is single-threaded, it can handle asynchronous operations by delegating time-consuming tasks to Web APIs and using the event loop to manage when their callbacks should run."

---

### Q2: What does it mean that JavaScript is single-threaded?

**How to Answer:**

"When we say JavaScript is single-threaded, it means it has only one call stack and can execute only one piece of code at a time. Think of it like having only one worker who can do only one task at a time.

For example:

```javascript
console.log('First');
console.log('Second');
console.log('Third');
```

These will always execute in order - First, Second, Third - because JavaScript processes them one by one on a single thread.

However, this doesn't mean JavaScript can't handle multiple operations. The browser provides Web APIs that run outside of JavaScript's single thread - things like setTimeout, fetch, DOM events. These operations happen in the background, and when they're done, their callbacks are queued up to be executed on the main thread.

So JavaScript itself is single-threaded, but it works in an environment (the browser or Node.js) that provides multi-threading capabilities for certain operations. The event loop coordinates everything to make it seem like multiple things are happening at once, even though JavaScript code itself only runs one thing at a time."

---

## Call Stack & Synchronous Execution

### Q3: What is the Call Stack and how does it work?

**How to Answer:**

"The call stack is a data structure that keeps track of function calls in your program. It works on a Last In, First Out (LIFO) principle - like a stack of plates where you can only add or remove from the top.

When a function is called, it gets pushed onto the call stack. When the function returns, it gets popped off the stack.

Let me show you with an example:

```javascript
function third() {
  console.log('Third function');
}

function second() {
  third();
  console.log('Second function');
}

function first() {
  second();
  console.log('First function');
}

first();
```

Here's what happens step by step:

1. `first()` is called → pushed onto stack
2. Inside `first()`, `second()` is called → pushed onto stack
3. Inside `second()`, `third()` is called → pushed onto stack
4. `third()` executes and returns → popped off stack
5. Back in `second()`, console.log runs, then it returns → popped off stack
6. Back in `first()`, console.log runs, then it returns → popped off stack
7. Stack is empty

The output would be:
```
Third function
Second function
First function
```

**Important point:** JavaScript can only execute code when the call stack is not empty. When the stack is empty, it checks the task queue for any pending callbacks. This is how the event loop works."

---

### Q4: What happens when the call stack overflows?

**How to Answer:**

"A stack overflow happens when you have too many function calls on the stack, usually from infinite recursion - when a function keeps calling itself without a proper exit condition.

For example:

```javascript
function recurse() {
  recurse(); // Calls itself forever
}

recurse(); // Error: Maximum call stack size exceeded
```

Each call to `recurse()` adds a new frame to the call stack, but nothing ever gets popped off because the function never returns. Eventually, the stack runs out of space and JavaScript throws a 'Maximum call stack size exceeded' error.

This is different from an infinite loop:

```javascript
while (true) {
  console.log('Loop');
}
```

An infinite loop doesn't cause a stack overflow because it doesn't keep adding function calls to the stack. It just keeps executing the same code. But it will freeze your program because the call stack never becomes empty, so the event loop can't process other tasks.

The way to avoid stack overflow is to always have a base case in recursive functions:

```javascript
function countdown(n) {
  if (n <= 0) return; // Base case
  console.log(n);
  countdown(n - 1);
}

countdown(5); // Works fine
```

Now the recursion has an exit condition, so the stack doesn't grow infinitely."

---

## setTimeout & setInterval

### Q5: How does setTimeout work?

**How to Answer:**

"setTimeout is a function that executes a callback after a specified delay. The syntax is:

```javascript
setTimeout(callback, delay);
```

For example:

```javascript
console.log('Start');

setTimeout(() => {
  console.log('This runs after 2 seconds');
}, 2000);

console.log('End');
```

The output will be:
```
Start
End
This runs after 2 seconds
```

Notice that 'End' prints before the setTimeout callback, even though the setTimeout comes first in the code. This is because setTimeout is asynchronous.

Here's what happens:
1. 'Start' is logged
2. setTimeout is called - it registers the callback with the Web API and sets a timer for 2000ms
3. JavaScript continues immediately to the next line (doesn't wait)
4. 'End' is logged
5. After 2 seconds, the callback is moved to the task queue
6. When the call stack is empty, the event loop picks up the callback and executes it

**Important points:**

The delay is not guaranteed to be exact. It's the minimum time before the callback can run. If the call stack is busy, the callback will have to wait:

```javascript
setTimeout(() => {
  console.log('Should run after 0ms');
}, 0);

// Some heavy operation
for (let i = 0; i < 1000000000; i++) {}

console.log('Heavy operation done');
```

Even with 0ms delay, the setTimeout callback runs after the loop finishes because the loop blocks the call stack."

---

### Q6: What's the difference between setTimeout and setInterval?

**How to Answer:**

"Both are timer functions, but they work differently:

**setTimeout** - Executes the callback once after the specified delay:

```javascript
setTimeout(() => {
  console.log('Runs once after 2 seconds');
}, 2000);
```

**setInterval** - Executes the callback repeatedly at the specified interval:

```javascript
setInterval(() => {
  console.log('Runs every 2 seconds');
}, 2000);
```

setInterval keeps running until you explicitly stop it using clearInterval:

```javascript
const intervalId = setInterval(() => {
  console.log('Tick');
}, 1000);

// Stop after 5 seconds
setTimeout(() => {
  clearInterval(intervalId);
  console.log('Interval stopped');
}, 5000);
```

**Important consideration:** setInterval doesn't wait for the callback to finish before scheduling the next one. If your callback takes longer than the interval, you might have issues:

```javascript
setInterval(() => {
  // If this takes 3 seconds but interval is 2 seconds,
  // calls can pile up
  someSlowOperation();
}, 2000);
```

A safer pattern is using setTimeout recursively:

```javascript
function repeatTask() {
  someSlowOperation();
  setTimeout(repeatTask, 2000); // Schedule next call after this one finishes
}

repeatTask();
```

This ensures there's always a 2-second gap between the end of one call and the start of the next."

---

### Q7: What is setTimeout 0 and why would you use it?

**How to Answer:**

"setTimeout with 0 delay doesn't execute immediately - it defers the callback until after the current call stack is clear.

```javascript
console.log('1');

setTimeout(() => {
  console.log('2');
}, 0);

console.log('3');

// Output: 1, 3, 2
```

Even though the delay is 0, the callback still goes through the event loop. The synchronous code runs first, then the callback executes.

**Why use it?**

**Use case 1: Breaking up long-running tasks**

```javascript
function processLargeArray(array) {
  // Process in chunks to avoid blocking
  const chunk = array.splice(0, 100);
  
  // Process this chunk
  chunk.forEach(item => processItem(item));
  
  // If more items, schedule next chunk
  if (array.length > 0) {
    setTimeout(() => processLargeArray(array), 0);
  }
}
```

This allows the browser to handle other tasks between chunks, keeping the UI responsive.

**Use case 2: Deferring code until DOM is ready**

```javascript
// Sometimes you need to ensure DOM has updated
element.style.display = 'block';

setTimeout(() => {
  // This runs after the browser has painted the change
  element.style.opacity = '1';
}, 0);
```

**Use case 3: Changing execution order**

```javascript
function doSomething() {
  console.log('Inside function');
}

console.log('Before');
setTimeout(doSomething, 0);
console.log('After');

// Output: Before, After, Inside function
```

So setTimeout(0) is a way to say 'do this, but let everything else in the current stack finish first.'"

---

## Callbacks & Callback Hell

### Q8: What is a callback function?

**How to Answer:**

"A callback is simply a function that you pass as an argument to another function, and it gets called later - usually after some operation completes.

The simplest example:

```javascript
function greet(name, callback) {
  console.log('Hello ' + name);
  callback();
}

function sayGoodbye() {
  console.log('Goodbye!');
}

greet('John', sayGoodbye);
// Output:
// Hello John
// Goodbye!
```

Callbacks are heavily used in asynchronous operations because they allow you to specify what should happen after an async operation completes:

```javascript
// Reading a file (async operation)
readFile('data.txt', function(error, data) {
  if (error) {
    console.log('Error reading file');
  } else {
    console.log('File content:', data);
  }
});

console.log('This runs before the file is read');
```

Here, the callback function is called once the file reading is complete. Meanwhile, JavaScript continues executing other code.

**Types of callbacks:**

**Synchronous callbacks** - Execute immediately:
```javascript
[1, 2, 3].forEach(function(num) {
  console.log(num); // Runs immediately for each item
});
```

**Asynchronous callbacks** - Execute later:
```javascript
setTimeout(function() {
  console.log('Runs after 1 second'); // Runs later
}, 1000);
```

The key concept is that callbacks let you say 'when this is done, do that' - which is essential for handling async operations."

---

### Q9: What is Callback Hell and how do you avoid it?

**How to Answer:**

"Callback hell, also called 'pyramid of doom,' happens when you have multiple nested callbacks, making the code hard to read and maintain.

Here's an example:

```javascript
getData(function(a) {
  getMoreData(a, function(b) {
    getMoreData(b, function(c) {
      getMoreData(c, function(d) {
        getMoreData(d, function(e) {
          console.log('Finally done!');
        });
      });
    });
  });
});
```

Look at how the code keeps indenting to the right - that's the 'pyramid.' It's hard to read, hard to debug, and hard to handle errors.

**Problems with callback hell:**

1. **Hard to read** - The logic is buried in nested functions
2. **Error handling nightmare** - You need to handle errors at each level
3. **Hard to maintain** - Adding or removing steps is difficult
4. **Difficult to debug** - Stack traces become confusing

**Solutions:**

**Solution 1: Named functions**
```javascript
function step1(data, callback) {
  // Process data
  callback(null, processedData);
}

function step2(data, callback) {
  // Process data
  callback(null, processedData);
}

step1(initialData, function(err, result1) {
  if (err) return handleError(err);
  step2(result1, function(err, result2) {
    if (err) return handleError(err);
    // Continue...
  });
});
```

**Solution 2: Promises (better)**
```javascript
getData()
  .then(getMoreData)
  .then(getMoreData)
  .then(getMoreData)
  .then(result => {
    console.log('Done!', result);
  })
  .catch(error => {
    console.log('Error:', error);
  });
```

**Solution 3: async/await (best)**
```javascript
async function fetchData() {
  try {
    const a = await getData();
    const b = await getMoreData(a);
    const c = await getMoreData(b);
    const d = await getMoreData(c);
    console.log('Done!', d);
  } catch (error) {
    console.log('Error:', error);
  }
}
```

Modern JavaScript strongly favors promises and async/await over nested callbacks because they make async code look and behave more like synchronous code."

---

## Promises

### Q10: What is a Promise in JavaScript?

**How to Answer:**

"A Promise is an object that represents the eventual completion or failure of an asynchronous operation. Think of it as a placeholder for a value that we don't have yet but will have in the future.

A promise can be in one of three states:

1. **Pending** - Initial state, the operation hasn't completed yet
2. **Fulfilled** - The operation completed successfully
3. **Rejected** - The operation failed

Here's how you create a promise:

```javascript
const myPromise = new Promise((resolve, reject) => {
  // Do some async operation
  setTimeout(() => {
    const success = true;
    
    if (success) {
      resolve('Operation successful!'); // Fulfilled
    } else {
      reject('Operation failed!'); // Rejected
    }
  }, 1000);
});
```

And here's how you use it:

```javascript
myPromise
  .then(result => {
    console.log(result); // Runs if fulfilled
  })
  .catch(error => {
    console.log(error); // Runs if rejected
  });
```

**Why promises are better than callbacks:**

1. **Cleaner syntax** - No deep nesting
2. **Better error handling** - One `.catch()` can handle errors from any step
3. **Chainable** - You can chain multiple async operations easily
4. **Built-in state management** - The promise keeps track of whether it's pending, fulfilled, or rejected

**Important points:**

- A promise can only be resolved or rejected once - it can't change after that
- You can't 'cancel' a promise once it's created
- Promises always resolve or reject asynchronously, even if the operation is synchronous"

---

### Q11: How do you create and use Promises?

**How to Answer:**

"Creating a promise involves using the Promise constructor with an executor function that takes two parameters: resolve and reject.

**Creating a Promise:**

```javascript
function fetchUserData(userId) {
  return new Promise((resolve, reject) => {
    // Simulate API call
    setTimeout(() => {
      if (userId > 0) {
        resolve({ id: userId, name: 'John' });
      } else {
        reject('Invalid user ID');
      }
    }, 1000);
  });
}
```

**Using a Promise with .then() and .catch():**

```javascript
fetchUserData(1)
  .then(user => {
    console.log('User:', user);
    return user.name; // Can return value for next .then()
  })
  .then(name => {
    console.log('User name:', name);
  })
  .catch(error => {
    console.log('Error:', error);
  });
```

**Using .finally():**

```javascript
fetchUserData(1)
  .then(user => console.log(user))
  .catch(error => console.log(error))
  .finally(() => {
    console.log('Cleanup - runs whether success or failure');
  });
```

**Real-world example - wrapping an async operation:**

```javascript
function delay(ms) {
  return new Promise(resolve => {
    setTimeout(resolve, ms);
  });
}

// Usage
console.log('Start');
delay(2000)
  .then(() => {
    console.log('2 seconds later');
  });
```

**Key patterns:**

1. **Always return promises from functions** so they can be chained
2. **Always handle errors** with .catch()
3. **Return values from .then()** to pass data to the next .then()
4. **Use .finally()** for cleanup code that should always run

The beauty of promises is that they make async code more readable and manageable compared to nested callbacks."

---

### Q12: What's the difference between Promise.resolve() and Promise.reject()?

**How to Answer:**

"These are convenience methods for creating promises that are already fulfilled or rejected.

**Promise.resolve()** - Creates a promise that's immediately fulfilled with a value:

```javascript
const promise = Promise.resolve('Hello');

promise.then(value => {
  console.log(value); // 'Hello'
});

// Equivalent to:
const promise = new Promise(resolve => {
  resolve('Hello');
});
```

**Promise.reject()** - Creates a promise that's immediately rejected with a reason:

```javascript
const promise = Promise.reject('Something went wrong');

promise.catch(error => {
  console.log(error); // 'Something went wrong'
});

// Equivalent to:
const promise = new Promise((resolve, reject) => {
  reject('Something went wrong');
});
```

**When to use them:**

**Use Promise.resolve() when:**
- You want to convert a value into a promise
- You need to ensure something is a promise

```javascript
function getData(value) {
  // If value is already a promise, return it
  // If it's a regular value, wrap it in a promise
  return Promise.resolve(value);
}

getData(42).then(console.log); // 42
getData(Promise.resolve(42)).then(console.log); // 42
```

**Use Promise.reject() when:**
- You want to create a rejected promise for testing
- You need to immediately return a rejected promise

```javascript
function validateUser(user) {
  if (!user.email) {
    return Promise.reject('Email is required');
  }
  return Promise.resolve(user);
}
```

These are particularly useful in functions where you sometimes need to return a promise and sometimes have the value immediately. They ensure consistent return types."

---

## Promise Methods

### Q13: Explain Promise.all() and when to use it.

**How to Answer:**

"Promise.all() takes an array of promises and returns a single promise that resolves when all the input promises have resolved, or rejects if any one of them rejects.

**Basic usage:**

```javascript
const promise1 = fetch('/api/users');
const promise2 = fetch('/api/posts');
const promise3 = fetch('/api/comments');

Promise.all([promise1, promise2, promise3])
  .then(([users, posts, comments]) => {
    console.log('All data loaded:', users, posts, comments);
  })
  .catch(error => {
    console.log('One of the requests failed:', error);
  });
```

**Key characteristics:**

1. **All or nothing** - If any promise rejects, the entire Promise.all() rejects immediately
2. **Maintains order** - Results are in the same order as the input promises
3. **Runs in parallel** - All promises execute concurrently, not sequentially

**When to use Promise.all():**

Use it when you have multiple independent async operations and you need all of them to complete before proceeding:

```javascript
async function loadDashboard() {
  try {
    const [user, settings, notifications] = await Promise.all([
      fetchUser(),
      fetchSettings(),
      fetchNotifications()
    ]);
    
    renderDashboard({ user, settings, notifications });
  } catch (error) {
    showError('Failed to load dashboard');
  }
}
```

**Important gotcha:**

```javascript
const promises = [
  Promise.resolve(1),
  Promise.reject('Error'),
  Promise.resolve(3)
];

Promise.all(promises)
  .then(results => console.log(results))
  .catch(error => console.log(error)); // 'Error'
  
// We never get results for promise 1 and 3!
```

If you need to handle some failures gracefully, use Promise.allSettled() instead.

**Performance benefit:**

Instead of this (sequential):
```javascript
const user = await fetchUser();      // 1 second
const posts = await fetchPosts();    // 1 second
const comments = await fetchComments(); // 1 second
// Total: 3 seconds
```

Use this (parallel):
```javascript
const [user, posts, comments] = await Promise.all([
  fetchUser(),
  fetchPosts(),
  fetchComments()
]);
// Total: 1 second (all run at once)
```

So Promise.all() is great for performance when you have multiple independent operations."

---

### Q14: What's the difference between Promise.all, Promise.race, Promise.allSettled, and Promise.any?

**How to Answer:**

"These are four different ways to handle multiple promises, each with different behavior:

**Promise.all()** - Waits for ALL promises to fulfill, or rejects if ANY rejects:

```javascript
Promise.all([promise1, promise2, promise3])
  .then(results => {
    // All succeeded - results is array of all values
  })
  .catch(error => {
    // Any one failed - error is the first rejection
  });
```

Use when: You need all results and any failure should stop everything.

**Promise.race()** - Returns as soon as ANY promise settles (fulfills or rejects):

```javascript
Promise.race([promise1, promise2, promise3])
  .then(result => {
    // First one to finish - result is from the fastest
  })
  .catch(error => {
    // First one to fail - error from the fastest
  });
```

Use when: You want the fastest result, like implementing timeouts:

```javascript
Promise.race([
  fetch('/api/data'),
  new Promise((_, reject) => 
    setTimeout(() => reject('Timeout'), 5000)
  )
]);
```

**Promise.allSettled()** - Waits for ALL promises to settle, never rejects:

```javascript
Promise.allSettled([promise1, promise2, promise3])
  .then(results => {
    // Always succeeds - results is array of objects:
    // { status: 'fulfilled', value: ... }
    // { status: 'rejected', reason: ... }
    
    results.forEach(result => {
      if (result.status === 'fulfilled') {
        console.log('Success:', result.value);
      } else {
        console.log('Failed:', result.reason);
      }
    });
  });
```

Use when: You want to try all operations and handle successes/failures individually.

**Promise.any()** - Returns as soon as ANY promise fulfills, rejects only if ALL reject:

```javascript
Promise.any([promise1, promise2, promise3])
  .then(result => {
    // First one to succeed - result is from first fulfillment
  })
  .catch(error => {
    // All failed - error is AggregateError with all rejections
  });
```

Use when: You have multiple sources for the same data (like multiple CDNs) and want the first successful one:

```javascript
Promise.any([
  fetch('https://cdn1.example.com/image.jpg'),
  fetch('https://cdn2.example.com/image.jpg'),
  fetch('https://cdn3.example.com/image.jpg')
]).then(response => {
  // Use the first successful response
});
```

**Quick comparison:**

| Method | Resolves when | Rejects when |
|--------|--------------|--------------|
| Promise.all | All fulfill | Any rejects |
| Promise.race | Any settles | First to reject |
| Promise.allSettled | All settle | Never |
| Promise.any | Any fulfills | All reject |

**Most common in interviews:** Promise.all() and Promise.race() are asked most often, but knowing allSettled() and any() shows deeper understanding."

---

## Promise Chaining

### Q15: How does Promise chaining work?

**How to Answer:**

"Promise chaining is when you chain multiple `.then()` calls together. Each `.then()` returns a new promise, so you can keep chaining.

**Basic chaining:**

```javascript
fetch('/api/user')
  .then(response => response.json())
  .then(user => {
    console.log('User:', user);
    return fetch(`/api/posts/${user.id}`);
  })
  .then(response => response.json())
  .then(posts => {
    console.log('Posts:', posts);
  })
  .catch(error => {
    console.log('Error at any step:', error);
  });
```

**Key concepts:**

**1. Each .then() returns a new promise:**

```javascript
const promise1 = fetch('/api/data');
const promise2 = promise1.then(response => response.json());
const promise3 = promise2.then(data => processData(data));
// Each step is a new promise
```

**2. Return values become the next promise's value:**

```javascript
Promise.resolve(5)
  .then(value => {
    console.log(value); // 5
    return value * 2;
  })
  .then(value => {
    console.log(value); // 10
    return value + 3;
  })
  .then(value => {
    console.log(value); // 13
  });
```

**3. If you return a promise, it's automatically unwrapped:**

```javascript
getUserId()
  .then(id => {
    return fetch(`/api/users/${id}`); // Returns a promise
  })
  .then(response => {
    // response is the fetch result, not a promise
    return response.json();
  })
  .then(user => {
    console.log(user);
  });
```

**4. Error propagates down the chain:**

```javascript
doStep1()
  .then(doStep2)
  .then(doStep3)
  .then(doStep4)
  .catch(error => {
    // Catches error from any step above
    console.log('Error:', error);
  });
```

**5. You can recover from errors:**

```javascript
fetch('/api/data')
  .then(response => response.json())
  .catch(error => {
    console.log('Error, using fallback data');
    return { fallback: true }; // Recovery
  })
  .then(data => {
    // This runs whether we got real data or fallback
    console.log(data);
  });
```

**Important gotcha - not returning the promise:**

```javascript
// Wrong - promise not returned
fetch('/api/user')
  .then(response => {
    fetch('/api/posts'); // Missing return!
  })
  .then(posts => {
    console.log(posts); // undefined!
  });

// Correct
fetch('/api/user')
  .then(response => {
    return fetch('/api/posts'); // Return the promise
  })
  .then(response => response.json())
  .then(posts => {
    console.log(posts); // Works!
  });
```

Promise chaining is much cleaner than callback hell, but async/await makes it even cleaner."

---

## async/await

### Q16: What is async/await and how does it work?

**How to Answer:**

"async/await is syntactic sugar built on top of promises that makes asynchronous code look and behave more like synchronous code. It makes async code easier to read and write.

**The async keyword** - Declares that a function returns a promise:

```javascript
async function getData() {
  return 'Hello'; // Automatically wrapped in Promise.resolve()
}

// Equivalent to:
function getData() {
  return Promise.resolve('Hello');
}

// Usage:
getData().then(value => console.log(value)); // 'Hello'
```

**The await keyword** - Pauses execution until a promise resolves:

```javascript
async function fetchUser() {
  const response = await fetch('/api/user');
  const user = await response.json();
  return user;
}
```

This is much cleaner than the promise chain equivalent:

```javascript
function fetchUser() {
  return fetch('/api/user')
    .then(response => response.json())
    .then(user => user);
}
```

**Key points:**

**1. await only works inside async functions:**

```javascript
// Wrong
function getData() {
  const data = await fetch('/api/data'); // Error!
}

// Correct
async function getData() {
  const data = await fetch('/api/data'); // Works!
}
```

**2. async functions always return promises:**

```javascript
async function test() {
  return 42;
}

test().then(value => console.log(value)); // 42
```

**3. Error handling with try/catch:**

```javascript
async function fetchData() {
  try {
    const response = await fetch('/api/data');
    const data = await response.json();
    return data;
  } catch (error) {
    console.log('Error:', error);
    throw error; // Re-throw if needed
  }
}
```

**4. Sequential vs Parallel execution:**

```javascript
// Sequential - takes 3 seconds total
async function sequential() {
  const user = await fetchUser();      // 1 second
  const posts = await fetchPosts();    // 1 second
  const comments = await fetchComments(); // 1 second
}

// Parallel - takes 1 second total
async function parallel() {
  const [user, posts, comments] = await Promise.all([
    fetchUser(),
    fetchPosts(),
    fetchComments()
  ]);
}
```

**Real-world example:**

```javascript
async function loadUserDashboard(userId) {
  try {
    // Load user data first
    const user = await fetchUser(userId);
    
    // Then load their posts (needs user ID)
    const posts = await fetchUserPosts(user.id);
    
    // Process and display
    return {
      user,
      posts,
      summary: posts.length + ' posts'
    };
  } catch (error) {
    console.error('Failed to load dashboard:', error);
    throw error;
  }
}
```

async/await is now the preferred way to handle promises because it's more readable and easier to debug."

---

### Q17: What are common mistakes with async/await?

**How to Answer:**

"There are several common mistakes people make with async/await:

**Mistake 1: Forgetting await**

```javascript
// Wrong
async function getData() {
  const data = fetch('/api/data'); // Returns a promise, not data!
  console.log(data); // Promise object, not the actual data
}

// Correct
async function getData() {
  const data = await fetch('/api/data');
  console.log(data); // Actual response
}
```

**Mistake 2: Using await in loops (making things sequential when they could be parallel)**

```javascript
// Slow - each fetch waits for the previous one
async function getUsers(ids) {
  const users = [];
  for (const id of ids) {
    const user = await fetchUser(id); // Wait... wait... wait...
    users.push(user);
  }
  return users;
}

// Fast - all fetches happen at once
async function getUsers(ids) {
  const promises = ids.map(id => fetchUser(id));
  const users = await Promise.all(promises);
  return users;
}
```

**Mistake 3: Not handling errors**

```javascript
// Wrong - errors crash the program
async function getData() {
  const data = await fetch('/api/data');
  return data;
}

// Correct - errors are handled
async function getData() {
  try {
    const data = await fetch('/api/data');
    return data;
  } catch (error) {
    console.error('Error fetching data:', error);
    return null; // Or throw, depending on your needs
  }
}
```

**Mistake 4: Using async when not needed**

```javascript
// Wrong - no await, so async is pointless
async function double(x) {
  return x * 2;
}

// Correct - no async operations, no need for async
function double(x) {
  return x * 2;
}
```

**Mistake 5: Not awaiting in forEach**

```javascript
// Wrong - forEach doesn't wait for async operations
async function processUsers(users) {
  users.forEach(async (user) => {
    await processUser(user); // This doesn't wait!
  });
  console.log('Done'); // Runs immediately, not after processing
}

// Correct - use for...of or Promise.all
async function processUsers(users) {
  for (const user of users) {
    await processUser(user); // This waits
  }
  console.log('Done'); // Runs after all processing
}

// Or parallel
async function processUsers(users) {
  await Promise.all(users.map(user => processUser(user)));
  console.log('Done');
}
```

**Mistake 6: Top-level await in wrong context**

```javascript
// Wrong in older JavaScript
const data = await fetch('/api/data'); // Error outside async function

// Correct - wrap in async function
(async () => {
  const data = await fetch('/api/data');
  console.log(data);
})();

// Or use top-level await (ES2022 in modules)
// This works in ES modules
const data = await fetch('/api/data');
```

The key is understanding that async/await is still promises under the hood, just with nicer syntax."

---

## Error Handling in Async Code

### Q18: How do you handle errors in Promises?

**How to Answer:**

"There are several ways to handle errors in promises:

**Method 1: Using .catch()**

```javascript
fetch('/api/user')
  .then(response => response.json())
  .then(user => console.log(user))
  .catch(error => {
    console.error('Something went wrong:', error);
  });
```

The .catch() will catch any error that occurs in any of the .then() blocks above it.

**Method 2: Using a second argument to .then()**

```javascript
fetch('/api/user')
  .then(
    user => console.log('Success:', user),
    error => console.error('Error:', error)
  );
```

This is less common and less flexible than .catch().

**Method 3: Using .finally() for cleanup**

```javascript
let loading = true;

fetch('/api/user')
  .then(response => response.json())
  .then(user => {
    console.log(user);
    loading = false;
  })
  .catch(error => {
    console.error(error);
    loading = false;
  })
  .finally(() => {
    // This runs whether success or failure
    console.log('Request completed');
  });
```

**Error propagation in chains:**

```javascript
doStep1()
  .then(doStep2)
  .then(doStep3)
  .catch(error => {
    // Catches error from any step
    console.error('Error in chain:', error);
  })
  .then(() => {
    // This runs even after an error
    console.log('Cleanup');
  });
```

**Recovering from errors:**

```javascript
fetch('/api/data')
  .catch(error => {
    console.error('Primary source failed, trying backup');
    return fetch('/api/backup/data');
  })
  .then(response => response.json())
  .then(data => {
    console.log('Got data from primary or backup');
  })
  .catch(error => {
    console.error('Both sources failed:', error);
  });
```

**Multiple catch blocks:**

```javascript
fetch('/api/user')
  .then(response => {
    if (!response.ok) {
      throw new Error('Bad response');
    }
    return response.json();
  })
  .catch(error => {
    console.error('Network or parsing error:', error);
    throw error; // Re-throw to next catch
  })
  .then(user => {
    // Process user
    if (!user.email) {
      throw new Error('Invalid user data');
    }
  })
  .catch(error => {
    console.error('Validation error:', error);
  });
```

**Important:** Always have a .catch() at the end of your promise chains, or you'll get unhandled promise rejection warnings."

---

### Q19: How do you handle errors with async/await?

**How to Answer:**

"With async/await, we use try/catch blocks - just like regular synchronous code:

**Basic try/catch:**

```javascript
async function fetchUser() {
  try {
    const response = await fetch('/api/user');
    const user = await response.json();
    return user;
  } catch (error) {
    console.error('Error fetching user:', error);
    throw error; // Re-throw if you want caller to handle it
  }
}
```

**Handling specific errors:**

```javascript
async function fetchUser(id) {
  try {
    const response = await fetch(`/api/users/${id}`);
    
    if (!response.ok) {
      if (response.status === 404) {
        throw new Error('User not found');
      } else if (response.status === 500) {
        throw new Error('Server error');
      }
    }
    
    const user = await response.json();
    return user;
  } catch (error) {
    if (error.message === 'User not found') {
      console.error('No such user');
      return null;
    } else if (error.name === 'TypeError') {
      console.error('Network error');
      return null;
    } else {
      console.error('Unexpected error:', error);
      throw error;
    }
  }
}
```

**Using finally for cleanup:**

```javascript
async function fetchData() {
  let loading = true;
  
  try {
    const data = await fetch('/api/data');
    return await data.json();
  } catch (error) {
    console.error('Error:', error);
    return null;
  } finally {
    loading = false;
    console.log('Request completed');
  }
}
```

**Handling multiple async operations:**

```javascript
async function loadDashboard() {
  try {
    const user = await fetchUser();
    const posts = await fetchPosts(user.id);
    const comments = await fetchComments(user.id);
    
    return { user, posts, comments };
  } catch (error) {
    // Any error from any step is caught here
    console.error('Dashboard load failed:', error);
    throw error;
  }
}
```

**Handling errors in Promise.all:**

```javascript
async function fetchAllData() {
  try {
    const [users, posts, comments] = await Promise.all([
      fetchUsers(),
      fetchPosts(),
      fetchComments()
    ]);
    
    return { users, posts, comments };
  } catch (error) {
    // If any promise rejects, we catch it here
    console.error('One of the requests failed:', error);
    throw error;
  }
}
```

**Graceful error handling with Promise.allSettled:**

```javascript
async function fetchAllDataGracefully() {
  const results = await Promise.allSettled([
    fetchUsers(),
    fetchPosts(),
    fetchComments()
  ]);
  
  const users = results[0].status === 'fulfilled' ? results[0].value : [];
  const posts = results[1].status === 'fulfilled' ? results[1].value : [];
  const comments = results[2].status === 'fulfilled' ? results[2].value : [];
  
  return { users, posts, comments };
}
```

**Pattern for wrapping try/catch:**

```javascript
// Utility function to avoid repetitive try/catch
async function tryCatch(promise) {
  try {
    const data = await promise;
    return [null, data]; // [error, data]
  } catch (error) {
    return [error, null];
  }
}

// Usage
async function fetchUser() {
  const [error, user] = await tryCatch(fetch('/api/user'));
  
  if (error) {
    console.error('Error:', error);
    return null;
  }
  
  return user;
}
```

The key advantage of try/catch with async/await is that it works just like synchronous error handling, making the code easier to read and reason about."

---

## fetch API

### Q20: How does the fetch API work?

**How to Answer:**

"The fetch API is a modern way to make HTTP requests in JavaScript. It returns a Promise that resolves to a Response object.

**Basic GET request:**

```javascript
fetch('https://api.example.com/users')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

**With async/await:**

```javascript
async function getUsers() {
  try {
    const response = await fetch('https://api.example.com/users');
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error('Error:', error);
  }
}
```

**Important: fetch only rejects on network errors, not HTTP errors:**

```javascript
async function fetchUser() {
  const response = await fetch('/api/user');
  
  // This is a 404 error, but fetch doesn't reject!
  // You need to check response.ok
  
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  
  const user = await response.json();
  return user;
}
```

**Making POST requests:**

```javascript
async function createUser(userData) {
  try {
    const response = await fetch('https://api.example.com/users', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(userData)
    });
    
    if (!response.ok) {
      throw new Error('Failed to create user');
    }
    
    const user = await response.json();
    return user;
  } catch (error) {
    console.error('Error:', error);
    throw error;
  }
}

// Usage
createUser({ name: 'John', email: 'john@example.com' });
```

**Other HTTP methods:**

```javascript
// PUT - Update
fetch('/api/users/1', {
  method: 'PUT',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ name: 'Updated Name' })
});

// DELETE
fetch('/api/users/1', {
  method: 'DELETE'
});

// PATCH - Partial update
fetch('/api/users/1', {
  method: 'PATCH',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ email: 'newemail@example.com' })
});
```

**Adding headers:**

```javascript
fetch('/api/protected', {
  headers: {
    'Authorization': 'Bearer ' + token,
    'Content-Type': 'application/json',
    'Custom-Header': 'value'
  }
});
```

**Response object properties:**

```javascript
const response = await fetch('/api/data');

console.log(response.ok);        // true if status 200-299
console.log(response.status);    // HTTP status code (200, 404, etc.)
console.log(response.statusText); // Status message ('OK', 'Not Found')
console.log(response.headers);   // Response headers

// Different ways to parse response
const json = await response.json();        // Parse as JSON
const text = await response.text();        // Get as text
const blob = await response.blob();        // For files/images
const arrayBuffer = await response.arrayBuffer(); // For binary data
```

**Complete real-world example:**

```javascript
async function apiRequest(url, options = {}) {
  try {
    const response = await fetch(url, {
      ...options,
      headers: {
        'Content-Type': 'application/json',
        ...options.headers,
      },
    });
    
    if (!response.ok) {
      const error = await response.json();
      throw new Error(error.message || 'Request failed');
    }
    
    return await response.json();
  } catch (error) {
    console.error('API Error:', error);
    throw error;
  }
}

// Usage
const user = await apiRequest('/api/users/1');
const newUser = await apiRequest('/api/users', {
  method: 'POST',
  body: JSON.stringify({ name: 'John' })
});
```

fetch is simpler than the old XMLHttpRequest and works well with promises and async/await."

---

## Event Loop

### Q21: What is the Event Loop and how does it work?

**How to Answer:**

"The event loop is the mechanism that allows JavaScript to perform non-blocking operations despite being single-threaded. It's what makes asynchronous code possible.

Here's how it works:

**Components of the event loop:**

1. **Call Stack** - Where JavaScript executes code
2. **Web APIs** - Browser-provided APIs (setTimeout, fetch, DOM events)
3. **Callback Queue (Task Queue)** - Where callbacks wait
4. **Microtask Queue** - Priority queue for promises
5. **Event Loop** - Checks if call stack is empty and moves tasks from queues

**The process:**

```javascript
console.log('Start');

setTimeout(() => {
  console.log('Timeout');
}, 0);

Promise.resolve().then(() => {
  console.log('Promise');
});

console.log('End');

// Output: Start, End, Promise, Timeout
```

Let me explain what happens step by step:

**Step 1:** `console.log('Start')` executes → prints 'Start'

**Step 2:** `setTimeout` is called → callback goes to Web API, which starts timer

**Step 3:** `Promise.resolve().then()` is called → callback goes to Microtask Queue

**Step 4:** `console.log('End')` executes → prints 'End'

**Step 5:** Call stack is now empty, event loop checks queues

**Step 6:** Microtask queue has priority → Promise callback executes → prints 'Promise'

**Step 7:** Timer completes → setTimeout callback moves from Web API to Callback Queue

**Step 8:** Event loop moves setTimeout callback to call stack → prints 'Timeout'

**Visual representation:**

```
Call Stack: [Currently executing code]
       ↓
  Is empty?
       ↓
Microtask Queue: [Promise callbacks] ← Higher priority
       ↓
Callback Queue: [setTimeout, events] ← Lower priority
       ↓
Back to Call Stack
```

**Why this order matters:**

```javascript
setTimeout(() => console.log('1'), 0);

Promise.resolve()
  .then(() => console.log('2'))
  .then(() => console.log('3'));

setTimeout(() => console.log('4'), 0);

// Output: 2, 3, 1, 4
// All promise callbacks run before any setTimeout
```

**Real-world example:**

```javascript
console.log('1: Sync');

setTimeout(() => {
  console.log('2: Timeout');
}, 0);

fetch('https://api.example.com/data')
  .then(response => {
    console.log('3: Fetch resolved');
    return response.json();
  })
  .then(data => {
    console.log('4: Data processed');
  });

Promise.resolve().then(() => {
  console.log('5: Promise');
});

console.log('6: Sync');

// Output: 1, 6, 5, 3, 4, 2
```

The event loop ensures that JavaScript can handle async operations without blocking the main thread. It keeps checking: 'Is the call stack empty? If yes, bring in the next task.'"

---

### Q22: Can you explain the event loop with a diagram or step-by-step example?

**How to Answer:**

"Let me walk through a concrete example step by step:

```javascript
console.log('A');

setTimeout(() => {
  console.log('B');
}, 0);

Promise.resolve().then(() => {
  console.log('C');
});

console.log('D');
```

**Step-by-step breakdown:**

**Initial State:**
- Call Stack: []
- Microtask Queue: []
- Callback Queue: []

**Step 1: Execute console.log('A')**
- Call Stack: [console.log('A')]
- Output: 'A'
- Call Stack: [] (after execution)

**Step 2: Execute setTimeout**
- setTimeout is called
- Web API starts 0ms timer
- Callback moves to Web API, waiting for timer
- Call Stack: [] (setTimeout itself finishes immediately)

**Step 3: Execute Promise.resolve().then()**
- Promise is already resolved
- Callback goes to Microtask Queue
- Call Stack: []
- Microtask Queue: [() => console.log('C')]

**Step 4: Execute console.log('D')**
- Call Stack: [console.log('D')]
- Output: 'D'
- Call Stack: [] (after execution)

**Step 5: Call stack is empty - Event loop checks Microtask Queue**
- Microtask Queue has callback from Promise
- Move to call stack and execute
- Call Stack: [() => console.log('C')]
- Output: 'C'
- Call Stack: []
- Microtask Queue: []

**Step 6: Timer completes (0ms)**
- Callback moves from Web API to Callback Queue
- Callback Queue: [() => console.log('B')]

**Step 7: Call stack empty, Microtask queue empty - Check Callback Queue**
- Move setTimeout callback to call stack
- Call Stack: [() => console.log('B')]
- Output: 'B'
- Call Stack: []

**Final output: A, D, C, B**

**More complex example with nesting:**

```javascript
console.log('1');

setTimeout(() => {
  console.log('2');
  Promise.resolve().then(() => {
    console.log('3');
  });
}, 0);

Promise.resolve().then(() => {
  console.log('4');
  setTimeout(() => {
    console.log('5');
  }, 0);
});

console.log('6');

// Output: 1, 6, 4, 2, 3, 5
```

**Why this order:**

1. Sync code first: 1, 6
2. Microtask queue (Promise): 4
3. During '4', setTimeout schedules '5' (goes to Callback Queue)
4. Callback queue (first setTimeout): 2
5. During '2', Promise schedules '3' (goes to Microtask Queue)
6. Microtask queue has priority: 3
7. Finally callback queue: 5

**Key takeaway:** 
- Synchronous code runs first
- Microtasks (Promises) run next
- Macrotasks (setTimeout, setInterval) run last
- After each macrotask, all microtasks run before the next macrotask

This is why promises always run before setTimeout callbacks, even if both have 0 delay."

---

## Microtasks vs Macrotasks

### Q23: What's the difference between Microtasks and Macrotasks?

**How to Answer:**

"Microtasks and macrotasks are two different types of asynchronous tasks in JavaScript, and they have different priorities in the event loop.

**Macrotasks (Task Queue):**
- setTimeout callbacks
- setInterval callbacks
- setImmediate (Node.js)
- I/O operations
- UI rendering

**Microtasks (Microtask Queue):**
- Promise callbacks (.then, .catch, .finally)
- async/await
- queueMicrotask()
- MutationObserver callbacks

**The key difference is priority:**

After each macrotask, ALL microtasks are processed before the next macrotask runs.

```javascript
setTimeout(() => console.log('Macro 1'), 0);

Promise.resolve()
  .then(() => console.log('Micro 1'))
  .then(() => console.log('Micro 2'));

setTimeout(() => console.log('Macro 2'), 0);

Promise.resolve().then(() => console.log('Micro 3'));

// Output: Micro 1, Micro 2, Micro 3, Macro 1, Macro 2
```

**Why this order:**

1. All synchronous code runs
2. Check Microtask Queue → Run all microtasks (1, 2, 3)
3. Check Macrotask Queue → Run one macrotask (Macro 1)
4. Check Microtask Queue again → Empty
5. Run next macrotask (Macro 2)

**Visual flow:**

```
┌───────────────────────┐
│  Execute Script       │
└───────────┬───────────┘
            │
┌───────────▼───────────┐
│  Microtask Queue      │ ← Process ALL
│  (Promises)           │
└───────────┬───────────┘
            │
┌───────────▼───────────┐
│  Render (if needed)   │
└───────────┬───────────┘
            │
┌───────────▼───────────┐
│  Macrotask Queue      │ ← Process ONE
│  (setTimeout)         │
└───────────┬───────────┘
            │
            └──────────────┐
                          │
            Loop back to check Microtasks
```

**Practical example:**

```javascript
console.log('Start');

setTimeout(() => {
  console.log('Timeout 1');
  Promise.resolve().then(() => console.log('Promise in Timeout 1'));
}, 0);

Promise.resolve()
  .then(() => {
    console.log('Promise 1');
    setTimeout(() => console.log('Timeout in Promise 1'), 0);
  })
  .then(() => console.log('Promise 2'));

setTimeout(() => {
  console.log('Timeout 2');
}, 0);

console.log('End');

// Output:
// Start
// End
// Promise 1
// Promise 2
// Timeout 1
// Promise in Timeout 1
// Timeout in Promise 1
// Timeout 2
```

**Why this matters:**

If you're doing heavy computation in microtasks, you can starve the macrotask queue:

```javascript
function recursiveMicrotask() {
  Promise.resolve().then(recursiveMicrotask);
}

recursiveMicrotask();
setTimeout(() => console.log('This never runs!'), 0);
```

The setTimeout never executes because microtasks keep getting added and processed before checking macrotasks.

**Best practice:** Understand the priority to predict execution order and avoid blocking the event loop."

---

## Global Execution Context

### Q24: What is the Global Execution Context?

**How to Answer:**

"The Global Execution Context is the environment where your JavaScript code runs. When your code first starts executing, JavaScript creates the global execution context.

Think of it as the 'default' or 'base' environment for your code. Every JavaScript program has one global execution context.

**What happens when Global Execution Context is created:**

**Phase 1: Creation Phase**
1. Creates the global object (window in browsers, global in Node.js)
2. Sets up memory for variables and functions (hoisting)
3. Initializes variables to undefined
4. Stores function declarations in memory

**Phase 2: Execution Phase**
1. Executes code line by line
2. Assigns values to variables
3. Executes function calls (creates new execution contexts)

**Example:**

```javascript
var name = 'John';

function greet() {
  console.log('Hello ' + name);
}

greet();
```

**During Creation Phase:**
- `name` is stored in memory and initialized to undefined
- `greet` function is stored in memory with its entire definition
- Global object (window) is created

**During Execution Phase:**
- Line 1: `name` is assigned 'John'
- Line 3-5: `greet` function definition (already in memory, nothing to do)
- Line 7: `greet()` is called → New execution context created for `greet`

**Global vs Function Execution Context:**

```javascript
var globalVar = 'global';

function outer() {
  var outerVar = 'outer';
  
  function inner() {
    var innerVar = 'inner';
    console.log(globalVar, outerVar, innerVar);
  }
  
  inner();
}

outer();
```

**Execution contexts created:**
1. Global Execution Context (has globalVar)
2. outer() Execution Context (has outerVar)
3. inner() Execution Context (has innerVar)

Each execution context has access to its own variables plus all outer contexts (scope chain).

**Global Object:**

In browsers:
```javascript
var globalVar = 'test';
console.log(window.globalVar); // 'test'
console.log(globalVar); // 'test'
// var creates properties on global object
```

With let/const:
```javascript
let notOnWindow = 'test';
console.log(window.notOnWindow); // undefined
console.log(notOnWindow); // 'test'
// let/const don't create properties on global object
```

**This in Global Context:**

```javascript
console.log(this); // window (in browsers)

function regularFunction() {
  console.log(this); // window (in non-strict mode)
}

const arrowFunction = () => {
  console.log(this); // window (inherits from global)
};
```

The global execution context is the foundation of JavaScript's execution environment. Everything starts here."

---

## Closures in Async Context

### Q25: How do closures work with asynchronous code?

**How to Answer:**

"Closures are when a function remembers and accesses variables from its outer scope, even after the outer function has returned. This is particularly important with async code because callbacks execute later but still need access to variables from when they were defined.

**Basic example:**

```javascript
function outer() {
  const message = 'Hello';
  
  setTimeout(() => {
    console.log(message); // Can still access message!
  }, 1000);
}

outer();
// Even though outer() has finished, the setTimeout callback
// can still access 'message' because of closure
```

**Common interview question - Loop with setTimeout:**

```javascript
// Problem: What does this print?
for (var i = 0; i < 3; i++) {
  setTimeout(() => {
    console.log(i);
  }, 1000);
}

// Output: 3, 3, 3 (all print 3!)
```

Why? Because `var` is function-scoped, all three callbacks reference the same `i`. By the time they execute, the loop has finished and `i` is 3.

**Solution 1: Use let (block-scoped)**

```javascript
for (let i = 0; i < 3; i++) {
  setTimeout(() => {
    console.log(i);
  }, 1000);
}

// Output: 0, 1, 2
```

With `let`, each iteration creates a new block scope with its own `i`.

**Solution 2: Use IIFE (Immediately Invoked Function Expression)**

```javascript
for (var i = 0; i < 3; i++) {
  (function(j) {
    setTimeout(() => {
      console.log(j);
    }, 1000);
  })(i);
}

// Output: 0, 1, 2
```

The IIFE creates a new scope for each iteration, capturing the current value of `i` as `j`.

**Solution 3: Pass parameter to setTimeout**

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout((i) => {
    console.log(i);
  }, 1000, i); // Third argument passes i to callback
}

// Output: 0, 1, 2
```

**Closures with event handlers:**

```javascript
function createButtons() {
  for (let i = 0; i < 3; i++) {
    const button = document.createElement('button');
    button.textContent = `Button ${i}`;
    
    button.addEventListener('click', () => {
      console.log(`Button ${i} clicked`); // Closure captures i
    });
    
    document.body.appendChild(button);
  }
}
```

Each event handler has its own closure capturing its respective `i` value.

**Practical async example:**

```javascript
function fetchUserData(userId) {
  const startTime = Date.now();
  
  return fetch(`/api/users/${userId}`)
    .then(response => response.json())
    .then(user => {
      const elapsed = Date.now() - startTime;
      console.log(`Fetched ${user.name} in ${elapsed}ms`);
      // Closure allows access to startTime and userId
      return user;
    });
}
```

**Memory consideration:**

```javascript
function createHeavyCallback() {
  const hugeArray = new Array(1000000).fill('data');
  
  setTimeout(() => {
    console.log('Done');
    // Closure keeps hugeArray in memory even though we don't use it!
  }, 1000);
}
```

Be careful - closures keep all outer scope variables in memory, even if unused. This can cause memory leaks with large data.

Closures are fundamental to JavaScript and essential for understanding how async callbacks work."

---

## this Keyword with Callbacks

### Q26: How does the 'this' keyword work in callbacks?

**How to Answer:**

"The `this` keyword in JavaScript is tricky, especially in callbacks, because its value depends on how the function is called, not where it's defined.

**Problem with regular functions as callbacks:**

```javascript
const user = {
  name: 'John',
  greet: function() {
    console.log('Hello, ' + this.name);
  }
};

user.greet(); // 'Hello, John' - works fine

setTimeout(user.greet, 1000); // 'Hello, undefined'
// this.name is undefined because 'this' is now window/global
```

When you pass `user.greet` to setTimeout, it loses its connection to `user`. The function is called without any object context, so `this` becomes the global object (or undefined in strict mode).

**Solution 1: Arrow functions**

```javascript
const user = {
  name: 'John',
  greet: function() {
    setTimeout(() => {
      console.log('Hello, ' + this.name);
      // Arrow function doesn't have its own 'this'
      // It uses 'this' from the outer scope (user)
    }, 1000);
  }
};

user.greet(); // 'Hello, John' after 1 second
```

Arrow functions don't have their own `this` - they inherit it from the surrounding scope.

**Solution 2: bind()**

```javascript
const user = {
  name: 'John',
  greet: function() {
    console.log('Hello, ' + this.name);
  }
};

setTimeout(user.greet.bind(user), 1000);
// bind() creates a new function with 'this' permanently set to user
```

**Solution 3: Wrapper function**

```javascript
setTimeout(() => user.greet(), 1000);
// The wrapper function calls greet() on user object
```

**Solution 4: Store 'this' in a variable**

```javascript
const user = {
  name: 'John',
  greet: function() {
    const self = this; // Store reference
    setTimeout(function() {
      console.log('Hello, ' + self.name);
    }, 1000);
  }
};
```

**Event handlers:**

```javascript
class Button {
  constructor(label) {
    this.label = label;
  }
  
  // Problem
  handleClick() {
    console.log(this.label); // 'this' is the button element!
  }
  
  // Solution 1: Arrow function
  handleClickArrow = () => {
    console.log(this.label); // Correct 'this'
  }
  
  // Solution 2: Bind in constructor
  constructor(label) {
    this.label = label;
    this.handleClick = this.handleClick.bind(this);
  }
}

const btn = new Button('Click me');
document.querySelector('button').addEventListener('click', btn.handleClick);
```

**Promises and this:**

```javascript
class DataFetcher {
  constructor() {
    this.data = null;
  }
  
  // Problem
  fetchData() {
    fetch('/api/data')
      .then(function(response) {
        this.data = response; // Error! 'this' is undefined
      });
  }
  
  // Solution 1: Arrow function
  fetchData() {
    fetch('/api/data')
      .then(response => {
        this.data = response; // Correct!
      });
  }
  
  // Solution 2: Store this
  fetchData() {
    const self = this;
    fetch('/api/data')
      .then(function(response) {
        self.data = response; // Works
      });
  }
}
```

**async/await and this:**

```javascript
class API {
  constructor() {
    this.baseURL = 'https://api.example.com';
  }
  
  async fetchUser(id) {
    // async functions preserve 'this' context
    const response = await fetch(`${this.baseURL}/users/${id}`);
    return response.json();
  }
  
  // But be careful when passing methods as callbacks
  async loadUser(id) {
    const user = await this.fetchUser(id);
    // This works when called directly
    // But would fail if passed as callback without binding
  }
}

const api = new API();
setTimeout(api.loadUser, 1000); // Error!
setTimeout(() => api.loadUser(1), 1000); // Works
setTimeout(api.loadUser.bind(api, 1), 1000); // Works
```

**General rule:** Use arrow functions for callbacks when you need to preserve `this` from the outer scope. They're the modern, clean solution."

---

## Modules (import/export)

### Q27: What are ES6 modules and how do import/export work?

**How to Answer:**

"ES6 modules are a way to organize and share code between files. Before modules, we had to use script tags or build tools. Now JavaScript has a native module system.

**Named Exports:**

```javascript
// math.js
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

export function multiply(a, b) {
  return a * b;
}

const divide = (a, b) => a / b;
export { divide };

// Importing
import { add, subtract, multiply } from './math.js';

console.log(add(5, 3)); // 8
```

**Default Export:**

```javascript
// user.js
export default class User {
  constructor(name) {
    this.name = name;
  }
}

// Or
const config = { theme: 'dark' };
export default config;

// Importing
import User from './user.js'; // Can name it anything
import AppConfig from './user.js'; // Same file, different name
```

**Mixing named and default:**

```javascript
// api.js
export default function fetchData() {
  // Main function
}

export const API_URL = 'https://api.example.com';
export const timeout = 5000;

// Importing
import fetchData, { API_URL, timeout } from './api.js';
```

**Import everything as an object:**

```javascript
// math.js
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// Importing
import * as math from './math.js';

console.log(math.add(5, 3)); // 8
console.log(math.subtract(5, 3)); // 2
```

**Renaming imports:**

```javascript
import { add as addition, subtract as subtraction } from './math.js';

console.log(addition(5, 3)); // 8
```

**Re-exporting:**

```javascript
// utils/index.js
export { add, subtract } from './math.js';
export { formatDate } from './date.js';
export { default as User } from './user.js';

// Now can import from one place
import { add, formatDate, User } from './utils/index.js';
```

**Dynamic imports (code splitting):**

```javascript
// Load module conditionally
async function loadModule() {
  if (condition) {
    const module = await import('./heavy-module.js');
    module.doSomething();
  }
}

// Load on user action
button.addEventListener('click', async () => {
  const { default: Chart } = await import('./chart.js');
  new Chart(data);
});
```

**Key differences from CommonJS:**

```javascript
// CommonJS (Node.js)
const module = require('./module');
module.exports = { something };

// ES6 Modules
import module from './module.js';
export default { something };
```

**Important points:**

1. **Static imports are hoisted** - they run before any other code in the file
2. **Imports are read-only** - you can't reassign them
3. **Imports are live bindings** - if the exported value changes, imports see the change
4. **Use .js extension** in imports (browsers require it)
5. **Module scope** - variables in modules are private by default

**Using in HTML:**

```html
<!-- Add type="module" to script tag -->
<script type="module" src="app.js"></script>

<!-- Inline module -->
<script type="module">
  import { greet } from './utils.js';
  greet('World');
</script>
```

ES6 modules are now the standard way to organize JavaScript code, both in browsers and Node.js."

---

### Q28: What's the difference between CommonJS and ES6 modules?

**How to Answer:**

"CommonJS and ES6 modules are two different module systems. CommonJS is the older system used in Node.js, while ES6 modules are the modern JavaScript standard.

**Syntax difference:**

```javascript
// CommonJS
const module = require('./module');
const { specific } = require('./module');
module.exports = { something };
exports.something = value;

// ES6 Modules
import module from './module.js';
import { specific } from './module.js';
export default { something };
export const something = value;
```

**Key differences:**

**1. Loading: Synchronous vs Asynchronous**

CommonJS loads modules synchronously:
```javascript
const fs = require('fs'); // Blocks until loaded
console.log('Loaded');
```

ES6 modules load asynchronously:
```javascript
import fs from 'fs'; // Non-blocking
console.log('Loaded');
```

**2. Timing: Runtime vs Parse time**

CommonJS: Modules are loaded at runtime
```javascript
if (condition) {
  const module = require('./module'); // Can be conditional
}
```

ES6: Imports are static and hoisted
```javascript
if (condition) {
  import module from './module'; // Syntax error!
}

// Must use dynamic import for conditional loading
if (condition) {
  const module = await import('./module.js'); // Works
}
```

**3. Values: Copies vs Live bindings**

CommonJS exports copies:
```javascript
// counter.js
let count = 0;
module.exports = {
  count,
  increment() { count++; }
};

// main.js
const counter = require('./counter');
console.log(counter.count); // 0
counter.increment();
console.log(counter.count); // Still 0! (copy, not live)
```

ES6 exports live bindings:
```javascript
// counter.js
export let count = 0;
export function increment() { count++; }

// main.js
import { count, increment } from './counter.js';
console.log(count); // 0
increment();
console.log(count); // 1 (live binding!)
```

**4. Tree shaking:**

ES6 modules support tree shaking (dead code elimination):
```javascript
// With ES6 modules, bundlers can detect unused exports
import { add } from './math.js'; // Only 'add' gets bundled

// CommonJS imports everything
const { add } = require('./math.js'); // Whole module bundled
```

**5. this keyword:**

CommonJS: `this` refers to `module.exports`
```javascript
console.log(this === module.exports); // true
```

ES6: `this` is undefined in modules
```javascript
console.log(this); // undefined
```

**6. File extensions:**

CommonJS: .js files are CommonJS by default in Node
```javascript
require('./file'); // .js assumed
```

ES6: Needs .mjs or "type": "module" in package.json
```javascript
import './file.js'; // Extension required in browsers
```

**Current state in Node.js:**

Node.js now supports both:

```javascript
// package.json
{
  "type": "module" // Makes .js files ES6 modules
}

// Or use .mjs for ES6, .cjs for CommonJS
```

**Interoperability:**

```javascript
// Can import CommonJS in ES6
import module from './commonjs-module.js';

// Cannot require() ES6 modules in CommonJS
// Must use dynamic import
const module = await import('./es6-module.js');
```

**Which to use:**

- **Frontend:** Always ES6 modules
- **Node.js:** ES6 modules are now recommended
- **Legacy code:** Still uses CommonJS

ES6 modules are the future. They're more powerful, better optimized, and work everywhere."

---

## NPM & NPX Basics

### Q29: What are NPM and NPX? What's the difference?

**How to Answer:**

"NPM and NPX are both Node.js tools, but they serve different purposes.

**NPM (Node Package Manager):**

NPM is a package manager for JavaScript. It helps you install, manage, and share code packages.

**Basic NPM commands:**

```bash
# Initialize a new project
npm init

# Install a package locally
npm install package-name
# or
npm i package-name

# Install globally
npm install -g package-name

# Install as dev dependency
npm install --save-dev package-name
# or
npm i -D package-name

# Remove a package
npm uninstall package-name

# Update packages
npm update

# List installed packages
npm list
```

**package.json:**

```json
{
  "name": "my-project",
  "version": "1.0.0",
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js",
    "test": "jest"
  },
  "dependencies": {
    "express": "^4.18.0",
    "react": "^18.2.0"
  },
  "devDependencies": {
    "nodemon": "^2.0.20",
    "jest": "^29.0.0"
  }
}
```

**Running scripts:**

```bash
npm run start
npm run dev
npm run test

# 'start' and 'test' can be run without 'run'
npm start
npm test
```

**NPX (Node Package Execute):**

NPX is a tool for executing packages without installing them globally.

**Key differences:**

**NPM:**
```bash
# Install first
npm install -g create-react-app

# Then use
create-react-app my-app
```

**NPX:**
```bash
# Execute directly without installing
npx create-react-app my-app

# Runs the latest version each time
```

**Why use NPX:**

**1. No global installations polluting your system**
```bash
# Old way
npm install -g typescript
tsc --version

# NPX way
npx tsc --version
```

**2. Always use latest version**
```bash
npx create-react-app my-app
# Uses latest version without updating global install
```

**3. Try packages without installing**
```bash
npx cowsay "Hello"
# Downloads, runs, then removes
```

**4. Run different versions**
```bash
npx typescript@4.5.0 --version
npx typescript@latest --version
```

**5. Execute package from GitHub**
```bash
npx github:user/repo
```

**Common NPX use cases:**

```bash
# Create new projects
npx create-react-app my-app
npx create-next-app my-app
npx degit user/template my-app

# Run build tools
npx webpack
npx vite build

# Run linters and formatters
npx eslint .
npx prettier --write .

# Database migrations
npx prisma migrate

# Run scripts from package.json without npm run
npx some-script
```

**Local vs Global:**

```bash
# If package is installed locally, npx uses local version
npm install typescript
npx tsc --version # Uses local version

# If not installed, npx downloads and runs it
npx some-package # Downloads temporarily
```

**package-lock.json:**

This file locks exact versions of dependencies:

```json
{
  "name": "my-project",
  "lockfileVersion": 2,
  "requires": true,
  "packages": {
    "node_modules/react": {
      "version": "18.2.0",
      "resolved": "https://registry.npmjs.org/react/-/react-18.2.0.tgz"
    }
  }
}
```

Always commit package-lock.json - it ensures everyone gets exact same versions.

**node_modules:**

This folder contains all installed packages:

```bash
my-project/
  node_modules/        # All packages (don't commit to Git!)
  package.json         # Dependencies list
  package-lock.json    # Exact versions
```

**Semantic Versioning:**

```json
{
  "dependencies": {
    "react": "^18.2.0",
    //        ^ = Compatible with version
    "express": "~4.18.0",
    //         ~ = Approximately equivalent
    "lodash": "4.17.21"
    //        No prefix = Exact version
  }
}
```

**Summary:**
- **NPM:** Package manager for installing and managing dependencies
- **NPX:** Package executor for running packages without installing them

In modern workflows, you use NPM for dependencies your project needs, and NPX for one-time commands and tools."

---

## Throttling & Debouncing

### Q30: What is Debouncing? Implement it.

**How to Answer:**

"Debouncing is a technique to limit how often a function executes. It ensures a function only runs after a certain amount of time has passed since it was last called.

Think of it like an elevator - it waits a few seconds after the last person enters before moving, rather than moving every time someone gets in.

**Use case:** Search input that calls an API

Without debouncing:
```javascript
// User types 'hello'
// API called: 'h'
// API called: 'he'
// API called: 'hel'
// API called: 'hell'
// API called: 'hello'
// 5 unnecessary API calls!
```

With debouncing:
```javascript
// User types 'hello'
// Wait 300ms after last keystroke
// API called once: 'hello'
```

**Implementation:**

```javascript
function debounce(func, delay) {
  let timeoutId;
  
  return function(...args) {
    // Clear previous timer
    clearTimeout(timeoutId);
    
    // Set new timer
    timeoutId = setTimeout(() => {
      func.apply(this, args);
    }, delay);
  };
}
```

**Usage:**

```javascript
// Search function
function searchAPI(query) {
  console.log('Searching for:', query);
  // API call here
}

// Create debounced version
const debouncedSearch = debounce(searchAPI, 300);

// In event handler
input.addEventListener('input', (e) => {
  debouncedSearch(e.target.value);
});

// Now it only calls API 300ms after user stops typing
```

**Real-world React example:**

```javascript
import { useState, useCallback } from 'react';

function SearchComponent() {
  const [query, setQuery] = useState('');
  
  // Debounced search function
  const debouncedSearch = useCallback(
    debounce((searchTerm) => {
      // API call
      fetch(`/api/search?q=${searchTerm}`)
        .then(res => res.json())
        .then(data => console.log(data));
    }, 300),
    []
  );
  
  const handleChange = (e) => {
    const value = e.target.value;
    setQuery(value);
    debouncedSearch(value);
  };
  
  return <input value={query} onChange={handleChange} />;
}
```

**Enhanced implementation with immediate execution option:**

```javascript
function debounce(func, delay, immediate = false) {
  let timeoutId;
  
  return function(...args) {
    const callNow = immediate && !timeoutId;
    
    clearTimeout(timeoutId);
    
    timeoutId = setTimeout(() => {
      timeoutId = null;
      if (!immediate) {
        func.apply(this, args);
      }
    }, delay);
    
    if (callNow) {
      func.apply(this, args);
    }
  };
}

// Usage
const debouncedScroll = debounce(handleScroll, 200, true);
// First call executes immediately, then waits
```

**Common use cases:**

1. **Search input** - Wait for user to stop typing
2. **Window resize** - Recalculate layout after resizing stops
3. **Form validation** - Validate after user finishes input
4. **Save draft** - Auto-save after user stops editing
5. **API calls** - Reduce unnecessary requests

**Vanilla JavaScript example:**

```javascript
// Debounced window resize handler
const handleResize = debounce(() => {
  console.log('Window resized:', window.innerWidth);
}, 250);

window.addEventListener('resize', handleResize);

// Debounced form validation
const validateForm = debounce((formData) => {
  console.log('Validating:', formData);
  // Validation logic
}, 500);

form.addEventListener('input', () => {
  validateForm(new FormData(form));
});
```

Debouncing saves resources by reducing the number of function calls, especially important for expensive operations like API calls or DOM manipulations."

---

### Q31: What is Throttling? How is it different from Debouncing?

**How to Answer:**

"Throttling limits the rate at which a function can execute. It ensures a function runs at most once every X milliseconds, regardless of how many times it's called.

Think of it like a toll booth that lets one car through every few seconds, no matter how many cars are waiting.

**Difference from Debouncing:**

**Debouncing:** 'Wait until activity stops'
- Only executes after quiet period
- Good for: search, form validation, resize events

**Throttling:** 'Execute at regular intervals'
- Executes at fixed rate
- Good for: scroll, mouse move, continuous events

**Implementation:**

```javascript
function throttle(func, limit) {
  let inThrottle;
  
  return function(...args) {
    if (!inThrottle) {
      func.apply(this, args);
      inThrottle = true;
      
      setTimeout(() => {
        inThrottle = false;
      }, limit);
    }
  };
}
```

**Usage:**

```javascript
function trackScroll() {
  console.log('Scroll position:', window.scrollY);
  // Update UI based on scroll
}

// Throttle to run at most once every 200ms
const throttledScroll = throttle(trackScroll, 200);

window.addEventListener('scroll', throttledScroll);

// Even if scroll fires 100 times per second,
// trackScroll only runs 5 times per second
```

**Enhanced implementation with trailing call:**

```javascript
function throttle(func, limit) {
  let inThrottle;
  let lastFunc;
  let lastRan;
  
  return function(...args) {
    if (!inThrottle) {
      func.apply(this, args);
      lastRan = Date.now();
      inThrottle = true;
    } else {
      clearTimeout(lastFunc);
      lastFunc = setTimeout(() => {
        if ((Date.now() - lastRan) >= limit) {
          func.apply(this, args);
          lastRan = Date.now();
        }
      }, limit - (Date.now() - lastRan));
    }
  };
}
```

**Visual comparison:**

```
User action: ||||||||||||||||||||||||||||||||
             0ms    500ms   1000ms   1500ms

Debounce (300ms delay):
Executes:                                  ✓
(Only after 300ms of silence)

Throttle (300ms limit):
Executes:    ✓      ✓       ✓        ✓
(Every 300ms regardless)

No optimization:
Executes:    ✓✓✓✓✓✓✓✓✓✓✓✓✓✓✓✓✓✓✓✓✓✓✓✓✓✓
(Too many!)
```

**Common use cases:**

**Throttling:**
1. **Infinite scroll** - Load more items as user scrolls
2. **Mouse tracking** - Update cursor position
3. **Game loop** - Limit frame rate
4. **Button clicks** - Prevent spam clicking
5. **Progress bar updates** - Smooth updates without overload

**Examples:**

**Scroll tracking:**
```javascript
const trackScrollPosition = throttle(() => {
  const scrolled = (window.scrollY / document.body.scrollHeight) * 100;
  updateProgressBar(scrolled);
}, 100);

window.addEventListener('scroll', trackScrollPosition);
```

**Mouse tracking:**
```javascript
const trackMousePosition = throttle((e) => {
  console.log(`Mouse at: ${e.clientX}, ${e.clientY}`);
  updateCursor(e.clientX, e.clientY);
}, 50);

document.addEventListener('mousemove', trackMousePosition);
```

**Button spam prevention:**
```javascript
const handleSubmit = throttle((e) => {
  e.preventDefault();
  // Submit form
  console.log('Form submitted');
}, 2000); // Can only submit once every 2 seconds

button.addEventListener('click', handleSubmit);
```

**Infinite scroll:**
```javascript
const loadMoreContent = throttle(() => {
  const scrollBottom = window.innerHeight + window.scrollY;
  const pageBottom = document.body.offsetHeight;
  
  if (scrollBottom >= pageBottom - 100) {
    console.log('Load more content');
    fetchMoreData();
  }
}, 200);

window.addEventListener('scroll', loadMoreContent);
```

**API rate limiting:**
```javascript
const apiCall = throttle((data) => {
  fetch('/api/update', {
    method: 'POST',
    body: JSON.stringify(data)
  });
}, 1000); // Max 1 call per second

// User makes many changes
input.addEventListener('input', () => {
  apiCall(getData()); // Throttled to 1 call/second
});
```

**Quick comparison:**

| Feature | Debouncing | Throttling |
|---------|-----------|-----------|
| Execution | After quiet period | At regular intervals |
| Use case | Search, validation | Scroll, mouse move |
| Frequency | Once after pause | Multiple times at fixed rate |
| Example | Auto-save | Progress updates |

**When to use which:**

**Use Debouncing when:**
- You want to wait for user to finish (search, form input)
- Last value is most important
- Action is expensive (API calls)

**Use Throttling when:**
- You want consistent updates (scroll progress, mouse tracking)
- Regular intervals matter
- Continuous feedback needed

Both techniques improve performance by reducing the number of function executions."

---

## AbortController

### Q32: What is AbortController and how do you use it?

**How to Answer:**

"AbortController is a Web API that allows you to cancel ongoing fetch requests. This is useful when a request is no longer needed - like when a user navigates away or types a new search query.

**Basic usage:**

```javascript
const controller = new AbortController();
const signal = controller.signal;

fetch('/api/data', { signal })
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => {
    if (error.name === 'AbortError') {
      console.log('Fetch aborted');
    } else {
      console.error('Fetch error:', error);
    }
  });

// Cancel the request
controller.abort();
```

**Real-world example - Search with cancellation:**

```javascript
let controller = null;

async function search(query) {
  // Cancel previous request if it exists
  if (controller) {
    controller.abort();
  }
  
  // Create new controller for this request
  controller = new AbortController();
  
  try {
    const response = await fetch(`/api/search?q=${query}`, {
      signal: controller.signal
    });
    
    const data = await response.json();
    displayResults(data);
  } catch (error) {
    if (error.name === 'AbortError') {
      console.log('Search cancelled');
    } else {
      console.error('Search error:', error);
    }
  }
}

// User typing
input.addEventListener('input', (e) => {
  search(e.target.value);
  // Each new keystroke cancels previous request
});
```

**With timeout:**

```javascript
async function fetchWithTimeout(url, timeout = 5000) {
  const controller = new AbortController();
  
  const timeoutId = setTimeout(() => {
    controller.abort();
  }, timeout);
  
  try {
    const response = await fetch(url, { signal: controller.signal });
    clearTimeout(timeoutId);
    return await response.json();
  } catch (error) {
    if (error.name === 'AbortError') {
      throw new Error('Request timeout');
    }
    throw error;
  }
}

// Usage
try {
  const data = await fetchWithTimeout('/api/data', 3000);
  console.log(data);
} catch (error) {
  console.error(error.message); // 'Request timeout' after 3 seconds
}
```

**React example:**

```javascript
import { useState, useEffect } from 'react';

function UserSearch() {
  const [query, setQuery] = useState('');
  const [results, setResults] = useState([]);
  
  useEffect(() => {
    if (!query) return;
    
    const controller = new AbortController();
    
    async function search() {
      try {
        const response = await fetch(
          `/api/search?q=${query}`,
          { signal: controller.signal }
        );
        const data = await response.json();
        setResults(data);
      } catch (error) {
        if (error.name === 'AbortError') {
          console.log('Request cancelled');
        } else {
          console.error('Error:', error);
        }
      }
    }
    
    search();
    
    // Cleanup: abort request if component unmounts or query changes
    return () => {
      controller.abort();
    };
  }, [query]);
  
  return (
    <div>
      <input value={query} onChange={(e) => setQuery(e.target.value)} />
      <ul>
        {results.map(item => <li key={item.id}>{item.name}</li>)}
      </ul>
    </div>
  );
}
```

**Multiple requests with one controller:**

```javascript
const controller = new AbortController();

// Abort all these requests at once
Promise.all([
  fetch('/api/users', { signal: controller.signal }),
  fetch('/api/posts', { signal: controller.signal }),
  fetch('/api/comments', { signal: controller.signal })
])
  .then(responses => Promise.all(responses.map(r => r.json())))
  .then(data => console.log(data))
  .catch(error => console.error(error));

// Cancel all
controller.abort();
```

**Custom abort reasons:**

```javascript
const controller = new AbortController();

// Abort with custom reason
controller.abort('User navigated away');

fetch('/api/data', { signal: controller.signal })
  .catch(error => {
    console.log(error.message); // 'User navigated away'
  });
```

**Using with other async operations:**

```javascript
// AbortController can be used beyond fetch
function sleep(ms, signal) {
  return new Promise((resolve, reject) => {
    const timeout = setTimeout(resolve, ms);
    
    signal.addEventListener('abort', () => {
      clearTimeout(timeout);
      reject(new DOMException('Aborted', 'AbortError'));
    });
  });
}

const controller = new AbortController();

sleep(5000, controller.signal)
  .then(() => console.log('Sleep completed'))
  .catch(error => console.log('Sleep aborted'));

// Cancel after 2 seconds
setTimeout(() => controller.abort(), 2000);
```

**Checking if aborted:**

```javascript
const controller = new AbortController();
const signal = controller.signal;

// Check if signal is aborted
console.log(signal.aborted); // false

controller.abort();

console.log(signal.aborted); // true

// Listen for abort event
signal.addEventListener('abort', () => {
  console.log('Aborted!');
});
```

AbortController is essential for modern web applications where users may trigger multiple requests or navigate before requests complete. It prevents memory leaks and unnecessary processing."

---

## Common Patterns & Best Practices

### Q33: What are some async/await best practices?

**How to Answer:**

"Here are the key best practices for writing async/await code:

**1. Always handle errors with try/catch**

```javascript
// Bad
async function fetchData() {
  const data = await fetch('/api/data');
  return data; // Errors will crash
}

// Good
async function fetchData() {
  try {
    const data = await fetch('/api/data');
    return data;
  } catch (error) {
    console.error('Error:', error);
    throw error; // Or handle gracefully
  }
}
```

**2. Run independent operations in parallel**

```javascript
// Bad - Sequential (3 seconds total)
async function loadData() {
  const users = await fetchUsers();      // 1 sec
  const posts = await fetchPosts();      // 1 sec
  const comments = await fetchComments(); // 1 sec
  return { users, posts, comments };
}

// Good - Parallel (1 second total)
async function loadData() {
  const [users, posts, comments] = await Promise.all([
    fetchUsers(),
    fetchPosts(),
    fetchComments()
  ]);
  return { users, posts, comments };
}
```

**3. Use Promise.allSettled for partial failures**

```javascript
async function loadDashboard() {
  const results = await Promise.allSettled([
    fetchUsers(),
    fetchPosts(),
    fetchStats()
  ]);
  
  const users = results[0].status === 'fulfilled' ? results[0].value : [];
  const posts = results[1].status === 'fulfilled' ? results[1].value : [];
  const stats = results[2].status === 'fulfilled' ? results[2].value : null;
  
  return { users, posts, stats };
}
```

**4. Avoid async in array methods (forEach, map, filter)**

```javascript
// Bad - doesn't wait
users.forEach(async (user) => {
  await updateUser(user); // Doesn't actually wait!
});

// Good - use for...of
for (const user of users) {
  await updateUser(user);
}

// Or Promise.all for parallel
await Promise.all(users.map(user => updateUser(user)));
```

**5. Return promises directly when possible**

```javascript
// Unnecessary async/await
async function getUser(id) {
  return await fetch(`/api/users/${id}`);
}

// Better - just return the promise
function getUser(id) {
  return fetch(`/api/users/${id}`);
}

// Only use async if you need to await something
async function getUser(id) {
  const response = await fetch(`/api/users/${id}`);
  return response.json(); // Need await here
}
```

**6. Use descriptive error messages**

```javascript
async function fetchUser(id) {
  try {
    const response = await fetch(`/api/users/${id}`);
    
    if (!response.ok) {
      throw new Error(`Failed to fetch user ${id}: ${response.status}`);
    }
    
    return await response.json();
  } catch (error) {
    console.error(`Error fetching user ${id}:`, error);
    throw error;
  }
}
```

**7. Create helper functions for repeated patterns**

```javascript
// Generic fetch wrapper
async function apiRequest(url, options = {}) {
  try {
    const response = await fetch(url, {
      headers: {
        'Content-Type': 'application/json',
        ...options.headers,
      },
      ...options,
    });
    
    if (!response.ok) {
      throw new Error(`HTTP ${response.status}: ${response.statusText}`);
    }
    
    return await response.json();
  } catch (error) {
    console.error('API request failed:', error);
    throw error;
  }
}

// Usage is much cleaner
const user = await apiRequest('/api/users/1');
const newPost = await apiRequest('/api/posts', {
  method: 'POST',
  body: JSON.stringify({ title: 'Hello' })
});
```

**8. Clean up async operations in useEffect (React)**

```javascript
useEffect(() => {
  let cancelled = false;
  
  async function fetchData() {
    try {
      const data = await fetch('/api/data');
      if (!cancelled) {
        setData(data);
      }
    } catch (error) {
      if (!cancelled) {
        setError(error);
      }
    }
  }
  
  fetchData();
  
  return () => {
    cancelled = true; // Cleanup
  };
}, []);
```

**9. Use timeout wrappers for reliability**

```javascript
async function fetchWithTimeout(url, timeout = 5000) {
  const controller = new AbortController();
  
  const timeoutId = setTimeout(() => controller.abort(), timeout);
  
  try {
    const response = await fetch(url, { signal: controller.signal });
    clearTimeout(timeoutId);
    return await response.json();
  } catch (error) {
    if (error.name === 'AbortError') {
      throw new Error('Request timeout');
    }
    throw error;
  }
}
```

**10. Retry failed requests**

```javascript
async function fetchWithRetry(url, maxRetries = 3) {
  for (let i = 0; i < maxRetries; i++) {
    try {
      const response = await fetch(url);
      return await response.json();
    } catch (error) {
      if (i === maxRetries - 1) throw error;
      
      // Wait before retry (exponential backoff)
      await new Promise(resolve => setTimeout(resolve, 1000 * (i + 1)));
      console.log(`Retry ${i + 1}/${maxRetries}`);
    }
  }
}
```

Following these practices makes async code more reliable, maintainable, and performant."

---

### Q34: What are common async interview questions/problems?

**How to Answer:**

"Here are some common async problems you might see in interviews:

**1. Implement promiseAll**

```javascript
function promiseAll(promises) {
  return new Promise((resolve, reject) => {
    if (promises.length === 0) {
      resolve([]);
      return;
    }
    
    const results = [];
    let completed = 0;
    
    promises.forEach((promise, index) => {
      Promise.resolve(promise)
        .then(value => {
          results[index] = value;
          completed++;
          
          if (completed === promises.length) {
            resolve(results);
          }
        })
        .catch(reject);
    });
  });
}

// Usage
promiseAll([Promise.resolve(1), Promise.resolve(2), Promise.resolve(3)])
  .then(results => console.log(results)); // [1, 2, 3]
```

**2. Implement sequential promise execution**

```javascript
async function executeSequentially(promises) {
  const results = [];
  
  for (const promise of promises) {
    const result = await promise();
    results.push(result);
  }
  
  return results;
}

// Usage
const tasks = [
  () => new Promise(resolve => setTimeout(() => resolve(1), 1000)),
  () => new Promise(resolve => setTimeout(() => resolve(2), 500)),
  () => new Promise(resolve => setTimeout(() => resolve(3), 1500))
];

executeSequentially(tasks).then(console.log); // [1, 2, 3] after 3 seconds total
```

**3. Retry mechanism**

```javascript
async function retry(fn, maxAttempts = 3, delay = 1000) {
  for (let attempt = 1; attempt <= maxAttempts; attempt++) {
    try {
      return await fn();
    } catch (error) {
      if (attempt === maxAttempts) {
        throw error;
      }
      
      console.log(`Attempt ${attempt} failed, retrying...`);
      await new Promise(resolve => setTimeout(resolve, delay));
    }
  }
}

// Usage
retry(() => fetch('/api/data'))
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('All attempts failed:', error));
```

**4. Rate limiter**

```javascript
function rateLimiter(fn, maxCalls, timeWindow) {
  const queue = [];
  let callsInWindow = 0;
  
  return async function(...args) {
    return new Promise((resolve, reject) => {
      const execute = async () => {
        try {
          callsInWindow++;
          const result = await fn(...args);
          resolve(result);
          
          setTimeout(() => {
            callsInWindow--;
            if (queue.length > 0) {
              const next = queue.shift();
              next();
            }
          }, timeWindow);
        } catch (error) {
          reject(error);
        }
      };
      
      if (callsInWindow < maxCalls) {
        execute();
      } else {
        queue.push(execute);
      }
    });
  };
}

// Usage: Max 3 calls per second
const limitedFetch = rateLimiter(fetch, 3, 1000);
```

**5. Implement sleep/delay**

```javascript
function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

// Usage
async function demo() {
  console.log('Start');
  await sleep(2000);
  console.log('2 seconds later');
}
```

**6. Race with timeout**

```javascript
async function fetchWithTimeout(url, timeout) {
  return Promise.race([
    fetch(url),
    new Promise((_, reject) =>
      setTimeout(() => reject(new Error('Timeout')), timeout)
    )
  ]);
}

// Usage
fetchWithTimeout('/api/data', 5000)
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error.message));
```

**7. Batch requests**

```javascript
async function batchRequests(items, batchSize, processFn) {
  const results = [];
  
  for (let i = 0; i < items.length; i += batchSize) {
    const batch = items.slice(i, i + batchSize);
    const batchResults = await Promise.all(batch.map(processFn));
    results.push(...batchResults);
  }
  
  return results;
}

// Usage: Process 100 items, 10 at a time
const items = Array.from({ length: 100 }, (_, i) => i);
const results = await batchRequests(items, 10, async (item) => {
  return await fetch(`/api/item/${item}`).then(r => r.json());
});
```

**8. Debounced async function**

```javascript
function debounceAsync(fn, delay) {
  let timeoutId;
  let pendingPromise = null;
  
  return function(...args) {
    clearTimeout(timeoutId);
    
    if (pendingPromise) {
      // Cancel previous promise
      pendingPromise = null;
    }
    
    return new Promise((resolve, reject) => {
      timeoutId = setTimeout(async () => {
        try {
          const result = await fn(...args);
          resolve(result);
        } catch (error) {
          reject(error);
        }
      }, delay);
    });
  };
}
```

**9. Implement Promise.race**

```javascript
function promiseRace(promises) {
  return new Promise((resolve, reject) => {
    promises.forEach(promise => {
      Promise.resolve(promise)
        .then(resolve)
        .catch(reject);
    });
  });
}
```

**10. Parallel execution with limit**

```javascript
async function parallelLimit(tasks, limit) {
  const results = [];
  const executing = [];
  
  for (const [index, task] of tasks.entries()) {
    const promise = Promise.resolve().then(() => task());
    results[index] = promise;
    
    if (limit <= tasks.length) {
      const e = promise.then(() => {
        executing.splice(executing.indexOf(e), 1);
      });
      executing.push(e);
      
      if (executing.length >= limit) {
        await Promise.race(executing);
      }
    }
  }
  
  return Promise.all(results);
}

// Usage: Run max 3 tasks at once
const tasks = Array.from({ length: 10 }, (_, i) => 
  () => new Promise(resolve => setTimeout(() => resolve(i), 1000))
);

parallelLimit(tasks, 3).then(console.log);
```

These problems test your understanding of promises, async/await, concurrency, and error handling. Practice implementing them from scratch!"

---

## Final Interview Tips

### How to Answer Async JavaScript Questions

**General Strategy:**

1. **Start with the concept** - Explain what it is in simple terms
2. **Show code example** - Demonstrate with actual code
3. **Explain why it matters** - What problem does it solve?
4. **Mention gotchas** - Common mistakes or edge cases
5. **Compare alternatives** - Show you understand tradeoffs

**Example approach:**
"The event loop is the mechanism that handles async operations in JavaScript. [concept] Let me show you how it works with an example... [code] This is important because it allows JavaScript to handle multiple operations without blocking. [why] A common mistake is thinking setTimeout(0) executes immediately. [gotcha] This is different from how threads work in other languages. [alternative]"

**During the Interview:**

- **Think out loud** - Explain your reasoning
- **Ask clarifying questions** - "Should I handle errors?" "Should this be parallel or sequential?"
- **Start simple, then optimize** - Get working code first
- **Test your logic** - Walk through your code with example values
- **Don't memorize, understand** - Focus on concepts, not exact syntax

**Common Topics by Frequency:**

**Very Common (Asked in 80%+ interviews):**
- Promises vs callbacks
- async/await
- Event loop basics
- Promise.all()
- Error handling

**Common (Asked in 50%+ interviews):**
- setTimeout/setInterval
- fetch API
- Microtasks vs macrotasks
- Closures with async
- Debouncing/Throttling

**Less Common (But good to know):**
- AbortController
- Promise.race/allSettled/any
- Custom promise implementations
- Advanced event loop questions

**Red Flags to Avoid:**

- Saying "I don't know" without trying
- Not handling errors
- Ignoring edge cases
- Overcomplicating simple problems
- Not testing your solution

**Remember:**

- It's okay to not know everything
- Show problem-solving skills
- Communicate clearly
- Write clean, readable code
- Handle errors gracefully

Good luck with your interviews! 🚀

---

**Practice Resources:**

1. **Code along with examples** - Type out all the examples yourself
2. **Modify examples** - Change parameters, add features
3. **Explain to someone else** - Teaching reinforces learning
4. **Build small projects** - Todo app with API, search with debounce
5. **Use browser console** - Test async code in real-time

**Key Takeaways:**

- JavaScript is single-threaded but can handle async operations
- Promises and async/await make async code manageable
- Event loop coordinates execution of sync and async code
- Microtasks have higher priority than macrotasks
- Always handle errors in async code
- Understand when to use parallel vs sequential execution
- Debounce/throttle for performance optimization
- AbortController for canceling requests
- Modules for code organization

Master these concepts and you'll be well-prepared for any async JavaScript interview!