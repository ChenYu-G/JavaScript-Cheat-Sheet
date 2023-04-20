collected from javascript.info, MDN, and react.dev

# ***JavaScript Cheat Sheet***

## **Array**

### To add/remove elements:  

> `push(...items)` – adds items to the end

> `pop()` – extracts an item from the end 

> `shift()` – extracts an item from the beginning

> `splice(pos, deleteCount, ...items)` – at index pos deletes deleteCount elements and inserts items.  
This method modifies the original array and returns the removed elements as a new array.

> `slice(start, end)` – creates a new array, copies elements from index start till end (not inclusive) into it.

> `concat(...items)` – returns a new arraay: copies all members of the current one and adds items to it. If any of items is an array, then its elements are taken.

--- 

### To search among elements:

> `indexOf/lastIndexOf(item [, pos]))` – look for item starting from position pos, return the index or -1 if not found.

> `includes(value)` – returns true if the array has value, otherwise false.

> `find/filter(func)` – filter elements through the function, return first/all values that make it return true. 

> `findIndex(func)` is like find, but returns the index instead of a value.

---

### To iterate over elements:

> `forEach(func)` – calls func for every element, does not return anything.

> `map(func)` – creates a new array from results of calling func for every element.

> `sort(compareFunc)` – sorts the array in-place, then returns it.  
> \> 0	sort a after b; < 0	sort a before b; === 0	keep original order of a and b.

> `reverse()` – reverses the array in-place, then returns it.

> `split/join(pattern)` – convert a string to array and back, return that array or string.

> `reduce/reduceRight(func [, initial])` – calculate a single value over the array by calling func for each element and passing an intermediate result between the calls.

> `Array.from(arrayLike, mapFn)`  - takes an iterable or array-like value and makes a “real” Array from it. 

---

### Destructuring

> `let [item1 = default, item2, ...rest] = array`

---

### Additionally:

> Methods **sort, reverse** and **splice** modify the array itself.

> `Array.isArray(value)` checks value for being an array, if so returns true, otherwise false.

> `arr.some(fn)/arr.every(fn)` check the array.  
The function fn is called on each element of the array similar to map. If any/all results are true, returns true, otherwise false. These methods behave sort of like || and && operators: Stop iterating when there is a true or false.

> `arr.fill(value, start, end)` – fills the array with repeating value from index start to end.

> `arr.copyWithin(target, start, end)` – copies its elements from position start till position end into itself, at position target (overwrites existing).

> `arr.flat(depth)/arr.flatMap(fn)` create a new flat array from a multidimensional array.

---

## **Map/weakMap and Set/WeakSet**

### Map/weakMap

> `new Map()` – creates the map.

> `map.set(key, value)` – stores the value by the key.

> `map.get(key)` – returns the value by the key, undefined if key doesn’t exist in map.

> `map.has(key)` – returns true if the key exists, false otherwise.

> `map.delete(key)` – removes the element (the key/value pair) by the key.

> `map.clear()` – removes everything from the map.

> `map.size` – returns the current element count.

> `map.keys()` – returns an iterable for keys,

> `map.values()` – returns an iterable for values,

> `map.entries()` – returns an iterable for entries [key, value], it’s used by default in for..of.

---

> `weakMap.set(key, value)`

> `weakMap.get(key)`

> `weakMap.delete(key)`

> `weakMap.has(key)`

---

### Set/WeakSet

> `new Set([iterable])` – creates the set, and if an iterable object is provided (usually an array), copies values from it into the set.

> `set.add(value)` – adds a value, returns the set itself.
 
> `set.delete(value)` – removes the value, returns true if value existed at the moment of the call, otherwise false.

> `set.has(value)` – returns true if the value exists in the set, otherwise false.

> `set.clear()` – removes everything from the set.

> `set.size` – is the elements count.

> `set.keys()` – returns an iterable object for values.

> `set.values()` – same as set.keys(), for compatibility with Map.

> `set.entries()` – returns an iterable object for entries [value, value], exists for compatibility with Map.

---

> `WeakSet.add(value)`

> `WeakSet.has(value)`

> `WeakSet.delete(value)`

---

## **Object**

> `Object.keys(obj)` – returns an array of keys.

> `Object.values(obj)` – returns an array of values.

> `Object.entries(obj)` – returns an array of [key, value] pairs.

> `structuredClone(value [, options])` - creates a deep clone of a given value using the structured clone algorithm.

> `Object.assign(dest, src1, ..., srcN)` – copies properties from src1..N into dest(Shallow Clone, no nested objects).

> `JSON.parse(JSON.stringify(obj))` - (Shallow Clone with data loss)

### Destructuring

> `let {prop : varName = default, ...rest} = object` - (Shallow Clone, no nested objects)

---

### Property flags

> `Object.getOwnPropertyDescriptor(obj, propertyName)` - querys the full information about a prperty.

> `Object.getOwnPropertyDescriptors(obj)` - returns an object containging all property descriptors of `obj`.

> `Object.defineProperty(obj, propertyName, descriptor)` - If the property exists, defineProperty updates its flags. Otherwise, it creates the property with the given value and flags.

> `Object.defineProperties(obj, { prop1: descriptor1, prop2: descriptor2 // ... })` - defines many properties at once.

---

### Prototype 

> `Object.getPrototypeOf(obj)` – returns the `[[Prototype]]` of `obj`.

> `Object.setPrototypeOf(obj, proto)` – sets the `[[Prototype]]` of `obj` to `proto`.

> `Object.create(proto [, propertiesObject])` -  creates a new object, using an existing object as the prototype of the newly created object.  
> `let clone = Object.create(Object.getPrototypeOf(obj), Object.getOwnPropertyDescriptors(obj))` - clones an object(Shallow Clone).

---

## Function

> `let func = function f() {/* */}` - Named Function Expression   
It allows the function to reference itself internally.  
It is not visible outside of the function.

> `let func = new Function ([arg1, arg2, ...argN], functionBody)` //`let sum = new Function('a', 'b', 'return a + b')`

### Decorators and forwarding, call/apply

> `func.call(context, arg1, arg2, ...)` - runs func providing the first argument as this, and the next as the arguments.

> `func.apply(context, args)` - like call but uses an array-like object `args` as the list of arguments.

> `func.call(context, ...args)`  
`func.apply(context, args)`   
these two calls are almost equivalent

---

### Function binding

> `let boundFunc = func.bind(context)` - is a special function-like “exotic object”, that is callable as function and transparently passes the call to `func` setting `this=context`.

> `let bound = func.bind(context, [arg1], [arg2], ...)` - binds context as this and starting arguments of the function.

---

### Scheduling: setTimeout and setInterval

> `let timerId = setTimeout(func|code, [delay], [arg1], [arg2], ...)` - runs a function once after the interval of time.

> `let timerId = setInterval(func|code, [delay], [arg1], [arg2], ...)` - runs a function repeatedly, starting after the interval of time, then repeating continuously at that interval.

> `clearInterval(timerId)` stops the further calls.

---

## Promise 

> `Promise.all(promises)` – waits for all promises to resolve and returns an array of their results. If any of the given promises rejects, it becomes the error of Promise.all, and all other results are ignored.

> `Promise.allSettled(promises)` – waits for all promises to settle and returns their results as an array of objects with:
status: "fulfilled" or "rejected"
value (if fulfilled) or reason (if rejected).

> `Promise.race(promises)` – waits for the first promise to settle, and its result/error becomes the outcome.

> `Promise.any(promises)` (recently added method) – waits for the first promise to fulfill, and its result becomes the outcome. If all of the given promises are rejected, AggregateError becomes the error of Promise.any.

> `Promise.resolve(value)` – makes a resolved promise with the given value.  
`Promise.reject(error)` – makes a rejected promise with the given error.

---

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

