# React Counter App

Create a new file `CounterApp.js` and add code:

```jsx
import React, { useState } from "react";

const CounterApp = () => {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(count + 1);
  };

  const decrement = () => {
    setCount(count - 1);
  };

  return (
    <div>
      <h1>Counter App</h1>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement}>Decrement</button>
    </div>
  );
};

export default CounterApp;
```

Now, we can use the CounterApp component in main `index.js`:

```jsx
import React from "react";
import ReactDOM from "react-dom";
import CounterApp from "./CounterApp";

ReactDOM.render(
  <React.StrictMode>
    <CounterApp />
  </React.StrictMode>,
  document.getElementById("root")
);
```
