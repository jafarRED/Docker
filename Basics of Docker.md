
# Chapter 2: Introduction to Docker Command Syntax

## Docker Command Structure
Docker commands follow two main syntaxes:

1. **Old Approach:**
   ```
   docker <command> [options]
   ```
   Example:
   ```
   docker ps -a
   ```

2. **Modern Approach (Using Management Commands):**
   ```
   docker <management-command> <command> [options]
   ```
   Example:
   ```
   docker container ls -a
   docker container run -it <image-name>
   ```
   Here:
   - `container` is the management command.
   - `ls` and `run` are the specific commands to list containers and run a new container, respectively.

---

## Basic Commands and Examples

### 1. Run a Container
```
docker container run -it <image-name>
```
- **Flags**:
  - `-i`: Keeps the input open, allowing interaction.
  - `-t`: Allocates a pseudo-terminal for interactive use.

**Example:**
```
docker container run -it ubuntu
```
This opens an interactive session inside the Ubuntu container.

---

### 2. Stop a Container
```
docker container stop <container-ID or name>
```
**Example:**
```
docker container stop red
```

---

### 3. List Containers
```
docker container ls [options]
```
- `ls`: Lists currently running containers.
- `ls -a`: Lists all containers, including stopped ones.

**Example:**
```
docker container ls -a
```

---

### 4. Passing Environment Variables to Containers
```
docker run --name <container-name> -e <env-variable>=<value> <image-name>
```
- The `-e` flag allows you to pass environment variables to the container.

**Example:**
```
docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw mysql:latest
```

---

### 5. Execute Commands Inside a Running Container
```
docker exec -it <container-ID or name> <command>
```
**Example:**
```
docker exec -it red date
```

---

## Container Lifecycle

### 1. Flow:
A container's lifecycle typically follows this pattern:
**Container Created → Command Executed → Container Stopped**

**Example:**
```
docker run -it --name red ubuntu date
```
**Output:**
```
Sat Jan 11 09:06:58 UTC 2025
```

---

### 2. Viewing Running Containers:
```
docker ps
```
**Example Output:**
```
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
```
docker run -it --name red ubuntu date
```
**Output:**
```
Sat Jan 11 09:06:58 UTC 2025
```

---

### 2. Attach to a Running Container:
```
docker attach <container-ID>
```

---

### 3. Execute Commands in a Running Container:
```
docker exec -it <container-ID> date
```

---

## Key Points to Remember
- **Interactive Mode**: Use `-it` to interact with the container’s shell.
- **Environment Variables**: Use `-e` to pass environment variables during container creation.
- **Detachment**: Use **Ctrl + p + q** to leave the container running while exiting the session.
- **Reattaching**: Use `docker attach` or `docker exec` to interact with a running container.
- **Dynamic Commands**: Containers allow dynamic execution of commands without needing to stop or restart them.
