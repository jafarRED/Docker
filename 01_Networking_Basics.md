# OSI Model: An Overview

The OSI (Open Systems Interconnection) model is a framework that standardizes how data is transmitted over a network. It consists of **7 layers**, each responsible for a specific function.

---

## **7 Layers of the OSI Model (with Real-Life Analogy: Sending a Letter)**
![image](https://github.com/user-attachments/assets/f9ff5aed-157c-4aaa-b8cb-3e10b9bcf687)
*Image Source: [Cisco Blog](https://blogs.cisco.com/cloud/an-osi-model-for-cloud)*

### 1. **Physical Layer (Layer 1)**
- **Function:** Handles the physical transmission of raw data (bits) through cables, switches, and signals.
- **Analogy:** The **postman’s route** – the physical path the letter takes (by road, train, airplane).
- **Examples:** Wires, fiber optics, network interface cards.

---

### 2. **Data Link Layer (Layer 2)**
- **Function:** Ensures error-free data transmission within the local network. Organizes data into frames.
- **Analogy:** The **mailman picking up your letter** – ensures it gets into the correct delivery system and fixes local errors (like an invalid address in your town).
- **Key Concepts:** MAC addresses, Ethernet, switches.

---

### 3. **Network Layer (Layer 3)**
- **Function:** Handles routing and addressing to ensure data reaches the correct destination.
- **Analogy:** The **sorting facility at the post office** – sorts letters based on destination (city or country).
- **Key Components:** IP addresses, routers.

---

### 4. **Transport Layer (Layer 4)**
- **Function:** Ensures reliable data transfer, correct sequencing, and error checking.
- **Analogy:** The **quality control department** at the post office – checks that letters are sealed and delivered without errors.
- **Key Concepts:** 
  - **TCP (Transmission Control Protocol):** Reliable, checks for errors.
  - **UDP (User Datagram Protocol):** Fast, but no error checking.
- **Example:** A delivery receipt ensures the letter reached the recipient.

---

### 5. **Session Layer (Layer 5)**
- **Function:** Manages and terminates communication sessions between devices.
- **Analogy:** The **conversation between you and a friend** – starts, continues, and ends without interruptions.
- **Example:** Logging into a website creates a session that ends when you log out.

---

### 6. **Presentation Layer (Layer 6)**
- **Function:** Translates data into a format readable by the application. Handles encryption, compression, and data formatting.
- **Analogy:** **Translating a foreign language** – ensures the recipient can understand the content (e.g., converting English to French).
- **Key Concepts:** 
  - Encryption (e.g., HTTPS).
  - File formats (JPEG, MP4).
- **Example:** Watching a video – this layer ensures the file format is compatible with the device.

---

### 7. **Application Layer (Layer 7)**
- **Function:** The layer where users interact directly. Provides services like web browsing, email, and file transfers.
- **Analogy:** The **person reading the letter** – the final step where the content is understood.
- **Key Components:** 
  - Web browsers (Chrome, Firefox).
  - Email clients (Gmail, Outlook).
  - File transfer protocols (FTP).

---

## **End-to-End Example: Sending a WhatsApp Message**

1. **Application Layer:** You type a message in WhatsApp.
2. **Presentation Layer:** WhatsApp encrypts the message.
3. **Session Layer:** A session is established with the recipient.
4. **Transport Layer:** The message is broken into packets.
5. **Network Layer:** Packets are labeled with IP addresses.
6. **Data Link Layer:** Data is framed for local delivery.
7. **Physical Layer:** Signals travel through cables/Wi-Fi.

At the recipient’s end, the process works in reverse, reassembling the message.

---


### **Fun Fact**
The OSI model is a theoretical framework. In practice, we use protocols like **TCP/IP**, which simplifies some layers.

---




# Basics of Networking: Packets, Frames, and Bits

When data is sent over a network, it doesn’t travel as one large chunk. Instead, it is broken down into smaller, manageable pieces like **packets**, **frames**, and **bits**. Let’s explore these concepts step by step.

---

## **1. Bits and Bytes: The Smallest Units**
- **Bits (Binary Digits):**
  - The smallest unit of data in a network, represented as **0s and 1s** (binary code).
  - Example: **01100001** represents the letter "a" in binary.

- **Bytes:**
  - A group of 8 bits.

---

## **2. Packets: Chunks of Data**
- **What is a Packet?**
  - A packet is a small piece of data that is sent over a network.
  - Each packet contains:
    - **Header:** Instructions like the source and destination address.
    - **Payload:** The actual data being sent (e.g., part of an email or video).
    - **Trailer:** Error-checking information to ensure data integrity.

- **Why Packets?**
  - Breaking data into packets makes transmission more efficient and reliable.
  - If a packet is lost or corrupted, only that piece needs to be resent.

**Analogy:**  
Packets are like **pages of a book** being sent individually through the mail.

---

## **3. Frames: The Local Delivery Units**
- **What is a Frame?**
  - A frame is a container for a packet, used in local networks.
  - It wraps the packet with additional information needed for local delivery, such as the **MAC address**.

- **Where are Frames Used?**
  - Frames operate at the **Data Link Layer (Layer 2)** of the OSI model.
  - Devices like switches use frames to send data within a local network.

**Analogy:**  
If a packet is like a **page of a book**, a frame is the **envelope** that helps deliver the page to a specific mailbox.

---

## **4. Putting It All Together**
When you send data over a network:
1. The data is broken into **packets**.
2. Each packet is wrapped into a **frame** for local delivery.
3. Frames are converted into **bits** (binary) and transmitted as electrical signals, light pulses, or radio waves over physical media.

---

## **End-to-End Example: Watching a YouTube Video**
1. The YouTube video is broken into **packets**.
2. Each packet is wrapped in a **frame** and sent across the network.
3. The frame is converted into **bits**, traveling as electrical signals through cables or Wi-Fi.
4. Your computer receives and reassembles the packets into the full video.

---


### **Fun Fact**
The process of breaking data into packets and wrapping them in frames ensures efficient, reliable communication across networks of all sizes.

---


# Networking Devices: Basics and Their Functions

Understanding networking devices is crucial to building and managing networks. Below is an overview of key devices like hubs, switches, routers, and more, with easy-to-understand analogies.

---

## **1. Hub**
### **Definition:**
- A hub is a basic networking device that connects multiple devices in a network and forwards data to **all connected devices**.
- Operates at the **Physical Layer (Layer 1)** of the OSI model.

### **How it Works:**
- When a device sends data to the hub, it broadcasts the data to every connected device, regardless of the intended recipient.

### **Key Characteristics:**
- Does not filter or intelligently forward data.
- Creates unnecessary network traffic.
- Rarely used today due to inefficiency.

### **Analogy:**
Think of a hub as a **loudspeaker**. When you speak into it, everyone in the room hears the message, even if it’s only meant for one person.

---

# Bridge Device and MAC Address Table Example

A **Bridge** is a networking device used to connect multiple Local Area Networks (LANs) into a larger network. It operates at the Data Link Layer (Layer 2) and is used to filter traffic between the networks based on MAC addresses.

**Example with MAC Address Table**
Let's assume the following network setup:

LAN-1: Lap1, Lap2, Lap3

LAN-2: Lap4, Lap5, Lap6

Bridge: Connecting LAN-1 and LAN-2

The MAC address table of the bridge will initially be empty. As devices send traffic, the bridge learns the MAC addresses and updates its table.

![image](https://github.com/user-attachments/assets/8dc4df81-4032-4da8-9463-3943a3964aee)



### 1. First Communication (Learning Phase)

- **Scenario**: `Lap1` in **LAN-1** sends a message to `Lap2` (also in **LAN-1**).
- The bridge doesn't know where `Lap2`'s MAC address is, so it **broadcasts the message to both LANs**.
  
#### MAC Address Table (Before)
| MAC Address        | Port  |  
|--------------------|-------|  
|                    |       |  

- After receiving the broadcast, `Lap2` responds, and the bridge learns that `Lap1`'s MAC address is connected to **port-1** (since `Lap1` is in LAN-1), and `Lap2`'s MAC address is connected to **port-1** (since `Lap2` is also in LAN-1).

#### MAC Address Table (After Learning)
| MAC Address        | Port  |  
|--------------------|-------|  
| 00:11:22:33:44:01  | Port-1 |  
| 00:11:22:33:44:02  | Port-1 |  

At this stage, the bridge knows where `Lap1` and `Lap2` are located (both in **LAN-1**), but doesn't yet know about `Lap3`, `Lap4`, `Lap5`, or `Lap6`.

---

### 2. Second Communication (Learning Phase Continues)

- **Scenario**: `Lap1` now sends a message to `Lap4` (in **LAN-2**).
- The bridge doesn't know `Lap4`'s MAC address yet, so it **broadcasts the message** to both **LAN-1** and **LAN-2**.
  
#### MAC Address Table (Before)
| MAC Address        | Port  |  
|--------------------|-------|  
| 00:11:22:33:44:01  | Port-1 |  
| 00:11:22:33:44:02  | Port-1 |  

- `Lap4` in **LAN-2** responds. The bridge then learns that `Lap4`'s MAC address is connected to **port-2** (since `Lap4` is in **LAN-2**).

#### MAC Address Table (After Learning)
| MAC Address        | Port  |  
|--------------------|-------|  
| 00:11:22:33:44:01  | Port-1 |  
| 00:11:22:33:44:02  | Port-1 |  
| 00:11:22:33:44:04  | Port-2 |  

---

### 3. Subsequent Communication (Filtered Traffic)

- **Scenario 1**: `Lap1` sends a message to `Lap2` (both in **LAN-1**).
  - The bridge already knows that `Lap2` is connected to **port-1**.
  - The bridge **does not broadcast** to **LAN-2** anymore. It simply forwards the message to **LAN-1** (to `Lap2`).

#### MAC Address Table
| MAC Address        | Port  |  
|--------------------|-------|  
| 00:11:22:33:44:01  | Port-1 |  
| 00:11:22:33:44:02  | Port-1 |  
| 00:11:22:33:44:04  | Port-2 |  

- **Scenario 2**: `Lap1` sends a message to `Lap4` (in **LAN-2**).
  - The bridge already knows that `Lap4` is connected to **port-2**.
  - The bridge **does not broadcast** to **LAN-1** anymore. It simply forwards the message to **LAN-2** (to `Lap4`).

---


1. **Learning Phase**:
   - The bridge broadcasts to both networks the first time it doesn't know a destination's MAC address.
   - It learns the MAC address and updates its **MAC address table**.

2. **After Learning**:
   - The bridge forwards frames to the correct network (LAN-1 or LAN-2) based on its MAC address table, instead of broadcasting to both networks.

This method helps to **reduce unnecessary network traffic** by only sending data where it's needed.

---

### Difference Between Hub and Bridge

| Feature               | Hub                                       | Bridge                                  |
|-----------------------|-------------------------------------------|-----------------------------------------|
| **Function**           | Repeats signals to all devices.           | Filters traffic and forwards frames based on MAC addresses. |
| **Layer**              | Layer 1 (Physical Layer)                 | Layer 2 (Data Link Layer)              |
| **Traffic Management** | Broadcasts to all devices.               | Forwards traffic only to the relevant network segment. |
| **Efficiency**         | Less efficient, as it causes congestion.  | More efficient, reduces collisions and traffic. |
| **MAC Address Table**  | Does not maintain a MAC address table.    | Maintains a MAC address table for learning and forwarding. |

---
# Hub, Bridge, and Router: Duplex Modes and Differences


Here’s the revised version of your explanation with the corrections included and sender/receiver in boxes for better clarity in **Markdown** syntax:

# Duplex Modes and Device Functions

## Half-Duplex Communication

In **half-duplex** communication, data transmission can only happen in **one direction** at a time. At any given moment, the device can either **send** or **receive** data, but **not both** simultaneously.

### Representation:



| Sender |------->| Receiver|
|---------|---------|---------|


| Receiver|**<**--------| Sender  |
|---------|---------|---------|

- **Sender** sends data to **Receiver**.
- **Receiver** sends data back to **Sender**.

In half-duplex systems, only **one direction** is active at any time—either sending or receiving, not both. This is why devices like **hubs** are considered half-duplex, as they allow all devices to send and receive data, but not at the same time.

---

## Full-Duplex Communication

In **full-duplex** communication, data can be transmitted in **both directions simultaneously**. This means that devices can send and receive data at the same time.

### Representation:



| Sender |**<------->**| Receiver|
|--------|---------|---------|


- **Sender** can send data while simultaneously **Receiver** can send data back.

Devices like **bridges** and **routers** operate in full-duplex mode, enabling more efficient communication without waiting for one side to finish before the other can start.

---

## Key Differences Between Half-Duplex and Full-Duplex:

| **Mode**         | **Description**                                                           | **Devices**                  |
|------------------|---------------------------------------------------------------------------|------------------------------|
| **Half-Duplex**  | Data can only flow in **one direction** at a time.                        | **Hubs** (Layer 1), Radios, Walkie-Talkies |
| **Full-Duplex**  | Data can flow in **both directions simultaneously**.                      | **Bridges** (Layer 2), **Routers** (Layer 3), Telephones |

---

## Summary of Device Characteristics

| **Device**  | **Duplex Mode** | **Function**                                       | **OSI Layer**     |
|-------------|-----------------|---------------------------------------------------|-------------------|
| **Hub**     | Half-Duplex     | Connects devices in a LAN, **broadcasts** data.   | Physical Layer (Layer 1) |
| **Bridge**  | Full-Duplex     | Connects and segments LANs, reduces collisions.   | Data Link Layer (Layer 2) |
| **Router**  | Full-Duplex     | Routes data between different networks or subnets. | Network Layer (Layer 3) |

---

In short:
- **Half-Duplex**: One-way data transfer at any given time.
- **Full-Duplex**: Two-way data transfer at the same time.

These concepts play a crucial role in network efficiency, device capabilities, and how data is transmitted in a network.





## 1. **Hub**
- **Duplex Mode**: **Half-Duplex**
- **Explanation**: 
  A **hub** is a simple networking device that connects multiple devices in a LAN. It operates in **half-duplex** mode, meaning that data transmission can only occur in one direction at a time. When one device sends data, all other devices on the hub must wait until the transmission is completed. If two devices try to send data simultaneously, a **collision** occurs, and the data is lost, requiring retransmission.

  ### Key Characteristics of Hub:
  - Operates at **Layer 1 (Physical Layer)** of the OSI model.
  - **Broadcasts** data to all connected devices.
  - **No intelligence**: Doesn't know which device to send data to.
  - Simple device but can cause **network congestion** and **collisions** due to its half-duplex nature.

  ### Example:
  If **Device A** sends data, all other devices (B, C, D) must wait for the transmission to finish before they can send their data.

---

## 2. **Bridge**
- **Duplex Mode**: **Full-Duplex**
- **Explanation**:
  A **bridge** is a more intelligent networking device that operates at the **Data Link Layer (Layer 2)**. It is used to connect two or more LAN segments. Unlike a hub, a bridge can forward data to the correct segment, reducing collisions. It also operates in **full-duplex** mode, meaning it can send and receive data at the same time on each segment. This improves performance as there is no need to wait for the other device to stop transmitting.

  ### Key Characteristics of Bridge:
  - Operates at **Layer 2 (Data Link Layer)** of the OSI model.
  - **Learns** and stores MAC addresses in a **MAC address table**.
  - Can reduce **collisions** by dividing networks into **separate collision domains**.
  - **Full-Duplex** operation allows simultaneous sending and receiving of data.

  ### Example:
  If **Device A** in LAN-1 sends data to **Device B** in LAN-2, the bridge forwards the data only to LAN-2, ensuring no collision occurs within the respective segments.

---

## 3. **Router**
- **Duplex Mode**: **Full-Duplex**
- **Explanation**:
  A **router** is a **Layer 3 (Network Layer)** device that connects different networks or subnets, enabling devices in different networks to communicate with each other. Routers operate in **full-duplex** mode, similar to bridges, as they need to send and receive data at the same time to maintain efficient communication. Routers use **IP addresses** to determine the best path for data to travel from source to destination.

  ### Key Characteristics of Router:
  - Operates at **Layer 3 (Network Layer)** of the OSI model.
  - **Routes** packets between different networks (or subnets).
  - Uses **routing tables** and **IP addresses** to forward data.
  - Can perform **Network Address Translation (NAT)** to enable multiple devices in a local network to share a single public IP.
  - **Full-Duplex** operation enables simultaneous sending and receiving.

  ### Example:
  If **Device A** (192.168.0.1) in Network 1 wants to send data to **Device B** (10.0.0.1) in Network 2, the router will determine the best path and forward the packet from one network to the other.

---

## Summary of Differences:

| **Device**  | **Duplex Mode** | **Function**                                       | **OSI Layer**     |
|-------------|-----------------|---------------------------------------------------|-------------------|
| **Hub**     | Half-Duplex     | Connects devices in a LAN, **broadcasts** data.   | Physical Layer (Layer 1) |
| **Bridge**  | Full-Duplex     | Connects and segments LANs, reduces collisions.   | Data Link Layer (Layer 2) |
| **Router**  | Full-Duplex     | Routes data between different networks or subnets. | Network Layer (Layer 3) |

---

In short:
- **Hub**: Half-duplex, broadcasts data to all devices in a network.
- **Bridge**: Full-duplex, connects multiple network segments and filters traffic.
- **Router**: Full-duplex, routes data between different networks based on IP addresses.

These differences directly impact **network performance**, **collision domains**, and **how data is forwarded** within networks.


---

# Understanding Collision Domains with Bridges

## Collision Domain Explanation

A **collision domain** is a network segment where data packets can "collide" if two devices try to send data at the same time on the same shared medium.

### Collision Domain in the Context of a Bridge

1. **Before using a bridge**: All devices in the same LAN are in a **single collision domain**, meaning they share the same bandwidth. If two devices send data at the same time, a **collision** occurs, causing data loss and requiring retransmission.

2. **After introducing a bridge**: The bridge divides the network into **separate collision domains**. Each segment (LAN-1, LAN-2) is now its own collision domain. This means that:
   - **LAN-1** has its own collision domain.
   - **LAN-2** has its own collision domain.

Devices in **LAN-1** can transmit simultaneously with devices in **LAN-2** without causing collisions.

### Why is this important?

- **Before the bridge**: All devices in the network share the same collision domain. If one device transmits, others must wait. This can lead to congestion and poor performance.
- **After the bridge**: The network is divided into separate collision domains, reducing the chances of collisions and improving overall network efficiency.

### The Importance of Collision Domains

- By using a bridge, the network can **scale better**. The bridge isolates collision domains, ensuring that larger networks can function smoothly without data collisions.
- It improves **performance** by reducing **network congestion**.

---

## Simple Example of Collision Domains in a Bridge Setup

Let’s go back to your example:

- **LAN-1** has `Lap1`, `Lap2`, `Lap3`.
- **LAN-2** has `Lap4`, `Lap5`, `Lap6`.

### Without a Bridge:

- All devices (Lap1, Lap2, Lap3, Lap4, Lap5, Lap6) are in a single collision domain. If **Lap1** and **Lap4** try to send data at the same time, their packets will **collide**.

### With a Bridge:

- **LAN-1** (with `Lap1`, `Lap2`, `Lap3`) is in **collision domain 1**.
- **LAN-2** (with `Lap4`, `Lap5`, `Lap6`) is in **collision domain 2**.

Now, **Lap1** and **Lap4** can send data at the same time without causing collisions, as they are in different collision domains.


---
**Bridge**:
  - A bridge connects two or more network segments (usually two LANs) and forwards frames between them based on MAC addresses.
    
  - It operates at Layer 2 (Data Link Layer) of the OSI model.
    
  - A bridge typically has two ports, one for each LAN segment it connects.
**Switch**:
  - A switch is essentially a multiport bridge because it performs the same function as a bridge—forwarding frames based on MAC addresses—but it has more ports.

  - A switch operates at Layer 2 (Data Link Layer) like a bridge, but it is designed to handle multiple devices, often within the same network.
  
  - Unlike a bridge, which connects only two segments, a switch can connect many devices within a network (multiple LAN segments), making it a multiport version of the bridge.
  
  - A switch creates a collision domain for each of its ports, reducing collisions compared to a hub, and can also perform learning (storing MAC addresses in its MAC address table).
  
  - So, while both bridges and switches are Layer 2 devices that forward data based on MAC addresses, the main difference is that a switch provides more ports and is designed for more complex networking.

**In short:**
Bridge: Typically used for connecting two segments.
Switch: A multiport bridge used to connect multiple devices in a network.


A 24-port switch would create 24 collision domains, one for each of its ports.

**Here’s why:**

A collision domain is a network segment where data packets can collide with each other if two devices transmit at the same time. This occurs in devices like hubs where all devices share the same transmission medium.

Switches, however, separate each port into its own collision domain. Each device connected to a switch port communicates independently with the switch and has its own dedicated bandwidth, reducing collisions.

In the case of a 24-port switch, each of the 24 ports represents a separate collision domain. So, if 24 devices are connected to a 24-port switch, each device will have its own isolated communication path, preventing packet collisions between them.

This is a key advantage of switches over hubs, which only have one collision domain for all connected devices.


---

## Summary

- A **bridge** divides the network into **two collision domains** (one for each connected segment).
- Each segment can **send data independently** without causing collisions with other segments.
- This reduces **network congestion** and improves **performance**.



        **HUB** – 
        We start with a hub because we should get rid of it as soon as possible. The reason being, it neither breaks a collision domain nor a broadcast domain,i.e a hub is neither a collision domain separator nor a broadcast domain separator. All the devices connected to a hub are in a single collision and single broadcast domain. Remember, hubs do not segment a network, they just connect network segments.
        **SWITCH** – 
        Coming to switches, we have an advantage over the hub. Every port on a switch is in a different collision domain, i.e a switch is a collision domain separator. So messages that come from devices connected to different ports never experience a collision. This helps us during designing networks but there is still a problem with switches. They never break broadcast domains, which means it is not a broadcast domain separator. All the ports on the switch are still in a single broadcast domain. If a device sends a broadcast message, it will still cause congestion.
        **ROUTER** – 
        Last, but not least, we have our savior. A router not only breaks collision domains but also breaks broadcast domains, which means it is both collisions as well as broadcast domain separators. A router creates a connection between two networks. A broadcast message from one network will never reach the other one as the router will never let it pass. 

---
## **3. Switch**
### **Definition:**
- A switch connects multiple devices but forwards data **only to the intended recipient**.
- Operates at the **Data Link Layer (Layer 2)** and sometimes at **Layer 3**.

### **How it Works:**
- Uses **MAC addresses** to identify devices and send data directly to the correct destination.

### **Key Characteristics:**
- Reduces network congestion.
- Supports full-duplex communication (data can flow both ways simultaneously).
- Commonly used in modern networks.

### **Analogy:**
A switch is like a **personal secretary**. When you give a message, it ensures it’s delivered only to the intended person, not the whole office.

---

## **4. Router**
### **Definition:**
- A router connects different networks and forwards data between them.
- Operates at the **Network Layer (Layer 3)** of the OSI model.

### **How it Works:**
- Uses **IP addresses** to determine the best path for data to travel from one network to another.

### **Key Characteristics:**
- Enables internet access by connecting local networks to the internet.
- Can include additional features like firewalls, DHCP, and NAT.

### **Analogy:**
A router is like a **GPS navigator**. It determines the best route to deliver your message to its destination.

---

## **5. Access Point (AP)**
### **Definition:**
- An access point allows wireless devices to connect to a wired network.
- Operates at the **Data Link Layer (Layer 2)**.

### **Key Characteristics:**
- Extends the wireless range of a network.
- Commonly used in Wi-Fi setups.

### **Analogy:**
An access point is like a **Wi-Fi hotspot** in a coffee shop that connects your device to the internet.

---

## **6. Firewall**
### **Definition:**
- A firewall is a security device that monitors and controls incoming and outgoing network traffic.
- Operates at the **Network Layer (Layer 3)** and above.

### **Key Characteristics:**
- Blocks unauthorized access.
- Can be hardware-based or software-based.

### **Analogy:**
A firewall is like a **security guard** at the entrance of a building, allowing only authorized people to enter.

---

## **7. Modem**
### **Definition:**
- A modem (Modulator-Demodulator) is a device that converts digital signals to analog for transmission over telephone lines and vice versa.
- Used to connect to the internet via an ISP.

### **Key Characteristics:**
- Works with DSL or cable networks.
- Often combined with routers in a single device.

### **Analogy:**
A modem is like a **translator** that converts one language (digital) to another (analog) so communication can happen.

---

## **8. Network Interface Card (NIC)**
### **Definition:**
- A NIC is a hardware component that allows a device to connect to a network.
- Can be wired (Ethernet) or wireless (Wi-Fi).

### **Key Characteristics:**
- Has a unique MAC address for identification.

### **Analogy:**
A NIC is like a **network passport** that gives your device an identity on the network.

---

### **Conclusion**
These devices form the backbone of networking, each playing a specific role in transmitting, securing, and routing data efficiently.

---

# Networking Basics: IP Addresses, LAN, WAN, and Communication

---




