# React Interview Preparation Guide
*How to Answer React Questions Confidently*

**Note for Students:** This guide is written exactly how you should answer in interviews. Practice reading these answers out loud to make them natural when speaking.

---

## Table of Contents

### Function-Based Components
1. [What are Function Components in React?](#q1-what-are-function-components-in-react)
2. [Why do we prefer Function Components over Class Components?](#q2-why-do-we-prefer-function-components-over-class-components)

### Props
3. [What are Props? How do they work?](#q3-what-are-props-how-do-they-work)
4. [What is Props Drilling and what problems does it cause?](#q4-what-is-props-drilling-and-what-problems-does-it-cause)

### State Management with useState
5. [What is useState and how do you use it?](#q5-what-is-usestate-and-how-do-you-use-it)
6. [Why should you use functional updates with setState?](#q6-why-should-you-use-functional-updates-with-setstate)
7. [Can you explain the difference between setState in Class Components and useState?](#q7-can-you-explain-the-difference-between-setstate-in-class-components-and-usestate)
8. [What does "Lifting State Up" mean?](#q8-what-does-lifting-state-up-mean)
9. [When should you lift state up vs using Context or Redux?](#q9-when-should-you-lift-state-up-vs-using-context-or-redux)
10. [What is lazy initialization in useState?](#q10-what-is-lazy-initialization-in-usestate)

### Side Effects and useEffect
11. [How do you handle async data fetching in React?](#q11-how-do-you-handle-async-data-fetching-in-react)
12. [What are the common patterns for managing loading and error states?](#q12-what-are-the-common-patterns-for-managing-loading-and-error-states)
13. [What is useEffect and when do you use it?](#q13-what-is-useeffect-and-when-do-you-use-it)
14. [Explain the dependency array in useEffect.](#q14-explain-the-dependency-array-in-useeffect)
15. [What is the cleanup function in useEffect?](#q15-what-is-the-cleanup-function-in-useeffect)
16. [What are the common mistakes with useEffect?](#q16-what-are-the-common-mistakes-with-useeffect)

### Context API
17. [What is Context API and when should you use it?](#q17-what-is-context-api-and-when-should-you-use-it)
18. [How does useContext work?](#q18-how-does-usecontext-work)
19. [What are the performance concerns with Context?](#q19-what-are-the-performance-concerns-with-context)

### useRef
20. [What is useRef and what are its use cases?](#q20-what-is-useref-and-what-are-its-use-cases)
21. [What's the difference between useRef and useState?](#q21-whats-the-difference-between-useref-and-usestate)
22. [Can you explain the previous value pattern with useRef?](#q22-can-you-explain-the-previous-value-pattern-with-useref)

### useReducer
23. [What is useReducer and when should you use it instead of useState?](#q23-what-is-usereducer-and-when-should-you-use-it-instead-of-usestate)
24. [How does useReducer relate to Redux?](#q24-how-does-usereducer-relate-to-redux)

### Redux
25. [What is Redux and what problem does it solve?](#q25-what-is-redux-and-what-problem-does-it-solve)
26. [What is Redux Toolkit and why do we use it?](#q26-what-is-redux-toolkit-and-why-do-we-use-it)
27. [Explain Redux data flow with an example.](#q27-explain-redux-data-flow-with-an-example)
28. [What are selectors in Redux? Why use them?](#q28-what-are-selectors-in-redux-why-use-them)
29. [What is Redux middleware? Explain Redux Thunk.](#q29-what-is-redux-middleware-explain-redux-thunk)
30. [How do you structure a Redux application?](#q30-how-do-you-structure-a-redux-application)

### Lifecycle and Performance
31. [What are the basic lifecycle methods in Class Components?](#q31-what-are-the-basic-lifecycle-methods-in-class-components)
32. [What are React.memo, useMemo, and useCallback? When do you use them?](#q32-what-are-reactmemo-usememo-and-usecallback-when-do-you-use-them)
33. [What are keys in React and why are they important?](#q33-what-are-keys-in-react-and-why-are-they-important)
34. [What are some common performance pitfalls in React?](#q34-what-are-some-common-performance-pitfalls-in-react)

### Best Practices
35. [What are some React best practices you follow?](#q35-what-are-some-react-best-practices-you-follow)
36. [How would you optimize a slow React application?](#q36-how-would-you-optimize-a-slow-react-application)

### Advanced Concepts
37. [Explain the concept of controlled vs uncontrolled components.](#q37-explain-the-concept-of-controlled-vs-uncontrolled-components)
38. [What happens when you call setState? Walk me through the process.](#q38-what-happens-when-you-call-setstate-walk-me-through-the-process)
39. [What are common mistakes beginners make with React hooks?](#q39-what-are-common-mistakes-beginners-make-with-react-hooks)
40. [How do you decide between Context, Redux, and prop drilling?](#q40-how-do-you-decide-between-context-redux-and-prop-drilling)

---

## Function-Based Components

### Q1: What are Function Components in React?

**How to Answer:**

"Function components are basically JavaScript functions that return JSX. So instead of writing a class, you just write a regular function that returns what you want to render on the screen.

For example, if I want to create a simple Welcome component, I can just write:

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

The main thing is that it's just a function - you pass in props as a parameter and return JSX. That's it. It's much simpler than class components because you don't have to deal with 'this' keyword or constructor or any of that stuff.

Since React 16.8, we've had hooks, so now function components can do everything class components can do - manage state, handle side effects, everything - but with much cleaner code."

**Key Points to Mention:**
- Just JavaScript functions that return JSX
- Simpler syntax, no 'this' keyword
- With hooks, they can do everything class components can do
- Recommended approach in modern React

---

### Q2: Why do we prefer Function Components over Class Components?

**How to Answer:**

"There are several reasons why function components are preferred nowadays.

First, the code is just much cleaner and easier to read. You don't have to write 'this.state' or 'this.props' everywhere. You also don't have to bind methods in the constructor, which was always a pain point with class components.

Second, with hooks like useState and useEffect, we can manage state and side effects in a really straightforward way. The logic is easier to follow because everything is in one place.

Third, it's easier to reuse logic with custom hooks. If I have some logic I want to share between components, I can just extract it into a custom hook and use it anywhere.

And finally, there's a small performance benefit and the code is generally easier to test because functions are more predictable than classes.

React team also recommends function components as the default approach now, so all the new features and optimizations are built with function components in mind."

---

## Props

### Q3: What are Props? How do they work?

**How to Answer:**

"Props stands for properties, and they're basically how we pass data from a parent component to a child component. Think of them like function arguments - you pass data in, and the child component receives it.

The important thing to remember is that props are read-only. A child component can't modify the props it receives. It can only read them and use them to render something.

Let me give you an example:

```javascript
// Parent component
function App() {
  return <UserCard name="John" age={25} />;
}

// Child component
function UserCard(props) {
  return (
    <div>
      <h2>{props.name}</h2>
      <p>Age: {props.age}</p>
    </div>
  );
}
```

Here, the App component is passing 'name' and 'age' as props to UserCard. The UserCard receives these props and displays them. We usually destructure props like this to make it cleaner:

```javascript
function UserCard({ name, age }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>Age: {age}</p>
    </div>
  );
}
```

This makes the code more readable because you can see exactly what props the component expects."

**Additional Point:** "One more thing - you can pass any JavaScript value as props: strings, numbers, booleans, objects, arrays, even functions. This is how we do things like passing callback functions from parent to child."

---

### Q4: What is Props Drilling and what problems does it cause?

**How to Answer:**

"Props drilling is when you have to pass props through multiple levels of components, even when the intermediate components don't actually need those props. They're just passing them down to their children.

Let me explain with an example. Say you have this component structure:

```
App (has user data)
  └─ Dashboard (doesn't need user data)
      └─ Sidebar (doesn't need user data)
          └─ UserProfile (needs user data)
```

To get user data from App to UserProfile, you have to pass it through Dashboard and Sidebar, even though those components don't use it at all. That's props drilling.

The problems with this are:
- It makes the code harder to maintain because if you need to change something, you have to update multiple components
- The intermediate components become less reusable because they're tightly coupled to props they don't even use
- It's just messy and makes the code harder to understand

The solution to props drilling is usually Context API or state management libraries like Redux. With Context, you can make data available to any component in the tree without passing it through every level."

---

## useState Hook

### Q5: What is useState and how do you use it?

**How to Answer:**

"useState is a hook that lets you add state to function components. Before hooks, you could only have state in class components, but now function components can manage state too.

The way it works is pretty simple. You call useState with an initial value, and it returns an array with two things: the current state value and a function to update it.

```javascript
const [count, setCount] = useState(0);
```

Here, 'count' is the state variable with initial value 0, and 'setCount' is the function I use to update it.

When you want to update the state, you just call the setter function:

```javascript
function Counter() {
  const [count, setCount] = useState(0);
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  );
}
```

Every time you call setCount, React re-renders the component with the new state value. That's how your UI stays in sync with your data.

You can have multiple useState calls in one component for different pieces of state, and you can store any type of value - numbers, strings, booleans, objects, arrays, whatever you need."

**Important Point:** "One thing to remember is that state updates are asynchronous. If you need to update state based on the previous state, you should use the functional form: `setCount(prevCount => prevCount + 1)`. This ensures you're working with the most recent value."

---

### Q6: Why should you use functional updates with setState?

**How to Answer:**

"This is a really important concept. When you're updating state based on the previous state, you should always use the functional form of setState.

Let me show you why with an example:

```javascript
// This can cause bugs
function handleClick() {
  setCount(count + 1);
  setCount(count + 1);
  setCount(count + 1);
}

// What you'd expect: count increases by 3
// What actually happens: count increases by 1
```

This happens because state updates are batched and asynchronous. All three calls see the same 'count' value, so they all set it to the same number.

The correct way is to use the functional form:

```javascript
function handleClick() {
  setCount(prev => prev + 1);
  setCount(prev => prev + 1);
  setCount(prev => prev + 1);
}

// Now count correctly increases by 3
```

With the functional form, each update receives the most recent state value, so they apply one after another correctly.

This is especially important when you're updating state in event handlers, useEffect, or when multiple updates might happen in quick succession. It's just a safer pattern that prevents subtle bugs."

---

### Q7: Can you explain the difference between setState in Class Components and useState?

**How to Answer:**

"Sure, there are a few key differences.

In class components, state is always an object and setState merges the new state with the old state automatically:

```javascript
// Class component
this.state = { name: 'John', age: 25 };
this.setState({ age: 26 }); // name is still 'John'
```

With useState, each piece of state is separate, and it doesn't merge - it replaces:

```javascript
// Function component
const [user, setUser] = useState({ name: 'John', age: 25 });
setUser({ age: 26 }); // name is now lost!
```

So with useState, if you want to update an object, you need to spread the old values manually:

```javascript
setUser(prev => ({ ...prev, age: 26 })); // Correct way
```

Another difference is that in class components, you have one state object for everything, but with useState, you can split state into multiple variables, which often makes the code cleaner:

```javascript
const [name, setName] = useState('John');
const [age, setAge] = useState(25);
const [isActive, setIsActive] = useState(true);
```

This makes it easier to organize related state and extract logic into custom hooks."

---

## Lifting State Up

### Q8: What does "Lifting State Up" mean?

**How to Answer:**

"Lifting state up is a pattern where you move state from a child component to a parent component so that multiple child components can share that state.

The idea is simple - if two or more components need to share the same data, you put that data in their closest common parent and pass it down as props.

Let me give you a practical example. Say you have a temperature converter with Celsius and Fahrenheit inputs, and they need to stay in sync:

```javascript
function TemperatureConverter() {
  const [temperature, setTemperature] = useState('');
  
  return (
    <div>
      <CelsiusInput 
        value={temperature} 
        onChange={setTemperature} 
      />
      <FahrenheitInput 
        value={temperature} 
        onChange={setTemperature} 
      />
    </div>
  );
}
```

Here, instead of each input managing its own state, we lifted the state up to the parent. Now the parent controls the temperature value and passes it down to both inputs. When either input changes, it calls the onChange function which updates the parent's state, and both inputs get the new value.

This is the React way of keeping components in sync - instead of trying to sync state between siblings, you lift it up to a common parent and let the data flow down through props."

**Key Principle:** "In React, there should be a single source of truth for any data. When multiple components need the same changing data, that's your signal to lift state up to their common parent."

---

### Q9: When should you lift state up vs using Context or Redux?

**How to Answer:**

"Good question. Lifting state up is great for simple cases where you have a few related components that need to share state and they're not too far apart in the component tree.

For example, if you have a form with multiple input fields that need to work together, lifting state to the form component makes perfect sense. The components are close together and it's very clear what's happening.

But if you find yourself passing props through 3-4 levels just to get data to a deeply nested component, that's props drilling and it's a sign you should consider Context API instead.

And if you have complex state with lots of actions, or state that needs to be accessed by many components across your entire app, that's when Redux or Redux Toolkit becomes useful.

My general rule is:
- Lift state up: for simple shared state between nearby components
- Context: for data that many components need but doesn't change super frequently (like theme, user auth)
- Redux/Redux Toolkit: for complex application state with lots of actions and logic

Start simple with lifting state up. Only add Context or Redux when you actually need them. Don't over-engineer early on."

---

## Lazy Initialization

### Q10: What is lazy initialization in useState?

**How to Answer:**

"Lazy initialization is when you pass a function to useState instead of a direct value. This function only runs once, on the initial render, to compute the initial state.

The reason you'd want to do this is performance. Sometimes calculating the initial state is expensive - maybe you're reading from localStorage, or doing some complex computation. You don't want to do that calculation on every render, only on the first render.

Here's an example:

```javascript
// Bad - this runs on every render
function Component() {
  const [state, setState] = useState(
    JSON.parse(localStorage.getItem('data'))
  );
}

// Good - this only runs once
function Component() {
  const [state, setState] = useState(() => {
    return JSON.parse(localStorage.getItem('data'));
  });
}
```

In the first example, even though useState only uses the initial value on the first render, JavaScript still has to parse that localStorage data on every render. That's wasted work.

In the second example, by passing a function, React knows to only call that function on the initial render. On subsequent renders, it just skips it completely.

So basically, if your initial state requires some computation or expensive operation, wrap it in a function. If it's just a simple value like 0 or an empty string, you don't need lazy initialization."

**When to Use:** "Use lazy initialization when your initial state involves: reading from localStorage, expensive calculations, creating new objects/arrays, or filtering/mapping data. For simple primitives, don't bother."

---

## Async States & Data Fetching

### Q11: How do you handle async data fetching in React?

**How to Answer:**

"When fetching data in React, you typically use useEffect to trigger the fetch and useState to store the data and loading/error states.

The common pattern is to have three states: loading, data, and error:

```javascript
function UserList() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  
  useEffect(() => {
    fetch('https://api.example.com/users')
      .then(response => response.json())
      .then(data => {
        setUsers(data);
        setLoading(false);
      })
      .catch(err => {
        setError(err.message);
        setLoading(false);
      });
  }, []);
  
  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error}</div>;
  
  return (
    <ul>
      {users.map(user => <li key={user.id}>{user.name}</li>)}
    </ul>
  );
}
```

This pattern covers all the states your UI needs to handle - loading state for showing a spinner, error state for when things go wrong, and the actual data state for displaying the results.

One important thing is to handle cleanup. If the component unmounts before the fetch completes, you can get a warning about setting state on an unmounted component. You can handle this with a cleanup function or an AbortController."

**Modern Approach:** "These days, many people use libraries like React Query or SWR which handle all this automatically - loading states, caching, refetching, error handling. But it's important to understand the fundamental pattern first."

---

### Q12: What are the common patterns for managing loading and error states?

**How to Answer:**

"There are a few common patterns for managing async states in React.

**Pattern 1: Multiple useState calls**
```javascript
const [data, setData] = useState(null);
const [loading, setLoading] = useState(false);
const [error, setError] = useState(null);
```

This is straightforward but you have to remember to update multiple states when fetching.

**Pattern 2: Single state object**
```javascript
const [state, setState] = useState({
  data: null,
  loading: false,
  error: null
});
```

This keeps everything together, but you need to spread the previous state when updating.

**Pattern 3: useReducer for complex async logic**
```javascript
const [state, dispatch] = useReducer(reducer, {
  data: null,
  loading: false,
  error: null
});

// Then dispatch actions like:
dispatch({ type: 'FETCH_START' });
dispatch({ type: 'FETCH_SUCCESS', payload: data });
dispatch({ type: 'FETCH_ERROR', error: error });
```

This is cleaner when you have multiple async operations or complex state transitions.

My personal preference is multiple useState for simple cases, and useReducer when the logic gets more complex. The single state object approach is okay but can get messy with the spreading."

**Pro Tip:** "Also consider creating a custom hook like `useFetch` or `useAsync` to encapsulate this logic so you don't repeat it everywhere."

---

## useEffect Hook

### Q13: What is useEffect and when do you use it?

**How to Answer:**

"useEffect is a hook that lets you perform side effects in function components. Side effects are basically anything that affects something outside the component - like data fetching, subscriptions, timers, manually changing the DOM, or logging.

The basic syntax is:

```javascript
useEffect(() => {
  // Your side effect code here
}, [dependencies]);
```

The first argument is the function that runs your side effect, and the second argument is the dependency array that controls when it runs.

Common use cases are:
- Fetching data when component mounts
- Setting up subscriptions or event listeners
- Syncing with external systems
- Updating document title
- Setting up timers

For example, fetching data:

```javascript
useEffect(() => {
  fetch('https://api.example.com/data')
    .then(res => res.json())
    .then(data => setData(data));
}, []); // Empty array means run once on mount
```

Or setting up a subscription:

```javascript
useEffect(() => {
  const subscription = subscribeToMessages(userId);
  
  return () => subscription.unsubscribe(); // Cleanup
}, [userId]); // Re-subscribe when userId changes
```

The key thing is that useEffect runs after render, not during render. This is important because it keeps your component function pure and prevents blocking the browser."

---

### Q14: Explain the dependency array in useEffect.

**How to Answer:**

"The dependency array is the second argument to useEffect, and it controls when your effect runs. It's one of the most important concepts to understand because getting it wrong causes bugs.

There are three cases:

**Case 1: No dependency array**
```javascript
useEffect(() => {
  console.log('Runs after every render');
});
```
The effect runs after every single render. This is usually not what you want and can cause performance issues or infinite loops.

**Case 2: Empty dependency array**
```javascript
useEffect(() => {
  console.log('Runs only once on mount');
}, []);
```
The effect runs only once after the initial render. This is like componentDidMount in class components. Use this for one-time setup like fetching initial data.

**Case 3: With dependencies**
```javascript
useEffect(() => {
  console.log('Runs when count changes');
}, [count]);
```
The effect runs on mount and whenever any value in the dependency array changes. React compares the values with the previous render using Object.is equality.

The rule is: include every value from the component scope that your effect uses. If your effect uses a state variable or prop, put it in the dependency array. Otherwise you'll have stale closure problems where your effect sees old values.

Modern React has ESLint rules that warn you if you forget to include a dependency, which is really helpful."

---

### Q15: What is the cleanup function in useEffect?

**How to Answer:**

"The cleanup function is what you return from useEffect. It's used to clean up side effects before the component unmounts or before the effect runs again.

```javascript
useEffect(() => {
  // Setup
  const timer = setInterval(() => {
    console.log('Tick');
  }, 1000);
  
  // Cleanup
  return () => {
    clearInterval(timer);
  };
}, []);
```

React calls the cleanup function in two situations:
1. Before the component unmounts - to clean up things like subscriptions, timers, event listeners
2. Before running the effect again - if dependencies changed, React cleans up the previous effect before running the new one

Common things you clean up:
- Timers (clearInterval, clearTimeout)
- Event listeners (removeEventListener)
- Subscriptions (unsubscribe)
- Abort controllers for fetch requests
- WebSocket connections

Not having proper cleanup can cause memory leaks. For example, if you set up an interval or event listener and never clean it up, it'll keep running even after the component is gone. That's why cleanup is so important.

A good rule of thumb: if you set something up in useEffect, you probably need to clean it up in the return function."

---

### Q16: What are the common mistakes with useEffect?

**How to Answer:**

"There are several common mistakes people make with useEffect.

**Mistake 1: Missing dependencies**
```javascript
useEffect(() => {
  console.log(count); // Uses count but doesn't include it
}, []); // Will always log the initial count value
```
This creates stale closures. Always include what you use.

**Mistake 2: Infinite loops**
```javascript
useEffect(() => {
  setCount(count + 1); // Sets state...
}, [count]); // ...which triggers effect...which sets state again
```
This creates an infinite loop. Be careful when setting state in effects.

**Mistake 3: Not cleaning up**
```javascript
useEffect(() => {
  const timer = setInterval(() => tick(), 1000);
  // Forgot to return cleanup function
}, []);
```
This causes memory leaks.

**Mistake 4: Putting objects/arrays in dependencies**
```javascript
useEffect(() => {
  // do something
}, [{ id: 1 }]); // New object every render, effect runs every time
```
Objects and arrays get new references every render, so the effect runs every time. Extract primitive values instead.

**Mistake 5: Treating useEffect like lifecycle methods**
Don't try to replicate exact componentDidMount/componentDidUpdate behavior. Think in terms of synchronization - you're synchronizing your component with external systems based on dependencies.

The key is to think about what your effect depends on and make sure those dependencies are in the array. Let React handle when to run it."

---

## Context API

### Q17: What is Context API and when should you use it?

**How to Answer:**

"Context API is React's built-in solution for sharing data across your component tree without having to pass props down manually at every level. It's designed to solve the props drilling problem.

The basic idea is you create a context, provide a value at a high level in your tree, and then any component below can consume that value without needing props passed through all the intermediate components.

Here's a simple example:

```javascript
// Create context
const ThemeContext = createContext();

// Provide value at top level
function App() {
  const [theme, setTheme] = useState('light');
  
  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      <Navbar />
      <Main />
    </ThemeContext.Provider>
  );
}

// Consume anywhere deep in the tree
function Button() {
  const { theme, setTheme } = useContext(ThemeContext);
  
  return (
    <button style={{ background: theme === 'light' ? '#fff' : '#000' }}>
      Click me
    </button>
  );
}
```

**When to use Context:**
- Theme data (light/dark mode)
- User authentication data
- Language/localization settings
- Data that many components need at different nesting levels

**When NOT to use Context:**
- Don't use it for everything - it's not a replacement for all state management
- Avoid it for data that changes very frequently (causes re-renders)
- Don't use it just to avoid passing props one level down

Context is great for low-frequency updates that affect many components. For high-frequency updates or complex state logic, consider Redux or other solutions."

---

### Q18: How does useContext work?

**How to Answer:**

"useContext is the hook that lets you consume a context value in a function component. It's much simpler than the old Context.Consumer pattern.

The way you use it is straightforward:

```javascript
// First, create the context (usually in a separate file)
const UserContext = createContext();

// Provide the value somewhere high in your tree
function App() {
  const user = { name: 'John', role: 'admin' };
  
  return (
    <UserContext.Provider value={user}>
      <Dashboard />
    </UserContext.Provider>
  );
}

// Use the context anywhere below the Provider
function UserProfile() {
  const user = useContext(UserContext);
  
  return <div>Welcome, {user.name}</div>;
}
```

When you call useContext with a context object, it returns the current context value. That value comes from the nearest Provider above it in the tree.

Important things to know:
- The component will re-render when the context value changes
- You must wrap consumers with a Provider, or you'll get the default value (which is undefined if you didn't provide one)
- If you have multiple contexts, you can use multiple useContext calls in the same component

One common pattern is to create a custom hook for your context:

```javascript
function useUser() {
  const context = useContext(UserContext);
  if (!context) {
    throw new Error('useUser must be used within UserProvider');
  }
  return context;
}
```

This makes it cleaner to use and gives you a clear error message if someone forgets the Provider."

---

### Q19: What are the performance concerns with Context?

**How to Answer:**

"The main performance issue with Context is that when the context value changes, every component that calls useContext with that context will re-render, even if they only use part of the value.

For example:

```javascript
const AppContext = createContext();

function App() {
  const [user, setUser] = useState({ name: 'John' });
  const [theme, setTheme] = useState('light');
  
  return (
    <AppContext.Provider value={{ user, theme, setUser, setTheme }}>
      <Children />
    </AppContext.Provider>
  );
}
```

If theme changes, every component using useContext(AppContext) re-renders, even if they only care about user data.

**Solutions:**

**Solution 1: Split contexts**
```javascript
<UserContext.Provider value={user}>
  <ThemeContext.Provider value={theme}>
    <App />
  </ThemeContext.Provider>
</UserContext.Provider>
```

Now changing theme doesn't affect components that only use UserContext.

**Solution 2: Memoize the context value**
```javascript
const value = useMemo(
  () => ({ user, theme, setUser, setTheme }),
  [user, theme]
);

return <AppContext.Provider value={value}>...</AppContext.Provider>
```

This prevents unnecessary re-renders when the component re-renders but the actual values haven't changed.

**Solution 3: Use selectors**
Instead of providing everything, provide only what's needed or use a state management library with selectors.

Generally, if you're worried about performance, split your contexts by concern and memoize values. But also, don't optimize prematurely - measure first to see if you actually have a performance problem."

---

## useRef Hook

### Q20: What is useRef and what are its use cases?

**How to Answer:**

"useRef is a hook that lets you create a mutable reference that persists across renders but doesn't cause re-renders when you change it.

It has two main use cases:

**Use Case 1: Accessing DOM elements**
```javascript
function TextInput() {
  const inputRef = useRef();
  
  const focusInput = () => {
    inputRef.current.focus();
  };
  
  return (
    <>
      <input ref={inputRef} />
      <button onClick={focusInput}>Focus Input</button>
    </>
  );
}
```

You attach the ref to a DOM element, and then you can access that element directly via inputRef.current. This is useful for things like focusing inputs, measuring dimensions, playing videos, scrolling, etc.

**Use Case 2: Storing mutable values**
```javascript
function Timer() {
  const [count, setCount] = useState(0);
  const intervalRef = useRef();
  
  const startTimer = () => {
    intervalRef.current = setInterval(() => {
      setCount(c => c + 1);
    }, 1000);
  };
  
  const stopTimer = () => {
    clearInterval(intervalRef.current);
  };
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={startTimer}>Start</button>
      <button onClick={stopTimer}>Stop</button>
    </div>
  );
}
```

Here we're storing the interval ID in a ref. We need to keep track of it to clear it later, but we don't want to trigger re-renders when it changes. That's perfect for useRef.

The key difference from useState is that changing a ref doesn't cause a re-render. The value persists across renders but is invisible to React's rendering process."

---

### Q21: What's the difference between useRef and useState?

**How to Answer:**

"The main difference is that useState causes re-renders when the state changes, while useRef doesn't.

With useState:
```javascript
const [count, setCount] = useState(0);
setCount(1); // Triggers re-render
```

With useRef:
```javascript
const countRef = useRef(0);
countRef.current = 1; // NO re-render
```

**When to use useState:**
- When you need the UI to update when the value changes
- When the value is part of what the user sees
- Like: form inputs, lists, toggle states, anything visual

**When to use useRef:**
- When you need to store a value but don't want re-renders
- When accessing DOM elements
- When storing things like interval IDs, previous values, timers
- Basically, implementation details that aren't part of the visual output

Another way to think about it: useState is for data that affects what the user sees. useRef is for behind-the-scenes data that your component logic needs but the user doesn't care about.

One common mistake is trying to display ref values in JSX:

```javascript
const countRef = useRef(0);
countRef.current++;

return <div>{countRef.current}</div>; // Won't update on screen!
```

The value updates, but the component doesn't re-render, so the screen shows the old value. For anything you're displaying, use useState."

---

### Q22: Can you explain the previous value pattern with useRef?

**How to Answer:**

"Sure, this is a common pattern where you use useRef to store the previous value of a state or prop.

The idea is that useRef persists across renders, so you can store a value in it, and on the next render, you can check what that value was before.

Here's a practical example:

```javascript
function Counter() {
  const [count, setCount] = useState(0);
  const prevCountRef = useRef();
  
  useEffect(() => {
    prevCountRef.current = count; // Store current count after render
  });
  
  const prevCount = prevCountRef.current;
  
  return (
    <div>
      <p>Current: {count}</p>
      <p>Previous: {prevCount}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

What happens here is:
1. Component renders with current count
2. After render, useEffect updates the ref to store the current count
3. On the next render, prevCountRef.current still has the old value (until useEffect runs again)
4. So we can display both current and previous values

This is useful for:
- Comparing if a value actually changed before doing something
- Animations where you need to know the previous state
- Tracking changes in props or state
- Debugging to see what value something had before

You can even make a custom hook for this:

```javascript
function usePrevious(value) {
  const ref = useRef();
  
  useEffect(() => {
    ref.current = value;
  });
  
  return ref.current;
}

// Usage
const prevCount = usePrevious(count);
```

This pattern is pretty common in real applications, especially when you need to react to changes but need to know what the old value was."

---

## useReducer Hook

### Q23: What is useReducer and when should you use it instead of useState?

**How to Answer:**

"useReducer is an alternative to useState for managing complex state logic. It's based on the reducer pattern from Redux.

The basic idea is that instead of calling setState directly, you dispatch actions, and a reducer function decides how to update the state based on those actions.

Here's the syntax:

```javascript
const [state, dispatch] = useReducer(reducer, initialState);
```

And here's a simple example:

```javascript
function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });
  
  return (
    <>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
    </>
  );
}
```

**When to use useReducer instead of useState:**

1. **Complex state logic** - When you have multiple state values that are related and updates to one affect the others

2. **Multiple state updates** - When a single action needs to update several pieces of state

3. **State transitions** - When next state depends on the previous state in complex ways

4. **Easier testing** - Reducers are pure functions, so they're easy to test independently

5. **Better organization** - All your state logic is in one place instead of scattered across multiple setState calls

For example, a form with validation would be good for useReducer:

```javascript
function reducer(state, action) {
  switch (action.type) {
    case 'SET_NAME':
      return { ...state, name: action.payload, nameError: '' };
    case 'SET_EMAIL':
      return { ...state, email: action.payload, emailError: '' };
    case 'SUBMIT':
      // Validate and set errors
      const errors = validate(state);
      return { ...state, ...errors };
    default:
      return state;
  }
}
```

If you have simple state like a boolean or a number, useState is fine. But when the logic gets complicated, useReducer makes it more maintainable."

---

### Q24: How does useReducer relate to Redux?

**How to Answer:**

"useReducer is actually based on the same pattern as Redux - the reducer pattern. The concepts are very similar, but useReducer is built into React and is component-scoped, while Redux is a separate library for global state.

**Similarities:**
- Both use reducers - pure functions that take (state, action) and return new state
- Both use actions - objects with a type and optional payload
- Both follow the same immutability principles
- Both make state updates predictable and testable

**Differences:**

**useReducer:**
- Built into React, no extra library
- State is local to a component (or shared via Context)
- No middleware support
- Simpler, less boilerplate
- Good for component-level complex state

**Redux:**
- Separate library
- Global state for entire app
- Middleware support (thunks, sagas, etc.)
- DevTools for time-travel debugging
- More boilerplate but more powerful
- Good for app-wide state management

You can think of useReducer as 'Redux lite' for component state. If you understand useReducer, learning Redux is much easier because the core concept is the same.

Many apps use both - useReducer for complex component state and Redux for global app state that needs to be accessed everywhere. Or you can use useReducer with Context to create a Redux-like global state without actually using Redux."

---

## Redux & Redux Toolkit

### Q25: What is Redux and what problem does it solve?

**How to Answer:**

"Redux is a predictable state management library for JavaScript apps. It provides a centralized store for all your application state, and it enforces rules about how and when state can be updated.

**The problems Redux solves:**

1. **Props drilling** - Instead of passing props through multiple levels, any component can access global state directly

2. **Shared state** - When multiple components need access to the same data, it's all in one place

3. **Predictability** - State updates follow a strict unidirectional data flow, making it easier to understand what happened and why

4. **Debugging** - With Redux DevTools, you can see every action that was dispatched and how it changed the state, even time-travel debug

5. **Organization** - For large apps, having all state logic in reducers keeps things organized

**Core concepts of Redux:**

**Store** - Holds the entire application state
```javascript
const store = createStore(reducer);
```

**Actions** - Plain objects describing what happened
```javascript
{ type: 'ADD_TODO', payload: { text: 'Learn Redux' } }
```

**Reducers** - Pure functions that take current state and an action, return new state
```javascript
function todosReducer(state = [], action) {
  switch (action.type) {
    case 'ADD_TODO':
      return [...state, action.payload];
    default:
      return state;
  }
}
```

**Dispatch** - The only way to trigger a state update
```javascript
store.dispatch({ type: 'ADD_TODO', payload: { text: 'Learn Redux' } });
```

The data flow is: UI dispatches action → reducer updates state → store notifies components → UI re-renders.

Redux is overkill for small apps, but for large apps with lots of shared state and complex interactions, it makes state management much more manageable."

---

### Q26: What is Redux Toolkit and why do we use it?

**How to Answer:**

"Redux Toolkit is the official, recommended way to write Redux logic. It's basically Redux with less boilerplate and better defaults.

The problem with vanilla Redux was that it required a lot of setup code - creating action types, action creators, writing immutable update logic with spread operators, setting up the store with middleware, etc. Redux Toolkit simplifies all of that.

**Key benefits of Redux Toolkit:**

1. **configureStore** - Sets up the store with good defaults automatically
```javascript
const store = configureStore({
  reducer: {
    todos: todosReducer,
    user: userReducer
  }
});
// Redux DevTools and thunk middleware are included by default
```

2. **createSlice** - Generates action creators and action types automatically
```javascript
const todosSlice = createSlice({
  name: 'todos',
  initialState: [],
  reducers: {
    addTodo: (state, action) => {
      state.push(action.payload); // Looks like mutation but uses Immer
    },
    removeTodo: (state, action) => {
      return state.filter(todo => todo.id !== action.payload);
    }
  }
});
```

Notice you can write code that looks like mutations, but Redux Toolkit uses Immer library behind the scenes to make it immutable.

3. **createAsyncThunk** - Handles async logic cleanly
```javascript
const fetchUsers = createAsyncThunk(
  'users/fetch',
  async () => {
    const response = await fetch('/api/users');
    return response.json();
  }
);
```

4. **Built-in TypeScript support** - Great TypeScript experience out of the box

**Bottom line:** If you're using Redux today, you should be using Redux Toolkit. It's less code, fewer bugs, and it's the official recommendation from the Redux team. All modern Redux projects use Redux Toolkit, not vanilla Redux."

---

### Q27: Explain Redux data flow with an example.

**How to Answer:**

"Redux follows a strict unidirectional data flow, which makes the application behavior predictable. Let me walk through it with a concrete example of adding a todo item.

**Step 1: User interaction**
User clicks 'Add Todo' button

**Step 2: Dispatch an action**
```javascript
dispatch({
  type: 'todos/addTodo',
  payload: { id: 1, text: 'Learn Redux', completed: false }
});
```

**Step 3: Action goes to the reducer**
The store calls the reducer with the current state and the action:

```javascript
function todosReducer(state = [], action) {
  switch (action.type) {
    case 'todos/addTodo':
      return [...state, action.payload];
    default:
      return state;
  }
}
```

**Step 4: Reducer returns new state**
The reducer returns a new state array with the todo added. It doesn't mutate the old state - it returns a brand new array.

**Step 5: Store updates**
The store saves the new state.

**Step 6: UI updates**
All components subscribed to that part of the state re-render with the new data:

```javascript
function TodoList() {
  const todos = useSelector(state => state.todos);
  
  return (
    <ul>
      {todos.map(todo => <li key={todo.id}>{todo.text}</li>)}
    </ul>
  );
}
```

The key points are:
- State is read-only - you can't modify it directly
- Changes are made by dispatching actions
- Reducers are pure functions - same input always gives same output
- The flow is always one direction: Action → Reducer → New State → UI Update

This makes it easy to trace exactly what happened in your app. You can look at the action log and replay the exact sequence of events."

---

### Q28: What are selectors in Redux? Why use them?

**How to Answer:**

"Selectors are functions that extract specific pieces of data from the Redux store. You use them with the useSelector hook to read state in your components.

**Basic selector:**
```javascript
function TodoList() {
  const todos = useSelector(state => state.todos);
  return <div>{/* render todos */}</div>;
}
```

That inline function `state => state.todos` is a selector. But for better code organization and reusability, you usually define them separately:

```javascript
// selectors.js
export const selectAllTodos = state => state.todos;
export const selectCompletedTodos = state => 
  state.todos.filter(todo => todo.completed);

// Component
const todos = useSelector(selectAllTodos);
```

**Why use selectors:**

1. **Reusability** - Write the logic once, use it in multiple components

2. **Testability** - Easy to test selectors independently

3. **Memoization** - You can use libraries like Reselect to memoize expensive computations:

```javascript
import { createSelector } from 'reselect';

const selectAllTodos = state => state.todos;

const selectCompletedTodos = createSelector(
  [selectAllTodos],
  todos => todos.filter(todo => todo.completed)
);
```

With createSelector, the filtering only runs when todos actually changes, not on every render. This is great for performance.

4. **Encapsulation** - Components don't need to know the shape of the state tree:

```javascript
// If you restructure your state, you only update selectors
// Before: state.todos
// After: state.data.todos
export const selectAllTodos = state => state.data.todos;
// Components don't need to change
```

So basically, selectors are your interface to the Redux store. They make your code cleaner, more performant, and easier to maintain."

---

### Q29: What is Redux middleware? Explain Redux Thunk.

**How to Answer:**

"Middleware in Redux is basically code that sits between dispatching an action and the moment it reaches the reducer. It can intercept actions and do things with them - log them, delay them, make API calls, whatever you need.

The most common middleware is Redux Thunk, which lets you write action creators that return functions instead of action objects. This is how you handle async operations in Redux.

**Without Thunk (won't work for async):**
```javascript
// This doesn't work because you can't dispatch async actions
const addTodo = () => {
  return { type: 'ADD_TODO' };
};
```

**With Thunk:**
```javascript
// This works - thunk lets you return a function
const fetchTodos = () => {
  return async (dispatch) => {
    dispatch({ type: 'FETCH_TODOS_START' });
    
    try {
      const response = await fetch('/api/todos');
      const data = await response.json();
      dispatch({ type: 'FETCH_TODOS_SUCCESS', payload: data });
    } catch (error) {
      dispatch({ type: 'FETCH_TODOS_ERROR', error: error.message });
    }
  };
};

// Usage
dispatch(fetchTodos());
```

When you dispatch a thunk (a function), the middleware intercepts it and calls that function with dispatch and getState as arguments. Inside the function, you can do async work and dispatch real actions when you're ready.

**In Redux Toolkit, it's even simpler with createAsyncThunk:**
```javascript
const fetchTodos = createAsyncThunk(
  'todos/fetch',
  async () => {
    const response = await fetch('/api/todos');
    return response.json();
  }
);

// It automatically creates pending/fulfilled/rejected actions
```

Thunk middleware is included by default when you use Redux Toolkit's configureStore, so you don't have to set it up manually.

The key concept is: middleware extends Redux's capabilities. Thunk specifically solves the async problem by letting action creators do async work before dispatching the real actions."

---

### Q30: How do you structure a Redux application?

**How to Answer:**

"There are different approaches, but the modern recommended structure with Redux Toolkit is the feature-based or 'slices' approach.

**Structure by feature:**
```
src/
  app/
    store.js          // Configure store
  features/
    todos/
      todosSlice.js   // All Redux logic for todos
      TodoList.jsx    // Component
    user/
      userSlice.js    // All Redux logic for user
      UserProfile.jsx // Component
```

**What goes in a slice file:**
```javascript
// features/todos/todosSlice.js
import { createSlice } from '@reduxjs/toolkit';

const todosSlice = createSlice({
  name: 'todos',
  initialState: [],
  reducers: {
    addTodo: (state, action) => {
      state.push(action.payload);
    },
    removeTodo: (state, action) => {
      return state.filter(todo => todo.id !== action.payload);
    }
  }
});

export const { addTodo, removeTodo } = todosSlice.actions;
export default todosSlice.reducer;

// Selectors
export const selectAllTodos = state => state.todos;
```

**Setting up the store:**
```javascript
// app/store.js
import { configureStore } from '@reduxjs/toolkit';
import todosReducer from '../features/todos/todosSlice';
import userReducer from '../features/user/userSlice';

export const store = configureStore({
  reducer: {
    todos: todosReducer,
    user: userReducer
  }
});
```

**Key principles:**

1. **Feature-based folders** - Group by feature, not by file type

2. **Co-location** - Keep related code together (slice, selectors, components)

3. **Single slice per feature** - Each feature has one slice that handles all its state

4. **Selectors in slice files** - Export selectors from the same file as the slice

5. **Async logic** - Use createAsyncThunk for API calls

For large applications, you might add:
- `hooks/` folder for custom Redux hooks
- `middleware/` for custom middleware
- Separate selector files if they get complex

The key is keeping things organized by feature so you can easily find all the related code. This scales much better than the old approach of separating by type (actions folder, reducers folder, etc.)."

---

## Class Components (Minimal Coverage)

### Q31: What are the basic lifecycle methods in Class Components?

**How to Answer:**

"Even though we mostly use function components now, you might encounter class components in legacy code, so it's good to know the basics.

The main lifecycle methods are:

**componentDidMount** - Runs once after the component first renders. This is like useEffect with empty dependencies [].

```javascript
componentDidMount() {
  // Fetch data, set up subscriptions
  fetch('/api/data')
    .then(res => res.json())
    .then(data => this.setState({ data }));
}
```

**componentDidUpdate** - Runs after every update. This is like useEffect with dependencies.

```javascript
componentDidUpdate(prevProps, prevState) {
  // React to prop or state changes
  if (prevProps.userId !== this.props.userId) {
    this.fetchUserData(this.props.userId);
  }
}
```

**componentWillUnmount** - Runs right before component is removed. This is like the cleanup function in useEffect.

```javascript
componentWillUnmount() {
  // Clean up subscriptions, timers
  clearInterval(this.timer);
}
```

**render** - Required method that returns JSX.

```javascript
render() {
  return <div>{this.state.count}</div>;
}
```

Here's a comparison with hooks:

```javascript
// Class component
class Counter extends React.Component {
  componentDidMount() {
    console.log('mounted');
  }
  
  componentDidUpdate() {
    console.log('updated');
  }
  
  componentWillUnmount() {
    console.log('unmounting');
  }
}

// Equivalent with hooks
function Counter() {
  useEffect(() => {
    console.log('mounted');
    
    return () => console.log('unmounting');
  }, []);
  
  useEffect(() => {
    console.log('updated');
  });
}
```

That's really all you need to know about class components for interviews. The focus now is on function components and hooks."

---

## Performance & Best Practices

### Q32: What are React.memo, useMemo, and useCallback? When do you use them?

**How to Answer:**

"These are all about optimization - preventing unnecessary re-renders or recalculations.

**React.memo** - Prevents a component from re-rendering if its props haven't changed:

```javascript
const TodoItem = React.memo(({ todo, onToggle }) => {
  console.log('Rendering', todo.text);
  return (
    <div onClick={() => onToggle(todo.id)}>
      {todo.text}
    </div>
  );
});
```

Without memo, TodoItem would re-render whenever the parent re-renders, even if that specific todo didn't change. With memo, it only re-renders if the todo prop actually changes.

**useMemo** - Memoizes expensive calculations:

```javascript
function TodoList({ todos, filter }) {
  const filteredTodos = useMemo(() => {
    console.log('Filtering...');
    return todos.filter(todo => todo.status === filter);
  }, [todos, filter]);
  
  return <div>{/* render filteredTodos */}</div>;
}
```

Without useMemo, the filtering runs on every render. With useMemo, it only runs when todos or filter actually changes.

**useCallback** - Memoizes functions:

```javascript
function TodoList() {
  const [todos, setTodos] = useState([]);
  
  const addTodo = useCallback((text) => {
    setTodos(prev => [...prev, { text, id: Date.now() }]);
  }, []); // Function doesn't change
  
  return <TodoForm onSubmit={addTodo} />;
}
```

Without useCallback, addTodo is a new function on every render, which would cause TodoForm to re-render even if nothing changed. With useCallback, it's the same function instance across renders.

**When to use them:**

1. **React.memo** - When a component renders the same output for the same props and you're seeing performance issues

2. **useMemo** - For expensive calculations that you don't want to repeat on every render

3. **useCallback** - When passing callbacks to memoized child components

**Important:** Don't use these optimizations prematurely. They have a cost too. Only use them when you've identified an actual performance problem. Most components don't need optimization."

---

### Q33: What are keys in React and why are they important?

**How to Answer:**

"Keys are special attributes you need to include when creating lists of elements in React. They help React identify which items have changed, been added, or been removed.

```javascript
function TodoList({ todos }) {
  return (
    <ul>
      {todos.map(todo => (
        <li key={todo.id}>{todo.text}</li>
      ))}
    </ul>
  );
}
```

**Why keys matter:**

When you don't use keys or use bad keys, React has a hard time figuring out what changed. It might re-render more than necessary or even reuse the wrong component instances, causing bugs.

**Common mistakes:**

**Mistake 1: Using array index as key**
```javascript
{todos.map((todo, index) => (
  <li key={index}>{todo.text}</li>
))}
```

This seems okay but causes problems when you reorder, add, or remove items. The key stays the same but the todo changes, confusing React.

**Mistake 2: Using random values**
```javascript
{todos.map(todo => (
  <li key={Math.random()}>{todo.text}</li>
))}
```

This is terrible because the key is different on every render, so React thinks every item is new and recreates everything.

**Correct approach: Use stable, unique IDs**
```javascript
{todos.map(todo => (
  <li key={todo.id}>{todo.text}</li>
))}
```

The key should be unique among siblings and stable across renders - usually an ID from your database.

**What happens with bad keys:**
- Components might not update when they should
- Input elements might lose focus or state
- Performance suffers from unnecessary re-creation
- Weird bugs that are hard to track down

Keys seem simple but they're really important for React to efficiently update the DOM. Always use stable, unique keys when rendering lists."

---

### Q34: What are some common performance pitfalls in React?

**How to Answer:**

"There are several common performance issues I've seen:

**1. Creating objects/arrays in render**
```javascript
// Bad - new array every render
function TodoList() {
  return <TodoItem styles={{ color: 'red' }} />;
}

// Good - constant reference
const styles = { color: 'red' };
function TodoList() {
  return <TodoItem styles={styles} />;
}
```

**2. Not memoizing context values**
```javascript
// Bad - new object every render
<UserContext.Provider value={{ user, setUser }}>

// Good - memoized value
const value = useMemo(() => ({ user, setUser }), [user]);
<UserContext.Provider value={value}>
```

**3. Large lists without virtualization**
If you're rendering thousands of items, you need virtualization with libraries like react-window or react-virtual:

```javascript
// Bad - renders 10,000 items
{items.map(item => <Item key={item.id} />)}

// Good - only renders visible items
<FixedSizeList
  height={600}
  itemCount={items.length}
  itemSize={35}
>
  {({ index, style }) => (
    <div style={style}>{items[index]}</div>
  )}
</FixedSizeList>
```

**4. Unnecessary effects**
```javascript
// Bad - runs on every render
useEffect(() => {
  document.title = `Count: ${count}`;
});

// Good - only when count changes
useEffect(() => {
  document.title = `Count: ${count}`;
}, [count]);
```

**5. State that's too high**
Don't put state in App.js if only one component needs it. Keep state as close as possible to where it's used.

**6. Not splitting bundles**
Use React.lazy and Suspense to split large components into separate bundles:

```javascript
const HeavyComponent = React.lazy(() => import('./HeavyComponent'));

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <HeavyComponent />
    </Suspense>
  );
}
```

The key is to measure first with React DevTools Profiler before optimizing. Don't guess - measure and optimize what's actually slow."

---

### Q35: What are some React best practices you follow?

**How to Answer:**

"Here are the best practices I always try to follow:

**1. Component organization**
- Keep components small and focused on one thing
- Extract reusable logic into custom hooks
- Use meaningful, descriptive names

**2. State management**
- Keep state as local as possible
- Lift state up only when necessary
- Use the right tool: useState for simple state, useReducer for complex logic, Context for shared data, Redux for global app state

**3. Props and typing**
- Destructure props for clarity
- Use PropTypes or TypeScript for type safety
- Keep prop drilling to 2-3 levels maximum

**4. Effects**
- Always include dependencies
- Clean up side effects properly
- Separate concerns into different useEffect calls

**5. Performance**
- Don't optimize prematurely - measure first
- Use keys properly in lists
- Memoize only when needed
- Split code with lazy loading

**6. Code style**
- Keep consistent formatting (use Prettier)
- Follow ESLint rules
- Write clear, self-documenting code
- Add comments only for complex logic

**7. Testing**
- Write tests for critical logic
- Test behavior, not implementation details
- Use React Testing Library for component tests

**8. File structure**
- Organize by feature, not by file type
- Keep related files together
- Use index files to simplify imports

**9. Error handling**
- Use Error Boundaries for component errors
- Handle loading and error states in data fetching
- Provide good error messages to users

**10. Accessibility**
- Use semantic HTML
- Include ARIA attributes where needed
- Ensure keyboard navigation works
- Test with screen readers

The most important thing is writing code that's easy to understand and maintain. Performance and optimization come second to clarity and correctness."

---

## Common Tricky Interview Questions

### Q36: How would you optimize a slow React application?

**How to Answer:**

"I'd approach this systematically:

**Step 1: Measure and identify the problem**
Use React DevTools Profiler to see which components are slow and rendering too often. Don't guess - you need data first.

**Step 2: Check for common issues**

- **Unnecessary re-renders**: Are components re-rendering when their props haven't changed? Use React.memo.

- **Expensive calculations**: Are you doing heavy computations on every render? Use useMemo.

- **Large lists**: Are you rendering thousands of items? Use virtualization.

- **Huge bundles**: Is your initial JS bundle too large? Use code splitting with React.lazy.

**Step 3: Optimize based on findings**

For example, if I see a list component re-rendering all items when only one changed:

```javascript
// Before
function TodoList({ todos }) {
  return todos.map(todo => <TodoItem todo={todo} />);
}

// After
const TodoItem = React.memo(({ todo }) => {
  return <div>{todo.text}</div>;
});

function TodoList({ todos }) {
  return todos.map(todo => <TodoItem key={todo.id} todo={todo} />);
}
```

**Step 4: Consider architecture changes**

If the problem is deeper:
- Move state closer to where it's used
- Split large contexts into smaller ones
- Consider Redux if you have complex global state
- Lazy load routes and heavy components

**Step 5: Measure again**

After each change, measure again to see if it actually helped. Sometimes optimizations don't make a noticeable difference.

The key is being methodical - measure, identify, fix, measure again. Don't just add useMemo everywhere and hope for the best."

---

### Q37: Explain the concept of controlled vs uncontrolled components.

**How to Answer:**

"This is about how form inputs handle their values.

**Controlled components** - React controls the input value through state:

```javascript
function Form() {
  const [name, setName] = useState('');
  
  return (
    <input
      value={name}
      onChange={(e) => setName(e.target.value)}
    />
  );
}
```

The input's value is always what's in React state. When you type, onChange updates state, which updates the input. React is the single source of truth.

**Uncontrolled components** - The DOM handles the value:

```javascript
function Form() {
  const inputRef = useRef();
  
  const handleSubmit = () => {
    console.log(inputRef.current.value);
  };
  
  return (
    <input ref={inputRef} defaultValue="John" />
  );
}
```

The input manages its own state internally. You access the value using a ref when you need it. The DOM is the source of truth.

**When to use each:**

**Controlled (most common):**
- When you need to validate as user types
- When you need to enforce formatting (like phone numbers)
- When you need to enable/disable buttons based on input
- When working with complex forms

**Uncontrolled (rare):**
- Simple forms where you only need values on submit
- Integrating with non-React code
- File inputs (these are always uncontrolled in React)

For example, controlled is better when you need this:

```javascript
function PasswordForm() {
  const [password, setPassword] = useState('');
  const isValid = password.length >= 8;
  
  return (
    <>
      <input
        type="password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
      />
      <button disabled={!isValid}>Submit</button>
    </>
  );
}
```

You need the password value in state to determine if the button should be disabled. That's only possible with controlled inputs.

In modern React, controlled components are the standard approach. Uncontrolled is only for special cases."

---

### Q38: What happens when you call setState? Walk me through the process.

**How to Answer:**

"When you call setState, several things happen:

**Step 1: React schedules an update**
React doesn't update immediately - it marks the component for update and batches multiple setState calls together for performance.

```javascript
setCount(1);
setCount(2);
setCount(3);
// Only triggers one re-render, not three
```

**Step 2: React determines what changed**
React compares the new state with the old state. If nothing changed (same reference), it might skip the update.

**Step 3: React re-renders the component**
React calls your component function again with the new state.

**Step 4: React compares the new JSX with the old JSX (Virtual DOM diffing)**
React doesn't immediately update the real DOM. First, it creates a new virtual DOM tree and compares it with the previous one to find the minimum changes needed.

**Step 5: React commits changes to the real DOM**
Only the parts that actually changed get updated in the real DOM. This is called reconciliation.

**Step 6: Effects run**
After the DOM is updated, useEffect hooks with the changed dependencies run.

**Step 7: Cleanup**
If the component unmounts or effect dependencies change, cleanup functions run.

**Important points:**

- **setState is asynchronous** - You can't read the new state immediately after calling it

- **Updates are batched** - Multiple setStates in the same event handler are batched

- **Use functional updates** - When new state depends on old state:
  ```javascript
  setCount(prev => prev + 1); // Correct
  setCount(count + 1); // Can be wrong
  ```

This process is why React is fast - it batches updates, uses virtual DOM diffing, and only updates what changed in the real DOM."

---

### Q39: What are common mistakes beginners make with React hooks?

**How to Answer:**

"I've seen these mistakes a lot, and I've made some of them myself when learning:

**Mistake 1: Calling hooks conditionally**
```javascript
// Wrong
if (condition) {
  useState(0);
}

// Wrong
while (someCondition) {
  useEffect(() => {});
}

// Correct - hooks always at top level
const [count, setCount] = useState(0);
if (condition) {
  // use count here
}
```

Hooks must be called in the same order every render. React relies on call order to match state with the right component.

**Mistake 2: Missing dependencies**
```javascript
// Wrong
useEffect(() => {
  console.log(count);
}, []); // count is missing!

// Correct
useEffect(() => {
  console.log(count);
}, [count]);
```

ESLint will warn you about this. Always include what you use.

**Mistake 3: Modifying state directly**
```javascript
// Wrong
const [todos, setTodos] = useState([]);
todos.push(newTodo); // Mutation!

// Correct
setTodos([...todos, newTodo]);
```

State should be treated as immutable.

**Mistake 4: Using stale state in effects**
```javascript
// Wrong
useEffect(() => {
  setInterval(() => {
    setCount(count + 1); // count is stale
  }, 1000);
}, []);

// Correct
useEffect(() => {
  setInterval(() => {
    setCount(c => c + 1); // Use functional update
  }, 1000);
}, []);
```

**Mistake 5: Forgetting cleanup**
```javascript
// Wrong - creates memory leak
useEffect(() => {
  const interval = setInterval(() => {}, 1000);
}, []);

// Correct
useEffect(() => {
  const interval = setInterval(() => {}, 1000);
  return () => clearInterval(interval);
}, []);
```

**Mistake 6: Too many state variables**
```javascript
// Wrong - could be one object
const [name, setName] = useState('');
const [age, setAge] = useState(0);
const [email, setEmail] = useState('');

// Better
const [user, setUser] = useState({
  name: '',
  age: 0,
  email: ''
});
```

Though sometimes separate states are better for independence.

The key is understanding the rules of hooks and why they exist. Once you get it, these mistakes become obvious."

---

### Q40: How do you decide between Context, Redux, and prop drilling?

**How to Answer:**

"This is a really practical question that comes up a lot. Here's how I think about it:

**Use prop drilling (no tool) when:**
- You're passing props just 1-2 levels down
- The relationship between components is clear
- It's a small app or feature
- You want the simplest solution

```javascript
<Parent>
  <Child data={data} /> {/* Just one level, totally fine */}
</Parent>
```

**Use Context when:**
- Many components at different levels need the same data
- The data doesn't change very frequently
- You want something built into React without external libraries
- Examples: theme, language, authenticated user info

```javascript
<ThemeContext.Provider value={theme}>
  {/* Any child can access theme without prop drilling */}
</ThemeContext.Provider>
```

**Use Redux/Redux Toolkit when:**
- You have complex state with many actions
- Multiple parts of your app need to trigger the same changes
- You need powerful debugging (Redux DevTools)
- State updates are frequent and complex
- Examples: shopping cart, complex forms, real-time data

```javascript
// Multiple components can dispatch actions
dispatch(addToCart(item));
dispatch(removeFromCart(itemId));
dispatch(updateQuantity(itemId, quantity));
```

**My general approach:**

1. **Start simple** - Use local state and prop drilling
2. **If prop drilling gets annoying** (3+ levels) - Consider Context
3. **If Context causes performance issues** - Split into multiple contexts
4. **If you need complex logic** - Consider Redux Toolkit

**Real example:**

For a todo app:
- Simple version: Prop drilling (fine for a small app)
- Medium version: Context for todos (avoid drilling to deeply nested components)
- Complex version: Redux if you add user auth, filters, categories, sharing, etc.

Don't reach for Redux immediately. I've seen people use Redux for apps that could have been just useState in App.js. But also don't be afraid of Redux when your app actually needs it - it makes complex state much easier to manage.

The best solution is usually the simplest one that solves your actual problem."

---

## Final Tips for Interviews

### General Interview Strategy

**How to answer any React question:**

1. **Start with a clear, simple explanation** - Explain the concept in one or two sentences
2. **Give a code example** - Show, don't just tell
3. **Explain why it matters** - What problem does it solve?
4. **Mention gotchas or common mistakes** - Shows experience
5. **If relevant, mention alternatives** - Shows you understand tradeoffs

**Example:**
"useState is a hook that adds state to function components. [explanation] You call it like this... [code example] This solves the problem of managing component state in functions. [why] A common mistake is not using functional updates when the new state depends on the old state. [gotcha] For complex state, you might use useReducer instead. [alternative]"

**Practice speaking your answers:**
- Read this guide out loud
- Record yourself answering questions
- Practice with a friend
- Don't memorize word-for-word - understand the concepts

**During the interview:**
- Think before you speak
- It's okay to say "Let me think about that for a second"
- If you don't know something, be honest but show how you'd figure it out
- Ask clarifying questions if needed

**Remember:**
- Confidence comes from preparation
- You've already learned all this - now you're just organizing it
- Interviewers want you to succeed
- It's okay to make mistakes - show how you'd fix them

Good luck! You've got this! 