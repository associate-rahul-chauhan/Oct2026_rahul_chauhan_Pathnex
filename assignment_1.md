# 🌐 Networking Basics

## Questions

1. What do you understand by **IP**?
2. What is the **OSI Layer**?
3. What is **DNS**?

---

# 1. IP — Internet Protocol

**IP** stands for **Internet Protocol**.

An **IP address** is a **logical address** assigned to a device or network interface. It helps devices identify and communicate with each other over a network.

> **Note:** IP is not a physical address. A **MAC address** is associated with the network hardware, while an IP address is a logical network address.

There are two major versions of IP:

- **IPv4**
- **IPv6**

---

## IPv4

**IPv4** = Internet Protocol Version 4

IPv4 uses a **32-bit address** and is divided into **4 groups**, called octets.

Example:

```text
123.34.34.45
```

Each octet can contain a value from:

```text
0 → 255
```

So an IPv4 address looks like:

```text
XXX.XXX.XXX.XXX
```

Since IPv4 uses 32 bits, it has approximately:

```text
2³² = 4.3 billion
```

possible addresses.

Therefore, the number of IPv4 addresses is limited.

---

## IPv6

**IPv6** = Internet Protocol Version 6

IPv6 uses a **128-bit address**.

Example:

```text
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```

IPv6 uses hexadecimal values separated by `:`.

Because IPv6 uses 128 bits, it provides a very large number of possible addresses:

```text
2¹²⁸
```

This is much larger than the IPv4 address space.

---

# 2. Public IP and Private IP

IP addresses can also be classified by their **scope**.

## Public IP

A **public IP address** is used for communication over the public Internet.

Example:

```text
54.252.251.146
```

A public IP can be assigned to an Internet-facing device such as a router or cloud server.

Example:

```text
Internet
    ↓
Public IP
    ↓
Router
   / \
Laptop Phone
```

---

## Private IP

A **private IP address** is used inside a private network.

For example, devices connected to the same home router may have:

```text
Laptop → 192.168.1.10
Phone  → 192.168.1.11
```

The router connects the private network to the Internet.

Common private IPv4 ranges are:

```text
10.0.0.0        → 10.255.255.255
172.16.0.0      → 172.31.255.255
192.168.0.0     → 192.168.255.255
```

---

# 3. Static IP and Dynamic IP

IP addresses can also be classified based on whether they are expected to change.

## Dynamic IP

A **dynamic IP** can change over time.

It is commonly assigned automatically using **DHCP**.

Example:

```text
Today  → 192.168.1.10
Later  → 192.168.1.15
```

---

## Static IP

A **static IP** is intended to remain fixed.

Example:

```text
Server → 192.168.1.100
```

The server can continue using the same IP address until the configuration is changed.

---

# 4. OSI Layer

**OSI** stands for:

> **Open Systems Interconnection**

The OSI model is a **7-layer model** used to understand how data travels between devices over a network.

There are **7 OSI layers**:

```text
7. Application
6. Presentation
5. Session
4. Transport
3. Network
2. Data Link
1. Physical
```

### Memory Trick

**All People Seem To Need Data Processing**

```text
A → Application
P → Presentation
S → Session
T → Transport
N → Network
D → Data Link
P → Physical
```

> The OSI model is commonly represented from **Layer 7 at the top to Layer 1 at the bottom**. During actual communication, data moves down the layers on the sending side and up the layers on the receiving side.

---

## Simple Example

Suppose you open:

```text
google.com
```

The communication can be understood approximately as:

```text
Application
    ↓
HTTPS / DNS
    ↓
Transport
    ↓
TCP / UDP
    ↓
Network
    ↓
IP
    ↓
Data Link
    ↓
MAC
    ↓
Physical
    ↓
Wi-Fi / Cable
```

### Important OSI Layers to Remember

```text
Application → HTTP, HTTPS, DNS, SSH
Transport   → TCP, UDP, Ports
Network     → IP, Routing
Data Link   → MAC, Ethernet, Switch
Physical    → Cable, Radio/Wi-Fi, Signals
```

---

# 5. DNS

**DNS** stands for:

> **Domain Name System**

DNS converts a **human-readable domain name** into an IP address.

For example:

```text
google.com
     ↓
    DNS
     ↓
IP Address
```

Humans find it easier to remember:

```text
google.com
```

rather than an IP address such as:

```text
142.250.x.x
```

So DNS works somewhat like the **phonebook of the Internet**.

### Simple Flow

```text
You type:

google.com
     ↓
DNS lookup
     ↓
IP address
     ↓
Your computer connects to the server
```

---

# 🧠 Quick Revision

```text
IP
↓
Logical address used for network communication

IPv4
↓
32-bit
4 octets
0–255 per octet

IPv6
↓
128-bit
Much larger address space

Public IP
↓
Used for Internet-facing communication

Private IP
↓
Used inside private networks

Dynamic IP
↓
Can change

Static IP
↓
Intended to remain fixed

OSI
↓
7-layer networking model

DNS
↓
Domain name → IP address
```
