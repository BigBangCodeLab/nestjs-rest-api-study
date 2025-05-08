# 📘 Learn REST API with NestJS & PostgreSQL

Welcome to this beginner-friendly guide for building a **REST API** using **NestJS** and **PostgreSQL**. This is for students who want to understand backend development step-by-step.

---

## 📌 What is an API?

**API** stands for **Application Programming Interface**.  
It allows two software systems to communicate with each other.

Example:  
If you use a food delivery app, the app talks to the server through an API to show your order status.

---

## 📌 What is a REST API?

**REST API** (Representational State Transfer) is a type of API that follows certain rules.  
It uses **HTTP methods** like:

- `GET` → to fetch data  
- `POST` → to send data  
- `PUT/PATCH` → to update data  
- `DELETE` → to remove data  

---

## ✅ What Can We Do with a REST API?

With a REST API, we can:

- Build websites or mobile apps that talk to a database
- Create login systems
- Fetch product lists, update user profiles, delete items
- And much more...

---

## 🔁 CRUD Operations with PostgreSQL

CRUD stands for:

- **C** → Create (Add new data)
- **R** → Read (Get data)
- **U** → Update (Change data)
- **D** → Delete (Remove data)

Here is how CRUD looks with a PostgreSQL database:

```
[ Client (frontend/app) ]
        |
        | HTTP Request (GET, POST, PUT, DELETE)
        v
[ NestJS REST API (Controller + Service) ]
        |
        | SQL Query
        v
[ PostgreSQL Database ]
```

Example:

| Method | Route        | Action             |
|--------|--------------|--------------------|
| GET    | /users       | Get all users      |
| POST   | /users       | Create a new user  |
| PUT    | /users/:id   | Update a user      |
| DELETE | /users/:id   | Delete a user      |

---

## 🛠️ Let's Build Our Own NestJS REST API (Step-by-Step)

### 1️⃣ Install Node.js

Download and install Node.js from: [https://nodejs.org](https://nodejs.org)  
Check version:  
```bash
node -v
npm -v
```

---

### 2️⃣ Install NestJS CLI

```bash
npm install -g @nestjs/cli
```

Check version:
```bash
nest --version
```

---

### 3️⃣ Create a New NestJS Project

```bash
nest new my-api
```

Choose `npm` or `yarn` when asked.

---

### 4️⃣ Add PostgreSQL Support

```bash
cd my-api
npm install @nestjs/typeorm typeorm pg
```

Then update `app.module.ts` to connect to PostgreSQL.

---

### 5️⃣ Create a Module for Users

```bash
nest generate module users
nest generate controller users
nest generate service users
```

---

### 6️⃣ Setup TypeORM Entity for Users

Create a `user.entity.ts` file with fields like name, email, etc.

---

### 7️⃣ Complete CRUD Functionality

In `users.service.ts` and `users.controller.ts`, write the logic to:

- Create User
- Get All Users
- Get User by ID
- Update User
- Delete User

---

### ✅ Run the API

```bash
npm run start:dev
```

Visit: [http://localhost:3000](http://localhost:3000)

---

## 🎓 For Students

- Clone this repo
- Run the above steps
- Try adding your own routes (e.g., /products, /orders)
- Learn by doing

---

## 🧠 Tips

- Use [Postman](https://www.postman.com/) or [Insomnia](https://insomnia.rest/) to test API requests.
- Always start simple. Then add features like authentication.

---

Happy Coding! 🚀
