# NetPractice Summary
NetPractice Project: Core Concepts Summary

This project is a practical introduction to the fundamentals of TCP/IP networking. The goal is to solve a series of puzzles by configuring simulated networks to correctly route traffic from a source to a destination. The following concepts are key to completing all 10 levels.

### 1. IP Address & Subnet Mask: The Foundation

An IP address and a subnet mask work together to define a device's place on a network.

- **IP Address**: A unique address for a single device (e.g., 118.198.14.2). Think of it as a house number.
- **Subnet Mask**: Defines the size of the local network (e.g., 255.255.255.0 or /24). It tells a device what "street" it's on.
- **The Golden Rule**: All devices on the same physical network segment must be configured with the same subnet mask.

### 2. Network & Broadcast Addresses: The Reserved IPs

In any subnet, two addresses can never be assigned to a device:

- **Network Address**: The very first address in the range. It acts as the identifier for the entire network (the "street name").
- **Broadcast Address**: The very last address in the range. It's used to send a message to all devices on the network at once.

### 3. Gateways & Routing: How Networks Communicate

Devices can only talk directly to other devices on their same local network. To communicate with a device on a different network, they need a router.

Default Gateway: When a computer needs to send a packet to a remote address, it sends it to its "default gateway." This is the IP address of the router interface on its own local network.

Routing Table: This is the router's "instruction manual." It contains a list of rules that tell it where to forward packets.

Default Route (0.0.0.0/0): This is the most important rule for this project. It is the "gateway of last resort." It tells the router: "If you don't have a specific rule for this destination, send the packet to this next-hop address."

### 4. Special IP Ranges to Avoid

You cannot use just any IP address. Certain ranges are reserved for special functions.

**Private IP Ranges**:

- 10.0.0.0 to 10.255.255.255 (/8)
- 172.16.0.0 to 172.31.255.255 (/12)
- 192.168.0.0 to 192.168.255.255 (/16)

These are for internal networks ONLY. Internet routers are designed to drop them, so they cannot be used to communicate across the simulated internet.

**Loopback Address (Localhost)**:

- 127.0.0.1 and the entire 127.0.0.0/8 block refer to "this computer." It's used for testing and can never be assigned to a physical network interface.

## General Workflow for Solving a Level

- Analyze the Goal: Identify the source and destination clients.
- Check the Clients: Ensure each client has a valid IP for its subnet and the correct subnet mask.
- Set the Gateway: Point each client's default gateway to the IP of the router on its local network.
- Configure the Routers: Trace the path from source to destination and back again. Add routes to each router's routing table to ensure it knows how to forward packets to the next router in the chain. Usually, this involves setting a default route.
