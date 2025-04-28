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

# Class based components

## 🚀 Why use super(props)

👉 In React, when you create a class component, you extend from React.Component.
This means your component is a child, and React.Component is the parent.

```js
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
  }
}
```

- constructor(props) is your component’s setup function.
- super(props) calls the parent’s constructor (React.Component's constructor).
- It gives your component access to this.props and other important React features.

## 🏁 Final Baby-Simple Summary:

- super(props) = telling React:
- "Hey parent, please do your setup! I need props and this."
- Without it = ❌ Error.
- With it = ✅ Everything works perfectly.

# 📌 ComponentDidMount Use Case for Class-Based Components

In class-based components, when a component initializes or mounts, the lifecycle steps happen in this order:

- First, constructor is called.
- Then, render method is called.
- After the component is placed into the DOM, the componentDidMount method is called.

```js
// ParentComponent.js
import React from "react";
import ChildComponent from "./ChildComponent";

class ParentComponent extends React.Component {
  constructor(props) {
    super(props);
    console.log("Parent Constructor Called");

    this.state = {
      message: "Welcome",
    };
  }

  componentDidMount() {
    console.log("Parent componentDidMount Called");
  }

  render() {
    console.log("Parent Render Called");

    return (
      <div>
        <h1>{this.state.message}</h1>

        {/* Using ChildComponent Twice with different props */}
        <ChildComponent name="first" />
        <ChildComponent name="second" />
      </div>
    );
  }
}

export default ParentComponent;
```

```js
// ChildComponent.js
import React from "react";

class ChildComponent extends React.Component {
  constructor(props) {
    super(props);
    console.log(this.props.name + " Constructor Called");
  }

  componentDidMount() {
    console.log(this.props.name + " componentDidMount Called");
  }

  render() {
    console.log("ChildComponent Rendered with name:", this.props.name);
    return <h2>Hello, {this.props.name}!</h2>;
  }
}

export default ChildComponent;
```
## 🛠 Lifecycle Steps Table

| Step | What Happens | Component |
|:---|:---|:---|
| 1 | Parent constructor | `ParentComponent` |
| 2 | Parent render starts | `ParentComponent` |
| 3 | First Child constructor | `ChildComponent ("first")` |
| 4 | First Child render | `ChildComponent ("first")` |
| 5 | Second Child constructor | `ChildComponent ("second")` |
| 6 | Second Child render | `ChildComponent ("second")` |
| 7 | Parent render finishes | `ParentComponent` |
| 8 | First Child componentDidMount | `ChildComponent ("first")` |
| 9 | Second Child componentDidMount | `ChildComponent ("second")` |
| 10 | Parent componentDidMount | `ParentComponent` |


## 🧠 Why this order?

Because DOM updates are expensive, React first prepares all components in memory (Virtual DOM) during the render phase.
Only after all renders are complete, React updates the real DOM and then calls componentDidMount() for each component.

This improves performance and gives a smooth user experience. 🚀

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
  
