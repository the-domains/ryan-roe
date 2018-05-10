---
inFeed: true
description: 'Thread: Network+'
dateModified: '2018-05-10T04:42:14.091Z'
datePublished: '2018-05-10T04:42:15.275Z'
title: Network Models
author: []
publisher: {}
via: {}
hasPage: true
sourcePath: _posts/2018-05-10-network-models.md
starred: false
datePublishedOriginal: '2018-05-10T04:30:34.390Z'
url: network-models/index.html
_type: Article

---
# Network Models

Thread: Network+
![](https://the-grid-user-content.s3-us-west-2.amazonaws.com/e51ebd17-8481-47ad-b540-74523b01df6f.jpg)

* Network Interface Card (NIC)
  * plugged into interface computers called a hub
  * back in time
  * where LAN came from

* Data is sent in Packets aka Frames
  * Binary
  * Up to 1500 bytes long
* Network Card creates the frame and shoots it out to the network or incoming data is wiped by the Network card

---

* HUB is a Repeater that sends frames to every computer in the network

* Media Access Control (MAC) Address is how the end computer determines if the information is meant for them or not 
* MACs are hard coded into every device that connects to the internet

    C:\Users\vkpatel>ipconfigipconfig /all **in order to see the MAC address**

* ipconfig
  * command prompt for displaying network information
  * ip information
  * have to type /all for MAC address
  * look for the network card that is working
  * physical address: in hexadecimal (each character represents 4 binary characters)

* MAC Addresses will be 48 bits.
  * broken up into 6 parts each consisting of two characters in hex

* OEM (Original Equipment Manufacturer): first three parts are owned by manufacturer
* Unique ID: it puts a different set of numbers on every network owned by the manufacturer. Every NIC has unique MAC address

Frame now consists of:

* Data
* Sender MAC
* Receiver MAC
* Cyclical Redundancy Check (CRC)

NICs use MAC addresses to determine whether they should process the frame.

---

### Broadcast vs Unicast

* Unicast situation

* Addressed to single device on network
* Exact MAC address matches NIC
* Keeps return MAC just in case

* Broadcast

* Destination MAC: all F's ex: FF-FF-FF-FF-FF-FF
* sends the data into the computer because it does not know the MAC address and may be asking for it.
* Broadcast Domain: every device connected

---

### Hubs vs Switches

* Hub
  * Repeater: computer sends frame, makes copies, then makes copies for each connected port

* Switch
  * Smart Hub: Keeps track of MAC addresses hooked to it based on ports
  * Port lined up to MAC
  * Checks destination MAC then sends it only to that computer

---

### Intro to IP Addressing

IP Addressing is a type of Logical Addressing

These are not fixed like MAC

32.44.17.231 \*\*change: IP is more like 227.0.0.1 or 192.168.1.255

First 3 numbers are assigned to every computer in the network

Network ID

Router

Usually have built in switch

Changes the frame to include the IP address of the computer they want to talk to

**Frames** now have:

* Data
* Source MAC
* Destination MAC
* CRC
* Source IP
* Destination IP

* Data
* Source MAC
* Destination MAC
* CRC
* Source IP
* Destination IP

* Default gateway

* Sender attaches its MAC and Router MAC to the IP Packet (Data, source & sender IP) which strips the  MAC info and user a... routing table to put the receivers MAC address

* Routing Table

* Tells where to send data within network

---

Packets and Ports

* Adding Port numbers to the Packet (frame)

* First is port to where its going to go
* Second is Port \# of sender so it knows where it needs to be sent back

* Port 80

* Web page

* Well-known Ports \*\*need to memorize popular reserved ports\*\*

* First 1024 port numbers

* Reserved
* Need to know these

* Can go up to 64,000

* TCP  (Transmission Control Protocol)

* Connection oriented conversation between two computers to make sure the data gets to you whole complete and in order
* Sequence Number: allows reassembly of packets
* Acknowledgement

* UDP (User Datagram Protocol)

* Not connection oriented (connectionless) also not always sent in order

---

Models

* OSI 7-Layer Model
* TCP/IP Model

---

* OSI 7-Layer Model

1. Physical: Cables
2. Data Link: Anything that works with MAC address: NIC, switches
3. Network Layer: Logical address (ip addresses), routers
4. Transport Layer: Dissassembles packets, assembles packets to make sure they get to the other system in good order
5. Session: Type of connection: Video? Email? File? How the connectivity works.
6. Presentation Layer: Old, converts data into a format applications could read
7. Applications: The smarts in the applications that make them network aware

1. API as a definition of the smarts that are built into an application that make them network aware

* TCP Model

1. Network Interface layer: Physical cables, MAC, NIC (hardware except routers)
2. Internet: Ip Addresses, Routers
3. Transport: Assembly, dissassembly, TCP vs UDP whatever it takes to get data from one application to the next
4. Application:  combined 5-7 of OSI, email? ftp? looks at applications as applications: email, ftp, telnet, things with distinct port numbers

---

OSI & TCP/IP Layer Functionality

* Example of reading in Frame to data applications can use

OSI LayerTCP/IP LayerSituationCheckExecution1 Physical and 2 Data Link1 Network InterfaceNIC receives ethernet frameVerify that is for me. Checks frame check sequenceStrips off mac address and stores the mac address because we may want to send frame back out3 Network Layer2 Internet LayerNow we have IP packet. Deal with IP AddressesIs IP for me? If yes..Pulls IP info off, and keeps the info to send packet back4 Transport Layer3 Transport LayerNow we have TCP segment. Could be web page or http request, or big chunksIf data is big, chop it up into chunks or reassemble using sequencing number (ex: 3/100)Take sequencing \# off. 5 Session: Connect server to client on remote system (not anymore, apps are smart), 6 Presentation: if data was received but not in right form (deprecated), 7 Application Layers: Smarts to interface to network4 Application LayerLeft with port numbers and dataLook at port numbers and determine where it goes (Ex: Port 80 for web server)Send data up to application

---

Quiz 1:

1. Switches use Mac addresses forward data packets
2. 1500 Bytes is maximum size of frame
3. Data packets are contained within frame during transmission
4. IP Packet is found in frame