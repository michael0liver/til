# Convert ISO 8601 timestamps to formatted string

I wanted to convert an ISO 8601 timestamp string like this `2019-09-07T15:50-04:00` into something more human readable like `'7 September 2019'`.

// [https://dockyard.com/blog/2020/02/14/you-probably-don-t-need-moment-js-anymore](https://dockyard.com/blog/2020/02/14/you-probably-don-t-need-moment-js-anymore)

```js
const date = new Date("2019-09-07T15:50-04:00");
const formattedDate = date.toLocaleDateString("en-gb", {
  year: "numeric",
  month: "long",
  day: "numeric",
});
```

## References

- [MDN Web Docs on `Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)
- [Blog Post "You Probably Don't Need Moment.js Anymore"](https://dockyard.com/blog/2020/02/14/you-probably-don-t-need-moment-js-anymore)
