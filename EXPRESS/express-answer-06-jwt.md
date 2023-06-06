# JWT Minor Project

```js
const express = require("express");
const bcrypt = require("bcrypt");
const jwt = require("jsonwebtoken");
const bodyParser = require("body-parser");

const app = express();
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());

const secretKey = "your-secret-key"; // Replace with a strong secret key in production

// Simulated user data
const users = [
  {
    id: 1,
    username: "user1",
    password: "asdd#0213192sadVw6",
  }, // password: password1
  {
    id: 2,
    username: "user2",
    password: "qZuM0Mx0x6tddgoj6pCZ8Oc.JfbrRlGyPa",
  }, // password: password2
];

// Signup/Register endpoint
app.post("/signup", (req, res) => {
  const { username, password } = req.body;

  // Check if the username already exists
  if (users.find((user) => user.username === username)) {
    return res.status(400).json({ message: "Username already exists" });
  }

  // Hash the password
  bcrypt.hash(password, 10, (err, hashedPassword) => {
    if (err) {
      return res.status(500).json({ message: "Error creating user" });
    }

    // Create a new user
    const newUser = {
      id: users.length + 1,
      username,
      password: hashedPassword,
    };
    users.push(newUser);

    res.status(201).json({ message: "User created successfully" });
  });
});

// Login endpoint
app.post("/login", (req, res) => {
  const { username, password } = req.body;

  // Find the user by username
  const user = users.find((user) => user.username === username);
  if (!user) {
    return res.status(401).json({ message: "Authentication failed" });
  }

  // Compare the provided password with the hashed password
  bcrypt.compare(password, user.password, (err, result) => {
    if (err || !result) {
      return res.status(401).json({ message: "Authentication failed" });
    }

    // Generate a JWT token
    const token = jwt.sign(
      { id: user.id, username: user.username },
      secretKey,
      { expiresIn: "1h" }
    );
    res.status(200).json({ message: "Authentication successful", token });
  });
});

// Protected route
app.get("/protected", (req, res) => {
  // Verify the JWT token
  const token = req.headers.authorization;
  if (!token) {
    return res.status(401).json({ message: "Authorization failed" });
  }

  jwt.verify(token, secretKey, (err, decoded) => {
    if (err) {
      return res.status(401).json({ message: "Authorization failed" });
    }

    // Authorization successful, return protected data
    res
      .status(200)
      .json({ message: "Authorization successful", data: decoded });
  });
});

// Start the server
const port = 3000;
app.listen(port, () => {
  console.log(`Server is listening on port ${port}`);
});
```
