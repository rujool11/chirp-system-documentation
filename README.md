# Chirp — Microservices-based Social Media Platform

![Go](https://img.shields.io/badge/Go-00ADD8?style=for-the-badge&logo=go&logoColor=white)
![Gin](https://img.shields.io/badge/Gin-4EB181?style=for-the-badge&logo=go&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![TailwindCSS](https://img.shields.io/badge/TailwindCSS-38B2AC?style=for-the-badge&logo=tailwindcss&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=jenkins&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)


## 📘 Overview

**Chirp** is a microservices-based modern social media application built stack.  
It is designed for scalability, modularity, and clean separation of concerns — with individual services for authentication, core social interactions, and reverse proxy API gateway that bridges the backend with the frontend.

Allows users to register, create posts, comment, like, follow other users and interact with others, while maintaining a flexible architecture that supports independent development and deployment of each component.

---

## ⚙️ Tech Stack

| Layer | Technology | Description |
|-------|-------------|-------------|
| **Frontend** | React, TypeScript, Vite, Tailwind CSS | User interface for the Chirp app |
| **Backend** | Go (Gin ) | REST APIs built as independent microservices |
| **Database** | PostgreSQL (NeonDB) | Neon serverless cloud-hosted relational database |
| **API Gateway** | Go (Gin Reverse Proxy) | Routes requests between frontend and backend so only single endpoint needs to be exposed to frontend |
| **CI/CD** | Jenkins, Docker, Kubernetes | Continuous integration and deployment pipelines on local minikube cluster |

---

## 🧩 Repositories

| Repository | Description |
|-------------|-------------|
| **chirp-auth-service** | Handles user authentication, registration, updation, and JWT-based authorization |
| **chirp-core-service** | Core features — posts, likes, comments, and follow |
| **chirp-api-gateway** | Reverse proxy that connects frontend and backend |
| **chirp-frontend** (wip) | React, TypeScript and Tailwind CSS frontend interface |
| **chirp-cicd** | CI/CD setup with Jenkins pipelines and k8s manifests |

---

## 🏗️ System Architecture

Chirp follows a **microservices-based architecture** built with a clear separation of concerns between frontend, gateway, backend services, and database.

### 🔹 Overview

- The frontend application sends API requests to a single **API Gateway**.  
- The **API Gateway** acts as a **reverse proxy**, routing requests to the appropriate backend microservice.  
- The backend consists of **chirp-auth-service** and **chirp-core-service**, each handling a distinct domain (authentication, core social features).  
- Using **Neon Serverless PostgreSQL (Cloud Database)** for persistent data storage, availability and scalability.
---

### Components

#### **API Gateway**
- Serves as a **reverse proxy** between the frontend and backend  
- Routes requests based on path prefixes:  
  - `/auth/{...}` → **Auth Service**  
  - `/core/{...}` → **Core Service**

#### **Auth Service**
- Responsible for **user registration**, **authentication**, and **JWT management**  
- Interacts primarily with the `users` table in the database

#### **Core Service**
- Manages core social features — posts, comments, likes, following. 
- Interacts with the following tables:
  - `posts`  
  - `comments`  
  - `post_likes`  
  - `comment_likes`  
  - `follow`

---

### 🔄 Request Flow

1. The **frontend** sends an API request to the **API Gateway**.  
2. The **gateway** forwards the request to the corresponding backend service (`auth` or `core`).  
3. The **service** interacts with the **Neon PostgreSQL** database as needed.  
4. The response flows back through the **gateway** to the **frontend**.

---

### 🗺️ Architecture Diagram

![Chirp System Architecture](figures/arch.png)

