# Destructuring Assignment

[ESLint](https://eslint.org) was complaining about unused variables in some of my React components where I had used the [`useState`](https://reactjs.org/docs/hooks-state.html) hook but had only consumed one of the values.

```javascript
import React, { useState } from "react";

const TestComponent = () => {
  const [thing, setThing] = useState(); // < ======= eslint complains that `setThing` is not being used.

  return <>{thing}</>;
};

export default TestComponent;
```

You can ignore unused values like this `const [thing] = useState();` or `const [,setThing] = useState();`. This is called [Destructuring Assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment). It can even be used for objects!
