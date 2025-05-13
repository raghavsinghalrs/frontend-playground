# Props drilling

Passing data from parent to child then child 1 to child 2 and so on....

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
[Click Add Button]
        ↓
[Dispatch Action]
        ↓
[Reducer Function]
        ↓
[Modify Redux Store Slice]
        ↓
[Update React Component] ←── Subscribe(selector)
```
