# 📘 REST API Learning Guide

## 🔹 What is REST?
REST (Representational State Transfer) ek **architectural style** hai jo web services banane ke liye use hota hai.  
REST API ek aisi API hoti hai jo **HTTP methods** (GET, POST, PUT, DELETE, etc.) use karke client aur server ke beech data exchange karti hai.

---

## 🔹 Key Principles of REST
1. **Stateless** → Har request independent hoti hai (server purani requests ko store nahi karta).  
2. **Client-Server** → Client (frontend) aur server (backend) alag hote hain.  
3. **Uniform Interface** → Endpoints ek standard follow karte hain.  
4. **Resource Based** → Har entity (user, product, post) ek resource hoti hai.  
5. **Representation** → Data JSON/XML ke format me exchange hota hai (mostly JSON).

---

## 🔹 Common HTTP Methods
| Method   | Use Case | Example |
|----------|----------|---------|
| **GET**    | Data fetch karna | `/users` → Get all users |
| **POST**   | Naya resource create karna | `/users` + JSON body |
| **PUT**    | Resource ko fully update karna | `/users/1` |
| **PATCH**  | Resource ko partially update karna | `/users/1` |
| **DELETE** | Resource delete karna | `/users/1` |

---

## 🔹 Example REST API (Users)
```
GET     /users        → Get all users
GET     /users/1      → Get user with id 1
POST    /users        → Create a new user
PUT     /users/1      → Update full user
PATCH   /users/1      → Update part of user
DELETE  /users/1      → Delete user
```

---

## 🔹 Status Codes
| Code | Meaning |
|------|----------|
| 200  | OK (Success) |
| 201  | Created |
| 400  | Bad Request |
| 401  | Unauthorized |
| 404  | Not Found |
| 500  | Internal Server Error |

---

## 🔹 Tools for Learning & Testing
- **Postman** → API testing tool  
- **Insomnia** → Alternative to Postman  
- **cURL** → Command line testing  
- **JSON Server** → Fake REST API for practice  

---

## 🔹 Practice Project Ideas
1. **Todo API** → Manage tasks  
2. **Blog API** → Posts + comments  
3. **E-commerce API** → Products, Orders, Users  
4. **Library API** → Books + Authors  

---

## 🔹 Learning Path
✅ Step 1 → HTTP basics seekho (request, response, status codes)  
✅ Step 2 → REST principles samjho  
✅ Step 3 → Dummy APIs ko Postman me test karo  
✅ Step 4 → Node.js + Express me REST API banao  
✅ Step 5 → Database (MongoDB / MySQL) integrate karo  
✅ Step 6 → Authentication & JWT implement karo  

---

## 🔹 Sample REST API (Node.js + Express)

```js
// index.js
const express = require("express");
const app = express();
app.use(express.json());

let users = [
  { id: 1, name: "Nikhil", email: "nikhil@example.com" },
  { id: 2, name: "Aman", email: "aman@example.com" }
];

// GET all users
app.get("/users", (req, res) => {
  res.json(users);
});

// GET single user
app.get("/users/:id", (req, res) => {
  const user = users.find(u => u.id === parseInt(req.params.id));
  user ? res.json(user) : res.status(404).send("User not found");
});

// POST create new user
app.post("/users", (req, res) => {
  const newUser = { id: users.length + 1, ...req.body };
  users.push(newUser);
  res.status(201).json(newUser);
});

// PUT update user
app.put("/users/:id", (req, res) => {
  const user = users.find(u => u.id === parseInt(req.params.id));
  if (!user) return res.status(404).send("User not found");
  user.name = req.body.name;
  user.email = req.body.email;
  res.json(user);
});

// DELETE user
app.delete("/users/:id", (req, res) => {
  users = users.filter(u => u.id !== parseInt(req.params.id));
  res.send("User deleted");
});

// Start server
app.listen(3000, () => {
  console.log("🚀 Server running on http://localhost:3000");
});
```

---

## 🔹 How to Run
```bash
# Step 1: Initialize project
npm init -y

# Step 2: Install Express
npm install express

# Step 3: Run server
node index.js
```

Now open 👉 [http://localhost:3000/users](http://localhost:3000/users)  
