# Dockerfile Instructions Overview

A Dockerfile is a text file that contains a set of instructions to automate the process of building a Docker image. Each instruction in the Dockerfile corresponds to a specific command that is executed during the build process to set up the environment inside the container.

## Common Dockerfile Instructions

### 1. `FROM`
- Specifies the base image to build your Docker image.
- **Example:**
  ```dockerfile
  FROM python:3.8-slim
  ```
  This means the Docker image will be built starting from the official `python:3.8-slim` image.

---

### 2. `LABEL`
- Adds metadata to the image, such as the version or maintainer information.
- **Example:**
  ```dockerfile
  LABEL maintainer="yourname@example.com"
  LABEL version="1.0"
  ```

---

### 3. `RUN`
- Executes commands inside the container at build time. These can be used to install dependencies, set up the environment, or perform other setup tasks.
- **Example:**
  ```dockerfile
  RUN apt-get update && apt-get install -y curl
  ```
  This updates the package list and installs the `curl` utility.

---

### 4. `COPY` / `ADD`
- `COPY` is used to copy files or directories from the host machine into the image.
- `ADD` is similar to `COPY`, but it also supports remote URLs and automatic extraction of compressed files.
- **Example:**
  ```dockerfile
  COPY ./myapp /app
  ```
  This copies the contents of the `./myapp` directory from the host into the `/app` directory inside the container.

---

### 5. `WORKDIR`
- Sets the working directory inside the container for subsequent commands. If the directory doesn’t exist, it will be created.
- **Example:**
  ```dockerfile
  WORKDIR /app
  ```
   ** Example **
  ```  dockerfile
    FROM ubuntu:20.04

    CMD ["echo", "First CMD"]
    CMD ["echo", "Second CMD"]
    CMD ["echo", "Third CMD"]
  ```
 ** What Happens?**
    Only the **last CMD** (i.e., CMD ["echo", "Third CMD"]) is executed when the container runs.
    The earlier CMD instructions are completely ignored.

---

### 6. `CMD`
- Specifies the command to execute when the container starts. Only one `CMD` instruction is allowed per Dockerfile.
- **Example:**
  ```dockerfile
  CMD ["python", "app.py"]
  ```
  This runs `python app.py` when the container starts.

---

### 7. `ENTRYPOINT`
- Defines a command to run when the container starts. Unlike `CMD`, `ENTRYPOINT` cannot be overridden at runtime unless explicitly specified.
- **Example:**
  ```dockerfile
  ENTRYPOINT ["python", "app.py"]
  ```

---

### 8. `EXPOSE`
- Indicates which ports the container will listen on at runtime. This serves as documentation but doesn’t actually publish the ports.
- **Example:**
  ```dockerfile
  EXPOSE 8080
  ```

---

### 9. `ENV`
- Sets environment variables inside the container.
- **Example:**
  ```dockerfile
  ENV APP_ENV=production
  ```

---

### 10. `USER`
- Sets the user for subsequent instructions in the Dockerfile.
- **Example:**
  ```dockerfile
  USER appuser
  ```

---

## Sample Dockerfile
```dockerfile
# Use official Python image as base
FROM python:3.8-slim

# Set maintainer and version labels
LABEL maintainer="yourname@example.com"
LABEL version="1.0"

# Set the working directory inside the container
WORKDIR /app

# Copy the application files into the container
COPY . /app

# Install dependencies
RUN pip install -r requirements.txt

# Expose port
EXPOSE 8080

# Set environment variables
ENV APP_ENV=production

# ENTRYPOINT will always run python when the container starts
ENTRYPOINT ["python"]

# CMD provides the default argument (app.py) to ENTRYPOINT
CMD ["app.py"]

# To test overriding CMD, run the container with:
# docker run <image_name> application.py
# This will run python application.py instead of python app.py
```

---

## Building the Docker Image

After creating the Dockerfile, you can build the image using the `docker build` command:

```bash
docker build -t my-python-app .
```

This builds the Docker image and tags it as `my-python-app`.

---

## CMD vs ENTRYPOINT

### CMD
- The `CMD` instruction provides default arguments for the `ENTRYPOINT`. If no arguments are supplied when running the container, `CMD` will be used as the command to run. It can be overridden at runtime if the user specifies a different command.

### ENTRYPOINT
- The `ENTRYPOINT` instruction specifies the main command to run when the container starts. The command specified by `ENTRYPOINT` cannot be overridden by passing different commands when running the container (unless you use `docker run --entrypoint` to override it).

---

### Key Differences in Action

| Feature            | CMD                                          | ENTRYPOINT                                      |
|--------------------|---------------------------------------------|------------------------------------------------|
| Default Command    | Provides a default command to run.         | Sets the main command to always run.          |
| Override Behavior  | Can be overridden at runtime.              | Cannot be overridden unless `--entrypoint` is used. |
| Typical Use        | Default arguments or commands.             | Core, unchangeable commands for the container. |

---

### Using CMD and ENTRYPOINT Together

When used together:
- `**ENTRYPOINT**` defines the main command.
- `**CMD**` provides default arguments to that command. These arguments can be overridden by the user at runtime.

**ENTRYPOINT** is the main command that is executed when the container starts (in this case, python). The CMD provides default arguments for that command (in this case, app.py).

Scenario 1: If you run docker run <image>, it will execute python app.py (because CMD provides the default argument).
Scenario 2: If you run docker run <image> application.py, it will execute python application.py (because the argument passed will override CMD).

Flexibility: With this setup, you ensure that the container will always run python as the command, but you give flexibility to change which script (app.py or application.py) to run based on the user's input.

**Example:**
```dockerfile
ENTRYPOINT ["python"]
CMD ["app.py"]
```
This configuration ensures that the container always runs `python`, but the script (`app.py`) can be overridden at runtime.

---

## Flexibility

### CMD
- You can override `CMD` by specifying a different command when running the container. 
- **Example:**
  ```dockerfile
  CMD ["python", "app.py"]
  ```
  Run with:
  ```bash
  docker run -p 8080:8080 <image_name>  python another_script.py
  ```
  This will execute `python another_script.py`.

### ENTRYPOINT
- Ensures a specific command is always executed. You can pass additional arguments to it, but it won’t be replaced unless explicitly overridden using `--entrypoint`.
- **Example:**
  ```dockerfile
  ENTRYPOINT ["python", "app.py"]
  ```
