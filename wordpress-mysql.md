# **Task: Understanding Link Communication Between Containers (WordPress & MySQL)**

## **Objective**
In this task, you will explore different ways containers can communicate with each other using Docker. You will deploy a **WordPress** container that connects to a **MySQL** database in three different ways:

1. **Using MySQL Container IP**  
2. **Using Docker Link (Deprecated Method)**  
3. **Using Docker Network (Recommended Approach)**  
4. **Using Docker Compose for Service Discovery**  

---

## **Step 1: Setup MySQL Container**
Run a MySQL container with a root password and a database for WordPress:

```sh
docker run -d --name mysql-container \
  -e MYSQL_ROOT_PASSWORD=rootpass \
  -e MYSQL_DATABASE=wordpress \
  mysql:5.7
```

Check the MySQL container IP:
```sh
docker inspect mysql-container | grep '"IPAddress"'
```

---

## **Step 2: Connect WordPress Using MySQL Container IP**
Run WordPress while passing the **MySQL container's IP** as the database host:

```sh
docker run -d --name wordpress-container \
  -e WORDPRESS_DB_HOST=<MYSQL_CONTAINER_IP> \
  -e WORDPRESS_DB_USER=root \
  -e WORDPRESS_DB_PASSWORD=rootpass \
  -e WORDPRESS_DB_NAME=wordpress \
  -p 8080:80 \
  wordpress
```

### **Verify**
Open `http://localhost:8080` and check if WordPress can connect.

**Limitations:**
- The IP address can change if the MySQL container restarts.
- Not scalable for production.

---

## **Step 3: Connect Using Docker Link (Deprecated Method)**
Stop and remove the WordPress container:
```sh
docker stop wordpress-container && docker rm wordpress-container
```

Run WordPress using the **Docker Link** option:

```sh
docker run -d --name wordpress-container \
  --link mysql-container:mysql \
  -e WORDPRESS_DB_HOST=mysql \
  -e WORDPRESS_DB_USER=root \
  -e WORDPRESS_DB_PASSWORD=rootpass \
  -e WORDPRESS_DB_NAME=wordpress \
  -p 8080:80 \
  wordpress
```

### **Why does this work?**
- The `--link` option allows the WordPress container to resolve `mysql` as a hostname.
- However, `--link` is **deprecated** and not recommended for modern Docker setups.

**Limitations:**
- No automatic name resolution updates.
- Cannot be used across multiple Docker networks.

---

## **Step 4: Connect Using Docker Network (Recommended Approach)**
Create a custom Docker network:

```sh
docker network create mynetwork
```

Run MySQL on this network:
```sh
docker run -d --name mysql-container --network mynetwork \
  -e MYSQL_ROOT_PASSWORD=rootpass \
  -e MYSQL_DATABASE=wordpress \
  mysql:5.7
```

Run WordPress using the **MySQL container name** as a hostname:
```sh
docker run -d --name wordpress-container --network mynetwork \
  -e WORDPRESS_DB_HOST=mysql-container \
  -e WORDPRESS_DB_USER=root \
  -e WORDPRESS_DB_PASSWORD=rootpass \
  -e WORDPRESS_DB_NAME=wordpress \
  -p 8080:80 \
  wordpress
```

### **Why does this work?**
- Both containers are in the same **user-defined network**.
- Docker allows **automatic DNS-based name resolution**.
- This is the **preferred** approach for container communication.

---

## **Step 5: Connect Using Docker Compose (Best Practice for Deployment)**
Instead of running containers manually, use a **Docker Compose** file.

Create a `docker-compose.yml` file:

```yaml
version: '3.8'
services:
  mysql:
    image: mysql:5.7
    container_name: mysql-container
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
      MYSQL_DATABASE: wordpress
    networks:
      - mynetwork

  wordpress:
    image: wordpress
    container_name: wordpress-container
    restart: always
    ports:
      - "8080:80"
    environment:
      WORDPRESS_DB_HOST: mysql-container
      WORDPRESS_DB_USER: root
      WORDPRESS_DB_PASSWORD: rootpass
      WORDPRESS_DB_NAME: wordpress
    networks:
      - mynetwork

networks:
  mynetwork:
```

Run everything with:
```sh
docker-compose up -d
```

### **Advantages of Docker Compose:**
- **Simplified Deployment**: Define and run multi-container applications easily.
- **Automatic Networking**: Creates an isolated network for communication.
- **Scalability**: Easily scale services by changing configurations.
- **Maintainability**: All configurations are stored in a single file.

### **Verify**
Open `http://localhost:8080` and complete the WordPress setup.

---

## **Comparison Table**
| Method                  | Pros | Cons |
|-------------------------|------|------|
| **MySQL IP Address**    | Simple, works immediately | IP changes on restart, not scalable |
| **Docker Link**         | Easy to use (legacy method) | Deprecated, lacks flexibility |
| **Docker Network**      | Recommended, scalable, automatic DNS resolution | Needs additional setup |
| **Docker Compose**      | Best for deployment, automates everything | Requires learning YAML syntax |

---

## **Conclusion**
Using **Docker Compose** and **Docker Networks** is the best approach for linking WordPress and MySQL containers. The `--link` option is outdated and should be avoided in modern projects.

Good luck! 🚀

