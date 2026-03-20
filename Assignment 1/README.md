# Containerized Web Application using Docker

## Overview
This project demonstrates containerization of a web application using Docker and Docker Compose. It consists of a Node.js backend and a PostgreSQL database.

## Technologies Used
- Node.js (Express)
- PostgreSQL
- Docker
- Docker Compose

## Features
- REST API (GET & POST)
- Database integration
- Persistent storage using Docker volumes
- Multi-stage Docker build

## Project Structure
- backend/ → Node.js application
- database/ → PostgreSQL Dockerfile
- docker-compose.yml → service orchestration

## How to Run
1. Navigate to project folder
2. Run:
   docker-compose up --build

## API Endpoints
- GET /users → Fetch all users
- POST /add → Add new user
- GET /health → Server status

## Output
Application runs on:
http://localhost:3000
