
# Chapter 2: Introduction to Docker Command Syntax

## Docker Command Structure
Docker commands follow two main syntaxes:

1. **Old Approach:**
   ```bash
   docker <command> [options]
   ```
   Example:
   ```bash
   docker ps -a
   ```

2. **Modern Approach (Using Management Commands):**
   ```bash
   docker <management-command> <command> [options]
   ```
   Example:
   ```bash
   docker container ls -a
   docker container run -it <image-name>
   ```
   Here:
   - `container` is the management command.
   - `ls` and `run` are the specific commands to list containers and run a new container, respectively.

---

## Basic Commands and Examples

### 1. Run a Container
```bash
docker container run -it <image-name>
```
- **Flags**:
  - `-i`: Keeps the input open, allowing interaction.
  - `-t`: Allocates a pseudo-terminal for interactive use.

**Example:**
```bash
docker container run -it ubuntu
```
This opens an interactive session inside the Ubuntu container.

---

### 2. Stop a Container
```bash
docker container stop <container-ID or name>
```
**Example:**
```bash
docker container stop red
```

---

### 3. List Containers
```bash
docker container ls [options]
```
- `ls`: Lists currently running containers.
- `ls -a`: Lists all containers, including stopped ones.

**Example:**
```bash
docker container ls -a
```

---

### 4. Passing Environment Variables to Containers
```bash
docker run --name <container-name> -e <env-variable>=<value> <image-name>
```
- The `-e` flag allows you to pass environment variables to the container.

**Example:**
```bash
docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw mysql:latest
```

---

### 5. Execute Commands Inside a Running Container
```bash
docker exec -it <container-ID or name> <command>
```
**Example:**
```bash
docker exec -it red date
```

---

## Container Lifecycle

### 1. Flow:
A container's lifecycle typically follows this pattern:
**Container Created → Command Executed → Container Stopped**

**Example:**
```bash
docker run -it --name red ubuntu date
```
**Output:**
```bash
Sat Jan 11 09:06:58 UTC 2025
```

---

### 2. Viewing Running Containers:
```bash
docker ps
```
**Example Output:**
```bash
CONTAINER ID   IMAGE     COMMAND       CREATED         STATUS         PORTS     NAMES
ede65a62afe6   ubuntu    "/bin/bash"   6 seconds ago   Up 5 seconds             red
```

---

## Detaching and Reattaching Containers

### 1. Detaching from a Container Without Stopping It
To detach from an active container without stopping it: Press **Ctrl + p + q**.

---

### 2. Reattach to a Running Container:
```bash
docker attach <container-ID or name>
```

---

## Common Use Case Examples

### 1. Run a Container with Date Command:
```bash
docker run -it --name red ubuntu date
```
**Output:**
```bash
Sat Jan 11 09:06:58 UTC 2025
```

---

### 2. Attach to a Running Container:
```bash
docker attach <container-ID>
```

---

### 3. Execute Commands in a Running Container:
```bash
docker exec -it <container-ID> date
```

---

## Key Points to Remember
- **Interactive Mode**: Use `-it` to interact with the container’s shell.
- **Environment Variables**: Use `-e` to pass environment variables during container creation.
- **Detachment**: Use **Ctrl + p + q** to leave the container running while exiting the session.
- **Reattaching**: Use `docker attach` or `docker exec` to interact with a running container.
- **Dynamic Commands**: Containers allow dynamic execution of commands without needing to stop or restart them.

---

## Docker Attach vs Docker Exec

- **`docker attach <container-ID>`:**
  - Attaches to the container's main process.
  - Exit: The container will stop when you exit (use `exit`).

- **`docker exec -it <container-ID> /bin/bash`:**
  - Executes commands inside a running container without stopping it.
  - Exit: You go inside the container and, even if you exit, the container won’t stop.

---

## To Check What is Going On in a Container Without Logging Into It

### View Logs:
```bash
docker logs <container-ID>
```

### To View in Real-Time:
```bash
docker logs -f <container-ID>
```

### Run a Command Without Logging In
Run Command Inside a Running Container:
```bash
docker exec <container-ID> <command>
```

### To Start a Container, Execute a Command, and Terminate It
Run and Execute Command:
```bash
docker run -it --rm --name red ubuntu date
```
This will execute the `date` command and terminate the container once the command is done.

---

## Next Steps
- Learn about Docker Images and how to build them using Dockerfiles.
- Explore Docker Compose for multi-container applications.
- Understand container networking and volume management.
