# Blog Application

This project is a simple microservices-based blog platform where users can create blog posts and comment on posts. The application is divided into two microservices:
- **Post Service**: Manages the creation and retrieval of blog posts.
- **Comment Service**: Manages user comments on blog posts.

Both services are containerized using Docker and use **Flask** as the backend framework and **SQLite** as the database.

---

## Table of Contents
- [Technologies](#technologies)
- [Microservices Architecture](#microservices-architecture)
- [Setup and Installation](#setup-and-installation)
- [API Endpoints](#api-endpoints)
- [Testing](#testing)
- [Future Enhancements](#future-enhancements)

---

## Technologies

- **Backend**: Flask (Python)
- **Database**: SQLite
- **Containers**: Docker
- **Tools**: curl (for API testing), Postman (optional)

---

## Microservices Architecture

### 1. Post Service
- Handles the creation and management of blog posts.
- Database: **SQLite** (`post.db`)

### 2. Comment Service
- Manages comments on blog posts.
- Database: **SQLite** (`comment.db`)

---

## Setup and Installation

### Prerequisites

- Docker installed on your machine.

### Clone the Repository

```bash
git clone <repository-url>
cd blog-app
