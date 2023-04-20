# React Hooks

## useState

> useState is a React Hook that lets you add a state variable to your component.

`const [state, setState] = useState(initialState)`

```js
import { useState } from 'react';

export default Counter() => {
    const [count, setCount] = useState(0)

    function handleClick() {
        setCount(ct => ct + 1)
    }

    return (
        <button onClick={handleClick}>
            You clicked {count} times.
        </button>
    )
}
```

---

## useReducer

> useReducer is a React Hook that lets you add a reducer to your component.

`const [state, dispatch] = useReducer(reducer, initialArg, init?)`

```js
import { useReducer } from "react";

/* write the reducer function outside to avoid re-creating the function each time when the component re-render. */

/*
    reducer should be a pure function, it has two parameters,
    state: the pervious state
    action: passed by dispatch()
    reducer returns the next state.
*/
function reducer(state, action) {

    // use switch to make the code more readable and organized.
    switch (action.type) {
        case 'incremented_age': {
        return {
            name: state.name,
            age: state.age + 1
        };
        }
        case 'changed_name': {
        return {
            name: action.nextName,
            age: state.age
        };
        }
    }
    throw Error('Unknown action: ' + action.type);
}

export default Form() => {
    const [state, dispatch] = useReducer(reducer, { name: 'CALI', age: 24 });

    /* the dispatch function pass an action(obj) to the reducer function, and itself has no return. */

    function handleButtonClick() {
        dispatch({ type: 'incremented_age'})
    }
    function handleInputChange(e) {
        dispatch({
            type: 'change_name',
            nextName: e.target.value
        })
    }
}

return (
    //...
)
```

---

## useRef

> useRef is a React Hook that lets you reference a value that’s not needed for rendering.

`const ref = useRef(initialValue)`

```js
import { useRef } from "react";

/*
    useRef usage:
*/

/* 1. Store a mutable value that does not cause a re-render when updated, also avoid recreating that ref contents */
//Click Counter
export default Counter() => {
    let ref = useRef(0);

    function handleClick() {
        ref.current = ref.current + 1;
        alert("You clicked " + ref.current + " times!");
    }

  return <button onClick={handleClick}>Click me!</button>;
}

/* 2. Access a DOM element directly. */
function MyComponent() {
    const inputRef = useRef(null);
}

function handleClick() {
    inputRef.current.focus();
}

//...
return <input ref={inputRef} />;
```

---

## useEffect

> useEffect is a React Hook that lets you synchronize a component with an external system.

`useEffect(setup, dependencies?)`

```js
import { useState, useEffect } from "react";
/* 
    useEffect has two parameters -->

    setup(optionally return a cleanup fn): 
    After every time that render the component with changed dependencies, React will run the setup function.
    React will first run the cleanup function (if provided) with the old values, and then run the setup function with the new values.

    dependencies: 
    The list of all reactive values referenced inside of the setup code.
    if not provide, effect will run every render;
    if empty array, effect will only run after the initial render;


    usage:
    1. connect the component to some external system(the network, some browser API, or a third-party library).
    2. Wrapping Effects in custom Hooks.
    3. Fetching data with Effects 
    4. Updating state based on previous state from an Effect 
*/

export default function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    const intervalId = setInterval(() => {
      setCount((c) => c + 1);
    }, 1000);
    return () => clearInterval(intervalId);
  }, []);
}
return <h1>{count}</h1>;
```

---

## useContext

> useContext is a React Hook that lets you read and subscribe to context from your component.

`const value = useContext(SomeContext)`

```js
import { createContext, useContext, useState } from "react";

/*
  create a context before using useContext, 
  it receives a value as default value for later if no value pass to provider
 */
const ThemeContext = createContext(null);

export default function MyApp() {
  const [theme, setTheme] = useState("light");
  return (
    // Provider provides value to its children, if no, use default value.
    <ThemeContext.Provider value={theme}>
      <Form />
      <label>//...</label>
    </ThemeContext.Provider>
  );
}

//...

function Panel({ title, children }) {
  // Child Component call useContext to receive values from the closest parent Provider.
  const theme = useContext(ThemeContext);
  //...
}

function Button({ children }) {
  const theme = useContext(ThemeContext);
  //...
}
```

---

## useCallback

> useCallback is a React Hook that lets you cache a function definition between re-renders.

`const cachedFn = useCallback(fn, dependencies)`

```js
import { useCallback } from "react";

/* 
    receive two parameters to useCallback:
    1. A function definition that you want to cache between re-renders.
    2. A list of dependencies including every value within your component that’s used inside your function.
*/

export default function ProductPage({ productId, referrer, theme }) {
  const handleSubmit = useCallback(
    (orderDetails) => {
      post("/product/" + productId + "/buy", {
        referrer,
        orderDetails,
      });
    },
    [productId, referrer]
  );
}
```

---

## useMemo

> useMemo is a React Hook that lets you cache the result of a calculation between re-renders.

`const cachedValue = useMemo(calculateValue, dependencies)`

```js
import { useMemo } from "react";
/*
  Two parameters: 
  1. A calculation function that takes no arguments, like () =>, and returns what you wanted to calculate.
  2. A list of dependencies including every value within your component that’s used inside your calculation.  
*/

function TodoList({ todos, tab }) {
  const visibleTodos = useMemo(() => filterTodos(todos, tab), [todos, tab]);
  // ...
}
```
