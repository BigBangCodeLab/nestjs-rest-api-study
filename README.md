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

## 🧠 Extra Knowledge for Students

### ✅ What is Node.js?

**Node.js** is a runtime environment that lets you run JavaScript outside the browser — mainly on servers.  
It helps you build **server-side applications**, like APIs or backends.

🧠 Think of Node.js as the engine that runs JavaScript on your computer like how a browser does, but without the browser.

---

### ✅ What is npm?

**npm** stands for **Node Package Manager**.  
It helps you **install and manage libraries** (also called packages) in your Node.js projects.

🛠 Example:  
You can run `npm install express` to add the Express.js framework to your project.

---

### ✅ What is a Framework?

A **framework** is a pre-built structure or toolkit for building software faster and in an organized way.  
It gives you **rules, patterns, and ready-made tools** so you don’t start from scratch every time.

🧱 Analogy:  
If programming is building a house, a framework is like a house-building kit with instructions and pre-made parts.

---

### ✅ What is NestJS?

**NestJS** is a **backend framework** built with and for **Node.js**.  
It uses **TypeScript** and helps you build **scalable, modular REST APIs** easily.

🌟 Why use NestJS?
- Clean and organized code
- Built-in support for dependency injection
- Uses decorators (like `@Get()`, `@Post()`) like Angular
- Works well with databases like PostgreSQL


---

## 🔄 What is Dependency Injection (DI) in NestJS?

In NestJS, **Dependency Injection (DI)** means you **don’t create objects manually** inside your class. Instead, **NestJS creates them for you** and gives them to you **when you need them**.

---

### 🔧 Think of NestJS Like a Factory with a Manager

- When your app starts, **NestJS's DI system acts like a manager**.
- This manager goes through all your modules and **creates one instance of each service, controller, etc.**
- These are stored **in a container (a kind of internal storage)**.

---

### 🧠 Then What Happens?

Whenever any class (like a Controller or another Service) **needs a service**, it **asks the DI manager**, like:

> “Hey, I need `UserService`!”

And the manager replies:

> “Here you go! I already have that instance ready. Use it.”

---

### ✅ Why is This Good?

- ✅ No duplicate objects — only one instance is created (singleton by default)
- ✅ Faster development — NestJS handles the object creation
- ✅ Clean code — no more `new SomeService()` inside your classes
- ✅ Easier testing — you can replace the real object with a fake one during testing

---

### 🔁 Example in NestJS

```ts
@Injectable()
export class UserService {
  findAll() {
    return ['John', 'Jane'];
  }
}
```

```ts
@Controller('users')
export class UserController {
  constructor(private userService: UserService) {} // DI manager gives this
}
```

- You didn’t write `new UserService()`
- NestJS created the instance when starting the app
- Then it **automatically gave** it to the controller

---

---

## 🏷️ What is a Decorator in TypeScript / NestJS?

A **decorator** is a special **function that adds extra behavior or information** to classes, methods, properties, or parameters.

In NestJS, decorators are used to **define routes, inject services, bind metadata, and control behavior** — all in a clean, readable way.

---

### 🧠 Think of It Like a Tag or Label

You place a **`@decorator`** above something (like a class or method), and that "tag" tells NestJS to treat it in a special way.

---

### 🔧 Common Decorators in NestJS:

| Decorator       | Use Case                                       |
|------------------|------------------------------------------------|
| `@Controller()`  | Marks a class as a controller (handles routes) |
| `@Get()`         | Maps a method to a GET HTTP request            |
| `@Post()`        | Maps a method to a POST HTTP request           |
| `@Injectable()`  | Marks a class as a service that can be injected |
| `@Param()`       | Gets a route parameter from the URL            |
| `@Body()`        | Gets the body of a POST request                |
| `@Query()`       | Gets query parameters from the URL             |

---

### 🔁 Example:

```ts
@Controller('users')
export class UserController {
  constructor(private userService: UserService) {}

  @Get()
  getUsers() {
    return this.userService.findAll();
  }

  @Post()
  createUser(@Body() userData: CreateUserDto) {
    return this.userService.create(userData);
  }
}
```

---


Quick, beginner-friendly explanations of key NestJS concepts for fast learners.

## Body
Data sent in the HTTP request's payload (e.g., JSON in POST). Use `@Body()` to access it.  
**Example**:  
```typescript
@Post() create(@Body() data: any) { return data; }
```

## Query
Key-value pairs in the URL after `?` (e.g., `?name=John`). Use `@Query()` to extract them.  
**Example**:  
```typescript
@Get() find(@Query('name') name: string) { return name; }
```

## Param
Dynamic URL path parts (e.g., `/users/:id`). Use `@Param()` to capture them.  
**Example**:  
```typescript
@Get(':id') getById(@Param('id') id: string) { return id; }
```

## Request
The full HTTP request object (headers, body, etc.). Use `@Req()`, but prefer specific decorators.  
**Example**:  
```typescript
@Get() getRequest(@Req() req) { return req.headers; }
```

## Response
The HTTP response object. Use `@Res()` for manual control, but NestJS handles it automatically.  
**Example**:  
```typescript
@Get() send(@Res() res) { res.status(200).send('Hello'); }
```

## Handlers
Controller methods handling HTTP requests. Use decorators like `@Get()`, `@Post()`.  
**Example**:  
```typescript
@Get('hello') getHello() { return 'Hello World'; }
```

## Status Code
Numeric code for response status (e.g., 200 OK, 404 Not Found). Override with `@HttpCode()`.  
**Example**:  
```typescript
@Post() @HttpCode(201) create() { return 'Created'; }
```

## DTO (Data Transfer Object)
TypeScript class defining data shape for validation. Use with `class-validator`.  
**Example**:  
```typescript
class CreateUserDto {
  @IsString() name: string;
  @IsInt() age: number;
}
@Post() create(@Body() dto: CreateUserDto) { return dto; }
```

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
