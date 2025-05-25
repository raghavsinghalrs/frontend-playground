# Virtual Dom

React uses a single Virtual DOM, but during updates, it creates two versions of the Virtual DOM:
- Previous Virtual DOM (before the update)
- New Virtual DOM (after the update)

```
function App() {
  return <span>Hello</span>;
}

ReactDOM.render(<App />, document.getElementById('root'));
```
🧱 What happens here:
- React reads your JSX (<span>Hello</span>) and builds a Virtual DOM representation of it — an object like:
```js
{
  type: 'span',
  props: { children: 'Hello' },
  ...
}
```
- This Virtual DOM is then used to create the real DOM, and React inserts the real <span>Hello</span> into #root.
- This Virtual DOM snapshot is saved internally by React as the "previous virtual DOM" for future updates.
🔄 Now you update the content:
Let’s say after 2 seconds, you change the content using state:

```js
function App() {
  const [text, setText] = React.useState('Hello');

  React.useEffect(() => {
    setTimeout(() => {
      setText('World');
    }, 2000);
  }, []);

  return <span>{text}</span>;
}
```
What happens now:
- When setText('World') runs, React re-renders the component.
- A new Virtual DOM is created:
```js
{
  type: 'span',
  props: { children: 'World' },
  ...
}
```
React now has:
- Old Virtual DOM: <span>Hello</span>
- New Virtual DOM: <span>World</span>
- React runs its diffing algorithm:
- It sees that only the text content has changed.
- React applies a minimal real DOM update:
- It doesn’t remove or replace the whole <span> — it just updates the text inside it.

## 🔧 Who creates the real DOM from the virtual DOM?
✅ React does it internally using its reconciliation engine.
1. You write JSX:
   ```js
     <span>Hello</span>
   ```
2. Babel transpiles it into:
   ```js
     React.createElement("span", null, "Hello");
   ```
3. React.createElement() produces a Virtual DOM object:
   ```js
   {
  type: 'span',
  props: {
    children: 'Hello'
  },
  ...
4. So the real DOM is created by: ✅ createRoot().render(<App />)


# use effect is the part of commit phase

```js
function MyComponent() {
  const [count, setCount] = useState(0);
  
  console.log("Rendering component...");

  useEffect(() => {
    console.log("Running useEffect...");
  }, []);

  return <div>Count: {count}</div>;
}
```

- First, the render happens ("Rendering component...")
- Then the DOM is updated with JSX (<div>Count: 0</div>)
- After that, the browser paints the UI
- Finally, useEffect runs ("Running useEffect...")

💡 Why is this useful?
This ensures that effects (like subscriptions, API calls, timers, DOM manipulation, etc.) don’t block rendering. Your app stays fast and responsive.


# Props drilling

Passing data from parent to child then child 1 to child 2 and so on....

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

# Controlled and Uncontrolled components 

There is not an exactly definition for this but if you are controlling a child component using parent component then parent component is known as a controlled component.

# Lifting the state up
For eg accordion if there are 4 accordion and you want when you try to expand anyone then other one which is already expanded should be close and the new one will only expand. For that we can use useState and pass the set function by parent component to the child component and whenever it will called by the index that only will be expand. (for more detailed video checkout the episode 11 data is the new oil)

# Redux

Redux store is like a big js object with a lot of data inside it and it has kept in a global central place. As like a js object when it will be a big full of data it can visible as a clumsy so redux store has slices like user data we can store in user slice, cart data we can store in cart slice

Suppose we want to make add to card functionality, let's see how to implement redux -
- When we click on add to cart button, it dispatch an action.
- And that action calls the function (This function is known as reducer).
- That function will modify the cart slice in redux store.
- This is all about the how to modify the cart.
- Now how to read the data using the selector.
- This is how we can modify the react component (selector will give data and we can rendor it)
- This is also known as subscribing to the store.

```js
[Click Add Button] -> [Dispatch Action] -> [Reducer Function] -> [Modify Redux Store Slice]
                                                                               ↓
                                      Modifies the react component  <-  Subscribe(selector)
```

Make sure you are subscribing to the items which you really want otherwise it can create hug performance loss

```js
//Here you are subscribing to all the stores
const store = useSelector((store) => store);
const items = store.cart.items;

//here you are accessing to the one which you really needed
const items = useSelector((store) => store.cart.items);
```
