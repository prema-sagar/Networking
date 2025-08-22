# Understanding IP Addresses

## What is an IP Address?

An IP (Internet Protocol) address is a unique numerical identifier assigned to each device connected to a computer network that uses the Internet Protocol for communication. It serves two main functions:
- Host or network interface identification
- Location addressing

## IP Address Versions

### IPv4
- 32-bit number
- Format: Four octets (0-255) separated by dots
- Example: 192.168.1.1
- Total possible addresses: ~4.3 billion (2^32)

### IPv6
- 128-bit number
- Format: Eight groups of four hexadecimal digits
- Example: 2001:0db8:85a3:0000:0000:8a2e:0370:7334
- Total possible addresses: 2^128 (vastly more than IPv4)

## Types of IP Addresses

### Public IP Addresses
- Globally unique addresses
- Directly accessible over the internet
- Assigned by Internet Service Providers (ISPs)
- Must be purchased or leased

### Private IP Addresses
- Used within private networks
- Cannot be routed over the internet
- Free to use
- Defined in RFC 1918

#### Private IP Ranges:
- Class A: 10.0.0.0 to 10.255.255.255
- Class B: 172.16.0.0 to 172.31.255.255
- Class C: 192.168.0.0 to 192.168.255.255

## IP Address Classes

### Class A
- First bit: 0
- Range: 1.0.0.0 to 126.255.255.255
- Default subnet mask: 255.0.0.0 (/8)
- First octet range: 1-126
- Available networks: 126
- Hosts per network: 16,777,214

### Class B
- First bits: 10
- Range: 128.0.0.0 to 191.255.255.255
- Default subnet mask: 255.255.0.0 (/16)
- First octet range: 128-191
- Available networks: 16,384
- Hosts per network: 65,534

### Class C
- First bits: 110
- Range: 192.0.0.0 to 223.255.255.255
- Default subnet mask: 255.255.255.0 (/24)
- First octet range: 192-223
- Available networks: 2,097,152
- Hosts per network: 254

### Class D (Multicast)
- First bits: 1110
- Range: 224.0.0.0 to 239.255.255.255
- Used for multicasting

### Class E (Reserved)
- First bits: 1111
- Range: 240.0.0.0 to 255.255.255.255
- Reserved for experimental use

## Subnetting

### What is Subnetting?
Subnetting is the practice of dividing a network into smaller network segments, each with its own range of IP addresses.

### Subnet Mask
- Used to divide IP addresses into network and host portions
- Consists of 1s (network portion) and 0s (host portion)
- Common subnet masks:
  - /24 (255.255.255.0)
  - /16 (255.255.0.0)
  - /8 (255.0.0.0)

### CIDR Notation
- Classless Inter-Domain Routing
- Format: IP address/prefix length
- Example: 192.168.1.0/24
- Prefix length indicates number of 1s in subnet mask

### Subnetting Example

Given network: 192.168.1.0/24
To create 4 subnets:

1. **First Subnet**
   - Network: 192.168.1.0/26
   - Range: 192.168.1.0 - 192.168.1.63
   - Usable: 192.168.1.1 - 192.168.1.62

2. **Second Subnet**
   - Network: 192.168.1.64/26
   - Range: 192.168.1.64 - 192.168.1.127
   - Usable: 192.168.1.65 - 192.168.1.126

3. **Third Subnet**
   - Network: 192.168.1.128/26
   - Range: 192.168.1.128 - 192.168.1.191
   - Usable: 192.168.1.129 - 192.168.1.190

4. **Fourth Subnet**
   - Network: 192.168.1.192/26
   - Range: 192.168.1.192 - 192.168.1.255
   - Usable: 192.168.1.193 - 192.168.1.254

### Special IP Addresses

1. **Network Address**
   - First address in subnet
   - Host portion all 0s
   - Cannot be assigned to devices

2. **Broadcast Address**
   - Last address in subnet
   - Host portion all 1s
   - Used for broadcast communication

3. **Localhost**
   - 127.0.0.1
   - Used for loopback testing

## Subnet Calculator Formula

To calculate number of available hosts:
- Available hosts = 2^h - 2
  (where h is number of host bits)
- Subtract 2 for network and broadcast addresses

Example:
- /24 subnet has 8 host bits
- 2^8 - 2 = 254 usable hosts

## Best Practices

1. **Network Planning**
   - Plan for future growth
   - Use appropriate subnet sizes
   - Document IP assignments

2. **IP Assignment**
   - Use DHCP for dynamic assignment
   - Reserve static IPs for servers
   - Maintain IP inventory

3. **Security**
   - Implement network segmentation
   - Use private IP addresses internally
   - Configure proper access controls

## Understanding Ports

### What is a Port?
A port is a logical endpoint for communication in a network. While IP addresses identify devices on a network, ports identify specific services or applications running on those devices. Think of an IP address as a building address, and ports as different room numbers within that building.

### Port Numbers
- Range: 0-65535 (16 bits)
- Well-known ports: 0-1023
- Registered ports: 1024-49151
- Dynamic/Private ports: 49152-65535

### Why Are Ports Used?
1. **Multiple Services**: Allows multiple applications to use the network simultaneously
2. **Service Identification**: Helps identify specific services running on a device
3. **Traffic Management**: Enables proper routing of data to correct applications
4. **Security**: Allows for port-based security measures

### Common Port Numbers

#### Well-Known Ports
- **Port 20/21**: FTP (File Transfer Protocol)
  - 20: Data transfer
  - 21: Control commands
- **Port 22**: SSH (Secure Shell)
- **Port 23**: Telnet
- **Port 25**: SMTP (Simple Mail Transfer Protocol)
- **Port 53**: DNS (Domain Name System)
- **Port 80**: HTTP (Hypertext Transfer Protocol)
- **Port 443**: HTTPS (HTTP Secure)
- **Port 110**: POP3 (Post Office Protocol v3)
- **Port 143**: IMAP (Internet Message Access Protocol)
- **Port 3389**: RDP (Remote Desktop Protocol)

#### Database Ports
- **Port 1433**: Microsoft SQL Server
- **Port 3306**: MySQL
- **Port 5432**: PostgreSQL
- **Port 27017**: MongoDB

#### Application Ports
- **Port 3000**: Common development server port
- **Port 8080**: Alternative HTTP port
- **Port 27015**: Source game servers

### Port Usage Examples

1. **Web Browsing**
   ```
   http://example.com -> IP:80
   https://example.com -> IP:443
   ```

2. **Email**
   ```
   Sending: SMTP -> Port 25
   Receiving: POP3 -> Port 110 or IMAP -> Port 143
   ```

3. **Database Connection**
   ```
   MySQL: mysql://localhost:3306
   PostgreSQL: postgresql://localhost:5432
   ```

### Best Practices for Port Usage

1. **Security**
   - Keep unnecessary ports closed
   - Use non-standard ports for sensitive services
   - Implement port scanning detection
   - Use firewalls to control port access

2. **Configuration**
   - Document port assignments
   - Avoid port conflicts
   - Use standard ports when possible
   - Configure proper port forwarding

3. **Monitoring**
   - Regular port scanning
   - Monitor port traffic
   - Log port access attempts
   - Track open ports

### Common Port-Related Commands

1. **Check Open Ports (Windows)**
   ```powershell
   netstat -an
   ```

2. **Check Open Ports (Linux)**
   ```bash
   netstat -tuln
   # or
   ss -tuln
   ```

3. **Test Port Connection**
   ```bash
   telnet server-ip port
   # or
   nc -zv server-ip port
   ```
