<<<<<<< HEAD
# Project6
=======
# Ecommerce Application (Spring Boot + React)

This is a full-stack ecommerce project developed using:

- Backend: Java Spring Boot (REST API)
- Frontend: React (Vite)
- Database: MySQL
- Build Tool: Maven
- Deployment: Render (Backend), Vercel (Frontend)
##  Features
- Add new item (POST API)
- Get all items
- Get item by ID
- Update item
- Delete item
- Frontend UI with API integration
##  Backend Setup (Spring Boot)

### 1 Prerequisites
- Java 17+
- Maven
- MySQL
- Git

### 2️ Clone Repository

```bash
git clone https://github.com/navya23-git/ecommerce.git
cd ecommerce
##
For deployement purpose i have used avien 
spring.datasource.url=jdbc:mysql://mysql-1696794b-somanavya6633-2779.c.aivencloud.com:17846/ministoredb  
spring.datasource.username=avnadmin
spring.datasource.password=AVNS_45KeC_bjywbTiMbiCsX
render must be running state it will work oterwise it wont work
Run Backend :mvn spring-boot:run
http://localhost:8080

Backend APIs
Add New Item
POST:
/api/items
Body (JSON):

{
  "name": "Mobile",
  "Description":"smart watch",
  "price": 15000,
  "category": "Electronics"
}
Get Item By ID
GET:
/api/items/{id}
Example:/api/items/1

Get All Items
GET:
/api/items
Frontend Setup (React + Vite)
Go to Frontend Folder
cd Frontend
Install Dependencies
npm install
Run Frontend
npm run dev
http://localhost:5173

import axios from "axios";

const API_URL = "http://localhost:8080/api/items";

export const getAllItems = async () => {
  const res = await axios.get(`${API_URL}/all`);
  return res.data;
};

export const addItem = async (item) => {
  const res = await axios.post(`${API_URL}/add`, item);
  return res.data;
};

export const deleteItem = async (id) => {
  const res = await axios.delete(`${API_URL}/${id}`);
  return res.data;
};

export const updateItem = async (id, item) => {
  const res = await axios.put(`${API_URL}/${id}`, item);
  return res.data;
};

// ✅ Add this function for SearchItem
export const getItemById = async (id) => {
  const res = await axios.get(`${API_URL}/${id}`);
  return res.data;
};

Backend Deployement Process 
Prerequisites
Local Machine
Java 21
Maven 3.9+
Docker Desktop
Git
Accounts
Render.com
Aiven.io
GitHub

2️⃣ Spring Boot Project Configuration
application.properties
server.port=${PORT:8081}

spring.datasource.url=jdbc:mysql://<AIVEN_HOST>:<PORT>/<DB_NAME>?ssl-mode=REQUIRED
spring.datasource.username=<AIVEN_USERNAME>
spring.datasource.password=<AIVEN_PASSWORD>

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

⚠️ Why ${PORT} is mandatory?
Render injects the port dynamically. Hardcoding causes crashes.

3️⃣ Dockerfile (Java 21 – Multi-Stage Build)
📄 Dockerfile (project root)
# ===============================
# 1️⃣ BUILD STAGE (Maven + Java 21)
# ===============================
FROM maven:3.9.9-eclipse-temurin-21 AS build
WORKDIR /app

COPY pom.xml .
RUN mvn dependency:go-offline

COPY src ./src
RUN mvn clean package -DskipTests


# ===============================
# 2️⃣ RUNTIME STAGE (Java 21 JRE)
# ===============================
FROM eclipse-temurin:21-jre
WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

EXPOSE 8081
ENTRYPOINT ["java", "-jar", "app.jar"]


4️⃣ Local Docker Testing
docker build -t myapp .
docker run -p 8081:8081 myapp

Test:
http://localhost:8081

✔ Confirms Docker + Java 21 setup

5️⃣ Push to GitHub
git add .
git commit -m "Dockerized Spring Boot Java 21 app"
git push origin main


6️⃣ Aiven Database Setup
Create MySQL/PostgreSQL service
Copy credentials
SSL enabled by default
Use JDBC with ssl-mode=REQUIRED
>>>>>>> 832e522 (backend frontend added)
