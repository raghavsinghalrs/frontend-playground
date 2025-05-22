# HTML & CSS

## Questions on semantic tags, CSS positioning, and the box model were common

# Closure and currying


curry function in JavaScript that transforms any function into its curried version:

```js
function curry(fn) {
    return function curried(...args) {
        if (args.length >= fn.length) {
            return fn(...args);
        } else {
            return function (...nextArgs) {
                return curried(...args, ...nextArgs);
            };
        }
    }
}

```
# Temporal API JavaScript Example

A Tech Co-Founder and Staff Software Engineer, recently shared an insightful LinkedIn post highlighting the upcoming Temporal API in JavaScript. This new API aims to address long-standing challenges developers face when working with dates and times.​

## 🚀 What’s Inside

A simple example that adds one month to a date using the `Temporal.PlainDate` class from the Temporal API.

### 📄 Example

```js
import { Temporal } from '@js-temporal/polyfill';

const date = Temporal.PlainDate.from('2025-04-26');
const newDate = date.add({ months: 1 });

console.log(newDate.toString()); // "2025-05-26"
```

# How `.map()` works inside JSX

(Becasue I was having a doubt like how it renders)

```js
<ul className="menu-list">
  {itemCards.map(card => <li key={card?.card?.info?.id}><span>{card?.card?.info?.name}</span></li>)}
</ul>
```

- `.map()` loops over every item in the array (`itemCard`).
- For each item, it **creates** a `<li>` element (but **does not render** it immediately).
- After `.map()` finishes **all iterations**, it produces an **array of `<li>` elements**.
- React then **renders the full array together** inside the `<ul>` at once.

---

**Important Notes:**
- React **does not** render after each item individually.
- It **waits** for `.map()` to complete creating the entire array.
- **Then** it renders everything together in one go. 🚀

This ensures better performance and smoother UI updates.



# Custom hook rerendering

- ✅ When the state variable updates inside your custom hook.
- ✅ React marks the component that uses the hook for re-render.
- ✅ During re-render, your component re-runs.
- ✅ Which means your custom hook is called again (because hooks are just part of the component render).

## 🔥 So it's like:

- State inside hook changes ➔ Component re-renders ➔ Hook runs again.
- It's not because of the hook itself, it's because the component re-renders that hook re-executes.

```js
[Inside Hook] setState() called 
        ↓
[React] Component re-render scheduled 
        ↓
[During re-render] Hook function called again
```
```js
function useJsonData() {
  const [data, setData] = useState({ name: "Raghav" });

  useEffect(() => {
    // maybe fetch data or update
    setTimeout(() => {
      setData({ name: "Bro" });
    }, 2000);
  }, []);

  return data;
}

function App() {
  const jsonData = useJsonData();

  console.log(jsonData);

  return <div>{jsonData.name}</div>;
}

```

## Important ⚡
- Hooks can't exist outside a component render — they live and breathe only because components render.
- When your component renders again, React restores the previous state properly inside the hook.


# JS Question (related to lexcial scope and shadowing)

```js
let a = 1;

function b() {
    console.log(a);
    a = 2;
}

b();
```

Important Concepts:
This code works without errors because:

- You are reading the value of a (console.log(a)) before you reassign it (a = 2;).
- There's no variable a declared inside the function b() (e.g., let a; inside b()), so JavaScript looks for a in the outer scope (lexical environment).

```js
let a = 1;

function b() {
    console.log(a); // ReferenceError
    let a = 2;
}

b();
```

Key Takeaways:
- Lexical scope still applies, but local declarations with let or const shadow outer ones.
- The shadowed variable exists in the TDZ until it's initialized.
- Accessing it before initialization throws a ReferenceError.
      
