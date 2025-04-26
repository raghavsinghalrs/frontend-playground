# javascript-notes


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

