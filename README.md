# Docker

# **Introduction to Docker**
**How the IT Industry Worked Before Docker**
**Physical Servers (Traditional Setup):**

Initially, companies relied on physical servers for hosting applications.

Let’s say we have a server with 24 GB RAM and 250 GB storage. We install two applications on it:

Application A: Requires Java 8 and Node.js 16 and uses 10 GB RAM.
Application B: Requires Java 11 and Node.js 22 and uses a similar amount of resources.
The Challenge:

You can’t install Java 8 and Java 11 on the same host as they might conflict.
Similarly, you can’t have two different versions of Node.js installed simultaneously without complex workarounds.
This forces companies to buy new servers to host applications with different dependencies.
Wasted Resources:
Each application uses only 40% of the server’s capacity, leaving the remaining resources idle and unutilized.
Over time, companies had to procure multiple servers to host their applications, leading to high costs and inefficiencies.
Invention of Virtual Machines (VMs):

To overcome these challenges, we moved to Virtual Machines (VMs).

A Hypervisor (like VMware or VirtualBox) is installed on the physical server, enabling the creation of multiple virtual machines.

How Virtual Machines Work:

Each VM acts as a fully isolated, independent system with its own operating system (OS), dedicated RAM, and storage.
Example:
On a 24 GB RAM server, you can create:
VM1: Allocated 10 GB RAM and 100 GB storage to run Application A (with Java 8 and Node.js 16).
VM2: Allocated 10 GB RAM and 100 GB storage to run Application B (with Java 11 and Node.js 22).
Advantages of VMs:

You don’t need to buy new physical servers.
Applications with different dependencies can run on isolated VMs.
Challenges with VMs:

Static Resource Allocation:
Resources are fixed during VM creation (e.g., 10 GB RAM, 100 GB storage) and cannot be dynamically adjusted.
Applications with low traffic may use only 50% of their allocated resources, leading to wastage.
Performance Overhead:
Each VM boots its own OS from scratch, taking 1–2 minutes or more to start.
In case of a crash, launching a new VM may take up to an hour.
Inefficient Resource Utilization:
Resources reserved for one VM cannot be used by another, even if the first VM is idle.
Introduction to Docker
Docker was invented to solve the limitations of physical servers and virtual machines.
It provides lightweight, faster, and more efficient virtualization through containers.
What is Docker?
Docker is a platform that allows you to package your application and its dependencies (libraries, binaries, etc.) into a single, portable unit called a container.
Why is Docker Better?
Shared Host OS:

Containers share the host machine’s operating system kernel, unlike VMs, which need their own OS.
This eliminates the need to boot a full OS, making containers lightweight and faster.
Dynamic Resource Utilization:

Containers use resources dynamically based on the load. If one container doesn’t need resources, others can use them.
Example:
Application A and Application B can now run on the same server without conflict. Docker ensures both have isolated environments using Java 8 and Java 11, respectively.
Startup Speed:

Containers start in milliseconds because they don’t boot an OS.
Example:
If a container crashes, a new container can spin up almost instantly (within seconds).
Higher Resource Utilization:

Unlike VMs, Docker doesn’t waste resources. Containers can use resources more efficiently, ensuring no idle capacity.
Examples and Scenarios
Scenario 1: Development Environments
Imagine a team of developers working on different projects:
Project 1 requires Python 3.9, PostgreSQL, and Redis.
Project 2 requires Python 3.8, MySQL, and Memcached.
Without Docker:
Developers need to set up these dependencies manually, leading to configuration conflicts.
With Docker:
Each developer gets a Docker container with the required dependencies, ensuring consistency across environments.
Scenario 2: Portability
With Docker, you can package an application and run it anywhere—on a developer’s laptop, a testing environment, or a production server—without worrying about dependency issues.
Example:
You develop an app on your laptop and deploy it to a cloud server. Docker ensures the app works identically in both environments.
Scenario 3: Microservices
In modern architectures, applications are broken into microservices (small, independent components).
Each microservice can run in its own Docker container with specific dependencies.
Example:
A payment service might run in one container, while a user authentication service runs in another, ensuring isolation and easier scaling.
Advantages of Docker Over Virtual Machines
Feature	Virtual Machines	Docker Containers
Startup Time	1–2 minutes or more	Few milliseconds
Resource Utilization	Fixed resources, leads to wastage	Dynamic, highly efficient
OS Requirement	Each VM needs a full OS	Shares host OS kernel
Performance	Higher overhead (due to OS per VM)	Lightweight, minimal overhead
Portability	Limited	Highly portable across environments
Conclusion
Docker has revolutionized the IT industry by providing a lightweight, efficient, and scalable way to run applications. It solves many of the problems faced with physical servers and virtual machines, making it a cornerstone of modern DevOps practices.

Next Steps:
In future sessions, you can dive deeper into:

Installing Docker and running your first container.
Understanding Docker Images, Dockerfiles, and Docker Compose.
Managing containers and volumes for data persistence.
Using Docker in CI/CD pipelines.
