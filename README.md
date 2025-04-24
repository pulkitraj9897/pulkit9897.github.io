# Task Manager Application

A containerized Flask-based Task Manager application with a modern Bootstrap UI, Docker Swarm deployment support, and SQLite database for task persistence.

## Features

- Create, update, and delete tasks
- Change task status (Pending, In Progress, Completed)
- Modern and responsive UI with Bootstrap 5
- Containerized application with Docker
- Scalable deployment with Docker Swarm

## Local Development Setup

1. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

2. Run the application:
   ```bash
   python app.py
   ```

3. Access the application at `http://localhost:5000`

## Docker Deployment

### Build and Run Locally

1. Build the Docker image:
   ```bash
   docker build -t task-manager .
   ```

2. Run the container:
   ```bash
   docker run -p 5000:5000 task-manager
   ```

### Deploy to Docker Hub

1. Login to Docker Hub:
   ```bash
   docker login
   ```

2. Tag your image:
   ```bash
   docker tag task-manager YOUR_DOCKERHUB_USERNAME/task-manager:latest
   ```

3. Push to Docker Hub:
   ```bash
   docker push YOUR_DOCKERHUB_USERNAME/task-manager:latest
   ```

### Deploy with Docker Swarm

1. Initialize Docker Swarm:
   ```bash
   docker swarm init
   ```

2. Set your Docker Hub username:
   ```bash
   export DOCKER_USERNAME=YOUR_DOCKERHUB_USERNAME
   ```

3. Deploy the stack:
   ```bash
   docker stack deploy -c docker-compose.yml task-manager
   ```

4. Check the service status:
   ```bash
   docker service ls
   ```

### Pull and Run from Docker Hub

```bash
docker pull YOUR_DOCKERHUB_USERNAME/task-manager:latest
docker run -p 5000:5000 YOUR_DOCKERHUB_USERNAME/task-manager:latest
```

## Architecture

- Frontend: HTML5, Bootstrap 5, JavaScript
- Backend: Flask, SQLAlchemy
- Database: SQLite
- Container: Docker
- Orchestration: Docker Swarm

## Notes

- The application uses SQLite for data persistence
- Data is stored in a Docker volume for persistence across container restarts
- The application is configured to run 2 replicas in Swarm mode
- Health checks and automatic restarts are configured in Swarm mode