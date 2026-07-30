## Overview

In this lab, I explored how a Cisco 2960 switch learns MAC addresses and forwards Ethernet frames. I configured two PCs on the same Local Area Network (LAN), verified connectivity using the `ping` command, and examined the switch's MAC Address Table (CAM Table).

---

# Objective

- Understand the role of a Layer 2 switch.
    
- Learn how switches build the MAC Address Table (CAM Table).
    
- Configure two hosts on the same network.
    
- Verify connectivity using `ping`.
    
- View learned MAC addresses using Cisco IOS commands.
    

---

# Network Topology

```text
                Cisco 2960 Switch
           +-------------------------+
           |                         |
      Fa0/1|                         |Fa0/2
           |                         |
         PC0                       PC1
    192.168.10.10             192.168.10.20
```

---

# Devices Used

|Device|Quantity|
|---|--:|
|Cisco 2960 Switch|1|
|PC-PT|2|
|Copper Straight-Through Cable|2|

---

# IP Addressing

|Device|Interface|IP Address|Subnet Mask|Default Gateway|
|---|---|---|---|---|
|PC0|FastEthernet0|192.168.10.10|255.255.255.0|Not Required|
|PC1|FastEthernet0|192.168.10.20|255.255.255.0|Not Required|

> Since both PCs are in the same subnet, a default gateway is not required.

---

# Configuration Steps

## Step 1 - Build the Topology

- Add one Cisco 2960 switch.
    
- Add two PC-PT devices.
    
- Connect each PC to the switch using Copper Straight-Through cables.
    

Connections:

- PC0 → Switch FastEthernet0/1
    
- PC1 → Switch FastEthernet0/2
    

---

## Step 2 - Configure the PCs

### PC0

- IP Address: `192.168.10.10`
    
- Subnet Mask: `255.255.255.0`
    

### PC1

- IP Address: `192.168.10.20`
    
- Subnet Mask: `255.255.255.0`
    

---

## Step 3 - Test Connectivity

Open the Command Prompt on PC0 and execute:

```bash
ping 192.168.10.20
```

The successful replies confirm that both hosts can communicate through the switch.

---

## Step 4 - View the MAC Address Table

Open the switch CLI.

Enter Privileged EXEC mode:

```bash
enable
```

Display the MAC Address Table:

```bash
show mac address-table
```

Example Output:

```text
Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
1       00D0.BC11.2233    Dynamic     Fa0/1
1       00D0.BC44.5566    Dynamic     Fa0/2
```

The switch dynamically learns the MAC addresses of connected devices and associates each address with the correct switch port.

---

## Step 5 - Verify Interface Status

```bash
show interfaces status
```

This command displays the operational status of each switch interface.

---

# Commands Used

|Command|Description|
|---|---|
|`enable`|Enter Privileged EXEC mode|
|`show mac address-table`|Display learned MAC addresses|
|`show interfaces status`|Display interface status|
|`show running-config`|Display current switch configuration|
|`show interfaces FastEthernet0/1`|Display interface information|
|`ping`|Verify network connectivity|

---

# Key Concepts

## Layer 2 Switch

A Layer 2 switch forwards Ethernet frames using MAC addresses. It operates at the **Data Link Layer (Layer 2)** of the OSI Model.

---

## MAC Address

A MAC (Media Access Control) address is a unique hardware address assigned to every network interface card (NIC).

Example:

```text
00:D0:BC:11:22:33
```

---

## CAM (MAC Address) Table

The Content Addressable Memory (CAM) table stores the MAC addresses learned by the switch.

Each entry contains:

- VLAN
    
- MAC Address
    
- Entry Type
    
- Switch Port
    

The switch uses this information to forward frames efficiently.

---

## MAC Learning Process

1. A device sends an Ethernet frame.
    
2. The switch records the **source MAC address**.
    
3. The switch associates that MAC address with the incoming port.
    
4. If the destination MAC address is known, the frame is forwarded only to that port.
    
5. If the destination MAC address is unknown, the switch floods the frame to all ports except the incoming port.
    

---

## Broadcast Frame

A broadcast frame is sent to every device within the same VLAN.

Example MAC Address:

```text
FF:FF:FF:FF:FF:FF
```

---

## Unicast Frame

A unicast frame is sent from one device to one specific destination device.

---

## Unknown Unicast

If the destination MAC address is not present in the CAM table, the switch temporarily floods the frame until it learns the destination.

---

# Troubleshooting

If communication fails:

- Verify IP addresses.
    
- Verify subnet masks.
    
- Check cable connections.
    
- Ensure switch ports are active.
    
- Confirm the PCs are connected to the correct switch ports.
    
- Verify learned MAC addresses using:
    

```bash
show mac address-table
```

---

# Skills Learned

- Cisco 2960 switch operation
    
- Layer 2 switching
    
- MAC Address learning
    
- CAM Table inspection
    
- Basic network verification
    
- Cisco IOS CLI commands
    
- Connectivity testing with `ping`
    

---

# Outcome

Successfully configured two hosts on the same LAN, verified communication, and observed how a Cisco switch dynamically learns MAC addresses and forwards Ethernet frames.

---