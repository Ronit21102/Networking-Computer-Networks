# Networking-Computer-Networks

An **IP address (Internet Protocol address)** is a unique identifier assigned to a device connected to a network that uses the Internet Protocol for communication. It serves two main purposes:  

1. **Identification** – It uniquely identifies a device on a network.  
2. **Location** – It helps in determining the device's geographical location and network address.  

### **Types of IP Addresses**  
1. **IPv4 (Internet Protocol version 4)**  
   - Uses a **32-bit** address format (e.g., `192.168.1.1`).  
   - Supports around **4.3 billion unique addresses**.  
   
2. **IPv6 (Internet Protocol version 6)**  
   - Uses a **128-bit** address format (e.g., `2001:db8::ff00:42:8329`).  
   - Supports **an almost unlimited number of addresses**.  

### **Categories of IP Addresses**  
1. **Public IP** – Assigned by an ISP and used to communicate over the internet.  
2. **Private IP** – Used within a local network (e.g., home, office) and not exposed to the internet.  
3. **Static IP** – Manually assigned and does not change.  
4. **Dynamic IP** – Automatically assigned by a DHCP server and may change over time.  

In a network architecture, especially in the context of cloud computing or virtual private networks (VPNs), subnets can be categorized as either **public** or **private**. Here's a breakdown of what each type typically means:

### Public Subnet
- **Internet Access:** A public subnet is a subnet that is connected to the public internet, meaning resources within it can be accessed from the internet.
- **Usage:** Commonly used for resources that need to be publicly accessible, such as web servers, load balancers, or bastion hosts.
- **Routing:** The public subnet has a route to the internet, typically through an internet gateway in cloud environments like AWS, Azure, or GCP.
- **Security:** Security groups or network access control lists (NACLs) can be used to manage the level of access to resources in the public subnet.

### Private Subnet
- **No Direct Internet Access:** A private subnet does not have direct access to the internet. Resources within this subnet cannot be reached from the internet without going through an intermediary.
- **Usage:** Typically used for sensitive or backend resources, such as databases, application servers, or internal services, which should not be directly exposed to the public.
- **Routing:** Resources in a private subnet may access the internet indirectly, for example, via a **NAT Gateway** or **NAT instance** in the public subnet. This allows private instances to initiate outbound internet traffic while keeping them secure from direct inbound internet traffic.
- **Security:** Like public subnets, private subnets are also protected by firewalls and other security measures to restrict access to sensitive resources.

In many setups, a **hybrid architecture** uses both public and private subnets. For example:
- A **load balancer** or **web server** could be placed in the public subnet to accept requests from users on the internet.
- The application logic or database servers, which do not need to be publicly accessible, would reside in the private subnet, protected from direct internet traffic.

This setup ensures that critical backend systems are secure while still providing access to the necessary frontend systems.
**CIDR** (Classless Inter-Domain Routing) is a method used to allocate IP addresses and routing IP packets. A **CIDR range** is a way of representing an IP address along with its associated network mask. CIDR notation is written as an IP address followed by a slash (`/`) and a number, which represents the number of bits used for the network portion of the address.

### CIDR Notation Breakdown:
- **IP Address**: The starting IP address of the subnet.
- **Slash ("/")**: Separates the IP address from the subnet mask.
- **Subnet Mask (or prefix length)**: The number after the slash indicates how many bits of the IP address are used to represent the network portion. The remaining bits are used for host addresses within the network.

### Example:
`192.168.1.0/24`

- **Network**: `192.168.1.0`
- **Prefix Length**: `/24` (meaning 24 bits are used for the network portion)
  - The subnet mask equivalent is `255.255.255.0`.
  - This means the first 24 bits are used to identify the network, and the last 8 bits are available for host addresses.

### Understanding CIDR Ranges:

1. **/8**: 
   - Network Mask: `255.0.0.0`
   - Range: 16,777,216 IP addresses (e.g., `10.0.0.0/8` is a common private range).
   
2. **/16**:
   - Network Mask: `255.255.0.0`
   - Range: 65,536 IP addresses (e.g., `172.16.0.0/16`).
   
3. **/24**:
   - Network Mask: `255.255.255.0`
   - Range: 256 IP addresses (e.g., `192.168.1.0/24`).
   
4. **/32**:
   - Network Mask: `255.255.255.255`
   - Range: 1 IP address (e.g., `192.168.1.1/32` would refer to a single IP address).

### Subnet Example:

Consider the subnet `192.168.1.0/24`:

- **Network Address**: `192.168.1.0`
- **Usable IP Range**: `192.168.1.1` to `192.168.1.254`
- **Broadcast Address**: `192.168.1.255`

This subnet gives you 254 usable IP addresses for devices (such as servers, computers, etc.).

### Private CIDR Ranges:
For private networks, there are specific CIDR ranges reserved for internal use:

1. **10.0.0.0/8** – This gives a range from `10.0.0.0` to `10.255.255.255`.
2. **172.16.0.0/12** – This gives a range from `172.16.0.0` to `172.31.255.255`.
3. **192.168.0.0/16** – This gives a range from `192.168.0.0` to `192.168.255.255`.

These ranges are typically used for private subnets in networks, especially in cloud environments like AWS, Azure, or GCP.

You're right that **DNS resolution** and **TCP handshake** happen before data flow occurs through the OSI model. Let's break this down and explain the order in which things happen.

### 1. **DNS Resolution (Before Data Flow)**
The **Domain Name System (DNS)** resolution process happens before the actual data transfer begins. This is because DNS is responsible for translating a human-readable domain name (like `www.example.com`) into an **IP address** that computers can understand and use for communication.

Here’s a breakdown of how this works:
- **User Requests a Website:** When you type a website address (URL) into your browser, the browser needs to communicate with that server.
- **DNS Resolution:**
  1. The browser checks its local cache (stored IP addresses) to see if the domain has been resolved recently.
  2. If it’s not found in the cache, it sends a DNS query to the local DNS resolver (usually provided by your ISP or a third-party service).
  3. If the local DNS resolver doesn’t have the answer, it queries other DNS servers (recursive resolution) or authoritative DNS servers until the IP address for the requested domain is found.
  4. Once the IP address is returned, the browser can then use that IP to initiate a connection.

### **DNS is part of the application layer (Layer 7) in the OSI model.** However, it occurs early in the process before a data connection can be established because it provides the necessary address (IP) that will be used in subsequent layers.

---

### 2. **TCP Handshake (Before Data Flow)**
Once DNS resolution provides the correct IP address, the **Transmission Control Protocol (TCP)** handshake occurs next. The TCP handshake is a mechanism used to establish a reliable connection between the client and server before any actual data transmission begins.

The TCP handshake works as follows:
1. **SYN (Synchronize):**
   - The client (usually the browser or application) sends a TCP packet with the SYN flag set, requesting a connection to the server at the resolved IP address.
   - This is an initial packet that starts the connection process.
  
2. **SYN-ACK (Synchronize-Acknowledge):**
   - The server receives the SYN request and responds with its own packet, which contains the SYN and ACK (acknowledgment) flags, indicating that it’s ready to accept the connection.
  
3. **ACK (Acknowledge):**
   - The client receives the SYN-ACK from the server and responds with an ACK packet, confirming that the connection has been established.

At this point, the **TCP connection** is successfully established, and both the client and server can begin communicating by sending and receiving data.

### **The TCP handshake happens at the transport layer (Layer 4) of the OSI model.** It ensures that both the client and server are synchronized, can communicate reliably, and can manage flow control, error checking, and data integrity. The handshake ensures the reliability of the data transfer that follows.

---

### **Data Flow (OSI Model Layers)**
Once the **TCP connection** is established, **data flow** begins, and this happens through the layers of the OSI model:

1. **Application Layer (Layer 7):** This is where the actual data (like an HTTP request, email, or file transfer) is created. For example, in a web request, the browser sends HTTP requests at the application layer.
   
2. **Presentation Layer (Layer 6):** Data is formatted and translated here, if necessary (e.g., encryption, compression).

3. **Session Layer (Layer 5):** Establishes, maintains, and terminates communication sessions between devices.

4. **Transport Layer (Layer 4):** The **TCP protocol** ensures reliable data transfer and flow control. It handles packet sequencing and retransmission in case of errors.

5. **Network Layer (Layer 3):** This is where **IP addressing** (IPv4/IPv6) takes place. The IP address from the DNS resolution comes into play here for routing the data packets.

6. **Data Link Layer (Layer 2):** Frames are created and addressed with MAC addresses, enabling communication over the physical medium.

7. **Physical Layer (Layer 1):** This is the actual transmission of data over the physical network medium (e.g., Ethernet cables, wireless signals).

---

### **Summary:**
- **DNS resolution** (Layer 7 - Application Layer) happens first to resolve a domain name into an IP address.
- Then, the **TCP handshake** (Layer 4 - Transport Layer) takes place to establish a reliable connection.
- After these steps, data flow occurs through the OSI layers (from the application layer down to the physical layer) for actual communication.

While **DNS resolution** and **TCP handshake** happen before data starts flowing through the OSI model layers, they are essential to ensuring the connection and addressing are correctly established so that the data transfer itself can proceed smoothly and reliably.
