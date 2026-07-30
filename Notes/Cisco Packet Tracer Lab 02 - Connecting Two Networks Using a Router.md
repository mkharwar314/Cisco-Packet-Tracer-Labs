## Overview

In this lab, I learned how to connect two different IP networks using a Cisco 1941 router. The router acts as a Layer 3 device, allowing communication between devices on different subnets.

---

## Objective

- Understand the role of a router in a network.
    
- Configure IP addresses on router interfaces.
    
- Configure IP addresses on end devices.
    
- Set the correct default gateway.
    
- Verify communication between different networks using the `ping` command.
    

---

## Network Topology

```text
                  Cisco 1941 Router
              +-----------------------+
              |                       |
     G0/0     |                       |     G0/1
192.168.1.1   |                       |   192.168.2.1
              +-----------------------+
             /                         \
            /                           \
         PC0                             PC1
192.168.1.10/24                  192.168.2.10/24
Gateway: 192.168.1.1             Gateway: 192.168.2.1
```

---

## Devices Used

|Device|Quantity|
|---|--:|
|Cisco 1941 Router|1|
|PC-PT|2|
|Copper Straight-Through Cable|2|

---

## IP Addressing

|Device|Interface|IP Address|Subnet Mask|
|---|---|---|---|
|Router|G0/0|192.168.1.1|255.255.255.0|
|Router|G0/1|192.168.2.1|255.255.255.0|
|PC0|FastEthernet0|192.168.1.10|255.255.255.0|
|PC1|FastEthernet0|192.168.2.10|255.255.255.0|

---

## Default Gateway

|Device|Default Gateway|
|---|---|
|PC0|192.168.1.1|
|PC1|192.168.2.1|

---

## Router Configuration

### Configure Interface G0/0

```bash
enable
configure terminal

interface gigabitEthernet0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
```

### Configure Interface G0/1

```bash
interface gigabitEthernet0/1
ip address 192.168.2.1 255.255.255.0
no shutdown
exit
```

### Save Configuration

```bash
end
copy running-config startup-config
```

---

## Verify Configuration

Display interface status:

```bash
show ip interface brief
```

Expected result:

- Both interfaces should be **up/up**.
    
- Correct IP addresses should be assigned.
    

---

## Connectivity Test

From **PC0**:

```bash
ping 192.168.2.10
```

From **PC1**:

```bash
ping 192.168.1.10
```

Both tests should succeed, confirming that the router is forwarding traffic between the two networks.

---

## Key Concepts Learned

### Router

A router is a **Layer 3 (Network Layer)** device that forwards packets between different IP networks.

### Network

A network is a group of devices that can communicate with each other.

Examples:

- 192.168.1.0/24
    
- 192.168.2.0/24
    

### Default Gateway

A default gateway is the router's IP address on the local network. It is used whenever a device needs to communicate with another network.

### Routing

Routing is the process of forwarding packets from one network to another using a router.

### IP Address

An IP address uniquely identifies a device on a network.

Example:

```
192.168.1.10
```

### Subnet Mask

A subnet mask separates the network portion of an IP address from the host portion.

```
255.255.255.0
```

---

## Commands Used

|Command|Purpose|
|---|---|
|`enable`|Enter Privileged EXEC mode|
|`configure terminal`|Enter Global Configuration mode|
|`interface gigabitEthernet0/0`|Select an interface|
|`ip address`|Assign an IP address|
|`no shutdown`|Enable an interface|
|`exit`|Return to the previous mode|
|`show ip interface brief`|Display interface status|
|`copy running-config startup-config`|Save the configuration|
|`ping`|Test connectivity|

---

## Troubleshooting

If devices cannot communicate:

- Verify all IP addresses.
    
- Verify the subnet masks.
    
- Verify the default gateway on each PC.
    
- Ensure router interfaces are **up/up**.
    
- Check cable connections.
    
- Confirm `no shutdown` has been applied to each router interface.
    

---

## Skills Gained

- Router configuration
    
- IP addressing
    
- Default gateway configuration
    
- Layer 3 networking
    
- Basic routing
    
- Cisco IOS CLI
    
- Network troubleshooting
    

---

## Outcome

Successfully connected two different IPv4 networks using a Cisco 1941 router and verified end-to-end communication with ICMP (`ping`).

---

## Next Lab

**Lab 03 – Switches and MAC Address Learning**

Topics to be covered:

- Layer 2 Switching
    
- MAC Addresses
    
- MAC Address Table (CAM Table)
    
- Frame Forwarding
    
- Broadcast vs Unicast
    
- `show mac address-table`