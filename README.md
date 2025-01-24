# 🚀 My First Docker Application
---

## 📖 Overview

This project is a simple demonstration of creating and running a Dockerized Node.js application. The steps include creating a Dockerfile and docker-compose.yml, building a Docker image, and running the application using Docker Compose. This application responds with a JSON message "Docker is easy 🐳" when accessed via HTTP.

---

## 📑 Table of Contents
- [Prerequisites](#prerequisites) 🔑
- [Architecture](#Architecture)
- [Architecture ](#setup-and-installation) 🗺️
- [Docker Setup](#docker-setup) 🐳
- [Docker Compose Setup](#docker-compose-setup) 🌐
- [Accessing the Application](#accessing-the-application) 🌐
- [Cleaning Up Resources](#cleaning-up-resources) 🧹
- [Conclusion](#conclusion) ✅

---

## 🔑 Prerequisites
Before you start, ensure you have the following:
- An AWS account 🌍
- **Node.js** and **npm**
- **Docker** and **Docker Compose** installed for building and pushing Docker images
- Basic understanding of JavaScript and Docker 🧑‍💻

---

## 🗺️ Architecture

The application consists of two main components:

- **Node.js Application:** A simple Express server serving an API.
- **MySQL Database:** A containerized MySQL instance managed using Docker Compose.


### Workflow:

- The Node.js application runs inside a Docker container.
- The application connects to a MySQL database running in another container.
- Both containers are managed using Docker Compose.
    
## 🛠️ Setup & Installation

### 1⃣ Setup Node Project

1. Initialize a Node.js project:
   ```bash
   npm init -y
   ```
2. Install dependencies and start the project:
   ```bash
   npm install
   npm start
   ```
3. Create an `index.js` file with the following content:
   ```javascript
   const app = require('express')();

   app.get('/', (req, res) =>
       res.json({ message: 'Docker is easy 🐳' })
   );

   const port = process.env.PORT || 5000;

   app.listen(port, () => console.log(`app listening on http://localhost:${port}`));
   ```
    
## 🐳 Docker Setup

### 2⃣ Create a Dockerfile

Create a file named `Dockerfile` in your project directory:

```dockerfile
FROM node:12

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

ENV PORT=5000

EXPOSE 5000

CMD [ "npm", "start" ]
```

### 3⃣ Build and Run the Docker Image

1. Build the Docker image:
   ```bash
   docker build -t iambot/myfirstnodeapp:1.0 .
   ```
2. List Docker images:
   ```bash
   docker image ls
   ```
3. Run the Docker container:
   ```bash
   docker run -p 5000:8080 <imageid>
   ```
4. Check running containers:
   ```bash
   docker ps -a
   ```

The application will now be accessible at [http://localhost:5000](http://localhost:5000).
    
### 🌐 Docker Compose Setup

### 4⃣ Create a `docker-compose.yml`

Create a file named `docker-compose.yml` with the following content:

```yaml
version: '3'
services:
  web:
    build: .
    ports:
      - "3000:5000"
  db:
    image: "mysql"
    environment:
      MYSQL_ROOT_PASSWORD: password
    volumes:
      - db-data:/foo

volumes:
  db-data:
```

### 5⃣ Run the Application with Docker Compose

1. Start the services:
   ```bash
   docker compose up
   ```
2. Stop and remove the services:
   ```bash
   docker compose down
   ```
    
### 🛡️ Accessing the Application

- Access the Node.js application at: [http://localhost:3000](http://localhost:3000).
- The application responds with:
  ```json
  { "message": "Docker is easy 🐳" }
  ```
    
### 🚹 Cleaning Up Resources

To clean up all resources:

1. Stop and remove containers:
   ```bash
   docker compose down
   ```
2. Remove unused Docker images:
   ```bash
   docker image prune
   ```
---

## ✅ Conclusion

This project demonstrates how to containerize a simple Node.js application and manage it using Docker and Docker Compose. The setup ensures an isolated and portable development environment for your application.

---

## 👨‍🏫 Instructor

This project was guided by ***Navin reddy*** and ***Telusko***, who provided valuable mentorship throughout the process.
