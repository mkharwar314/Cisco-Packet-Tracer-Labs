## Overview

This is my first Cisco Packet Tracer lab. The objective was to understand how devices communicate within the same Local Area Network (LAN) using a Layer 2 switch.

---

## Objective

- Learn the Cisco Packet Tracer interface.
- Connect two PCs using a Cisco 2960 Switch.
- Configure static IPv4 addresses.
- Verify network connectivity using the `ping` command.
- Observe how a switch learns MAC addresses.

---

## Network Topology

```
              +----------------+
              | Cisco 2960     |
              | Layer 2 Switch |
              +----------------+
               |              |
               |              |
           Fa0/1            Fa0/2
               |              |
             PC0            PC1
      192.168.1.10    192.168.1.20
```

---

## Devices Used

|Device|Quantity|
|---|---|
|PC-PT|2|
|Cisco 2960 Switch|1|
|Copper Straight-Through Cable|2|

---

## IP Addressing

|   |   |   |
|---|---|---|
|Device|IP Address|Subnet Mask|
|PC0|192.168.1.10|255.255.255.0|
|PC1|192.168.1.20|255.255.255.0|

Default Gateway: **Not Required** (Both PCs are in the same subnet.)

---

## Configuration Steps

### Step 1 - Add Devices

- Added two **PC-PT** devices.
- Added one **Cisco 2960 Switch**.

### Step 2 - Connect Devices

Connected the devices using **Copper Straight-Through** cables.

- PC0 FastEthernet0 → Switch FastEthernet0/1
- PC1 FastEthernet0 → Switch FastEthernet0/2

### Step 3 - Configure IP Addresses

Configured the following static IP addresses:

**PC0**

- IP Address: 192.168.1.10
- Subnet Mask: 255.255.255.0

**PC1**

- IP Address: 192.168.1.20
- Subnet Mask: 255.255.255.0

### Step 4 - Test Connectivity

From PC0:

```
ping 192.168.1.20
```

From PC1:

```
ping 192.168.1.10
```

Both devices successfully replied, confirming network connectivity.

---

## Switch Verification

Entered the switch CLI and executed:

```
enable
show mac address-table
```

This command displayed the MAC addresses learned by the switch and the interfaces associated with them.

---

## Key Concepts Learned

### Local Area Network (LAN)

A LAN is a network that connects devices within a limited geographical area such as a home, office, or school.

### Switch

A switch operates at **Layer 2 (Data Link Layer)** of the OSI Model. It forwards Ethernet frames based on MAC addresses.

### MAC Address

A MAC address is a unique hardware identifier assigned to every network interface.

Example:

```
00D0.BC7A.1F22
```

### IP Address

An IP address uniquely identifies a device on a network.

Example:

```
192.168.1.10
```

### Subnet Mask

The subnet mask defines which portion of an IP address represents the network and which represents the host.

```
255.255.255.0
```

### Ping

`ping` is a network utility that uses ICMP Echo Request and Echo Reply messages to verify communication between devices.

Example:

```
ping 192.168.1.20
```

---

## Commands Used

|   |   |
|---|---|
|Command|Purpose|
|`enable`|Enter Privileged EXEC mode|
|`show mac address-table`|Display MAC addresses learned by the switch|
|`ping`|Test network connectivity|

---

## Troubleshooting

If communication fails:

- Verify cable connections.
- Ensure all interfaces are active.
- Check IP addresses and subnet masks.
- Confirm both devices are in the same subnet.
- Wait a few seconds for the switch to learn MAC addresses.

---

## Outcome

Successfully established communication between two hosts connected through a Cisco 2960 switch and verified connectivity using ICMP.

---

## Skills Gained

- Cisco Packet Tracer basics
- Static IP configuration
- Switch connectivity
- MAC address learning
- Basic network troubleshooting
- Using the Cisco CLI
- Connectivity testing with `ping`