---

# 📌 Packet Analysis & Network Basics  

## **1️⃣ Understanding Packet Analysis**  
Packet analysis is the process of capturing and examining network traffic to understand how data flows, troubleshoot issues, or detect security threats.  
To analyze packets effectively, you need to understand how **computers communicate** and how **network protocols** function.  

---

## **2️⃣ What is a Protocol?**  
A **protocol** is a set of rules that define how two computers communicate, similar to how human languages have grammar and structure.  

### **🔹 Common Network Protocols:**  
| Protocol | Description |
|----------|------------|
| **TCP (Transmission Control Protocol)** | Ensures reliable data transmission |
| **IP (Internet Protocol)** | Provides logical addressing and routing |
| **ARP (Address Resolution Protocol)** | Maps IP addresses to MAC addresses |
| **DHCP (Dynamic Host Configuration Protocol)** | Assigns IP addresses dynamically |

---

## **3️⃣ The Seven-Layer OSI Model**  
The **OSI Model** divides network communication into **seven distinct layers**, each with a specific role.  

### **📌 Layers of the OSI Model**  
| Layer | Description | Protocols Used |
|--------|------------|----------------|
| **Application (L7)** | The only layer visible to users, provides the interface for network activities. | **HTTP, HTTPS, SMTP, FTP, Telnet** |
| **Presentation (L6)** | Converts data formats for Layer 7, handles encryption/decryption. | **ASCII, MPEG, JPEG, MIDI** |
| **Session (L5)** | Manages sessions between two computers (establishing, managing, terminating). Handles duplex/half-duplex connections. | **NetBIOS, SAP, SDP, NWLink** |
| **Transport (L4)** | Provides reliable data transport, flow control, segmentation, error correction. | **TCP, UDP, SPX** |
| **Network (L3)** | Handles logical addressing and packet routing between networks. | **IP, IPX, DHCP** |
| **Data Link (L2)** | Identifies devices using MAC addresses, ensures reliable transmission over the physical medium. | **Ethernet, Token Ring, FDDI, AppleTalk** |
| **Physical (L1)** | Defines hardware (cabling, switches, network adapters). Manages electrical signaling and connection establishment. | **Hubs, Cables, Network Interfaces** |

---

## **4️⃣ Packet Analysis Using Wireshark**
### **📌 Capturing OSI Layer Traffic in Wireshark**  
| OSI Layer | Wireshark Filter Example |
|-----------|--------------------------|
| **Application (L7)** | `http` to capture HTTP traffic |
| **Transport (L4)** | `tcp.port == 80` for HTTP traffic, `udp` for UDP packets |
| **Network (L3)** | `ip.addr == 192.168.x.x` to filter packets from a specific IP |
| **Data Link (L2)** | `eth.addr == aa:bb:cc:dd:ee:ff` to track a specific MAC address |

### **🔹 Practical Example: Capturing HTTP Packets**
1. Open **Wireshark**.  
2. Select the network interface (e.g., Wi-Fi or Ethernet).  
3. Apply the filter:  
   ```plaintext
   http
   ```
4. Start capturing packets.  
5. Visit any website using HTTP (e.g., `http://example.com`).  
6. Analyze the captured packets and inspect the **GET/POST requests**.  

---

## **5️⃣ Traffic Classification**
### **📌 Broadcast (One-to-All)**
- Data is sent to **all devices** on the network, even if they don’t need it.  
- Commonly used in **ARP Requests & DHCP Discovery**.  
- **Disadvantage**: Consumes bandwidth as it reaches every device.  

#### **🛠 Example:**  
When a device wants to find the MAC address of another device, it sends an **ARP Request** as a **Broadcast** to all devices.  

🔹 **Wireshark Filter for Broadcast Packets:**  
```plaintext
eth.dst == ff:ff:ff:ff:ff:ff
```

---

### **📌 Multicast (One-to-Many)**
- Data is sent from **one sender to multiple specific recipients** instead of all devices.  
- Used in applications like **video streaming, network updates (OSPF, VRRP)**.  

#### **🛠 Example:**  
When using **OSPF (Open Shortest Path First)** to update routing tables, data is sent to **a group of routers only** rather than all devices.  

🔹 **Wireshark Filter for Multicast Packets:**  
```plaintext
ip.dst == 224.0.0.0/4
```

---

### **📌 Unicast (One-to-One)**
- Data is sent from **one sender to one specific recipient**.  
- Used in **web browsing, email sending, file downloads**.  

#### **🛠 Example:**  
When you visit **http://example.com**, data is transmitted as **Unicast** between your device and the server.  

🔹 **Wireshark Filter for Unicast Traffic:**  
```plaintext
ip.dst == <target_device_ip>
```

