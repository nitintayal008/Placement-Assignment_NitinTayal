# Simple Server with Express

```js
const express = require("express");

// instance of Express
const app = express();

const posts = [
  { id: 1, title: "Post 1", body: "This is post 1" },
  { id: 2, title: "Post 2", body: "This is post 2" },
  // Add more posts here...
];

// "/post" endpoint
app.get("/post", (req, res) => {
  res.json(posts);
});

// Start the server
const port = 3000;
app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});
```
