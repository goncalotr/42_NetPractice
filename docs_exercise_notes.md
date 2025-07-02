# NetPractice Exercise Notes

## Level 1

Repeat IP addresses with different host (last part of the address).

An IP address (A.B.C.D) has two parts:
- Network Part: Identifies the "neighborhood."
- Host Part: Identifies a specific "house" within that neighborhood.

## Level 2

### Left Network

Each configured device has:
- An IP Address (its unique house number)
- A Subnet Mask (the map of its neighborhood)
- A Gateway (the address of the router for talking to other neighborhoods)

For devices to be on the same local network and communicate directly, they must have the same subnet mask.

The mask 255.255.255.224 is already set so:

256 - 224 = 32 total addresses with the networks starting at multiples of 32.

- Network 1: starts at .0 -> 192.168.116.0 to 192.168.116.31
- Network 2: starts at .32 -> 192.168.116.32 to 192.168.116.63
- Network 3: starts at .64 -> 192.168.116.64 to 192.168.116.95
- Network 4: starts at .96 -> 192.168.116.96 to 192.168.116.127
- Network 5: starts at .128 -> 192.168.116.128 to 192.168.116.159
- Network 6: starts at .160 -> 192.168.116.160 to 192.168.116.191
- Network 7: starts at .192 -> 192.168.116.192 to 192.168.116.223
- Network 8: starts at .224 -> 192.168.116.224 to 192.168.116.255

Since 192.168.116.222 is already set so we need to respect this range:

|Network Address (Reserved)|Usable IP Range (VALID)|Broadcast Address (Reserved)|
|-|-|-|
|192.168.116.192|.193 to .222|192.168.116.223|

### Right Network

`Mask: /30` CIDR (Classless Inter-Domain Routing), it's simply a shorthand way to write a subnet mask.notation.

The number after the `/` tells us how many bits (out of the 32 total bits in an IP address) are used for the "network" part of the address. The remaining bits are for the "host" part.
- Network bits: 30
- Host bits: 32 - 30 = 2 bits, so we get 2² = 4 addresses in this network.
	- Network Address: The first one, reserved.
	- Host 1: The first usable IP.
	- Host 2: The second usable IP.
	- Broadcast Address: The last one, reserved.

The "long form" of a /30 mask is 255.255.255.252 (already set)

Here is a quick reference for common CIDR notations:
| CIDR | Long Mask | Block Size | Usable IPs |
| :--- | :--- | :--- | :--- |
| /24 | 255.255.255.0 | 256 | 254 |
| /25 | 255.255.255.128 | 128 | 126 |
| /26 | 255.255.255.192 | 64 | 62 |
| /27 | 255.255.255.224 | 32 | 30 |
| /30 | 255.255.255.252 | 4 | 2 |

So with 4 Block Size we get

- 192.168.1.0 to 192.168.1.3
- 192.168.1.4 to 192.168.1.7
- 192.168.1.8 to 192.168.1.11
- 192.168.1.12 to 192.168.1.15
- ...and so on, in blocks of 4, all the way up to .255.

127.0.0.1 (already asigned wrongly in the exercise) is wrong because 127.x.x. block of addresses is reserved for a special purpose called **loopback**.
Example: 127.0.0.1 is known by the hostname localhost.

## Level 3

Select the same masks for all interfaces.
For 255.255.255.128 (already assigned and locked) we have the following range of IPs:
Network Address (Reserved)|Usable IP Range (VALID)|Broadcast Address (Reserved)
-|-|-
.0|.1 to .126|.127
.128|.129 to .254|.255

Since 104.198.162.125 is also already assigned and locked for one of the interfaces we need to select values for the last octet (Host Part) of the IP from .1 to .126 excluding .125.

## Level 4

A /23 mask is written in long form as 255.255.254.0. Sometimes called a **supernet**.

A /23 mask effectively "merges" two adjacent /24 networks into one single, larger network. It doubles the number of available addresses.

The total block size is 2^9 = 512 addresses. This means the network spans across 512 addresses, or two blocks of 256.
- The network range would be from 10.0.4.0 all the way to 10.0.5.255.

Network Address (Reserved)|Usable IP Range (VALID)|Broadcast Address (Reserved)
-|-|-
10.0.4.0|10.0.4.1 to 10.0.5.254|10.0.5.255

### About CIDR (Classless Inter-Domain Routing).

Case 1: The Familiar /24 (Mask 255.255.255.0)
- Total bits: 32
- The /24 tells us the Network Part is the first 24 bits.
- This leaves 32 - 24 = **8 bits** for the Host Part.
- How many different house numbers can you make with 8 bits? 2⁸ = 256.
- This is why a /24 network has 256 total addresses.

Case 2: The New /23 (Mask 255.255.254.0)
- Total bits: 32
- The /23 tells us the Network Part is the first 23 bits.
- This leaves 32 - 23 = **9 bits** for the Host Part.
- How many different house numbers can you make with 9 bits? 2⁹ = 512.
- This is why a /23 network has 512 total addresses.

/24 Mask:
11111111.11111111.11111111.00000000
(24 ones, then 8 zeroes)

/23 Mask:
11111111.11111111.1111111**0**.00000000
(23 ones, then 9 zeroes)

## Level 5

Theme: routing

We need to define the default gateway for each device this time.
- The Client Device: A house.
- The Subnet: The neighborhood.
- The Router: The post office.
- The Default Gateway: The address of the post office (123 Main Street).

>The gateway address we configure on a client is ALWAYS the IP address of the router interface that is on the SAME LOCAL NETWORK as the client.

Destination => Gateway
- Left Side: 0.0.0.0 (This means "for any destination") - actually we need to use `default` here.
- Right Side: The IP address of the router interface on the same network as Host A.

Term|What it is|Meaning
-|-|-
0.0.0.0|The technical standard. It's the actual address and mask (/0) that networking hardware uses to define the default route.|"For any destination IP address..."
default|The user-friendly keyword. It's a shortcut provided by some systems' command lines or interfaces for ease of use.|"This is the default route."

## Level 6

We can not use the the default route as the destination of the internet.

The Internet device looks at this address and asks itself two questions:
- WHAT network am I trying to reach? (This is the Left Side of the route)
- WHO do I give the packet to to get it there? (This is the Right Side of the route)

Left side of routes box
- The Internet device cannot have a default route. It needs a specific rule to find your network.
- You must tell it the exact "name" of the network it's looking for.
- The name of a network is its Network Address + Subnet Mask.

We check the IP of the host: 84.35.205.227 and it's IP mask: 255.255.255.128, this mask is equivalent to /27.

This results in: 84.35.205.227/27 but this is a **Host Address** so to convert it to the **Network Address**: 84.35.205.224/27

To do: Check if there is an error on the simulator. Loop detected? Accepts the host and network addresses.

## Level 7

Create at least 3 subnets for each network.

## Level 8

The routing table on the router 1 (R1) represents the traffic, Egress Traffic and Upstream Traffic, if the traffic is internal to the network or goes to the internet.

We need to define it using the special "catch-all" destination address: 0.0.0.0/0. This literally means "any IP address with any subnet mask."

Internet: 163.161.194.0/26 (locked)
Packets IPs: 163.14.136.0 to 163.14.136.63

/28 = 255.255.255.240

## Level 9

/18 = 255.255.192.0

11111111.11111111.11000000.00000000

79.105.152.18 does not belong to the network 79.105.152.0/18

79.105.152.18 range is 79.105.128.1 to 79.105.191.254
resulting in 79.105.128.0/18

## Level 10
