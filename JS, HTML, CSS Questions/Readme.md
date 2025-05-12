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







