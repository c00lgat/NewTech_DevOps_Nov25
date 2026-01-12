# Docker Commands Quick Reference

## Essential Commands for Lab 1

### Building Images
```bash
# Build an image
docker build -t image-name:tag ./path

# Example
docker build -t my-web-app:1.0 ./app
```

### Running Containers
```bash
# Run a container
docker run [options] image-name

# Common options:
-d              # Run in detached mode (background)
-p host:container  # Map ports (e.g., -p 5000:5000)
--name name     # Give container a name
-it             # Interactive terminal

# Example
docker run -d -p 5000:5000 --name my-app my-web-app:1.0
```

### Managing Containers
```bash
docker ps              # List running containers
docker ps -a           # List all containers
docker stop <name>     # Stop a container
docker start <name>    # Start a stopped container
docker restart <name>  # Restart a container
docker rm <name>       # Remove a container (must be stopped)
docker logs <name>     # View container logs
docker exec -it <name> /bin/bash  # Execute command in container
```

### Managing Images
```bash
docker images          # List all images
docker rmi <image>     # Remove an image
docker tag <old> <new> # Tag an image
docker push <image>    # Push to registry
docker pull <image>    # Pull from registry
```

### Cleanup
```bash
docker system prune           # Remove unused data
docker system prune -a        # Remove all unused images
docker container prune        # Remove stopped containers
```

## Dockerfile Keywords
- `FROM` - Base image
- `WORKDIR` - Set working directory
- `COPY` - Copy files from host to container
- `RUN` - Execute commands during build
- `EXPOSE` - Document which port app uses
- `CMD` - Default command to run
- `ENV` - Set environment variables

## Common Issues & Solutions

| Problem | Solution |
|---------|----------|
| Port already in use | Use different host port: `-p 8080:5000` |
| Container won't start | Check logs: `docker logs <name>` |
| File not found | Verify COPY paths in Dockerfile |
| Permission denied | Ensure Docker Desktop is running |
| Can't connect to app | Check port mapping and firewall |
