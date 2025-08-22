# How a Web Request Travels Through OSI Layers

Let's follow the journey of what happens when you type "www.google.com" in your browser, from initial checks through the OSI layers.

## Pre-OSI Steps (Browser Process)

1. **Browser Cache Check**
   - Browser first checks its local DNS cache
   - Checks browser's local cache for previously visited content
   - Checks if there's a valid cached version of google.com

2. **Operating System Cache Check**
   - If not found in browser cache, checks OS DNS resolver cache
   - Checks hosts file (/etc/hosts or C:\Windows\System32\drivers\etc\hosts)

3. **DNS Resolution Process**
   - If not in local caches, asks DNS resolver
   - DNS resolver queries root servers
   - Receives IP address for www.google.com

4. **TCP 3-Way Handshake**
   ```
   Client                Server
     |   1. SYN          |
     |------------------>|
     |   2. SYN-ACK     |
     |<-----------------|
     |   3. ACK         |
     |------------------>|
   ```
   - Step 1: Client sends SYN (Synchronize) packet
   - Step 2: Server responds with SYN-ACK packet
   - Step 3: Client acknowledges with ACK packet
   - Connection established!

## OSI Layer Journey

### 7. Application Layer
1. After connection establishment, HTTP GET request is prepared
2. Browser formats the request headers and body
3. DNS resolution information is used from earlier cache checks

### 6. Presentation Layer
1. Data is formatted into HTTP protocol format
2. If using HTTPS, SSL/TLS encryption is applied
3. Text is converted to standard ASCII/Unicode format

### 5. Session Layer
1. Session is established between your browser and web server
2. Session parameters are negotiated
3. Session tracking is initiated

### 4. Transport Layer
1. TCP connection is established (3-way handshake)
2. Data is broken into smaller segments
3. Each segment gets a sequence number
4. Port numbers are assigned (e.g., HTTP port 80 or HTTPS port 443)

### 3. Network Layer
1. IP addresses are added to each packet
   - Source IP (your computer)
   - Destination IP (Google's server)
2. Best route is determined using routing protocols
3. Packets are routed through the internet

### 2. Data Link Layer
1. Packets are converted to frames
2. MAC addresses are added to frames
   - Source MAC (your network card)
   - Destination MAC (next hop router)
3. Error detection bits are added

### 1. Physical Layer
1. Frames are converted to bits (1s and 0s)
2. Bits are transmitted through physical medium
   - Through your ethernet cable or WiFi signals
   - Through various network cables and fiber optics

## Response Flow (Bottom to Top)

The response from Google's servers follows the same layers in reverse:

1. **Physical Layer**: Bits are received
2. **Data Link Layer**: Frames are reassembled and checked for errors
3. **Network Layer**: Packets are reassembled and routed
4. **Transport Layer**: Segments are ordered and reassembled
5. **Session Layer**: Data is synced between sessions
6. **Presentation Layer**: Data is decrypted and formatted
7. **Application Layer**: Web page is displayed in your browser

## Key Points to Remember

- Each layer adds its own header information to the data
- The process is known as encapsulation (going down) and de-encapsulation (going up)
- If any layer fails, error handling occurs at that specific layer
- Security can be implemented at multiple layers (e.g., HTTPS at Presentation, Firewalls at Network)

## Visual Example of Encapsulation

```
Application Data
[HTTP Header + Application Data]           <- Application Layer
[SSL + HTTP Header + Application Data]     <- Presentation Layer
[Session info + SSL + HTTP + Data]         <- Session Layer
[TCP Header + Session + SSL + HTTP + Data] <- Transport Layer
[IP Header + TCP + Session + SSL + HTTP + Data] <- Network Layer
[Frame Header + IP + TCP + ... + Data + Frame Trailer] <- Data Link Layer
01001010101... <- Physical Layer
```
