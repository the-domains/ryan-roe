---
inFeed: true
description: 'Thread: Network+'
dateModified: '2018-07-20T05:37:00.702Z'
datePublished: '2018-07-20T05:37:01.245Z'
title: Modern Ethernet
author: []
publisher: {}
via: {}
hasPage: true
sourcePath: _posts/2018-07-20-chapter-5-modern-ethernet.md
starred: false
datePublishedOriginal: '2018-07-20T05:33:49.651Z'
url: chapter-5-modern-ethernet/index.html
_type: Article

---
# Modern Ethernet
![](https://the-grid-user-content.s3-us-west-2.amazonaws.com/76a0fc61-2da8-42ff-afd4-49f47df1ef14.jpg)

[Thread: Network+][0]

July 20, 2018

---

Modern Ethernet, Switches, and Duplex

* 100BaseT == 100BaseTX
* 100 Mbps
* 1024 nodes per hub
* 100 meters between hub and node
* Cat 5e or better
* 100BaseF == 100BaseFX
* Fiberoptic version
* Multimode
* Two Kilometers
* Moving from hubs to switches
* Switch monitors traffic going in and out associating respective MAC addresses
* Hub just sends it to all the other ports, Switch sends it to only 1 port
* If its a broadcast: then it gets sent out to all other ports
* Switch Benefits over Hub:
* Dramatically improves bandwidth of network
* Switch allows individual computers to talk at same speed instead of sharing speeds because of point to point connections
* Duplex Communication
* Half Duplex: Like a trucker radio: Send or Receive but cant do both at the same time
* 10BaseT
* Full Duplex: Talk and listen at the same time
* Starts with 100BaseT

---

Connecting Switches

* Patch Cables
* Regular: wired the same on both ends, aka straight through cable
* Crossover: wired TIA 568A to TIA 568B meaning
* Sends go to receives and receives go to the sends
* Can't tell by looking at it
* Plug into any port on switches to get them to work together
* Uplink Port
* PreCrossovered port so you can use straight cord
* Auto Sensing Ports
* Modern Switches

---

Gigabit Ethernet and 10 Gb Ethernet Obj 5.4 Given a scenario, deploy the appropriate wired connectivity standard 

* Four Gb Standards:
* 1000BaseCX
* Copper based standard but uses a coaxiall called twinax with a whole 25 meters
* 1000BaseSX
* Multimode Fiber optic up to 500 meter
* 1000BaseLX
* single-mode fiber up to 5kms
* 1000BaseT
* Cat6 UTP, 100 meters
* 10 GB Ethernet Standards:
* 10GBaseT
* Cat6 - 55m
* Cat6a - 100m
* 10GBaseSR corresponding 10GBase SW designed to work on an old type of network
* multimode fiber 26m to 400m
* 10GBaseLR or LW
* single-mode
* 1310 nm (size of
* 10 km
* 10GBaseER or EW
* single-mode
* 1550 nm
* 40 km
* **Must know the corresponding names and lengths**

---

Switch Backbones Obj 2.6 Given a scenario, configure a switch using proper features 

* Backbone
* HighSpeed switch in center that only connects to other switches that then connect to lower speed networks
* Gigabit Interface Converter (GBIC), interchangeable devices designed to switch in and out of switches
* Bridge Loop caused by improper cabling
* Spanning tree protocol (STP) prevents the network from going down

---

Quiz: 4

1. 10GBaseFW is not a fiber optic standard
2. 1000BaseCX uses the shortes distance between hub and node
3. Crossover cables, uplink ports, and autosensiong increase the switching capacity in a network
4. GBIC (Gigabit Interface Converter) provides a flexible interface for different gigabit fiber-optic standards on a switch

[0]: http://ryanroe.io/thread-network