
# Blog Application

### Screenshots

The screenshots of the Kubernetes running state and the application running are included in the `screenshots` folder in the repository.

---

This project is a microservices-based blog platform where users can create blog posts and comment on posts. The application is divided into two microservices:
- **Post Service**: Manages the creation and retrieval of blog posts.
- **Comment Service**: Manages user comments on blog posts.

Both services are containerized using Docker, deployed on a Kubernetes cluster using **kind**, and use **Flask** as the backend framework and **SQLite** as the database.

---

## Table of Contents
- [Technologies](#technologies)
- [Microservices Architecture](#microservices-architecture)
- [Setup and Installation](#setup-and-installation)
- [API Endpoints](#api-endpoints)
- [Kubernetes Deployment](#kubernetes-deployment)
- [Testing](#testing)
- [Future Enhancements](#future-enhancements)

---

## Technologies

- **Backend**: Flask (Python)
- **Database**: SQLite
- **Containers**: Docker
- **Cluster**: Kubernetes (kind)

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

- Docker and kind installed on your machine.
- Kubernetes CLI (`kubectl`) installed.

### Clone the Repository

```bash
git clone <repository-url>
cd blog-app
```

### 1. Build and Run Post Service

```bash
cd post-service
docker build -t post-service .
docker run -d -p 5003:5003 post-service
```

### 2. Build and Run Comment Service

```bash
cd comment-service
docker build -t comment-service .
docker run -d -p 5004:5004 comment-service
```

---

## API Endpoints

### Post Service

| Method | Endpoint       | Description                |
|--------|----------------|----------------------------|
| `GET`  | `/posts`       | Retrieve all posts         |
| `POST` | `/posts`       | Create a new post          |
| `DELETE` | `/posts/<post_id>` | Delete a specific post |

**Example:**
- **Create a Post**:
  ```bash
  curl -X POST http://localhost:5003/posts -H "Content-Type: application/json" -d '{"title": "My First Post", "content": "This is a test post.", "user_id": 1}'
  ```

- **Delete a Post**:
  ```bash
  curl -X DELETE http://localhost:5003/posts/1
  ```

### Comment Service

| Method | Endpoint              | Description                        |
|--------|-----------------------|------------------------------------|
| `POST` | `/comments`           | Add a comment                      |
| `GET`  | `/comments/<post_id>` | Get all comments for a specific post |
| `DELETE` | `/comments/<comment_id>` | Delete a specific comment          |

**Example:**
- **Add a Comment**:
  ```bash
  curl -X POST http://localhost:5004/comments -H "Content-Type: application/json" -d '{"content": "Nice post!", "post_id": 1, "user_id": 1}'
  ```

- **Delete a Comment**:
  ```bash
  curl -X DELETE http://localhost:5004/comments/1
  ```

---

## Kubernetes Deployment

### 1. Create a Kind Cluster

```bash
kind create cluster
```

### 2. Load Docker Images into the Cluster

```bash
kind load docker-image post-service:latest
kind load docker-image comment-service:latest
```

### 3. Apply Kubernetes YAML Files

```bash
kubectl apply -f k8s/post-service.yaml
kubectl apply -f k8s/comment-service.yaml
```

### 4. Port Forward to Access Services

#### Port Forward Post Service

```bash
kubectl port-forward service/post-service 31716:80
```

Access Post Service at: `http://localhost:31716/posts`

#### Port Forward Comment Service

```bash
kubectl port-forward service/comment-service 30389:80
```

Access Comment Service at: `http://localhost:30389/comments`

---

## Testing

You can test the application using **curl** commands or **Postman** by hitting the API endpoints listed above.

1. **Create a Post**: Test creating posts using the `/posts` endpoint.
2. **Retrieve Posts**: Use the `/posts` endpoint to retrieve all posts.
3. **Add a Comment**: Add comments to the posts using the `/comments` endpoint.
4. **Delete Post/Comment**: Test deleting posts and comments using the DELETE endpoints.

---

## Future Enhancements

- **Authentication Service**: Add a user authentication service to manage user login and secure the endpoints.
- **Frontend**: Implement a frontend for easier interaction with the API using React or another frontend framework.
- **Notification Service**: Send email notifications when a comment is posted.

---

## Project Structure

```
├── post-service
│   ├── Dockerfile
│   ├── app.py
│   ├── post.db (generated after running the container)
│   └── requirements.txt
├── comment-service
│   ├── Dockerfile
│   ├── app.py
│   ├── comment.db (generated after running the container)
│   └── requirements.txt
├── k8s
│   ├── post-service.yaml
│   └── comment-service.yaml
├── Screenshots
```

---

## Contributing

Feel free to submit issues or pull requests for any bugs or improvements!
