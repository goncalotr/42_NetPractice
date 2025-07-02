# NetPractice Notes

## Level 1

Repeat IP addresses with different host (last part of the address).

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

## Level 4

## Level 5

## Level 6

## Level 7

## Level 8

## Level 9

## Level 10
