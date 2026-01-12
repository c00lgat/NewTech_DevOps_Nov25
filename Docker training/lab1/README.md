# Docker Lab 1: Containerize a Simple Web Application

## Learning Objectives
By the end of this lab, you will be able to:
- Understand the difference between Docker images and containers
- Write a basic Dockerfile
- Build a Docker image
- Run a containerized application
- Use basic Docker commands
- Push an image to Docker Hub (optional)


## Lab Overview
You have been given a simple Python Flask web application. Your task is to containerize it using Docker so it can run in any environment.

## The Application
This is a simple "Hello World" web application that:
- Runs on port 5000
- Displays a welcome message
- Shows the current time
- Has a simple API endpoint

## Lab Tasks

### Task 1: Explore the Application
1. Navigate to the `app` directory
2. Review the application code (`app.py`)
3. Check the `requirements.txt` file to see dependencies
4. Try running the app locally (optional - not required for Docker lab):
   ```bash
   # Make sure you're in your virtual environment, then:
   pip install -r requirements.txt
   python app.py
   ```
   Visit `http://localhost:5000` in your browser
   
   **Note:** If you get a "ModuleNotFoundError", make sure:
   - Your virtual environment is activated
   - You've run `pip install -r requirements.txt`
   - You're using the correct Python interpreter from your venv
   
   **Remember:** This step is optional! The main goal is to containerize the app with Docker, so you can skip local testing if you prefer.

### Task 2: Create a Dockerfile
1. Create a file named `Dockerfile` in the `app` directory
2. Your Dockerfile should:
   - Use a Python base image (suggested: `python:3.9-slim`)
   - Set a working directory
   - Copy the application files
   - Install dependencies from `requirements.txt`
   - Expose port 5000
   - Define the command to run the application

**Hints:**
- Use `FROM` to specify the base image
- Use `WORKDIR` to set the working directory
- Use `COPY` to copy files
- Use `RUN` to execute commands (like installing dependencies)
- Use `EXPOSE` to document which port the app uses
- Use `CMD` to define the default command

### Task 3: Build the Docker Image
1. Build your Docker image with a tag (e.g., `my-web-app:1.0`)
   ```bash
   docker build -t my-web-app:1.0 ./app
   ```
2. Verify the image was created:
   ```bash
   docker images
   ```

### Task 4: Run the Container
1. Run your containerized application:
   ```bash
   docker run -d -p 5000:5000 --name my-web-app my-web-app:1.0
   ```
2. Visit `http://localhost:5000` in your browser to verify it works
3. Test the API endpoint: `http://localhost:5000/api/time`

### Task 5: Explore Docker Commands
Try these commands and understand what they do:
- `docker ps` - List running containers
- `docker ps -a` - List all containers (including stopped)
- `docker logs my-web-app` - View container logs
- `docker stop my-web-app` - Stop the container
- `docker start my-web-app` - Start the container again
- `docker rm my-web-app` - Remove the container (must be stopped first)
- `docker exec -it my-web-app /bin/bash` - Execute a command in the container

### Task 6: Clean Up
1. Stop and remove your container
2. Remove your image (optional):
   ```bash
   docker rmi my-web-app:1.0
   ```

### Task 7: Push to Docker Hub (Optional)
1. Tag your image with your Docker Hub username:
   ```bash
   docker tag my-web-app:1.0 your-username/my-web-app:1.0
   ```
2. Log in to Docker Hub:
   ```bash
   docker login
   ```
3. Push your image:
   ```bash
   docker push your-username/my-web-app:1.0
   ```

## Troubleshooting
- **Port already in use**: 
  - **Option 1**: Change the host port (e.g., `-p 8080:5000`)
  - **Option 2**: Find and kill the process using port 5000:
    ```bash
    # Find the process
    lsof -i :5000
    
    # Kill the process (replace PID with the number from lsof output)
    kill -9 <PID>
    
    # Or kill all processes on port 5000 in one command
    lsof -ti :5000 | xargs kill -9
    ```
    **Note**: On macOS, port 5000 is often used by AirPlay. You can disable it in System Settings > General > AirDrop & Handoff > AirPlay Receiver (turn it off).

- **Container won't start**: Check logs with `docker logs my-web-app`
- **Can't find files**: Verify your Dockerfile COPY paths are correct
- **Permission errors**: Make sure Docker Desktop is running

## Key Concepts to Remember
- **Image**: A read-only template used to create containers
- **Container**: A running instance of an image
- **Dockerfile**: Instructions for building an image
- **Port Mapping**: `-p host_port:container_port` maps host ports to container ports

## Next Steps
After completing this lab, you should understand:
- How to containerize a simple application
- Basic Docker commands
- The relationship between images and containers

## Solution
A sample Dockerfile solution is provided in `Dockerfile.solution` (check this only after attempting the lab yourself!)
