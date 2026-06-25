# Dockerized Python Application

## Overview

This project demonstrates how to containerize a simple Python Flask application using Docker. The application is packaged into a Docker image using an optimized Dockerfile and can be executed consistently across different environments.

## Objective

* Create a simple Python Flask application.
* Write a Dockerfile from scratch.
* Build and run Docker images.
* Understand Docker image layers and caching.
* Optimize the Docker image size.

---

## Project Structure

```text
docker-python-app/
│── app.py
│── requirements.txt
│── Dockerfile
│── .dockerignore
└── README.md
```

---

## Technologies Used

* Python 3.12
* Flask
* Docker
* Docker Desktop
* Windows Subsystem for Linux (WSL)

---

## Prerequisites

Before running this project, ensure you have:

* Docker Desktop installed
* WSL 2 installed and configured
* Python (optional for local testing)

---

## Application

The application is a simple Flask web server that returns:

```text
Hello from Docker!
```

---

## Dockerfile

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY app.py .

EXPOSE 5000

CMD ["python", "app.py"]
```

---

## Build the Docker Image

Navigate to the project directory:

```bash
cd docker-python-app
```

Build the Docker image:

```bash
docker build -t python-docker-app .
```

---

## Verify the Image

```bash
docker images
```

Example output:

```text
REPOSITORY          TAG       IMAGE ID       SIZE
python-docker-app   latest    xxxxxxxxxxxx   170MB
```

---

## Run the Docker Container

```bash
docker run -p 5000:5000 python-docker-app
```

---

## Access the Application

Open your browser and visit:

```text
http://localhost:5000
```

Expected output:

```text
Hello from Docker!
```

---

## Docker Image Layers

The Docker image consists of the following layers:

1. FROM python:3.12-slim
2. WORKDIR /app
3. COPY requirements.txt .
4. RUN pip install --no-cache-dir -r requirements.txt
5. COPY app.py .
6. EXPOSE 5000
7. CMD ["python", "app.py"]

Each instruction creates a separate image layer.

---

## Docker Layer Caching

Docker caches each layer to speed up future builds.

If only `app.py` changes:

* Cached:

  * FROM
  * WORKDIR
  * COPY requirements.txt
  * RUN pip install

* Rebuilt:

  * COPY app.py
  * CMD

This reduces build time because dependencies are not reinstalled.

---

## Image Optimization

The Docker image is optimized by:

* Using the lightweight `python:3.12-slim` base image.
* Installing packages with `--no-cache-dir`.
* Copying `requirements.txt` before application files to maximize cache reuse.
* Using a `.dockerignore` file to exclude unnecessary files.
* Copying only the required application files.

---

## Commands Used

Build Image

```bash
docker build -t python-docker-app .
```

Run Container

```bash
docker run -p 5000:5000 python-docker-app
```

View Images

```bash
docker images
```

View Running Containers

```bash
docker ps
```

Stop Container

```bash
docker stop <container_id>
```

Remove Container

```bash
docker rm <container_id>
```

Remove Image

```bash
docker rmi python-docker-app
```

---

## Output

* Docker image built successfully.
* Flask application runs inside a Docker container.
* Application is accessible at `http://localhost:5000`.
* Docker layer caching verified.
* Docker image optimized using best practices.

---

## Conclusion

This project demonstrates the complete workflow of Dockerizing a Python Flask application. It covers image creation, container execution, layer caching, and image optimization, providing a portable and efficient deployment solution.
