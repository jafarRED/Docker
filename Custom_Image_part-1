
# Chapter 3: Custom Docker Images

## Why Do We Need Custom Images?
Docker allows users to create their own images. These custom images are useful in various scenarios:

- **Customization**: Docker images can be customized with specific software, dependencies, or configurations needed for a particular environment.
- **Portability**: Once an image is created, it can be used across different systems, making the setup process consistent and repeatable.
- **Version Control**: You can maintain versions of custom images for development, staging, or production environments.
- **Efficiency**: By building custom images, you can avoid manual setup of environments every time you create a container.

You can create custom Docker images in two ways:
1. Using `docker commit`
2. Using a Dockerfile (which we will cover in a later chapter)

In this chapter, we will focus on creating a custom image using the `docker commit` method.

---

## Creating a Custom Image Using `docker commit`
First, let's create a container with the required dependencies and then commit the changes to create a new image.

### Step-by-Step Process:
1. **Start a Container**: Run a basic Ubuntu container.
   ```bash
   docker run -it ubuntu bash
   ```

2. **Install Necessary Packages**: Inside the container, install the required software or utilities. For example, let's install `dnsutils` to use the `nslookup` command.
   ```bash
   apt update -y
   apt install dnsutils
   ```

3. **Test the Installed Package**: Test the installed `nslookup` command.
   ```bash
   nslookup google.com
   ```

4. **Commit the Changes**: Once the required software is installed and configured, you can commit the changes to create a custom image. To do this, use the `docker commit` command.
   ```bash
   docker commit <container-id or name> custom_image:v1
   ```
   **Example:**
   ```bash
   docker commit 490bd60541b9 custom_image:v1
   ```

5. **Verify the New Image**: After committing, you can verify the newly created image by running:
   ```bash
   docker images
   ```
   **Output:**
   ```bash
   REPOSITORY     TAG       IMAGE ID       CREATED         SIZE
   custom_image   v1        cfbd1e0fbf6b   5 seconds ago   169MB
   ```

6. **Run the Custom Image**: To test if the custom image works as expected, run the container from the custom image and execute the `nslookup` command.
   ```bash
   docker run -it --rm custom_image:v1 nslookup google.com
   ```
   **Output:**
   ```bash
   Server:    192.168.0.1
   Address:   192.168.0.1#53

   Non-authoritative answer:
   Name:    google.com
   Address: 142.250.183.238
   ```

---

## Sharing Custom Images
Once you've created a custom image, you may need to share it with others or move it to different systems. You can share images in two ways:

### 1. Export/Import Method
- **Export the Image**: To export the image to a `.tar` file, use the `docker save` command.
  ```bash
  docker save <image-id> -o custom_image.tar
  ```
  **Example:**
  ```bash
  docker save cfbd1e0fbf6b -o custom_image.tar
  ```

- **Import the Image**: To import the image on another system, use the `docker load` command.
  ```bash
  docker load -i custom_image.tar
  ```

### 2. Push to Docker Registry
To push a custom image to Docker Hub or a private registry, you first need to log in to your Docker account using the `docker login` command.

- **Login to Docker**:
  ```bash
  docker login -u <username>
  ```
  **Example:**
  ```bash
  docker login -u redid
  ```

- **Push the Image**: Use the following syntax to push the image to Docker Hub.
  ```bash
  docker push <username>/<repository-name>:<tag>
  ```
  **Example:**
  ```bash
  docker push redid/docker_basics:custom_image
  ```
  If the push is successful, you will see output indicating that the image has been pushed to the registry.

---

## Retrieving Custom Images
Once an image is pushed to Docker Hub or a private registry, others can retrieve it in two ways:

1. **Load the `.tar` File**: If you have received the `.tar` file, use `docker load` to import the image.
   ```bash
   docker load -i custom_image.tar
   ```

2. **Pull the Image from the Registry**: You can use `docker pull` to retrieve the image from Docker Hub.
   ```bash
   docker pull <username>/<repository-name>:<tag>
   ```
   **Example:**
   ```bash
   docker pull redid/docker_basics:custom_image
   ```

---


### Custom Image Lifecycle
Once a custom image is created, it can be reused to create multiple containers. Any changes made inside a container created from this image will not affect the original image unless you commit those changes again.

### Commit vs. Dockerfile
- **`docker commit`** is useful for quick and ad-hoc changes. However, it's not the best practice for reproducible environments because it's not version-controlled and can lead to inconsistencies.
- **Dockerfile** allows you to define the steps required to build an image in a reproducible and version-controlled manner. This is more suitable for larger projects or production environments.

### Best Practices for Creating Custom Images
- Always try to keep your images as small as possible by minimizing unnecessary dependencies.
- Regularly tag your images to track versions.
- If possible, use a Dockerfile instead of `docker commit` for more reproducible and maintainable images.
