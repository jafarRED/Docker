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

## **What is Docker Volume Mapping?**

Docker containers are **ephemeral** in the sense that the data inside the container is not automatically persisted when the container is removed. 
However, data inside a running container does **persist** during the **container’s life cycle**, **even if the container is stopped and then restarted**. 

The data will be lost only **if the container is removed** or **killed** without any external storage like volumes or bind mounts.

**Key Points:**
 - Data is persistent during the container’s life cycle: While the container is running (or even stopped), any data written inside the container will persist.
 - Data is lost when the container is removed: If the container is deleted (removed), the data inside it will be deleted too, unless it's saved in a Docker volume or bind mount.
 - Volumes and Bind Mounts are used to persist data beyond the container's lifecycle.

**Volume Mapping** allows you to link a directory or file from the **host machine** to a **container**, making it possible to **persist data** across container restarts and removals.

## **Why is Volume Mapping Important?**

- **Persistence**: Keeps data safe even if the container is removed.
- **Data Sharing**: Allows multiple containers to share data.
- **Backups**: Makes it easy to back up and restore data.
- **Development**: Enables developers to sync code between the host and containers in real-time.

---

## **Types of Volume Mapping in Docker**

There are **three main ways** to map volumes in Docker:

### 1. **Volumes (Docker Managed)**

- **What are Volumes?**  
  Volumes are storage areas managed by Docker. They are independent of containers, and data stored in them persists even if the container is stopped or deleted.
  
- **Where are Volumes stored?**  
  Volumes are stored on the host machine in Docker's internal storage path: `/var/lib/docker/volumes/`.

- **When to use?**  
  Volumes are ideal for persistent data (e.g., databases), and they are the preferred option for most use cases in production environments.

### 2. **Bind Mounts (Host to Container)**

- **What are Bind Mounts?**  
  Bind Mounts allow you to link any **specific directory or file** on the host system to a container. Changes made on the host will immediately reflect in the container and vice versa.

- **Where are Bind Mounts used?**  
  Bind mounts are commonly used during **development** because they allow for real-time syncing between the host and the container (e.g., syncing application code).

- **When to use?**  
  Bind mounts are great for syncing source code, logs, or config files between the host and the container.

### 3. **Tmpfs Mounts (Memory-Only Storage)**

- **What are Tmpfs Mounts?**  
  Tmpfs mounts are used to store data **temporarily** in the container's memory. This data is not persisted when the container stops.

- **When to use?**  
  Tmpfs mounts are used when you need fast, temporary storage for data that doesn't need to persist.

---

## **How to Do Volume Mapping in Docker**

There are two main ways to map volumes when you run a Docker container: **using the `-v` flag** or the **`--mount` flag**.

### 1. **Using the `-v` Flag (Volume Mapping)**
```bash
docker run -v <host_path>:<container_path> <image_name>
```
- **host_path**: The path to the directory or file on the **host system**.
- **container_path**: The path where the volume is mounted inside the **container**.
  
Example:
```bash
docker run -v /home/user/app:/app node
```
- This maps the `/home/user/app` directory on the host to `/app` inside the container. Any changes made in the host's `/home/user/app` directory will be reflected inside the container at `/app`, and vice versa.

### 2. **Using the `--mount` Flag (Volume Mapping)**
```bash
docker run --mount type=bind,source=<host_path>,target=<container_path> <image_name>
```
- **type=bind**: Specifies that you are using a **bind mount**.
- **source=<host_path>**: The path to the directory or file on the **host system**.
- **target=<container_path>**: The path where the volume is mounted inside the **container**.
  
Example:
```bash
docker run --mount type=bind,source=/home/user/app,target=/app node
```
- This achieves the same result as the previous `-v` example, linking the host's `/home/user/app` to the container's `/app`.

---

## **Creating and Using Volumes**

### **Step 1: Create a Docker Volume**
You can create a Docker volume using the following command:
```bash
docker volume create my_volume
```

### **Step 2: Mount the Volume to a Container**
You can then mount the volume to a container:
```bash
docker run -d -v my_volume:/data busybox
```
- This command runs the `busybox` container and mounts the `my_volume` volume to `/data` inside the container. Any data written to `/data` inside the container will be stored in the `my_volume` volume.

### **Step 3: Inspect the Volume**
To see information about the volume:
```bash
docker volume inspect my_volume
```

### **Step 4: Back Up and Restore Data**
Since volumes exist on the host, you can easily back up and restore data by interacting with the volume directly.

---

## **Examples of Volume Mapping in Use**

### Example 1: Persisting Database Data
- **Use Case**: You have a MySQL container running, and you want to persist the database data.
- **Solution**: You can map a Docker volume to the MySQL container's data directory.
```bash
docker run -d -v mysql_data:/var/lib/mysql mysql
```
- Now, even if the container stops or is removed, the database data will persist in the `mysql_data` volume.

### Example 2: Sharing Code Between Host and Container
- **Use Case**: You’re developing an application and want to sync your code between the host and the container.
- **Solution**: You can use a bind mount to map the host's code directory to the container.
```bash
docker run -d -v /home/user/app:/app node
```
- Now, changes made to `/home/user/app` on the host will reflect inside the container at `/app` and vice versa.

---

## **Key Points to Remember:**
- **Volumes** are Docker-managed and provide persistent storage. They are the preferred method for storing data in production.
- **Bind Mounts** allow direct linking of host directories and are great for development, as they sync changes in real-time between the host and container.
- **Tmpfs Mounts** store data temporarily in memory and are deleted when the container stops.

By using Docker volume mapping, you can ensure that important data persists across container lifecycles, share data between containers, and improve your development workflow.

