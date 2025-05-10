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
# Controlled and Uncontrolled components 

There is not an exactly definition for this but if you are controlling a child component using parent component then parent component is known as a controlled component.

# Lifting the state up

For eg accordion if there are 4 accordion and you want when you try to expand anyone then other one which is already expanded should be close and the new one will only expand. For that we can use useState and pass the set function by parent component to the child component and whenever it will called by the index that only will be expand. (for more detailed video checkout the episode 11 data is the new oil)

