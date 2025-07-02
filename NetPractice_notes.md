# NetPractice Notes

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

## Level 6

## Level 7

## Level 8

## Level 9

## Level 10
