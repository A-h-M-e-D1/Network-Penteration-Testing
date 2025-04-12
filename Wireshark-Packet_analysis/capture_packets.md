# Wireshark - Working with Capture Files and Filters

### 1. **Working with Capture Files:**
#### 1.1. **Saving and Exporting Files:**
- Users can save capture data in `.pcap` files, and export data to formats such as plain text, **CSV**, and **XML** via "File > Export."
- In the "Save As" dialog, you can choose to:
  - **Save all packets**.
  - **Save marked packets**.
  - **Save specific packets** using the **Display Filter**.

#### 1.2. **Merging Capture Files:**
- Multiple capture files can be merged into one file for comparing or combining separately captured traffic streams. To do this, go to "File > Merge" and select the files.

#### 1.3. **Finding Packets:**
- Packets can be located using the "Find Packet" dialog (Ctrl+F), based on:
  - **Display Filter**.
  - **Hex value**.
  - **String**.

#### 1.4. **Marking Packets:**
- You can mark packets of interest to make them easier to find later by using "Mark Packet" or **Ctrl+M**. 
- **Shift+Ctrl+N** to navigate between marked packets.

#### 1.5. **Printing Packets:**
- Captured data can be printed via **File > Print**, with options to select the packet range and print format.

---

### 2. **Setting Time Display Formats and References:**
#### 2.1. **Time Display Formats:**
- The time format can be adjusted from **View > Time Display Format**, with options like seconds since the beginning of capture or date and time of day.

#### 2.2. **Packet Time Referencing:**
- Using "Edit > Set Time Reference," you can set a specific packet as a time reference, and all subsequent packets' timestamps will be relative to this packet.

---

### 3. **Capture Settings:**
#### 3.1. **Capture Options:**
- **Network Interface**: Select the network interface to begin capturing.
- **Capture Filter**: Set filters to capture specific types of traffic.
- **File Size**: Set file sizes for capture files or configure automatic stopping at a certain number of packets.

---

### 4. **Using Filters in Wireshark:**
#### 4.1. **Capture Filters:**
- Applied during the capture process to determine which packets will be saved to the capture file.
- Filters use **BPF** (Berkeley Packet Filter) like:
  - **host 172.16.16.149**: Capture traffic from/to a specific IP address.
  - **port 80**: Capture traffic over port 80 (HTTP).
  - **tcp**: Capture only TCP traffic.

#### 4.2. **Display Filters:**
- Applied after the capture has been completed to view a subset of the captured packets.
- Filters provide a flexible way to review data.

#### Examples of Display Filters:
- **tcp.flags.syn == 1**: Show packets containing the SYN flag (used in TCP connections).
- **ip.src == 192.168.1.1**: Show packets sent from a specific IP address.
- **http.request.method == "GET"**: Show HTTP GET requests.
- **frame.time > "2024-01-01 12:00:00"**: Show packets after a certain time.

---

### 5. **Examples of Filters with Additional Use Cases:**
#### Examples of Display Filters in Wireshark:

**Filter to display packets over port 443 (HTTPS):**

    tcp.port == 443 


**Filter to display packets from/to a specific IP address:**

    ip.addr == 192.168.0.1 

**Filter to display packets containing the RST flag (to close a TCP connection):**

    tcp.flags.reset == 1

**Filter to display HTTP POST requests:**

    http.request.method == "POST"

**Filter to display packets with a specific port number:**

    tcp.port == 80

**Filter to display packets containing DNS protocol data:**

    dns

**Filter to display packets after a specific time:**

    frame.time > "2024-04-01 12:00:00"

**Filter to display packets with a specific size:**

    frame.len == 1500

**Filter to display packets containing ICMP protocol (usually for ping testing):**

    icmp

**Filter to display packets containing HTTP protocol data:**

    http
