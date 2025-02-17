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
