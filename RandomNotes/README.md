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


#how react uses map function

(Becasue I was having a doubt like how it renders)

```js
<ul className="menu-list">
  {itemCards.map(card => <li key={card?.card?.info?.id}><span>{card?.card?.info?.name}</span></li>)}
</ul>
```

### How `.map()` works inside JSX

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


