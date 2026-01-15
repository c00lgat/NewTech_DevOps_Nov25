# Solution Dockerfile - Check this only after attempting the lab yourself!
# This is one possible solution - there are multiple correct ways to write a Dockerfile

# Use Python 3.9 slim image as base (smaller size)
FROM python:3.9-slim

# Set working directory inside the container
WORKDIR /app

# Copy requirements file first (for better Docker layer caching)
COPY app/requirements.txt .

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application files
COPY app/app.py .

# Expose port 5000 (this documents which port the app uses)
EXPOSE 5000

# Define the command to run the application
CMD ["python", "app.py"]

# Notes:
# - Using slim image reduces image size
# - Copying requirements.txt first allows Docker to cache the pip install step
# - Using --no-cache-dir reduces image size
# - EXPOSE documents the port but doesn't actually publish it (that's done with -p flag)
# - CMD uses array form which is preferred over shell form
