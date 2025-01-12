# Introduction to Docker

## How the IT Industry Worked Before Docker

### 1. Physical Servers (Traditional Setup)

Initially, companies relied on physical servers for hosting applications.

Let’s say we have a server with **24 GB RAM** and **250 GB storage**. We install two applications on it:

- **Application A**: Requires Java 8 and Node.js 16 and uses 10 GB RAM.
- **Application B**: Requires Java 11 and Node.js 22 and uses a similar amount of resources.

#### The Challenge:
- **Dependency Conflicts**:
  - You can’t install Java 8 and Java 11 on the same host as they might conflict.
  - Similarly, you can’t have two different versions of Node.js installed simultaneously without complex workarounds.

- **Resource Wastage**:
  - Each application uses only 40% of the server’s capacity, leaving the remaining resources idle and unutilized.
  - Companies had to procure multiple servers, leading to high costs and inefficiencies.

---

### 2. Invention of Virtual Machines (VMs)

To overcome these challenges, the industry introduced **Virtual Machines (VMs)**.

#### How Virtual Machines Work:
- A **Hypervisor** (e.g., VMware, VirtualBox) is installed on the physical server, enabling the creation of multiple virtual machines.
- Each VM acts as an independent system with its own operating system (OS), dedicated RAM, and storage.

#### Example Setup:
On a **24 GB RAM server**, you can create:
- **VM1**: Allocated 10 GB RAM and 100 GB storage to run Application A.
- **VM2**: Allocated 10 GB RAM and 100 GB storage to run Application B.

#### Advantages of VMs:
- Applications with different dependencies can run on isolated VMs.
- No need to purchase additional physical servers.

#### Challenges with VMs:
- **Static Resource Allocation**:
  - Resources are fixed during VM creation (e.g., 10 GB RAM, 100 GB storage) and cannot be dynamically adjusted.
  - Applications with low traffic may only utilize 50% of allocated resources, leading to wastage.

- **Performance Overhead**:
  - Each VM boots its own OS, taking **1–2 minutes or more** to start.
  - In case of a crash, launching a new VM may take up to an hour.

- **Resource Inefficiency**:
  - Resources reserved for one VM cannot be used by another, even if the first VM is idle.

---

## Introduction to Docker

Docker was invented to solve the limitations of physical servers and virtual machines. It provides lightweight, faster, and more efficient virtualization through **containers**.

### What is Docker?
Docker is a platform that allows you to **package your application and its dependencies** (libraries, binaries, etc.) into a single, portable unit called a **container**.

---

### Why is Docker Better?

1. **Shared Host OS**:
   - Containers share the host machine’s OS kernel, unlike VMs, which need their own OS.
   - This eliminates the need to boot a full OS, making containers lightweight and faster.

2. **Dynamic Resource Utilization**:
   - Containers use resources dynamically based on the load.

   **Example**:  
   Application A and Application B can now run on the same server without conflict, each in its isolated container.

3. **Startup Speed**:
   - Containers start in **milliseconds** because they don’t boot an OS.

   **Example**:  
   If a container crashes, a new container can spin up almost instantly.

4. **Higher Resource Utilization**:
   - Unlike VMs, Docker doesn’t waste resources. Containers use resources efficiently, ensuring no idle capacity.

---

### Examples and Scenarios

#### Scenario 1: Development Environments
**Problem**:  
Developers working on multiple projects require different dependencies, leading to configuration conflicts.

**Solution with Docker**:  
Each developer gets a container with the required dependencies, ensuring consistency across environments.

---

#### Scenario 2: Portability
Docker ensures applications run identically on a developer’s laptop, testing environments, and production servers.

**Example**:  
You develop an app locally and deploy it to a cloud server without worrying about dependency issues.

---

#### Scenario 3: Microservices
In microservices architecture, applications are broken into independent components.

**Example**:  
A payment service runs in one container, and a user authentication service runs in another, ensuring isolation and easier scaling.

---

### Advantages of Docker Over Virtual Machines

| **Feature**         | **Virtual Machines**         | **Docker Containers**     |
|----------------------|------------------------------|---------------------------|
| **Startup Time**     | 1–2 minutes or more         | Milliseconds              |
| **Resource Utilization** | Fixed resources, leads to wastage | Dynamic and efficient    |
| **OS Requirement**   | Each VM needs a full OS     | Shares host OS kernel     |
| **Performance**      | Higher overhead (due to OS per VM) | Lightweight, minimal overhead |
| **Portability**      | Limited                    | Highly portable           |

<img src="https://github.com/user-attachments/assets/e0896169-ce75-48e8-8570-c3dccf53e06c" alt="image" width="400" height="300">



---

### Conclusion

Docker revolutionized the IT industry by providing a lightweight, efficient, and scalable way to run applications. It solves many problems faced with physical servers and virtual machines, making it a cornerstone of modern DevOps practices.

---

### Next Steps:

[ 🛠️ Installing Docker and running your first container.](./Docker_Installation.md)

[📌Basics _of_Docker](Basics_of_Docker.md)

[ 🎯 Understanding Docker Images, Dockerfiles, and Docker Compose part1.](Custom_Image_part-1.md) 

[ 🚀 Understanding Docker Images, Dockerfiles, and Docker Compose part2.](Custom_Image_Dockerfile_part-2.md) 

[ 📌 Best_Practices_Dockerfile](Best_Practices_Dockerfile.md)


[🚀 Managing volumes for data persistence & Port Mappping.](Docker_Port_Volume_Mapping.md)

4. Using Docker in CI/CD pipelines.


## Linux Notes
[ 📌 Linux_Basic_Commands](Basics _of_Docker.md)

[ 📌Linux_Basic_File_Permissions.md](Linux_Basic_File_Permissions.md)

[ 📌Linux_Basics_Inode_and_Links.md](Linux_Basics_Inode_and_Links.md)
