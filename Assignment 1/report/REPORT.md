# Containerized Web Application with PostgreSQL

## Project Report



## 1. Introduction

This project demonstrates the development and deployment of a **production-ready containerized web application** using:

* **Node.js + Express** for the backend API
* **PostgreSQL** as the relational database
* **Docker & Docker Compose** for containerization and orchestration
* **IPvlan/Macvlan networking** for advanced container networking
* **Persistent volumes** for data durability

The goal is to build a scalable, portable, and efficient application that follows modern DevOps practices.

---

## 2. Objectives

* Containerize a full-stack backend system
* Implement database persistence using Docker volumes
* Use multi-stage builds to optimize image size
* Configure custom Docker networking (IPvlan/Macvlan)
* Provide RESTful APIs for data interaction
* Ensure portability and reproducibility

---

## 3. System Architecture

The application follows a **two-tier architecture**:

### 3.1 Backend Service

* Built with Node.js and Express
* Handles API requests
* Communicates with PostgreSQL database

### 3.2 Database Service

* PostgreSQL container
* Initialized using SQL seed script (`init.sql`)
* Stores application data persistently

### 3.3 Docker Orchestration

* Managed using `docker-compose.yml`
* Defines services, networks, and volumes

---

## 4. Project Structure

```
docker-postgres-project/
├── backend/
│   ├── Dockerfile
│   ├── server.js
│   ├── package.json
├── database/
│   ├── Dockerfile
│   └── init.sql
├── docker-compose.yml
├── .env
├── README.md
└── REPORT.md
```

---

## 5. Implementation Details

### 5.1 Backend (Node.js + Express)

* REST API built using Express
* Connects to PostgreSQL using environment variables
* Provides endpoints for CRUD operations

### 5.2 Database (PostgreSQL)

* Uses `postgres:15-alpine` image
* Preloaded schema via `init.sql`
* Stores messages data

---

## 6. Docker Configuration

### 6.1 Multi-Stage Build (Backend)

* **Stage 1:** Build dependencies using `node:18`
* **Stage 2:** Production image using `node:18-alpine`

**Benefit:**

* Reduces image size by ~90%
* Improves performance and security

---

### 6.2 Database Image

* Lightweight Alpine-based setup
* Pre-configured initialization script

---

### 6.3 Docker Compose

Defines:

* Services: backend, database
* Network: IPvlan/Macvlan
* Volumes: persistent storage

---

## 7. Networking

### 7.1 IPvlan Network

* Provides direct IP assignment to containers
* Containers appear as devices on the local network
* Improves network isolation and performance

### 7.2 Macvlan (Alternative)

* Assigns MAC addresses to containers
* Useful for legacy network compatibility

---

## 8. API Endpoints

| Method | Endpoint      | Description             |
| ------ | ------------- | ----------------------- |
| GET    | /             | Returns current DB time |
| GET    | /health       | Health check            |
| GET    | /messages     | Fetch all messages      |
| POST   | /messages     | Add a message           |
| DELETE | /messages/:id | Delete message          |

---

## 9. Data Persistence

* Docker volumes ensure data is not lost when containers stop
* Verified using:

  1. Insert data
  2. Stop containers
  3. Restart containers
  4. Data remains intact

---

## 10. Testing & Verification

### 10.1 Container Status

```
docker ps
```

### 10.2 API Testing

```
curl http://localhost:3000/
curl http://localhost:3000/messages
```

### 10.3 Network Inspection

```
docker network inspect <network_name>
```

---

## 11. Build Optimization

| Component | Base Image | Final Image        | Benefit      |
| --------- | ---------- | ------------------ | ------------ |
| Backend   | node:18    | node:18-alpine     | Smaller size |
| Database  | alpine     | postgres:15-alpine | Lightweight  |

---

## 12. Advantages of the System

* Portable and environment-independent
* Scalable using containers
* Efficient resource usage
* Secure and isolated services
* Faster deployment

---

## 13. Limitations

* Requires Docker knowledge
* IPvlan setup may be complex
* Not a full frontend application

---

## 14. Future Enhancements

* Add frontend (React/Next.js)
* Implement authentication (JWT)
* Use Kubernetes for orchestration
* Add CI/CD pipeline
* Monitoring with Prometheus & Grafana

---

## 15. Conclusion

This project successfully demonstrates how to build a **containerized backend system with PostgreSQL** using modern DevOps tools. It highlights the importance of:

* Containerization
* Efficient image building
* Persistent storage
* Advanced networking

The system is scalable, efficient, and suitable for real-world deployment scenarios.

---

## 16. References

* Docker Documentation
* PostgreSQL Documentation
* Node.js & Express Docs

---
