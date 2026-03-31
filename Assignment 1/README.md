# Containerization and DevOps Lab
Student Details
Name: Akshay Kumar
SAP ID: 500120477
Batch: 3
## Project Overview

This project demonstrates the development and deployment of a containerized web application using Docker and Docker Compose.

The system consists of:

A Node.js backend API
A PostgreSQL database
Communication through Docker networks

The goal is to understand:

Containerization
Multi-container architecture
Networking between containers
Deployment using Docker Compose
## Architecture
User (Browser / curl)
        ↓
   Node.js Backend (Container)
        ↓
   PostgreSQL DB (Container)
Explanation:
User sends request → backend
Backend processes → interacts with DB
DB returns data → backend → user
## Network Design
Docker uses a bridge network (default)
Both containers are connected via Docker Compose network
Containers communicate using service names

Example:

backend → connects to → postgres_db:5432

- No need for IP addresses
- DNS-based communication inside Docker

## Tech Stack
Component	Technology
Backend	Node.js + Express
Database	PostgreSQL
Containerization	Docker
Orchestration	Docker Compose
Deployment	GitHub Pages (frontend docs)
## Tech Stack Comparison
Feature	Docker	Virtual Machine
Startup Time	Fast 	Slow 
Resource Usage	Low	High
Isolation	Process-level	Full OS
Portability	High	Medium
Use Case	Microservices	Full OS apps
## Prerequisites

Before starting, install:

Docker
Docker Compose
Git
Ubuntu (WSL recommended)

Check installation:

docker --version
docker-compose --version
## Step-by-Step Implementation
 Step 1: Create Project Structure
project/
│
├── backend/
├── db/
├── docker-compose.yml
 Step 2: Backend Setup
Create app.js
Add Express server
Add routes:
/users
/add
/health
 Step 3: Database Setup
Use PostgreSQL image
Set environment variables:
DB name
user
password
 Step 4: Dockerfile (Backend)
FROM node:18-alpine
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 3000
CMD ["node", "app.js"]
 Step 5: Docker Compose
version: '3.8'

services:
  postgres_db:
    image: postgres:15-alpine
    environment:
      POSTGRES_DB: mydb
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass

  backend_app:
    build: ./backend
    ports:
      - "3000:3000"
    depends_on:
      - postgres_db
 Step 6: Run Project
docker-compose up --build
 Step 7: Test
curl http://localhost:3000/health

Expected:

OK
## Image Size Optimization
Techniques used:
- Alpine base image (lightweight)
- Multi-stage build
- Remove unnecessary files
- Use .dockerignore
Benefits:
Smaller image size
Faster build
Faster deployment
## IPVLAN vs MACVLAN Comparison
Feature	IPVLAN	MACVLAN
MAC Address	Same as host	Unique per container
Performance	High	High
Isolation	Less	More
Use Case	Simple setups	Advanced networking
Complexity	Low	Medium
## Docker Compose Features Used
Multi-container setup
Service dependency (depends_on)
Port mapping
Environment variables
Automatic network creation
## API Endpoints
Get Users
GET /users
Add User
POST /add
Health Check
GET /health
## Testing Commands
curl http://localhost:3000/users
## Output Example
[
  {"id":1,"name":"Akshay"},
  {"id":2,"name":"Akshay"}
]
## GitHub Pages Deployment

Live URL:
 https://kumaxshay.github.io/Containerization_and_DevOps_Lab/

## Learning Outcomes
Docker fundamentals
Container networking
Multi-container orchestration
Backend-database integration
Deployment practices
## Conclusion

This project successfully demonstrates:

End-to-end containerized application deployment
Efficient use of Docker and Docker Compose
Real-world DevOps workflow

It highlights how containerization simplifies development, testing, and deployment across environments.

 Author

Akshay Kumar

 
