# Deployment Guide for Task Manager

## Prerequisites

- Docker installed on your machine
- Docker Hub account
- Docker Swarm enabled

## Step 1: Build the Docker Image

```bash
# Build the image locally
docker build -t task-manager .

# Test the build locally
docker run -p 5000:5000 task-manager
```

## Step 2: GitHub Actions Deployment

The application is automatically built and deployed to GitHub Container Registry when code is pushed to the main branch.

The workflow:
1. Code is pushed to GitHub repository
2. GitHub Actions workflow builds the Docker image
3. The image is pushed to GitHub Container Registry using the personal access token stored as 'devops' secret
4. The image is tagged with both 'latest' and the commit SHA

No manual steps are required for this process, as authentication is handled by the personal access token configured as a repository secret named 'devops'.

## Step 3: Deploy with Docker Swarm

### Initialize Swarm (if not already done)
```bash
docker swarm init
```

### Deploy the Stack
```bash
# Set your Docker Hub username
export DOCKER_USERNAME=YOUR_USERNAME

# Deploy the stack
docker stack deploy -c docker-compose.yml task-manager
```

### Verify Deployment
```bash
# Check service status
docker service ls

# Check running containers
docker ps

# View service logs
docker service logs task-manager_task-manager
```

## Step 4: Scale the Application

```bash
# Scale to more replicas
docker service scale task-manager_task-manager=3
```

## Step 5: Update the Application

```bash
# Pull the latest image from GitHub Container Registry
docker pull ghcr.io/pulkit9897/task-manager:latest

# Update the service
docker service update --image ghcr.io/pulkit9897/task-manager:latest task-manager_task-manager
```

## Troubleshooting

### Check Service Status
```bash
docker service ps task-manager_task-manager
```

### View Service Logs
```bash
docker service logs task-manager_task-manager
```

### Common Issues

1. **Port Conflicts**
   - Ensure port 5000 is not in use by another service
   - Change the port mapping in docker-compose.yml if needed

2. **Volume Permissions**
   - Check if the task-data volume is properly created
   - Verify permissions on the host system

3. **Network Issues**
   - Ensure the swarm network is properly configured
   - Check if containers can communicate with each other

## Maintenance

### Backup Data
```bash
# Locate the volume
docker volume ls

# Create a backup
docker run --rm -v task-manager_task-data:/source -v $(pwd):/backup alpine tar czf /backup/task-data-backup.tar.gz -C /source .
```

### Restore Data
```bash
# Restore from backup
docker run --rm -v task-manager_task-data:/source -v $(pwd):/backup alpine sh -c "cd /source && tar xzf /backup/task-data-backup.tar.gz"
```

### Monitor Resources
```bash
# View resource usage
docker stats

# Check system-wide information
docker info
```