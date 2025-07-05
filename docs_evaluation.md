# NetPractice Peer-Evaluation Strategy

This document outlines a step-by-step strategy for the NetPractice defense. The goal is to solve 3 random levels (from 6-10) within the time limit by remaining calm and methodical.

---

### Step 1: The Clean Slate (Reset the Board)

Before you begin configuring, reset the puzzle to a blank state.

1. **Delete all pre-filled, editable fields** (IPs, masks, and routes).
2. **Why?** This prevents you from being misled by incorrect default values and forces you to build the solution logically from the ground up.

### Step 2: Analyze the Goal and Trace the Path

Don't type anything yet. First, understand the problem completely.

1. **Read the Goal:** Identify the **source** client and the **destination** client.
2. **Trace the Forward Path:** Mentally (or on scratch paper) trace the full path a packet must take from source to destination (e.g., `Client A -> Router1 -> Router2 -> Client B`).
3. **Trace the Return Path:** This is critical. Trace the path the reply packet must take to get back. A network only works if communication is two-way.

### Step 3: The "Leaf-to-Root" Configuration Strategy

Start with the devices on the edges of the network (the "leaves") and work your way inwards toward the central routers (the "roots").

1. **Configure the Clients (Leaves):**
	* Assign a **simple, valid IP address** from its subnet (e.g., `.1`, `.2`, etc., avoiding reserved addresses).
	* Assign the correct **Subnet Mask**. All devices on the same local network segment *must* have the same mask.
	* Set the **Default Gateway** to the IP address of the router interface on its local network.

2. **Configure the Routers (Roots):**
	* Assign a valid IP address and the correct subnet mask to **every interface**.
	* For each router, set up the necessary routes. For most levels, the easiest solution is to add a **Default Route (`0.0.0.0/0`)** that points to the IP address of the *next router* in the path.

### Step 4: Verify and Debug

1. Click the **`Check again`** button.
2. If it fails, **read the logs at the bottom of the page.** The logs are your best friend. They will tell you exactly which device the packet failed on (e.g., `on R2: ...`) and usually why (e.g., `packet not for me` means a missing route).
3. Fix the single issue described in the log and repeat.

---

### Key Reminders for Success

* **Check for Typos:** A single wrong number in an IP or mask will break the network.
* **Remember Reserved IPs:** Do not use private IPs (`192.168...`, `10...`, etc.) on "public" internet segments. Never use the loopback address (`127.0.0.1`).
* **Subnet Masks Must Match:** This is the most important rule for devices on the same local network.
