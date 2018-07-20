---
inFeed: false
description: 'Thread: Network+'
dateModified: '2018-07-20T05:36:27.161Z'
datePublished: '2018-07-20T05:36:27.847Z'
title: Ethernet Basics
author: []
publisher: {}
via: {}
hasPage: true
sourcePath: _posts/2018-07-20-ethernet-basics.md
starred: false
datePublishedOriginal: '2018-07-20T05:24:06.560Z'
url: ethernet-basics/index.html
_type: Blurb

---
# Ethernet Basics
![](https://the-grid-user-content.s3-us-west-2.amazonaws.com/03469e00-52c5-42c5-994d-3090058706fc.jpg)

[Thread: Network+][0]

July 20, 2018

---

Introduction to Ethernet

* Ethernet
* IEEE got together in 1980 created a standard:
* **IEEE 802.3** "Ethernet": cables, speed, frame, communications protocol of network in 1980
* IEEE 802.3a-ai etc. changed many times but ethernet framework stayed the same
* IEEE: Institute of Electrical and Electronics Engineers
* CRC (Cyclical Redundancy Check) is known as Frame Check Sequence when referring to Ethernet
* frame has not changed so backwards compatibility is available
* Standard Nomenclature or **Types of Ethernet**
* 10Base5
* 10 = speed in Mb/sec
* Base or Broad:
* Broadband: same cable running multiple conversations at once
* Base: entire bandwidth is used for one conversation at a time
* 5 = before switches, the length of the cable you plugged into (500 meters)
* Now you see base T which means switch in the middle

---

Early Ethernet

* Segmented Ethernet (no switch, one big cable in ceiling)
* 10Base5 is thick and isn't used but the important part is up in the ceiling and "dropped" whenever a computer wants to connect. Vampire switch transceiver
* CSMA/CD (Carrier Sense Multiple Access/Collision Detection)
* MA: multiple computers can talk on the same cable
* CS: computer must listen to see if other computers are talking
* Frame goes both directions and when it hits end of cable it bounces back
* Terminator Resistors solved this
* CD: if collision, wait a random amount of ms before re-transmitting
* 10Base2
* 185 meter segments which allows for a smaller cable
* BNC connector or T connector with terminating resistor
* Up to 30 devices

---

10BaseT - Daddy of Internet

* IBM invented TokenRing in 1980 which competed with ethernet because all computers connected to a box which solved the problem that if one computer on segmented ethernet went down whole internet went down
* Shrunk down the one large bus to one box using UTP called 10BaseT
* Specs
* 10 Mb/sec
* 100 Meters max between Hub and Node
* Max 1024 nodes per switch
* Cat 3 or better UTP

---

Quiz 3

1. 10BaseT uses 10 Mbps using UTP
2. CSMA/CD avoids transmission collisions
3. Weakest part of early ethernet: one break disable network
4. 10BaseT supports 100 meters between hub and node

[0]: http://ryanroe.io/thread-network/