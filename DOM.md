# DOM, OOP & Prototypes Interview Preparation Guide
*How to Answer DOM, OOP, and Prototype Questions Confidently*

**Note for Students:** This guide is written exactly how you should answer in interviews. Practice reading these answers out loud to make them natural when speaking. Focus is on theoretical understanding and verbal explanations.

---

## Table of Contents

### DOM (Document Object Model)
1. [What is the DOM?](#q1-what-is-the-dom)
2. [DOM Selection Methods](#q2-dom-selection-methods)
3. [DOM Manipulation](#q3-dom-manipulation)
4. [Creating and Removing Elements](#q4-creating-and-removing-elements)
5. [DOM Traversal](#q5-dom-traversal)
6. [Attributes vs Properties](#q6-attributes-vs-properties)

### Events
7. [Event Handling](#q7-event-handling)
8. [Event Bubbling and Capturing](#q8-event-bubbling-and-capturing)
9. [Event Delegation](#q9-event-delegation)
10. [preventDefault and stopPropagation](#q10-preventdefault-and-stoppropagation)

### Browser APIs
11. [Window vs Document](#q11-window-vs-document)
12. [localStorage vs sessionStorage](#q12-localstorage-vs-sessionstorage)
13. [Browser Navigation and History](#q13-browser-navigation-and-history)

### OOP Fundamentals
14. [What is OOP?](#q14-what-is-oop)
15. [Classes and Objects](#q15-classes-and-objects)
16. [Constructor Functions](#q16-constructor-functions)
17. [The 'new' Keyword](#q17-the-new-keyword)
18. [Static Methods and Properties](#q18-static-methods-and-properties)

### Prototypes & Inheritance
19. [What is Prototype?](#q19-what-is-prototype)
20. [Prototype Chain](#q20-prototype-chain)
21. [\_\_proto\_\_ vs prototype](#q21-__proto__-vs-prototype)
22. [Prototypal Inheritance](#q22-prototypal-inheritance)
23. [Classical vs Prototypal Inheritance](#q23-classical-vs-prototypal-inheritance)

### Advanced OOP
24. [Inheritance with Classes](#q24-inheritance-with-classes)
25. [Method Overriding](#q25-method-overriding)
26. [Private Fields and Methods](#q26-private-fields-and-methods)
27. [Getters and Setters](#q27-getters-and-setters)
28. [instanceof Operator](#q28-instanceof-operator)

### OOP Principles
29. [Encapsulation](#q29-encapsulation)
30. [Abstraction](#q30-abstraction)
31. [Inheritance](#q31-inheritance)
32. [Polymorphism](#q32-polymorphism)

### Design Patterns
33. [Module Pattern](#q33-module-pattern)
34. [Revealing Module Pattern](#q34-revealing-module-pattern)
35. [Singleton Pattern](#q35-singleton-pattern)
36. [Factory Pattern](#q36-factory-pattern)
37. [Observer Pattern](#q37-observer-pattern)

---

## DOM (Document Object Model)

### Q1: What is the DOM?

**How to Answer:**

"The DOM (Document Object Model) is a programming interface for HTML and XML documents. It represents the page as a tree structure where each HTML element is a node that can be accessed and manipulated using JavaScript.

**Key points about DOM:**

The DOM is NOT JavaScript - it's a Web API provided by the browser. JavaScript uses this API to interact with the webpage.

**How DOM works:**

When a browser loads an HTML page, it creates a DOM tree:

```
Document
  └── html
       ├── head
       │    ├── title
       │    └── meta
       └── body
            ├── h1
            ├── p
            └── div
                 ├── span
                 └── button
```

Each element, text, and attribute becomes a node in this tree.

**Why DOM is important:**

1. **Dynamic manipulation** - Change content without reloading page
2. **Interactivity** - Respond to user actions
3. **Real-time updates** - Update parts of page dynamically
4. **Structure** - Provides organized way to access elements

**DOM is language-agnostic:**

While we use JavaScript most commonly, the DOM can be accessed by any programming language. Python, Ruby, etc. can also interact with DOM.

**Types of nodes:**

1. **Element nodes** - HTML tags like `<div>`, `<p>`
2. **Text nodes** - Text content inside elements
3. **Attribute nodes** - Element attributes like `class`, `id`
4. **Comment nodes** - HTML comments
5. **Document node** - Root of the tree

**Example structure:**

```html
<div id="container" class="main">
  Hello World
  <span>Text</span>
</div>
```

Creates this DOM structure:
- Element node: div
  - Attribute: id="container"
  - Attribute: class="main"
  - Text node: "Hello World"
  - Element node: span
    - Text node: "Text"

**DOM represents live structure:**

The DOM is 'live' - if you modify it with JavaScript, the changes are immediately reflected on the page.

**Interview tip:** Explain that DOM is a tree structure representation of HTML that allows JavaScript to access and manipulate webpage elements. It's not part of JavaScript itself, but a browser API."

---

### Q2: What are the different ways to select DOM elements?

**How to Answer:**

"JavaScript provides several methods to select DOM elements, each with different use cases.

**1. getElementById() - Select by ID:**

Returns a single element with the specified ID. IDs should be unique.

```javascript
const element = document.getElementById('myId');

// Returns the element or null if not found
```

**Characteristics:**
- Very fast (optimized by browsers)
- Returns single element or null
- Most specific selector
- Case-sensitive

**When to use:** When you have a unique ID and need that specific element.

**2. getElementsByClassName() - Select by class:**

Returns a live HTMLCollection of all elements with specified class.

```javascript
const elements = document.getElementsByClassName('myClass');

// Returns HTMLCollection (array-like)
// Can have multiple classes: getElementsByClassName('class1 class2')
```

**Characteristics:**
- Returns live collection (updates automatically)
- Returns all matching elements
- Can select by multiple classes

**When to use:** When you need all elements with a specific class.

**3. getElementsByTagName() - Select by tag:**

Returns live HTMLCollection of all elements with specified tag name.

```javascript
const paragraphs = document.getElementsByTagName('p');
const allElements = document.getElementsByTagName('*'); // All elements
```

**Characteristics:**
- Returns live collection
- Case-insensitive for HTML documents
- Very common for selecting all of a type

**When to use:** When you need all elements of a specific type (all paragraphs, all divs, etc.).

**4. querySelector() - CSS selector (single element):**

Returns the FIRST element matching the CSS selector.

```javascript
const element = document.querySelector('.myClass');
const element = document.querySelector('#myId');
const element = document.querySelector('div.container > p');
const element = document.querySelector('[data-id="123"]');
```

**Characteristics:**
- Uses CSS selector syntax
- Returns first match only
- Returns null if not found
- Static (not live)
- Most flexible selector

**When to use:** When you need the first matching element with complex selection criteria.

**5. querySelectorAll() - CSS selector (all elements):**

Returns a static NodeList of ALL elements matching the CSS selector.

```javascript
const elements = document.querySelectorAll('.myClass');
const elements = document.querySelectorAll('div p'); // All p inside div
const elements = document.querySelectorAll('[data-active="true"]');
```

**Characteristics:**
- Uses CSS selector syntax
- Returns all matches
- Returns static NodeList (doesn't update)
- More flexible than getElementsBy*

**When to use:** Modern approach for selecting multiple elements with complex criteria.

**Comparison table:**

| Method | Returns | Live/Static | Speed | Use Case |
|--------|---------|-------------|-------|----------|
| getElementById | Element | N/A | Fastest | Single element by ID |
| getElementsByClassName | HTMLCollection | Live | Fast | Multiple by class |
| getElementsByTagName | HTMLCollection | Live | Fast | Multiple by tag |
| querySelector | Element | Static | Slower | First match, complex |
| querySelectorAll | NodeList | Static | Slower | All matches, complex |

**Live vs Static:**

```javascript
// Live collection - updates automatically
const liveList = document.getElementsByClassName('item');
console.log(liveList.length); // 3

// Add new element with class 'item'
document.body.innerHTML += '<div class="item">New</div>';
console.log(liveList.length); // 4 (automatically updated!)

// Static collection - snapshot at query time
const staticList = document.querySelectorAll('.item');
console.log(staticList.length); // 4

// Add new element
document.body.innerHTML += '<div class="item">Another</div>';
console.log(staticList.length); // Still 4 (not updated)
```

**HTMLCollection vs NodeList:**

```javascript
// HTMLCollection (live, only elements)
const htmlColl = document.getElementsByClassName('item');
// Can't use forEach directly
Array.from(htmlColl).forEach(item => { });

// NodeList (static, can be any node)
const nodeList = document.querySelectorAll('.item');
// Can use forEach
nodeList.forEach(item => { });
```

**Modern recommendation:**

Use `querySelector()` and `querySelectorAll()` for most cases:
- More flexible (CSS selectors)
- Consistent API
- Easier to maintain

Use `getElementById()` when:
- You need maximum performance
- You have a unique ID

**Complex selector examples:**

```javascript
// Attribute selectors
document.querySelector('[type="text"]');
document.querySelector('[data-id]'); // Has attribute

// Combinators
document.querySelector('div > p'); // Direct child
document.querySelector('div p'); // Any descendant
document.querySelector('h1 + p'); // Adjacent sibling

// Pseudo-classes
document.querySelector('li:first-child');
document.querySelector('input:checked');
document.querySelector('div:not(.exclude)');

// Multiple conditions
document.querySelector('div.container.active[data-id="1"]');
```

**Performance considerations:**

1. **getElementById** - Fastest, O(1)
2. **getElementsBy*** - Fast, native implementation
3. **querySelector*** - Slower, more complex parsing

For most applications, the performance difference is negligible. Prioritize code readability.

**Interview tip:** Know all methods but emphasize querySelector/querySelectorAll as the modern approach. Mention that getElementById is fastest for simple selections. Explain the difference between live and static collections."

---

### Q3: How do you manipulate DOM elements?

**How to Answer:**

"DOM manipulation means changing the content, structure, or styling of elements after the page has loaded. There are several ways to do this.

**1. Changing content:**

**textContent - Plain text only:**

```javascript
const element = document.querySelector('p');

// Get text
console.log(element.textContent); // "Hello World"

// Set text (safe, no HTML parsing)
element.textContent = 'New text';
element.textContent = '<strong>Text</strong>'; // Shows literally, not as HTML
```

**innerHTML - HTML content:**

```javascript
const element = document.querySelector('div');

// Get HTML
console.log(element.innerHTML); // "<p>Hello</p>"

// Set HTML (parses HTML)
element.innerHTML = '<p>New content</p>';
element.innerHTML = '<strong>Bold text</strong>'; // Renders as bold
```

**innerText vs textContent:**

```javascript
// innerText - respects CSS styling (slower)
// textContent - returns all text, ignores styling (faster)

const element = document.querySelector('div');
element.innerHTML = '<span style="display:none">Hidden</span> Visible';

console.log(element.innerText); // 'Visible' (skips hidden)
console.log(element.textContent); // 'Hidden Visible' (includes hidden)
```

**Security note:**

```javascript
// Dangerous - XSS vulnerability
const userInput = '<img src=x onerror="alert(1)">';
element.innerHTML = userInput; // Executes script!

// Safe
element.textContent = userInput; // Shows as text, doesn't execute
```

**2. Changing styles:**

**Inline styles:**

```javascript
const element = document.querySelector('div');

// Set individual style
element.style.color = 'red';
element.style.backgroundColor = 'blue'; // camelCase for CSS properties
element.style.fontSize = '20px';

// Get computed style (read-only)
const styles = window.getComputedStyle(element);
console.log(styles.color); // rgb(255, 0, 0)
```

**CSS classes (better approach):**

```javascript
const element = document.querySelector('div');

// Add class
element.classList.add('active');
element.classList.add('class1', 'class2'); // Multiple classes

// Remove class
element.classList.remove('active');

// Toggle class
element.classList.toggle('active'); // Add if not present, remove if present

// Check if has class
if (element.classList.contains('active')) {
  console.log('Has active class');
}

// Replace class
element.classList.replace('old', 'new');
```

**Why classList is better than className:**

```javascript
// className - overwrites all classes
element.className = 'new-class'; // Loses all existing classes

// classList - works with individual classes
element.classList.add('new-class'); // Keeps existing classes
```

**3. Changing attributes:**

```javascript
const element = document.querySelector('img');

// Get attribute
const src = element.getAttribute('src');

// Set attribute
element.setAttribute('src', 'new-image.jpg');
element.setAttribute('data-id', '123');

// Remove attribute
element.removeAttribute('data-id');

// Check if has attribute
if (element.hasAttribute('src')) {
  console.log('Has src attribute');
}
```

**Direct property access (for standard attributes):**

```javascript
const link = document.querySelector('a');

// These work for standard HTML attributes
link.href = 'https://example.com';
link.id = 'myLink';
link.className = 'link';

const input = document.querySelector('input');
input.value = 'New value';
input.disabled = true;
```

**4. Modifying structure:**

This is covered in detail in Q4, but brief overview:

```javascript
// Create new element
const newDiv = document.createElement('div');
newDiv.textContent = 'New content';

// Add to DOM
parent.appendChild(newDiv);

// Remove from DOM
element.remove();
```

**Best practices:**

**1. Prefer classList over inline styles:**

```javascript
// Bad
element.style.display = 'none';

// Good - CSS in stylesheet
element.classList.add('hidden'); // .hidden { display: none; }
```

**2. Use textContent for plain text:**

```javascript
// Safer and faster
element.textContent = userInput;
```

**3. Batch DOM updates:**

```javascript
// Bad - multiple reflows
element.style.width = '100px';
element.style.height = '100px';
element.style.background = 'red';

// Good - single reflow
element.style.cssText = 'width: 100px; height: 100px; background: red;';

// Or use class
element.classList.add('styled'); // CSS defines all styles
```

**4. Cache DOM references:**

```javascript
// Bad - queries DOM every time
for (let i = 0; i < 100; i++) {
  document.querySelector('#element').textContent += i;
}

// Good - cache reference
const element = document.querySelector('#element');
for (let i = 0; i < 100; i++) {
  element.textContent += i;
}
```

**Common patterns:**

**Toggle visibility:**

```javascript
const element = document.querySelector('#menu');

// Option 1: classList
element.classList.toggle('hidden');

// Option 2: style
element.style.display = element.style.display === 'none' ? 'block' : 'none';
```

**Change content based on condition:**

```javascript
const button = document.querySelector('button');

if (condition) {
  button.textContent = 'Active';
  button.classList.add('active');
} else {
  button.textContent = 'Inactive';
  button.classList.remove('active');
}
```

**Update multiple elements:**

```javascript
const items = document.querySelectorAll('.item');

items.forEach(item => {
  item.classList.add('highlighted');
  item.style.color = 'blue';
});
```

**Interview tip:** Explain the difference between textContent (safe, plain text) and innerHTML (parses HTML). Emphasize using classList for styling rather than inline styles. Mention security concerns with innerHTML and user input."

---

### Q4: How do you create, insert, and remove DOM elements?

**How to Answer:**

"Creating, inserting, and removing elements allows you to dynamically modify the page structure.

**Creating elements:**

**1. createElement() - Create new element:**

```javascript
// Create element
const newDiv = document.createElement('div');
const newPara = document.createElement('p');
const newButton = document.createElement('button');

// Element exists in memory but not in DOM yet
```

**2. Set up the element:**

```javascript
const newDiv = document.createElement('div');

// Add content
newDiv.textContent = 'Hello World';

// Add classes
newDiv.classList.add('container', 'active');

// Add attributes
newDiv.setAttribute('data-id', '123');
newDiv.id = 'myDiv';

// Add styles (prefer classes)
newDiv.style.color = 'blue';
```

**Inserting elements into DOM:**

**1. appendChild() - Add as last child:**

```javascript
const parent = document.querySelector('#parent');
const newChild = document.createElement('div');

parent.appendChild(newChild);
// Adds newChild as last child of parent
```

**2. append() - Modern alternative (can append text too):**

```javascript
const parent = document.querySelector('#parent');

// Can append multiple items
parent.append(newElement, 'Some text', anotherElement);

// append vs appendChild:
// append() - multiple items, can add text, no return value
// appendChild() - single element only, returns element
```

**3. prepend() - Add as first child:**

```javascript
const parent = document.querySelector('#parent');
const newChild = document.createElement('div');

parent.prepend(newChild);
// Adds newChild as first child
```

**4. insertBefore() - Insert before specific element:**

```javascript
const parent = document.querySelector('#parent');
const referenceNode = document.querySelector('#reference');
const newNode = document.createElement('div');

parent.insertBefore(newNode, referenceNode);
// Inserts newNode before referenceNode
```

**5. insertAdjacentElement() - Insert at specific position:**

```javascript
const element = document.querySelector('#target');
const newElement = document.createElement('div');

// Four positions:
element.insertAdjacentElement('beforebegin', newElement); // Before element
element.insertAdjacentElement('afterbegin', newElement);  // First child
element.insertAdjacentElement('beforeend', newElement);   // Last child
element.insertAdjacentElement('afterend', newElement);    // After element
```

**Visual representation:**

```
<!-- beforebegin -->
<div id="target">
  <!-- afterbegin -->
  Content here
  <!-- beforeend -->
</div>
<!-- afterend -->
```

**6. insertAdjacentHTML() - Insert HTML string:**

```javascript
const element = document.querySelector('#target');

element.insertAdjacentHTML('beforeend', '<p>New paragraph</p>');
// Same positions as insertAdjacentElement
```

**Removing elements:**

**1. remove() - Remove element (modern):**

```javascript
const element = document.querySelector('#toRemove');
element.remove();
// Element is removed from DOM
```

**2. removeChild() - Remove child element:**

```javascript
const parent = document.querySelector('#parent');
const child = document.querySelector('#child');

parent.removeChild(child);
// Returns the removed element
```

**3. Remove all children:**

```javascript
const parent = document.querySelector('#parent');

// Option 1: innerHTML
parent.innerHTML = '';

// Option 2: Loop and remove
while (parent.firstChild) {
  parent.removeChild(parent.firstChild);
}

// Option 3: replaceChildren() - modern
parent.replaceChildren();
```

**Replacing elements:**

**1. replaceChild():**

```javascript
const parent = document.querySelector('#parent');
const oldChild = document.querySelector('#old');
const newChild = document.createElement('div');

parent.replaceChild(newChild, oldChild);
```

**2. replaceWith() - modern:**

```javascript
const oldElement = document.querySelector('#old');
const newElement = document.createElement('div');

oldElement.replaceWith(newElement);
```

**Cloning elements:**

```javascript
const original = document.querySelector('#original');

// Shallow clone (element only)
const shallowClone = original.cloneNode();

// Deep clone (element + all children)
const deepClone = original.cloneNode(true);

// Add clone to DOM
document.body.appendChild(deepClone);
```

**Practical examples:**

**1. Create and add a list item:**

```javascript
// Get list
const ul = document.querySelector('ul');

// Create new item
const li = document.createElement('li');
li.textContent = 'New item';
li.classList.add('list-item');

// Add to list
ul.appendChild(li);
```

**2. Create complex structure:**

```javascript
// Create card
const card = document.createElement('div');
card.classList.add('card');

// Create title
const title = document.createElement('h3');
title.textContent = 'Card Title';

// Create description
const description = document.createElement('p');
description.textContent = 'Card description here';

// Create button
const button = document.createElement('button');
button.textContent = 'Click me';

// Assemble card
card.appendChild(title);
card.appendChild(description);
card.appendChild(button);

// Add to page
document.body.appendChild(card);
```

**3. Remove all items with a class:**

```javascript
const itemsToRemove = document.querySelectorAll('.remove-me');

itemsToRemove.forEach(item => {
  item.remove();
});
```

**4. Replace element content:**

```javascript
const container = document.querySelector('#container');

// Clear existing content
container.innerHTML = '';

// Add new content
const newContent = document.createElement('div');
newContent.textContent = 'Fresh content';
container.appendChild(newContent);
```

**Performance considerations:**

**Document Fragment for multiple insertions:**

```javascript
// Bad - causes multiple reflows
const parent = document.querySelector('#parent');
for (let i = 0; i < 100; i++) {
  const div = document.createElement('div');
  parent.appendChild(div); // Reflow each time
}

// Good - single reflow
const fragment = document.createDocumentFragment();
for (let i = 0; i < 100; i++) {
  const div = document.createElement('div');
  fragment.appendChild(div); // No reflow
}
parent.appendChild(fragment); // Single reflow
```

**Template elements:**

```javascript
// HTML template
<template id="item-template">
  <div class="item">
    <h3></h3>
    <p></p>
  </div>
</template>

// JavaScript
const template = document.querySelector('#item-template');
const clone = template.content.cloneNode(true);

// Modify clone
clone.querySelector('h3').textContent = 'Title';
clone.querySelector('p').textContent = 'Description';

// Add to DOM
document.body.appendChild(clone);
```

**Best practices:**

1. **Create elements in JavaScript, not innerHTML strings** (safer)
2. **Use DocumentFragment for multiple insertions** (faster)
3. **Cache parent references** before manipulating
4. **Remove event listeners** before removing elements (avoid memory leaks)
5. **Use templates** for repeated structures

**Interview tip:** Explain that createElement creates elements in memory, and you need methods like appendChild or append to add them to the DOM. Mention remove() for removing elements. Show you know about DocumentFragment for performance with multiple insertions."

---

### Q5: What is DOM traversal? Explain parent, child, and sibling relationships.

**How to Answer:**

"DOM traversal means navigating through the DOM tree to find related elements - parents, children, or siblings of a given element.

**Understanding the DOM tree:**

```html
<div id="parent">
  <p id="first">First paragraph</p>
  <p id="second">Second paragraph</p>
  <span id="third">Span element</span>
</div>
```

In this structure:
- `div` is the parent
- `p` and `span` are children of `div`
- The two `p` tags and `span` are siblings

**Parent relationships:**

**1. parentElement - Get parent element:**

```javascript
const child = document.querySelector('#first');
const parent = child.parentElement;
console.log(parent.id); // 'parent'
```

**2. parentNode - Get parent node:**

```javascript
const child = document.querySelector('#first');
const parent = child.parentNode;
// Usually same as parentElement
```

**Difference:** parentElement returns only elements, parentNode can return any node type (including document). For most cases, they're the same.

**3. closest() - Find nearest ancestor matching selector:**

```javascript
const element = document.querySelector('#first');

// Find nearest ancestor with class 'container'
const container = element.closest('.container');

// Very useful for event delegation
const card = element.closest('.card');
```

**Child relationships:**

**1. children - Get child elements (HTMLCollection):**

```javascript
const parent = document.querySelector('#parent');
const children = parent.children;

console.log(children.length); // 3 (p, p, span)
console.log(children[0]); // First p element
```

Returns only element nodes, not text nodes.

**2. childNodes - Get all child nodes (NodeList):**

```javascript
const parent = document.querySelector('#parent');
const nodes = parent.childNodes;

// Includes text nodes (whitespace), comments, elements
console.log(nodes.length); // More than 3 (includes whitespace)
```

**3. firstElementChild / lastElementChild:**

```javascript
const parent = document.querySelector('#parent');

const first = parent.firstElementChild; // First p
const last = parent.lastElementChild;   // Span
```

**4. firstChild / lastChild:**

```javascript
const parent = document.querySelector('#parent');

// Includes text nodes
const first = parent.firstChild; // Might be text node (whitespace)
const last = parent.lastChild;   // Might be text node
```

**Sibling relationships:**

**1. nextElementSibling - Next sibling element:**

```javascript
const first = document.querySelector('#first');
const next = first.nextElementSibling;
console.log(next.id); // 'second'
```

**2. previousElementSibling - Previous sibling element:**

```javascript
const second = document.querySelector('#second');
const previous = second.previousElementSibling;
console.log(previous.id); // 'first'
```

**3. nextSibling / previousSibling:**

```javascript
// Includes text nodes
const first = document.querySelector('#first');
const next = first.nextSibling; // Might be text node (whitespace)
```

**Element vs Node methods:**

| Element Methods (Elements only) | Node Methods (All nodes) |
|--------------------------------|-------------------------|
| parentElement | parentNode |
| children | childNodes |
| firstElementChild | firstChild |
| lastElementChild | lastChild |
| nextElementSibling | nextSibling |
| previousElementSibling | previousSibling |

**Recommendation:** Use Element methods (they're cleaner and skip text nodes).

**Traversal patterns:**

**1. Get all siblings:**

```javascript
function getAllSiblings(element) {
  const siblings = [];
  let sibling = element.parentElement.firstElementChild;
  
  while (sibling) {
    if (sibling !== element) {
      siblings.push(sibling);
    }
    sibling = sibling.nextElementSibling;
  }
  
  return siblings;
}
```

**2. Get all ancestors:**

```javascript
function getAllAncestors(element) {
  const ancestors = [];
  let current = element.parentElement;
  
  while (current) {
    ancestors.push(current);
    current = current.parentElement;
  }
  
  return ancestors;
}
```

**3. Get all descendants:**

```javascript
function getAllDescendants(element) {
  return Array.from(element.querySelectorAll('*'));
}
```

**Practical examples:**

**1. Find parent with specific class:**

```javascript
const button = document.querySelector('button');
const card = button.closest('.card');

if (card) {
  card.classList.add('selected');
}
```

**2. Toggle siblings:**

```javascript
const activeTab = document.querySelector('.tab.active');

// Get all sibling tabs
let sibling = activeTab.parentElement.firstElementChild;
while (sibling) {
  if (sibling !== activeTab) {
    sibling.classList.remove('active');
  }
  sibling = sibling.nextElementSibling;
}
```

**3. Loop through children:**

```javascript
const parent = document.querySelector('#parent');

for (const child of parent.children) {
  child.classList.add('styled');
}

// Or with forEach
Array.from(parent.children).forEach(child => {
  child.textContent = 'Updated';
});
```

**4. Navigate to specific relative:**

```javascript
const element = document.querySelector('#target');

// Parent's next sibling's first child
const relative = element.parentElement
                       .nextElementSibling
                       .firstElementChild;
```

**Common use cases:**

**Event delegation (closest):**

```javascript
document.querySelector('#list').addEventListener('click', (e) => {
  const item = e.target.closest('.list-item');
  if (item) {
    console.log('Clicked item:', item);
  }
});
```

**Navigation menus:**

```javascript
const menuItem = document.querySelector('.menu-item.active');

// Deactivate siblings
let sibling = menuItem.parentElement.firstElementChild;
while (sibling) {
  sibling.classList.remove('active');
  sibling = sibling.nextElementSibling;
}

// Activate clicked item
menuItem.classList.add('active');
```

**Form validation:**

```javascript
const input = document.querySelector('input');
const formGroup = input.closest('.form-group');
const errorMsg = formGroup.querySelector('.error-message');

if (!input.value) {
  errorMsg.textContent = 'Required field';
  formGroup.classList.add('error');
}
```

**Performance tip:**

Cache parent references instead of traversing repeatedly:

```javascript
// Bad - traverses every time
for (let i = 0; i < 100; i++) {
  element.parentElement.classList.add('class');
}

// Good - traverse once
const parent = element.parentElement;
for (let i = 0; i < 100; i++) {
  parent.classList.add('class');
}
```

**Interview tip:** Explain the difference between Element methods (firstElementChild, nextElementSibling) and Node methods (firstChild, nextSibling). Element methods only return elements and skip text nodes, making them easier to work with. Mention closest() as very useful for finding ancestors."

---

### Q6: What's the difference between attributes and properties?

**How to Answer:**

"Attributes and properties are related but different concepts in the DOM. This is a common source of confusion.

**Attributes:**

Attributes are defined in HTML. They're the things you write in your HTML tags.

```html
<input type="text" value="Hello" id="myInput" data-custom="123">
```

Here, `type`, `value`, `id`, and `data-custom` are attributes.

**Properties:**

Properties are defined on the DOM object in JavaScript. When the browser parses HTML, it creates DOM objects with properties.

```javascript
const input = document.querySelector('#myInput');

// These are properties
console.log(input.type);      // 'text'
console.log(input.value);     // 'Hello'
console.log(input.id);        // 'myInput'
```

**Key differences:**

**1. Attributes are in HTML, Properties are in JavaScript:**

```html
<!-- Attribute in HTML -->
<input value="Hello">
```

```javascript
// Property in JavaScript
const input = document.querySelector('input');
console.log(input.value); // Property
```

**2. Attributes are always strings, Properties have types:**

```html
<input type="checkbox" checked>
<input type="number" value="42">
```

```javascript
const checkbox = document.querySelector('[type="checkbox"]');
const numberInput = document.querySelector('[type="number"]');

// Attributes (always strings)
console.log(checkbox.getAttribute('checked')); // '' (empty string)
console.log(numberInput.getAttribute('value')); // '42' (string)

// Properties (typed)
console.log(checkbox.checked); // true (boolean)
console.log(numberInput.value); // '42' (string, but input type matters)
console.log(numberInput.valueAsNumber); // 42 (number)
```

**3. Properties are live, Attributes are initial state:**

This is the most important difference:

```html
<input type="text" value="Initial">
```

```javascript
const input = document.querySelector('input');

// User types "Modified" in the input
console.log(input.getAttribute('value')); // 'Initial' (HTML attribute)
console.log(input.value);                  // 'Modified' (current property)
```

The attribute holds the initial value from HTML.
The property holds the current value.

**4. Standard vs custom attributes:**

Standard HTML attributes have corresponding properties:

```javascript
const link = document.querySelector('a');

// Standard attributes → properties
link.href = 'https://example.com';  // Property
link.setAttribute('href', 'https://example.com'); // Attribute
```

Custom attributes DON'T automatically become properties:

```html
<div data-user-id="123" my-custom="value"></div>
```

```javascript
const div = document.querySelector('div');

// data-* attributes accessible via dataset
console.log(div.dataset.userId); // '123'

// Custom attributes need getAttribute
console.log(div.myCustom);                // undefined (no property)
console.log(div.getAttribute('my-custom')); // 'value' (attribute exists)
```

**Working with attributes:**

```javascript
const element = document.querySelector('#myElement');

// Get attribute
const id = element.getAttribute('id');
const dataValue = element.getAttribute('data-custom');

// Set attribute
element.setAttribute('data-custom', 'new value');
element.setAttribute('title', 'Tooltip text');

// Remove attribute
element.removeAttribute('data-custom');

// Check if attribute exists
if (element.hasAttribute('data-custom')) {
  console.log('Has attribute');
}
```

**Working with properties:**

```javascript
const input = document.querySelector('input');

// Get property
const value = input.value;
const isChecked = input.checked;

// Set property
input.value = 'New value';
input.disabled = true;
input.checked = false;
```

**dataset for data-* attributes:**

```html
<div 
  data-user-id="123"
  data-user-name="John"
  data-is-active="true"
></div>
```

```javascript
const div = document.querySelector('div');

// Access via dataset (camelCase)
console.log(div.dataset.userId);     // '123'
console.log(div.dataset.userName);   // 'John'
console.log(div.dataset.isActive);   // 'true' (string!)

// Set via dataset
div.dataset.userId = '456';
div.dataset.newProperty = 'value';
```

**Special cases:**

**1. class attribute vs className property:**

```html
<div class="container active"></div>
```

```javascript
const div = document.querySelector('div');

// Attribute
console.log(div.getAttribute('class')); // 'container active'

// Property
console.log(div.className); // 'container active'

// Modern way - classList
div.classList.add('new-class');
```

**2. Boolean attributes:**

```html
<input type="checkbox" checked>
<button disabled>Click</button>
```

```javascript
const checkbox = document.querySelector('input');
const button = document.querySelector('button');

// Attribute (presence = true)
checkbox.hasAttribute('checked'); // true
checkbox.getAttribute('checked'); // '' or 'checked'

// Property (boolean)
checkbox.checked; // true

// Set boolean attributes
checkbox.checked = false; // Property way (better)
checkbox.removeAttribute('checked'); // Attribute way
```

**3. href attribute vs property:**

```html
<a href="/page">Link</a>
```

```javascript
const link = document.querySelector('a');

// Attribute - relative
console.log(link.getAttribute('href')); // '/page'

// Property - absolute
console.log(link.href); // 'http://example.com/page' (full URL)
```

**When to use which:**

**Use properties when:**
- Working with standard HTML attributes
- Need current state (like input value)
- Want type conversion (boolean, number)
- Better performance

**Use attributes when:**
- Working with custom attributes
- Need initial HTML value
- Working with data-* attributes
- Manipulating HTML structure

**Best practices:**

```javascript
// Prefer properties for standard attributes
input.value = 'text';      // Good
input.disabled = true;     // Good

// Use attributes for custom data
element.setAttribute('data-id', '123');  // Good
element.dataset.id = '123';              // Better for data-*

// Don't mix unnecessarily
input.setAttribute('value', 'text');  // Works but awkward
```

**Common confusion - value attribute:**

```javascript
const input = document.querySelector('input');

// Initial state
console.log(input.getAttribute('value')); // HTML value
console.log(input.value);                  // Current value

// User types "Hello"
console.log(input.getAttribute('value')); // Still initial value
console.log(input.value);                  // 'Hello'

// Changing attribute doesn't update display
input.setAttribute('value', 'New');
console.log(input.value); // Still 'Hello' (user's input)

// Changing property updates display
input.value = 'New';
console.log(input.value); // 'New' (visible change)
```

**Interview tip:** The key point is that attributes are the initial HTML state (strings), while properties are the live JavaScript state (typed). Properties reflect current state, attributes reflect initial state. For standard HTML attributes, prefer properties. For custom data, use attributes or dataset."

---

## Events

### Q7: How do you handle events in JavaScript?

**How to Answer:**

"Event handling in JavaScript allows you to respond to user interactions like clicks, key presses, mouse movements, and more.

**Three ways to handle events:**

**1. HTML event attributes (bad practice - don't use):**

```html
<!-- Inline event handler - avoid this -->
<button onclick="alert('Clicked')">Click me</button>
```

Why avoid:
- Mixes HTML and JavaScript
- Hard to maintain
- No separation of concerns
- Only one handler per event

**2. DOM property (on + eventname):**

```javascript
const button = document.querySelector('button');

button.onclick = function() {
  console.log('Clicked!');
};

// Arrow function works too
button.onclick = () => {
  console.log('Clicked!');
};
```

Limitation: Only one handler per event type

```javascript
button.onclick = handler1;
button.onclick = handler2; // Overwrites handler1
```

**3. addEventListener() - Modern and recommended:**

```javascript
const button = document.querySelector('button');

button.addEventListener('click', function(event) {
  console.log('Button clicked!');
  console.log('Event object:', event);
});

// Can add multiple handlers
button.addEventListener('click', handler1);
button.addEventListener('click', handler2); // Both will run
```

**Advantages of addEventListener:**
- Multiple handlers for same event
- More control (capture vs bubble phase)
- Can remove handlers
- Better separation of concerns
- Works with custom events

**Event object:**

Every event handler receives an event object with useful information:

```javascript
element.addEventListener('click', function(event) {
  // Common properties
  console.log(event.type);       // 'click'
  console.log(event.target);     // Element that triggered event
  console.log(event.currentTarget); // Element handler is attached to
  console.log(event.timeStamp);  // When event occurred
  
  // Mouse events
  console.log(event.clientX, event.clientY); // Mouse position
  console.log(event.button);     // Which mouse button clicked
  
  // Keyboard events
  console.log(event.key);        // Which key pressed
  console.log(event.code);       // Physical key code
  console.log(event.ctrlKey);    // Was Ctrl pressed?
  console.log(event.shiftKey);   // Was Shift pressed?
});
```

**Common events:**

**Mouse events:**

```javascript
element.addEventListener('click', handler);       // Click
element.addEventListener('dblclick', handler);    // Double click
element.addEventListener('mousedown', handler);   // Mouse button pressed
element.addEventListener('mouseup', handler);     // Mouse button released
element.addEventListener('mousemove', handler);   // Mouse moved
element.addEventListener('mouseenter', handler);  // Mouse entered element
element.addEventListener('mouseleave', handler);  // Mouse left element
element.addEventListener('mouseover', handler);   // Mouse over (bubbles)
element.addEventListener('mouseout', handler);    // Mouse out (bubbles)
```

**Keyboard events:**

```javascript
element.addEventListener('keydown', handler);   // Key pressed
element.addEventListener('keyup', handler);     // Key released
element.addEventListener('keypress', handler);  // Deprecated

// Example
document.addEventListener('keydown', (e) => {
  console.log(`Key pressed: ${e.key}`);
  
  if (e.key === 'Enter') {
    console.log('Enter was pressed!');
  }
  
  if (e.ctrlKey && e.key === 's') {
    e.preventDefault(); // Prevent browser's Save dialog
    console.log('Ctrl+S pressed - save functionality');
  }
});
```

**Form events:**

```javascript
form.addEventListener('submit', handler);         // Form submitted
input.addEventListener('input', handler);         // Input value changed
input.addEventListener('change', handler);        // Input lost focus after change
input.addEventListener('focus', handler);         // Element focused
input.addEventListener('blur', handler);          // Element lost focus

// Example
form.addEventListener('submit', (e) => {
  e.preventDefault(); // Stop form from submitting normally
  
  const formData = new FormData(form);
  console.log('Form data:', Object.fromEntries(formData));
});
```

**Document/Window events:**

```javascript
window.addEventListener('load', handler);         // Page fully loaded
window.addEventListener('DOMContentLoaded', handler); // DOM ready
window.addEventListener('resize', handler);       // Window resized
window.addEventListener('scroll', handler);       // Page scrolled
window.addEventListener('beforeunload', handler); // Before page unload
```

**Removing event listeners:**

```javascript
// Named function required for removal
function handleClick() {
  console.log('Clicked');
}

// Add listener
button.addEventListener('click', handleClick);

// Remove listener (same function reference needed)
button.removeEventListener('click', handleClick);

// Anonymous functions CAN'T be removed
button.addEventListener('click', function() {
  console.log('This handler cannot be removed!');
});
```

**Event listener options:**

```javascript
element.addEventListener('click', handler, {
  once: true,       // Remove after first trigger
  capture: false,   // Use capture phase?
  passive: true     // Won't call preventDefault
});

// Examples
// Run only once
button.addEventListener('click', handler, { once: true });

// Passive scroll listener (better performance)
window.addEventListener('scroll', handler, { passive: true });
```

**'this' in event handlers:**

```javascript
const button = document.querySelector('button');

// Regular function - 'this' is element
button.addEventListener('click', function() {
  console.log(this); // button element
  this.textContent = 'Clicked';
});

// Arrow function - 'this' from outer scope
button.addEventListener('click', () => {
  console.log(this); // window or outer scope
});

// In object methods
const obj = {
  name: 'MyObject',
  handleClick: function() {
    button.addEventListener('click', () => {
      console.log(this.name); // 'MyObject' - arrow function inherits this
    });
  }
};
```

**Practical examples:**

**1. Click counter:**

```javascript
const button = document.querySelector('button');
let count = 0;

button.addEventListener('click', () => {
  count++;
  button.textContent = `Clicked ${count} times`;
});
```

**2. Form validation:**

```javascript
const form = document.querySelector('form');
const input = document.querySelector('input[type="email"]');

input.addEventListener('input', (e) => {
  const email = e.target.value;
  const isValid = email.includes('@');
  
  if (isValid) {
    input.classList.remove('error');
  } else {
    input.classList.add('error');
  }
});

form.addEventListener('submit', (e) => {
  e.preventDefault();
  console.log('Form submitted');
});
```

**3. Keyboard shortcuts:**

```javascript
document.addEventListener('keydown', (e) => {
  // Ctrl/Cmd + S to save
  if ((e.ctrlKey || e.metaKey) && e.key === 's') {
    e.preventDefault();
    saveDocument();
  }
  
  // Escape to close modal
  if (e.key === 'Escape') {
    closeModal();
  }
});
```

**4. Debounced search:**

```javascript
const searchInput = document.querySelector('#search');
let timeout;

searchInput.addEventListener('input', (e) => {
  clearTimeout(timeout);
  
  timeout = setTimeout(() => {
    search(e.target.value);
  }, 300); // Wait 300ms after typing stops
});
```

**Interview tip:** Explain that addEventListener is the modern recommended way because it allows multiple handlers and better control. Show you understand the event object and its properties. Mention common events like click, input, and submit. Know how to remove event listeners (requires named function)."

---

(Content continues with remaining topics: Event Bubbling, Event Delegation, OOP concepts, Prototypes, Inheritance, Design Patterns, etc...)


### Q8: What is event bubbling and capturing? Explain event propagation.

**How to Answer:**

"Event propagation is the process by which an event travels through the DOM tree. There are three phases: capturing phase, target phase, and bubbling phase.

**The three phases:**

1. **Capturing phase (trickling down)** - Event travels from root to target
2. **Target phase** - Event reaches the target element
3. **Bubbling phase (bubbling up)** - Event travels from target back to root

**Visual representation:**

```
Window → Document → HTML → Body → Parent → Target Element
  ↓         ↓         ↓       ↓       ↓          ↓
(Capturing phase - goes down)                     
                                                  | (Target phase)
  ↑         ↑         ↑       ↑       ↑          ↑
(Bubbling phase - goes up)
```

**Event Bubbling (default):**

When an event occurs on an element, it first runs handlers on that element, then on its parent, then all the way up to ancestors.

```html
<div id="outer">
  <div id="middle">
    <button id="inner">Click me</button>
  </div>
</div>
```

```javascript
document.querySelector('#outer').addEventListener('click', () => {
  console.log('Outer clicked');
});

document.querySelector('#middle').addEventListener('click', () => {
  console.log('Middle clicked');
});

document.querySelector('#inner').addEventListener('click', () => {
  console.log('Inner clicked');
});

// When you click the button:
// Output:
// Inner clicked
// Middle clicked  
// Outer clicked
// (bubbles from inner to outer)
```

**Event Capturing:**

Event travels from root down to target element. Use third parameter `true` or `{ capture: true }`.

```javascript
document.querySelector('#outer').addEventListener('click', () => {
  console.log('Outer clicked');
}, true); // Capturing

document.querySelector('#middle').addEventListener('click', () => {
  console.log('Middle clicked');
}, true);

document.querySelector('#inner').addEventListener('click', () => {
  console.log('Inner clicked');
}, true);

// When you click the button:
// Output:
// Outer clicked   (capturing phase)
// Middle clicked  (capturing phase)
// Inner clicked   (target phase)
```

**event.target vs event.currentTarget:**

```javascript
document.querySelector('#outer').addEventListener('click', (e) => {
  console.log('Target:', e.target.id);           // Element that triggered
  console.log('CurrentTarget:', e.currentTarget.id); // Element with handler
});

// Click inner button:
// Target: inner (the button that was clicked)
// CurrentTarget: outer (the element with the handler)
```

**Stopping propagation:**

```javascript
document.querySelector('#inner').addEventListener('click', (e) => {
  e.stopPropagation(); // Stops bubbling
  console.log('Inner clicked');
});

// Now only 'Inner clicked' will log
// Event doesn't bubble to middle or outer
```

**stopImmediatePropagation:**

Stops all handlers on current element and stops propagation:

```javascript
button.addEventListener('click', (e) => {
  e.stopImmediatePropagation();
  console.log('Handler 1');
});

button.addEventListener('click', () => {
  console.log('Handler 2'); // Won't run
});
```

**Events that don't bubble:**

Some events don't bubble:
- focus / blur (use focusin / focusout instead)
- load / unload
- mouseenter / mouseleave (use mouseover / mouseout instead)

**Interview tip:** Explain that events bubble up from target to ancestors by default. This is useful for event delegation. Use stopPropagation() to prevent bubbling. Know the difference between target (what was clicked) and currentTarget (what has the handler).

---

### Q9: What is event delegation?

**How to Answer:**

"Event delegation is a pattern where instead of adding event listeners to multiple child elements, you add a single listener to a parent element and use event bubbling to handle events on children.

**Why event delegation?**

**Without delegation:**

```javascript
// Bad - creates many listeners
const buttons = document.querySelectorAll('.button');

buttons.forEach(button => {
  button.addEventListener('click', (e) => {
    console.log('Button clicked');
  });
});

// Problem: If you add new buttons dynamically, they won't have listeners
```

**With delegation:**

```javascript
// Good - single listener on parent
const container = document.querySelector('#container');

container.addEventListener('click', (e) => {
  if (e.target.matches('.button')) {
    console.log('Button clicked:', e.target);
  }
});

// Works for existing AND future buttons!
```

**Benefits:**

1. **Performance** - Fewer event listeners (less memory)
2. **Dynamic elements** - Works with elements added later
3. **Simpler code** - One listener instead of many
4. **Better for large lists** - Efficient for many items

**Practical example - Todo list:**

```javascript
const todoList = document.querySelector('#todo-list');

todoList.addEventListener('click', (e) => {
  // Delete button clicked
  if (e.target.classList.contains('delete-btn')) {
    e.target.closest('li').remove();
  }
  
  // Checkbox clicked
  if (e.target.type === 'checkbox') {
    e.target.closest('li').classList.toggle('completed');
  }
});

// Add new todos - they automatically work!
const newTodo = document.createElement('li');
newTodo.innerHTML = `
  <input type="checkbox">
  <span>New todo</span>
  <button class="delete-btn">Delete</button>
`;
todoList.appendChild(newTodo);
// Events work without adding listeners!
```

**Using closest() for delegation:**

```javascript
document.querySelector('#table').addEventListener('click', (e) => {
  // Find closest row (even if span or icon was clicked)
  const row = e.target.closest('tr');
  
  if (row) {
    console.log('Row clicked:', row);
  }
});
```

**When NOT to use delegation:**

- Events that don't bubble (focus, blur, scroll on specific elements)
- Need very different handlers for each element
- Performance-critical individual handlers

**Interview tip:** Explain that event delegation uses a single listener on a parent instead of many listeners on children. It's more efficient and works with dynamically added elements. Show practical example like a list where items can be added/removed."

---

### Q10: What's the difference between preventDefault() and stopPropagation()?

**How to Answer:**

"preventDefault() and stopPropagation() are both methods on the event object, but they do completely different things.

**preventDefault():**

Prevents the browser's default action for that event.

```javascript
// Prevent form submission
form.addEventListener('submit', (e) => {
  e.preventDefault(); // Form won't submit
  // Handle with AJAX instead
});

// Prevent link navigation
link.addEventListener('click', (e) => {
  e.preventDefault(); // Won't navigate
  // Open in modal instead
});

// Prevent checkbox toggle
checkbox.addEventListener('click', (e) => {
  e.preventDefault(); // Won't check/uncheck
  // Custom toggle logic
});

// Prevent right-click menu
document.addEventListener('contextmenu', (e) => {
  e.preventDefault(); // Context menu won't open
});
```

**Common default behaviors:**

- Click on link → Navigate to href
- Submit form → Send data and reload
- Click checkbox → Toggle checked state
- Press key in input → Insert character
- Right-click → Show context menu
- Drag image → Browser drag preview

**stopPropagation():**

Stops the event from bubbling up to parent elements.

```javascript
<div id="parent">
  <button id="child">Click me</button>
</div>

document.querySelector('#parent').addEventListener('click', () => {
  console.log('Parent clicked');
});

document.querySelector('#child').addEventListener('click', (e) => {
  e.stopPropagation(); // Event won't bubble to parent
  console.log('Child clicked');
});

// Click button → Only logs "Child clicked"
// Parent handler doesn't run
```

**Key differences:**

| preventDefault() | stopPropagation() |
|-----------------|-------------------|
| Stops browser's default action | Stops event bubbling |
| Affects browser behavior | Affects event propagation |
| Link won't navigate | Parent handlers won't run |
| Form won't submit | Event stays at current level |

**Can use both:**

```javascript
button.addEventListener('click', (e) => {
  e.preventDefault();     // Stop default behavior
  e.stopPropagation();    // Stop event bubbling
  // Custom handling
});
```

**return false (not recommended):**

In jQuery and inline handlers, `return false` does both, but avoid this pattern:

```javascript
// jQuery (not recommended in vanilla JS)
$('a').click(function(e) {
  return false; // Prevents default AND stops propagation
});

// Vanilla JS - be explicit instead
element.addEventListener('click', (e) => {
  e.preventDefault();    // Clear intent
  e.stopPropagation();   // Clear intent
});
```

**Interview tip:** Explain that preventDefault() stops the browser's default action (like form submit or link navigation), while stopPropagation() stops the event from bubbling to parent elements. They serve different purposes and can be used together."

---

## Browser APIs

### Q11: What's the difference between window and document?

**How to Answer:**

"window and document are both global objects in the browser, but they represent different things.

**window:**

The global object representing the browser window. It's the top-level object containing everything.

```javascript
// Global object
console.log(window); // The window object itself

// Global variables are properties of window
var myVar = 'hello';
console.log(window.myVar); // 'hello'

// Window properties
console.log(window.innerWidth);  // Viewport width
console.log(window.innerHeight); // Viewport height
console.log(window.location);    // Current URL
console.log(window.history);     // Browser history
console.log(window.localStorage); // Local storage
```

**document:**

Represents the HTML document loaded in the window. It's a property of window.

```javascript
// document is property of window
console.log(window.document === document); // true

// Document represents the DOM
console.log(document.body);        // Body element
console.log(document.title);       // Page title
console.log(document.querySelector); // DOM methods
```

**Key differences:**

| window | document |
|--------|----------|
| Browser window | HTML document |
| Global scope | DOM tree |
| window.alert() | document.querySelector() |
| window.location | document.body |
| window.innerWidth | document.title |

**window methods and properties:**

```javascript
// Dialogs
window.alert('Message');
window.confirm('Are you sure?');
window.prompt('Enter name:');

// Timing
window.setTimeout(() => {}, 1000);
window.setInterval(() => {}, 1000);

// Navigation
window.open('url');
window.close();
window.location.href = 'url';

// Dimensions
window.innerWidth;
window.innerHeight;
window.outerWidth;
window.outerHeight;

// Scroll
window.scrollTo(0, 0);
window.scrollBy(0, 100);
```

**document methods and properties:**

```javascript
// DOM selection
document.getElementById('id');
document.querySelector('.class');

// DOM manipulation
document.createElement('div');
document.createTextNode('text');

// Document info
document.title;
document.URL;
document.domain;
document.cookie;

// Events
document.addEventListener('click', handler);
```

**Hierarchy:**

```
window (browser window)
  ├── document (HTML document)
  │     ├── html
  │     └── body
  ├── location (URL)
  ├── history (navigation history)
  ├── localStorage (storage)
  └── ... (other browser APIs)
```

**Interview tip:** window is the global browser object containing everything including document. document represents the HTML DOM tree and is a property of window. window has browser-related APIs, document has DOM manipulation methods."

---

### Q12: What's the difference between localStorage, sessionStorage, and cookies?

**How to Answer:**

"All three store data in the browser, but they differ in capacity, expiration, and scope.

**localStorage:**

Stores data with no expiration. Data persists even after browser is closed.

```javascript
// Set item
localStorage.setItem('username', 'John');
localStorage.setItem('user', JSON.stringify({ name: 'John', age: 30 }));

// Get item
const username = localStorage.getItem('username'); // 'John'
const user = JSON.parse(localStorage.getItem('user'));

// Remove item
localStorage.removeItem('username');

// Clear all
localStorage.clear();

// Check length
console.log(localStorage.length);

// Iterate
for (let i = 0; i < localStorage.length; i++) {
  const key = localStorage.key(i);
  console.log(key, localStorage.getItem(key));
}
```

**sessionStorage:**

Same API as localStorage, but data clears when tab/browser closes.

```javascript
// Same methods as localStorage
sessionStorage.setItem('temp', 'data');
sessionStorage.getItem('temp');
sessionStorage.removeItem('temp');
sessionStorage.clear();
```

**Cookies:**

Older storage method, sent to server with every request.

```javascript
// Set cookie
document.cookie = 'username=John; max-age=3600; path=/';

// Get all cookies (as string)
console.log(document.cookie); // 'username=John; theme=dark'

// Delete cookie (set expired)
document.cookie = 'username=; max-age=0';
```

**Comparison table:**

| Feature | localStorage | sessionStorage | Cookies |
|---------|-------------|----------------|---------|
| Capacity | ~10MB | ~10MB | ~4KB |
| Expiration | Never | Tab close | Set manually |
| Scope | All tabs/windows | Single tab | Domain |
| Sent to server | No | No | Yes (auto) |
| API | Simple | Simple | String-based |
| Use case | Long-term | Temporary | Auth tokens |

**When to use:**

**localStorage:**
- User preferences (theme, language)
- Cart data (persists across sessions)
- Cached data
- Draft content

**sessionStorage:**
- Form data during session
- Temporary state
- Multi-step processes
- Tab-specific data

**Cookies:**
- Authentication tokens
- Session IDs
- Server needs the data
- Cross-domain situations

**Security considerations:**

```javascript
// localStorage/sessionStorage - visible in DevTools
// Don't store sensitive data!
localStorage.setItem('password', '123'); // Bad!

// For sensitive data, use httpOnly cookies (server-side only)
// Can't be accessed by JavaScript
```

**Interview tip:** localStorage persists forever, sessionStorage clears on tab close, cookies expire based on settings and are sent to server. localStorage/sessionStorage hold ~10MB, cookies only ~4KB. Use localStorage for user preferences, sessionStorage for temporary data, cookies for auth."

---

## OOP Fundamentals

### Q14: What is Object-Oriented Programming?

**How to Answer:**

"Object-Oriented Programming (OOP) is a programming paradigm based on the concept of objects, which contain data (properties) and code (methods).

**Core concept:**

Instead of having separate functions and data, OOP bundles them together into objects. An object represents a real-world entity with characteristics (properties) and behaviors (methods).

**Example without OOP:**

```javascript
// Procedural approach
const userName = 'John';
const userAge = 30;

function greetUser() {
  console.log(`Hello ${userName}`);
}

function getUserInfo() {
  return `${userName} is ${userAge}`;
}
```

**Example with OOP:**

```javascript
// Object-oriented approach
const user = {
  name: 'John',
  age: 30,
  
  greet() {
    console.log(`Hello ${this.name}`);
  },
  
  getInfo() {
    return `${this.name} is ${this.age}`;
  }
};

user.greet(); // 'Hello John'
```

**Four pillars of OOP:**

1. **Encapsulation** - Bundle data and methods together
2. **Abstraction** - Hide complex details, show only necessary
3. **Inheritance** - Reuse code from parent classes
4. **Polymorphism** - Same interface, different implementations

These are covered in detail in later questions.

**Benefits of OOP:**

1. **Organization** - Code is structured and logical
2. **Reusability** - Inheritance allows code reuse
3. **Maintainability** - Easier to update and debug
4. **Scalability** - Better for large applications
5. **Modularity** - Independent objects
6. **Real-world modeling** - Objects represent real entities

**OOP in JavaScript:**

JavaScript uses prototypal inheritance, not classical inheritance like Java/C++, but achieves OOP principles.

**Interview tip:** OOP organizes code around objects that contain both data and behavior. The four pillars are encapsulation, abstraction, inheritance, and polymorphism. Benefits include better organization, reusability, and maintainability."

---

### Q15: What are classes in JavaScript?

**How to Answer:**

"Classes in JavaScript (ES6+) are templates for creating objects. They provide a cleaner syntax for creating objects and dealing with inheritance.

**Basic class:**

```javascript
class Person {
  // Constructor - runs when object is created
  constructor(name, age) {
    this.name = name; // Instance property
    this.age = age;
  }
  
  // Method
  greet() {
    console.log(`Hello, I'm ${this.name}`);
  }
  
  // Method
  getInfo() {
    return `${this.name} is ${this.age} years old`;
  }
}

// Create instance
const john = new Person('John', 30);
john.greet(); // 'Hello, I'm John'
```

**Constructor:**

Special method that runs when creating an instance:

```javascript
class Car {
  constructor(brand, model) {
    console.log('Creating car...');
    this.brand = brand;
    this.model = model;
    this.speed = 0; // Default value
  }
}

const myCar = new Car('Toyota', 'Camry');
// Logs: 'Creating car...'
```

**Class vs Object Literal:**

```javascript
// Object literal - single object
const john = {
  name: 'John',
  greet() { console.log('Hello'); }
};

// Class - template for multiple objects
class Person {
  constructor(name) {
    this.name = name;
  }
  greet() { console.log('Hello'); }
}

const john = new Person('John');
const jane = new Person('Jane'); // Reusable!
```

**Interview tip:** Classes are templates for creating objects introduced in ES6. They have a constructor method that initializes properties and can have methods. Classes are syntactic sugar over JavaScript's prototypal inheritance."

---

### Q19: What is Prototype in JavaScript?

**How to Answer:**

"Prototype is the mechanism by which JavaScript objects inherit properties and methods from other objects. Every object in JavaScript has an internal link to another object called its prototype.

**How prototype works:**

```javascript
function Person(name) {
  this.name = name;
}

// Add method to prototype
Person.prototype.greet = function() {
  console.log(`Hello, I'm ${this.name}`);
};

const john = new Person('John');
john.greet(); // 'Hello, I'm John'
// john doesn't have greet(), but its prototype does
```

**Prototype chain:**

When you access a property on an object:
1. JavaScript first looks on the object itself
2. If not found, looks at the object's prototype
3. If not found, looks at the prototype's prototype
4. Continues until reaches null (end of chain)

```javascript
const obj = { a: 1 };

// obj → obj.__proto__ (Object.prototype) → null

console.log(obj.toString); // Found on Object.prototype
// Even though obj doesn't have toString, it inherits it
```

**Why use prototype:**

**Without prototype (inefficient):**

```javascript
function Person(name) {
  this.name = name;
  this.greet = function() { // New function for EACH instance
    console.log(`Hello ${this.name}`);
  };
}

const john = new Person('John');
const jane = new Person('Jane');

console.log(john.greet === jane.greet); // false (different functions)
// Memory waste - 1000 instances = 1000 copies of greet!
```

**With prototype (efficient):**

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() { // Shared by ALL instances
  console.log(`Hello ${this.name}`);
};

const john = new Person('John');
const jane = new Person('Jane');

console.log(john.greet === jane.greet); // true (same function)
// One function in memory, shared by all instances
```

**Checking prototype:**

```javascript
const john = new Person('John');

// Get prototype
console.log(Object.getPrototypeOf(john));
console.log(john.__proto__); // Non-standard but widely supported

// Check if property is own or inherited
console.log(john.hasOwnProperty('name')); // true (own)
console.log(john.hasOwnProperty('greet')); // false (inherited)
```

**Interview tip:** Prototype is JavaScript's inheritance mechanism. Properties/methods on prototype are shared by all instances (memory efficient). When accessing a property, JavaScript searches the prototype chain until it finds it or reaches null."

---

### Q20: What is the prototype chain?

**How to Answer:**

"The prototype chain is how JavaScript implements inheritance. It's a series of links between objects through their prototypes.

**Visual representation:**

```
instance → Constructor.prototype → Object.prototype → null
```

**Example:**

```javascript
function Animal(name) {
  this.name = name;
}

Animal.prototype.eat = function() {
  console.log(`${this.name} is eating`);
};

function Dog(name, breed) {
  Animal.call(this, name);
  this.breed = breed;
}

Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

Dog.prototype.bark = function() {
  console.log('Woof!');
};

const myDog = new Dog('Max', 'Labrador');

// Prototype chain:
// myDog → Dog.prototype → Animal.prototype → Object.prototype → null

myDog.bark();  // Found on Dog.prototype
myDog.eat();   // Found on Animal.prototype
myDog.toString(); // Found on Object.prototype
```

**How lookup works:**

```javascript
myDog.bark();

// 1. Check myDog itself? No
// 2. Check Dog.prototype? YES - found!
// Execute it

myDog.eat();

// 1. Check myDog itself? No
// 2. Check Dog.prototype? No
// 3. Check Animal.prototype? YES - found!
// Execute it
```

**End of chain:**

```javascript
console.log(Object.getPrototypeOf(Object.prototype)); // null
// null is the end of the prototype chain
```

**Interview tip:** The prototype chain is a linked list of prototypes. When accessing a property, JavaScript walks up the chain until it finds it or reaches null. This is how inheritance works in JavaScript."

---

## OOP Principles

### Q29: What is Encapsulation?

**How to Answer:**

"Encapsulation is bundling data (properties) and methods that operate on that data within a single unit (object), and restricting direct access to some components.

**Benefits:**

1. **Data hiding** - Internal state is protected
2. **Controlled access** - Only expose what's necessary
3. **Easier maintenance** - Implementation can change without affecting external code
4. **Prevent accidents** - Can't accidentally modify internal state

**Example with private fields (ES2022):**

```javascript
class BankAccount {
  #balance = 0; // Private field (# makes it private)
  
  constructor(initialBalance) {
    this.#balance = initialBalance;
  }
  
  // Public method to access private data
  getBalance() {
    return this.#balance;
  }
  
  deposit(amount) {
    if (amount > 0) {
      this.#balance += amount;
    }
  }
  
  withdraw(amount) {
    if (amount > 0 && amount <= this.#balance) {
      this.#balance -= amount;
    }
  }
}

const account = new Bank Account(1000);
console.log(account.getBalance()); // 1000
account.deposit(500);
// account.#balance = 0; // Error! Can't access private field
```

**Interview tip:** Encapsulation means bundling data and methods together and hiding internal details. Use private fields (#) to restrict direct access. Expose only necessary methods (public interface) to interact with the object."

---

### Q31: What is Inheritance?

**How to Answer:**

"Inheritance allows a class to inherit properties and methods from another class, promoting code reuse.

**ES6 class inheritance:**

```javascript
// Parent class
class Animal {
  constructor(name) {
    this.name = name;
  }
  
  eat() {
    console.log(`${this.name} is eating`);
  }
}

// Child class inherits from Animal
class Dog extends Animal {
  constructor(name, breed) {
    super(name); // Call parent constructor
    this.breed = breed;
  }
  
  bark() {
    console.log('Woof!');
  }
}

const myDog = new Dog('Max', 'Labrador');
myDog.eat();  // Inherited from Animal
myDog.bark(); // Own method
```

**Key points:**

- `extends` creates inheritance
- `super()` calls parent constructor
- Child has access to parent methods
- Child can add own methods
- Child can override parent methods

**Interview tip:** Inheritance lets one class inherit from another using extends keyword. Use super() to call parent constructor. Child class gets all parent methods plus can add its own. This promotes code reuse."

---

### Q32: What is Polymorphism?

**How to Answer:**

"Polymorphism means 'many forms' - the ability of different objects to respond to the same method call in different ways.

**Example:**

```javascript
class Animal {
  makeSound() {
    console.log('Some generic sound');
  }
}

class Dog extends Animal {
  makeSound() {
    console.log('Woof!');
  }
}

class Cat extends Animal {
  makeSound() {
    console.log('Meow!');
  }
}

const animals = [new Dog(), new Cat(), new Animal()];

// Same method call, different behavior
animals.forEach(animal => {
  animal.makeSound();
});
// Woof!
// Meow!
// Some generic sound
```

**Benefits:**

- Same interface, different implementations
- Easier to add new types
- More flexible code
- Treat objects generically

**Interview tip:** Polymorphism allows different classes to respond differently to the same method. Method overriding is a form of polymorphism - child class provides its own implementation of parent method."

---

## Design Patterns

### Q33: What is the Module Pattern?

**How to Answer:**

"The Module Pattern is a design pattern that provides encapsulation and creates private/public members using closures.

**Basic module:**

```javascript
const myModule = (function() {
  // Private
  let privateVar = 'I am private';
  
  function privateMethod() {
    console.log(privateVar);
  }
  
  // Public interface
  return {
    publicMethod: function() {
      privateMethod();
    },
    
    getPrivateVar: function() {
      return privateVar;
    }
  };
})();

myModule.publicMethod(); // Works
myModule.privateMethod(); // Error! Not accessible
```

**Benefits:**

- Encapsulation - private members
- Namespace - avoid global pollution
- Organization - related code together

**Interview tip:** Module Pattern uses IIFEs and closures to create private data and public API. The returned object is the public interface, everything else is private."

---

### Q35: What is Singleton Pattern?

**How to Answer:**

"Singleton Pattern ensures a class has only one instance and provides global access to it.

**Implementation:**

```javascript
class Singleton {
  constructor() {
    if (Singleton.instance) {
      return Singleton.instance;
    }
    Singleton.instance = this;
    this.data = [];
  }
  
  addData(item) {
    this.data.push(item);
  }
  
  getData() {
    return this.data;
  }
}

const instance1 = new Singleton();
const instance2 = new Singleton();

console.log(instance1 === instance2); // true (same instance!)

instance1.addData('test');
console.log(instance2.getData()); // ['test']
```

**Use cases:**

- Database connections
- Configuration objects
- Logger instances
- Cache managers

**Interview tip:** Singleton ensures only one instance exists. Useful for shared resources like database connections or configuration. First call creates instance, subsequent calls return existing instance."

---

### Q36: What is Factory Pattern?

**How to Answer:**

"Factory Pattern provides a way to create objects without specifying the exact class. A factory function decides which class to instantiate based on conditions.

**Example:**

```javascript
class Car {
  constructor(type) {
    this.type = type;
    this.wheels = 4;
  }
}

class Bike {
  constructor(type) {
    this.type = type;
    this.wheels = 2;
  }
}

class Truck {
  constructor(type) {
    this.type = type;
    this.wheels = 6;
  }
}

// Factory function
function VehicleFactory(type, model) {
  switch(type) {
    case 'car':
      return new Car(model);
    case 'bike':
      return new Bike(model);
    case 'truck':
      return new Truck(model);
    default:
      return null;
  }
}

const myCar = VehicleFactory('car', 'sedan');
const myBike = VehicleFactory('bike', 'mountain');
```

**Benefits:**

- Centralized object creation
- Easy to add new types
- Hides creation complexity
- Decouples code from specific classes

**Interview tip:** Factory Pattern uses a function to create objects based on parameters. Useful when creation logic is complex or when the exact type isn't known until runtime."

---

## Final Tips

**Most Important Topics for Interviews:**

1. **DOM Manipulation** - querySelector, createElement, classList
2. **Event Handling** - addEventListener, event object, delegation
3. **Event Bubbling** - Understand propagation phases
4. **Prototypes** - How inheritance works in JS
5. **Classes** - Modern OOP syntax
6. **Encapsulation** - Private fields, data hiding
7. **Inheritance** - extends, super keyword

**Common Interview Questions:**

- "Implement event delegation for a list"
- "Explain the prototype chain"
- "What's the difference between __proto__ and prototype?"
- "Create a class with private properties"
- "Explain how this works in different contexts"

**Practice Tips:**

1. Build small DOM projects (todo list, calculator)
2. Implement OOP concepts from scratch
3. Explain concepts out loud
4. Draw diagrams for prototype chain
5. Write code without looking at references

**Red Flags to Avoid:**

❌ Confusing attributes and properties
❌ Not knowing event bubbling
❌ Mixing up __proto__ and prototype
❌ Can't explain prototype chain
❌ Don't know when to use event delegation

**Green Flags to Show:**

✅ Understand event flow
✅ Know prototype-based inheritance
✅ Can implement OOP principles
✅ Understand closures with modules
✅ Know performance implications
✅ Can write clean, organized code

Good luck with your interviews! 