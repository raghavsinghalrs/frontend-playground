# HTML & CSS

## Questions on semantic tags, CSS positioning, and the box model were common

# Closure and currying


curry function in JavaScript that transforms any function into its curried version:

```js
function curry(fn) {
  const arity = fn.length;

  function curried(...args) {
    if (args.length >= arity) {
      return fn.apply(this, args);
    } else {
      return function (...nextArgs) {
        return curried.apply(this, args.concat(nextArgs));
      };
    }
  }

  return curried;
}
```


