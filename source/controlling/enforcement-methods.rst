Policy Enforcement Methods
==========================

You need a way to control what devices violate network access control policies defined by your organization. Genian NAC provides multiple
layers of enforcement methods from Layer 2 network to agent-based. Depending on your network environment or security level requirements,
you can leverage the following options:

ARP Poisoning
-------------

Controlling network access according to the status of devices in the internal network has always been a challenge. Setting ACLs on routers
to control access between internal networks can provide only a simple access control. 

ACLs can be difficult to enforce in a DHCP environment where devices move frequently or devices that use IP change frequently. Moreover,
access control between multiple devices connected to the same sub-net is the most challenging task and there are not many solutions.

A possible choice is to apply the Port based Access Control function using 802.1x to the switch port to which the device is connected.
However, 802.1x can be expensive, requiring large network configuration changes, such as replacing it with a supported device and replacing
it with the same manufacturer's product for ease of management.

In addition, because all network devices do not support 802.1x, manual configuration is frequently required for each switch port connected.
In an enormous enterprise network, setting an exception or MAC address for 802.1x for each switch port will cause a very large management problem,
which will take a very long time to deploy and manage.

Another option is to use network access control with ARP Poisoning. ARP Poisoning uses the characteristics of the ARP protocol to allow a device
to perform access control by intercepting packets generated by impersonating the other party when the other party obtains the MAC through
an ARP request. 

Genian NAC performs ARP Poisoning using the following procedure.

- The device to be blocked generates an ARP request.
- Respond to the request with the MAC of the network sensor.
- The device to be blocked transmits the packet to the network sensor.
- The network sensor drops according to the access control policy or delivers it to the actual destination.

In order to prevent bypass ARP poisoning by setting static ARP on the blocking target device, bidirectional poisoning function is provided
to control the reply packet generated from the communication target such as gateway, and static ARP setting can be blocked through Agent.

Genian NAC has a built-in RADIUS server for 802.1x and ARP poisoning via network sensor, so users can select and use it according to their
network environment.

Port Mirroring (SPAN)
---------------------

Genian NAC provides access control using Port Mirroring (SPAN in Cisco) as a way to provide access control with minimal network configuration
changes. It monitors newly connected sessions through Mirroring port and blocks connection by transmitting TCP RST or ICMP Destination
Unreachable packet.

To do this, you need to transfer the traffic to Genian NAC using a Port Mirroring supported switch or a Network TAP device.

Genian NAC offers two types of port mirroring modes.

**Global Mirror Sensor**

The Global Mirror Sensor has information on all nodes registered in Genian NAC and can perform information collection and access control.
In general, it is located in the boundary network connected to the Internet, and access control is performed while monitoring
all the internal traffic.

It is recommended to use dedicated high performance hardware separately from network sensor because it controls all nodes while monitoring
all traffic generated in the network.

**Local Mirror Sensor**

Unlike ARP Poisoning, the global mirror sensor can only control packets passing through a specific network segment at that location.
To solve this problem, it is possible to add a mirroring port to the network sensor installed in each end network.
This makes it possible to control connections occurring within the local network.

Since the local mirror sensor is only detected from the network sensor equipment and performs only the control on the existing node,
it can be operated in the hardware of relatively low specification as compared with the global mirror sensor.

802.1x (RADIUS)
---------------

802.1x port based access control is the most ideal access control method that can be applied in enterprise wireless LAN environment.
User-based authentication allows only authorized users to access the network. Also, depending on the compliance status of the device,
it is possible to connect to a specific VLAN or forcibly release a connected connection.

This requires a user device that supports 802.1x, a network access device such as an 802.1x-capable access point or switch,
and a RADIUS server. Genian NAC provides a built-in RADIUS server and provides the following access control functions.

**User Authentication**

802.1x allows access to the network through user-based authentication instead of a weak authentication method such as a shared secret.
For more information about User Authentication, see :doc:`/authentication/enabling-authentication/8021x`

**Quarantine VLAN**

If an 802.1x-capable access point or switch supports the RADIUS *Tunnel-Private-Group-ID* attribute, you can control access to a specific
VLAN based on the device's state. When the RADIUS server transmits the result of user authentication success, this attribute is added
and transmitted, and the access point or switch receives the VLAN ID and assigns the corresponding VLAN ID to the access port.

**Change of Authorization**

If network access needs to be restricted due to device state changes, the device can be terminated using a RADIUS CoA (Change or Authorization).
The disconnected device will try a new connection and connect to the isolated VLAN at this time to securely isolate the device from the network.
To do this, the access point or switch must support the *RFC 5176 - Dynamic Authorization Extensions to RADIUS* standard.

DHCP
----

Genian NAC can allocate or not allocate IP according to IP / MAC policy through built-in DHCP server. This prevents unauthorized devices from
accessing the network or assigns a fixed IP address to devices with a specific MAC address..

Switch Port Block
-----------------

If you use a switch that supports SNMP, Genian NAC will collect SNMP and switch and port information connected to each node.
This information can be used to shut down the switch port according to the security policy of the device. Switch port block is done
via SNMP Write. The switch MUST provide a writable *SNMP MIB-2 ifAdminStatus* property.

Agent Action
------------

Agents provide Network Interface Shutdown, Wireless Connection Block, PC Shutdown and Notification plugins to help control devices directly.


