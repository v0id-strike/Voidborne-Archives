# Overview

## **1. What Is a Network?**

A **network** connects computers so they can talk to each other.
They use:

* Different **shapes** (like star or mesh)
* Different **ways to connect** (like cables or Wi-Fi)
* Different **rules** (called protocols like TCP and UDP)

A **flat network** puts all devices together. It's simple, but not safe—like a house with only one lock.
A **divided network** (with subnets and access rules) is safer—like adding rooms and extra locks.

## **2. Why Splitting Networks Helps (Examples)**

* **Example 1:** If printers and servers are on different networks, it’s like having a fence. Attackers can try to jump it, but it’s harder.
* **Example 2:** Keeping a network map is like having lights outside. If something weird happens (like a printer contacting the internet), you notice.
* **Example 3:** Tools like Snort are like security bushes—they alert you if someone is sneaking around (like scanning ports).

## **3. Mistakes to Avoid**

Hackers or testers may think all devices are in one group (`/24`), but if it’s split into smaller groups (`/25`), they might miss key systems like the Domain Controller.

## **4. How the Internet Works (Mail Example)**

* A **website address** (like `www.hackthebox.eu`) is like a home address.
* **Routers** are like local post offices, and **ISPs** are like the central mail service.
* **DNS** is the address book that finds where to send your message.
  When you go online, your request goes:
  **Your Computer → Router → ISP → DNS → Website → Back to You**  
  ![net_overview](264343691557171.png)

## **5. Tips for Safer Networks**

* Put **web servers** in a special area (DMZ), away from your main network.
* Keep **work computers** on a separate network with firewalls.
* **Network equipment** like routers should be in an admin-only area.
* Give **IP phones** their own space so they work better and stay private.
* Keep **printers** on their own—hackers can use them to steal info.

## **Main Point**

Good network design is like a secure house—with fences, alarms, and lights. It keeps attackers out, makes strange behavior stand out, and protects your most important stuff.
 
---

# Network Types

When learning about computer networks, it's easy to get overwhelmed by the different types and terms. Some are used every day, while others mostly appear in textbooks or exams. This guide separates **common terms** from **book terms** so you can focus on what's important for practical use and still understand the rest.

## **Common Network Types (You’ll See These Often)**

|             **Type**              |                                    **What It Means**                                    |
| --------------------------------- | --------------------------------------------------------------------------------------- |
| **WAN (Wide Area Network)**       | The Internet or any large network that connects many smaller networks.                  |
| **LAN (Local Area Network)**      | Your home or office network—usually wired.                                                |
| **WLAN (Wireless LAN)**           | A LAN that works over Wi-Fi instead of cables.                                          |
| **VPN (Virtual Private Network)** | A secure “tunnel” that connects you to another network as if you were physically there. |

### **WAN – The Big Network**

WAN stands for Wide Area Network and usually means the **Internet**. It connects many LANs together across cities, countries, or even the world. Big organizations may have private WANs too, using special setups like **BGP** routing and public IPs (not private ones like 192.168.x.x).

### **LAN and WLAN – Local Networks**

* **LAN**: A group of computers connected in a small area (like your house). Uses IPs like `192.168.1.x`.
* **WLAN**: A LAN that uses Wi-Fi instead of cables—same idea, just wireless.

You might get a public IP in hotels or schools, but most home networks use **private IP ranges** from RFC1918.

### **VPN – Your Remote Connection**

VPNs help you access a network **securely and privately**, even from far away. There are three types:

* **Site-to-Site VPN**: Connects entire networks together. Common in companies with multiple branches.
* **Remote Access VPN**: Lets your device act like it’s inside a network. Hack The Box uses this to access labs via OpenVPN.
* **SSL VPN**: Works inside your browser. Good for remote access to desktops or apps. Example: Hack The Box’s Pwnbox.

> 🔐 **Split-Tunnel VPNs** only send traffic for certain networks through the VPN. Others go out normally. Great for lab use, but not always safe for companies.

## **Book Terms (Good to Know, Not Used Daily)**

| **Type**                             | **What It Means**                                                      |
| ------------------------------------ | ---------------------------------------------------------------------- |
| **GAN (Global Area Network)**        | Huge networks like the Internet or company-wide global networks.       |
| **MAN (Metropolitan Area Network)**  | Connects LANs in one city or region (like branches of a company).      |
| **PAN/WPAN (Personal Area Network)** | Very small networks around one person (like Bluetooth or USB sharing). |

### **GAN – Global Networks**

GANs connect multiple WANs. Think of **worldwide corporate networks** that aren’t part of the public Internet. They use fast connections like undersea cables or satellites.

### **MAN – City-Level Networks**

MANs link LANs in a specific **city or region**. Companies use MANs to connect offices in different buildings. These are faster than Internet connections and use fiber-optic cables.

### **PAN/WPAN – Personal Networks**

PANs and WPANs are tiny networks around a single person or device. Examples:

* **PAN**: USB cable connection between your laptop and phone.
* **WPAN**: Bluetooth connection for headphones, smartwatches, or IoT devices.
  Smart homes often use WPAN protocols like ZigBee or Z-Wave to control lights, locks, or sensors.

---

# Network Topologies

Network topology refers to the layout and arrangement of various elements—nodes, links, and devices—in a computer network. It defines how different devices in a network are connected and how they communicate with each other. Topologies play a critical role in determining the performance, scalability, reliability, and troubleshooting strategies of a network. They can be classified into two main types: **physical topology**, which shows the actual physical connections, and **logical topology**, which represents the flow of data within the network.

A well-designed network topology enhances data flow efficiency, minimizes network congestion, and ensures high availability and fault tolerance.

## **Types of Network Topologies**

### 1. **Point-to-Point Topology**

The **point-to-point** topology is the simplest form of network configuration, where two devices are directly connected to each other. This topology offers a dedicated connection, ensuring minimal latency and high data security. It is often used in leased line networks and traditional telephony systems. However, it lacks scalability since it only connects two devices.

![topo_p2p](83685467523186.png)

### 2. **Bus Topology**

In a **bus topology**, all devices are connected to a single central cable, called the bus or backbone. Devices share the medium, and data is broadcast to all nodes. Only the intended recipient accepts the data; others ignore it. This topology is cost-effective and simple to implement for small networks but suffers from performance issues as more devices are added. Additionally, a failure in the central cable can bring down the entire network.

![topo_bus](317606709852447.png)

### 3. **Star Topology**

The **star topology** connects all devices to a central hub, switch, or router. This central device manages data traffic and acts as a controller. Star topology is widely used in modern LANs due to its robustness and ease of troubleshooting. If one cable fails, only the corresponding device is affected. However, if the central hub fails, the entire network becomes inoperative.

![topo_star](599126672218303.png)

### 4. **Ring Topology**

In a **ring topology**, each device connects to exactly two other devices, forming a circular data path. Data travels in one direction (or sometimes bidirectionally in dual-ring networks). Token passing is often used to manage access to the network medium. While this topology avoids data collisions and ensures orderly transmission, a single point of failure can disrupt communication unless a redundant ring is in place.

![topo_ring](264007125147707.png)

### 5. **Mesh Topology**

A **mesh topology** offers high redundancy and fault tolerance by connecting every device to every other device. In a **full mesh**, each node has a dedicated link to all other nodes. In a **partial mesh**, some nodes are fully connected, while others are only connected to a few nodes. Mesh topologies are ideal for networks where reliability is crucial, such as in WANs or critical infrastructure systems. However, they are expensive and complex to maintain due to the large number of connections required.

![topo_mesh](571568476148351.png)

### 6. **Tree Topology**

The **tree topology** is a hierarchical structure that combines characteristics of star and bus topologies. It consists of groups of star-configured networks connected to a linear bus backbone. This structure is scalable and well-suited for large organizations with different departments or floors. However, it relies heavily on the backbone; failure in the main line can affect the entire network.

![topo_tree](247926236481904.png)

### 7. **Hybrid Topology**

A **hybrid topology** integrates two or more different types of topologies to leverage their individual advantages. For example, a company might use a star topology within departments and connect them using a bus backbone, forming a tree topology. Hybrid networks offer flexibility, scalability, and performance optimization but can be more complex to design and manage.

![topo_hybrid](415856589617625.png)

### 8. **Daisy Chain Topology**

In a **daisy chain topology**, devices are connected in a linear series, one after another. While simple and cost-effective for small-scale applications, this topology has serious limitations: if one device fails, downstream devices lose connectivity. It is rarely used in modern networks except in specific scenarios like industrial automation.

![topo_daisy-chain](32297751438653.png)

## **Conclusion**

Network topology is a foundational concept in computer networking that shapes the structure and function of a network. Each topology has its strengths and weaknesses, and the choice depends on specific use cases, scalability requirements, and budget constraints. A clear understanding of these topologies allows network designers to build resilient, efficient, and scalable networks that meet organizational or personal needs. As networking technologies evolve, hybrid and mesh topologies are becoming more prevalent due to their robustness and adaptability in complex environments.

---

# Understanding Proxy Servers

In the world of networking and cybersecurity, the term **"proxy"** often comes up in conversations among IT professionals, developers, and even everyday internet users. Despite being a common term, many people misunderstand what a proxy truly is and how it works. This essay aims to clarify the concept of a proxy server, its types, and its real-world applications.

## **What Is a Proxy?**

A **proxy server** acts as an intermediary between a client (such as a computer or browser) and a destination server (such as a website). Instead of connecting directly to the target resource, the client sends its request to the proxy, which then forwards the request on behalf of the client. Once the response is received, the proxy relays the information back to the client.

The word **"proxy"** itself means "on behalf of," which perfectly describes its function: a proxy acts on behalf of the user.

## **Why Use a Proxy?**

Proxies serve many purposes across different industries and user needs:

* **Security**: To filter or monitor traffic for malicious activity.
* **Privacy**: To hide the client’s IP address or location.
* **Access Control**: To block or allow specific websites or services.
* **Performance**: To cache data and reduce bandwidth usage.
* **Testing**: To intercept and modify network traffic for debugging (e.g., Burp Suite in cybersecurity).

## **Types of Proxies**

There are several different types of proxies, each with specific roles and use cases. The most important ones are:

### 1. **Forward Proxy (Dedicated Proxy)**

A forward proxy sits between a client and the internet. It receives requests from internal users and forwards them to external resources. Organizations often use forward proxies to:

* Enforce internet usage policies.
* Monitor and log web activity.
* Prevent access to certain sites.

**Example**: A company blocks social media access by routing all employee traffic through a forward proxy with filtering rules.

![forward_proxy](475515712744141.png)

### 2. **Reverse Proxy**

Unlike a forward proxy, a reverse proxy sits in front of a server, intercepting requests from clients on the internet before they reach the server. It is commonly used for:

* Load balancing across multiple servers.
* Protecting internal servers from direct exposure.
* Acting as a Web Application Firewall (WAF).

**Example**: Services like Cloudflare act as reverse proxies to protect websites from DDoS attacks and malicious users.

![reverse_proxy](25646395741809.png)

### 3. **Transparent Proxy**

A transparent proxy intercepts traffic without requiring any configuration on the client side. Users often do not even realize they are behind a proxy. These are typically used in public Wi-Fi or educational environments to monitor or restrict access.

**Example**: A school uses a transparent proxy to block certain websites for students without modifying any device settings.

## **Proxy vs. VPN**

Many people confuse proxies with VPNs (Virtual Private Networks). While both can hide your IP address and offer privacy, they operate differently:

* A **proxy** usually works at the **application layer** (Layer 7 of the OSI model) and affects specific software, like a browser.
* A **VPN** works at the **network layer**, encrypting all traffic from the device, not just web requests.

In short, VPNs are more secure but also more resource-intensive, while proxies are lightweight and serve specific use cases.

## **Proxies in Cybersecurity**

In cybersecurity, proxies are powerful tools:

* **Burp Suite** is used to intercept and modify HTTP traffic between a browser and a web server.
* **SOCKS or SSH proxies** allow attackers or testers to "pivot" within networks, reaching otherwise unreachable systems.
* **Proxy-aware malware** can bypass filtering systems by adapting to proxy settings.

Understanding how proxies work helps defenders set up better controls and helps attackers test for weaknesses.

## **Conclusion**

Proxy servers are essential tools in modern networking, offering privacy, security, control, and efficiency. Whether used by corporations to secure their networks, by developers to debug applications, or by individuals to access restricted content, proxies play a critical role in managing how devices communicate with each other.

By understanding the different types of proxies and their specific functions, we can better utilize them in both defensive and offensive contexts. A proxy is more than just a way to hide your IP—it’s a strategic point of control in the flow of information across the internet.
