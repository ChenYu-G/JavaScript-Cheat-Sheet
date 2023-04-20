# ***JavaScript Cheat Sheet***

## **Array**

### To add/remove elements:  

> `push(...items)` – adds items to the end

> `pop()` – extracts an item from the end 

> `shift()` – extracts an item from the beginning

> `splice(pos, deleteCount, ...items)` – at index pos deletes deleteCount elements and inserts items.  
This method modifies the original array and returns the removed elements as a new array.

> `slice(start, end)` – creates a new array, copies elements from index start till end (not inclusive) into it.

> `concat(...items)` – returns a new array: copies all members of the current one and adds items to it. If any of items is an array, then its elements are taken.

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

