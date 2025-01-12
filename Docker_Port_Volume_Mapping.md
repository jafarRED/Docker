# Docker Port Mapping

Port mapping in Docker is an essential concept that allows containers to communicate with the outside world. 

---

### **Network Isolation:**
   - Containers run in their own **virtual network** by default.
   - Without port mapping, container services are not accessible outside this **virtual network.**


## **What is Port Mapping?**

Port mapping in Docker allows a container running an application to be accessible from outside the container (e.g., from your host system or other devices in the network). Containers have their own internal network, and their services are typically not exposed outside unless you map their internal ports to ports on the host machine.

### **Why is Port Mapping Important?**

1. **Access the Containerized Application:**
   - If you’re running a web server or API inside a container, you need to make it available outside the container. Port mapping achieves this.

2. **Isolation and Security:**
   - Docker containers are isolated environments. By default, their services aren’t exposed to the external world, which is secure. Port mapping gives you control over what gets exposed.

3. **Networking Flexibility:**
   - You can customize how containers communicate with the host or other containers by mapping ports to avoid conflicts.

4. **Run Multiple Containers:**
   - By mapping internal container ports to different host ports, you can run multiple containers hosting similar services (e.g., multiple web apps) without conflicts.

---

## **How Does Port Mapping Work in Docker?**

Docker uses the `-p` or `--publish` flag to map ports between the host and the container.

### **Syntax of Port Mapping:**

```bash
docker run -p <host_port>:<container_port> <image_name>
```

- **`host_port`:** The port on the host machine you want to use.
- **`container_port`:** The port the application is using inside the container.
- **`image_name`:** The Docker image you’re running.

---

### **Example: Exposing a Web Server**

1. **Start a Web Server in a Container:**

   Suppose you have an Nginx image running on port `80` inside the container. You can expose it to your host system's port `8080`:

   ```bash
   docker run -d -p 8080:80 nginx
   ```

2. **Access the Application:**

   Open a browser or use `curl` to access `http://localhost:8080`. This forwards requests from port `8080` on the host to port `80` in the container.

3. **Verify the Port Mapping:**

   Run the following command to check the mapped ports:

   ```bash
   docker ps
   ```

   Output:
   ```
   CONTAINER ID   IMAGE    COMMAND       PORTS                    NAMES
   abc123def456   nginx    "nginx -g …"  0.0.0.0:8080->80/tcp     friendly_nginx
   ```

---

### **Different Port Mapping Modes**


1. **Mapping Multiple Ports:**

   You can map multiple ports in one command:

   ```bash
   docker run -d -p 5000:5000 -p 5001:5001 myapp
   ```

2. **Random Host Ports:**
   Use `-P` (uppercase) to randomly map **all exposed ports** in the container to available host ports:

   ```bash
   docker run -d -P nginx
   ```

   Then check which ports were randomly assigned with `docker ps`.

---

### **Advanced Topics in Port Mapping**

1. **Binding to Specific IP Addresses:**

   By default, Docker binds to all network interfaces (`0.0.0.0`). You can restrict this:

   ```bash
   docker run -p 127.0.0.1:8080:80 nginx
   ```

   This ensures the service is only accessible from the local machine.

2. **Avoid Port Conflicts:**

   If another service is already using the host port, Docker will throw an error. Make sure to choose unused ports on the host.

3. **Docker Compose:**
   Port mapping can also be defined in a `docker-compose.yml` file:

   ```yaml
   services:
     web:
       image: nginx
       ports:
         - "8080:80"
   ```

   Then start the services with:
   ```bash
   docker-compose up
   ```

---


## **Best Practices for Port Mapping**

1. **Use Non-Default Ports on the Host:**
   - Avoid exposing container ports directly to common host ports (like `80`) to prevent conflicts.

2. **Restrict External Access:**
   - Bind services to `127.0.0.1` if they don’t need to be accessed publicly.

3. **Use Firewalls:**
   - Combine port mapping with firewalls (e.g., `iptables`) to enhance security.



---

## **Conclusion**

Port mapping is fundamental when working with Docker containers to expose services securely and efficiently. Use `-p` and `-P` effectively, and combine this knowledge with real-world examples to build a robust understanding of Docker networking.

---

# Docker Volume Mapping

Volume mapping in Docker allows you to persist data generated or used by a container. It helps ensure that data remains intact even if the container is stopped, restarted, or removed. Here's everything you need to know about volume mapping!

## What is Volume Mapping?

- Docker containers are ephemeral by design, meaning their data is lost when the container is removed.
- Volume mapping is a feature that allows you to link directories or files from the host system to the container.
- With volume mapping, you can store, retrieve, and share data between containers and the host.

## Why Do We Need Volume Mapping?

### Persist Data:
- Containers are stateless, but many applications (e.g., databases) require persistent storage. Volumes solve this problem.

### Share Data:
- Volumes enable multiple containers to share data by accessing the same storage.

### Simplify Backups:
- Since volumes exist on the host, you can easily back up and restore the data.

### Improve Workflow:
- Developers can sync code from the host to the container in real time, improving productivity.

### Separate Application from Data:
- Keeps the application logic within the container, while the data is safely stored on the host or in Docker volumes.

## How Does Volume Mapping Work?

Docker allows three main ways to manage storage:

1. **Volumes:**
   - Managed by Docker and stored in the `/var/lib/docker/volumes/` directory on the host.

2. **Bind Mounts:**
   - Link any directory or file from the host to the container.

3. **Tmpfs Mounts:**
   - Temporarily store data in the container's memory. Data is deleted when the container stops.

## Volume Mapping Syntax

The `-v` or `--mount` flag is used to specify volume mapping during `docker run`.

Using `-v`:
```bash
docker run -v <host_path>:<container_path> <image_name>
```

- `host_path`: Path on the host system.
- `container_path`: Path where the volume is mounted inside the container.


Using `--mount`:

```shellscript
docker run --mount type=bind,source=<host_path>,target=<container_path> <image_name>
```

## Example: Persisting Data with Volumes

### Creating a Volume:

Use Docker to create a volume:

```shellscript
docker volume create my_volume
```

### Run a Container with the Volume:

Mount the volume to the container:

```shellscript
docker run -d -v my_volume:/data busybox
```

### Verify Volume Usage:

Inspect the volume:

```shellscript
docker volume inspect my_volume
```

### Access Volume Data:

Data written to `/data` in the container will persist on the host in the `my_volume` directory.

## Example: Sharing Code Between Host and Container

Suppose you have a directory on your host:

```shellscript
/home/user/app
```

Mount this directory to the container:

```shellscript
docker run -d -v /home/user/app:/app node
```

Now, any changes made in `/home/user/app` on the host will be reflected inside the container at `/app`, and vice versa.

## Difference Between Volumes and Bind Mounts

| Feature | Volumes | Bind Mounts
|-----|-----|-----
| Managed By Docker | Yes | No
| Path Configuration | Abstract path | Specific host path
| Best For | Persistent application data | Development workflows


## Common Scenarios for Volume Mapping

### Databases:

Mount a volume to store database files persistently:

```shellscript
docker run -d -v db_data:/var/lib/mysql mysql
```

### Logs:

Mount a host directory to access container logs in real time:

```shellscript
docker run -d -v /host/logs:/container/logs my_app
```

### Development:

Mount code directories to sync changes between the host and container:

```shellscript
docker run -d -v /path/to/code:/app my_dev_container
```

### Shared Data:

Share configuration files between multiple containers by mounting the same volume.

---
**Best Practices for Volume Mapping**
**Use Named Volumes for Persistence:**
 - Named volumes are more reliable and easier to manage than bind mounts.
 - 
**Restrict Access to Sensitive Files:**
 - Avoid exposing sensitive files (e.g., SSH keys) through volume mapping unless necessary.
 - 
**Separate Application from Data:**
- Store data in volumes and keep the application in containers for modularity.
  
**Clean Up Unused Volumes:**
 - Regularly remove unused volumes to free up space:
   ```bash
   docker volume prune
   ```
