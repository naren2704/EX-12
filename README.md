# PERFORM A CASE STUDY ABOUT THE DIFFERENT ROUTING ALGORITHMS TO SELECT THE NETWORK PATH WITH ITS OPTIMUM AND ECONOMICAL DURING DATA TRANSFER.
# EXP: 12
# DATE: 25.05.2023
# I. LINK STATE ROUTING
# AIM:
To study the link state routing protocol in NS Simulator.
# Link State routing
Routing is the process of selecting best paths in a network. In the past, the term routing was also used
to mean forwarding network traffic among networks. However this latter function is much better
described as simply forwarding. Routing is performed for many kinds of networks, including the
telephone network (circuit switching), electronic data networks (such as the Internet), and
transportation networks. This article is concerned primarily with routing in electronic data networks
using packet switching technology.
In packet switching networks, routing directs packet forwarding (the transit of logically addressed
network packets from their source toward their ultimate destination) through intermediate nodes.
Intermediate nodes are typically network hardware devices such as routers, bridges, gateways,
firewalls, or switches. General-purpose computers can also forward packets and perform routing,
though they are not specialized hardware and may suffer from limited performance. The routing
process usually directs forwarding on the basis of routing tables which maintain a record of the routes
to various network destinations. Thus, constructing routing tables, which are held in the router's
memory, is very important for efficient routing. Most routing algorithms use only one network path at
a time. Multipath routing techniques enable the use of multiple alternative paths.
In case of overlapping/equal routes, the following elements are considered in order to decide which
routes get installed into the routing table (sorted by priority):
1. Prefix-Length: where longer subnet masks are preferred (independent of whether it is within a
routing protocol or over different routing protocol)
2. Metric: where a lower metric/cost is preferred (only valid within one and the same routing
protocol)
3. Administrative distance: where a lower distance is preferred (only valid between different
routing protocols)
Routing, in a more narrow sense of the term, is often contrasted with bridging in its assumption that
network addresses are structured and that similar addresses imply proximity within the network.
Structured addresses allow a single routing table entry to represent the route to a group of devices. In
large networks, structured addressing (routing, in the narrow sense) outperforms unstructured
addressing (bridging). Routing has become the dominant form of addressing on the Internet. Bridging
is still widely used within localized environments.
# II. FLOODING
Flooding s a simple routing algorithm in which every incoming packet is sent through every outgoing
link except the one it arrived on. Flooding is used in bridging and in systems such as Usenet and peerto-peer file sharing and as part of some routing protocols, including OSPF, DVMRP, and those used

in ad-hoc wireless networks. There are generally two types of flooding available, Uncontrolled
Flooding and Controlled Flooding. Uncontrolled Flooding is the fatal law of flooding. All nodes have
neighbours and route packets indefinitely. More than two neighbours creates a broadcast storm.
Controlled Flooding has its own two algorithms to make it reliable, SNCF (Sequence Number
Controlled Flooding) and RPF (Reverse Path Flooding). In SNCF, the node attaches its own address
and sequence number to the packet, since every node has a memory of addresses and sequence
numbers. If it receives a packet in memory, it drops it immediately while in RPF, the node will only
send the packet forward. If it is received from the next node, it sends it back to the sender.
# Algorithm
There are several variants of flooding algorithm. Most work roughly as follows:
1. Each node acts as both a transmitter and a receiver.
2. Each node tries to forward every message to every one of its neighbours except the source
node.
This results in every message eventually being delivered to all reachable parts of the network.
Algorithms may need to be more complex than this, since, in some case, precautions have to be taken
to avoid wasted duplicate deliveries and infinite loops, and to allow messages to eventually expire
from the system. A variant of flooding called selective flooding partially addresses these issues by
only sending packets to routers in the same direction. In selective flooding the routers don't send
every incoming packet on every line but only on those lines which are going approximately in the
right direction.

# Advantages
1. if a packet can be delivered, it will (probably multiple times).
2. Since flooding naturally utilizes every path through the network, it will also use the shortest
path.
3. This algorithm is very simple to implement.
# Disadvantages
1. Flooding can be costly in terms of wasted bandwidth. While a message may only have one
destination it has to be sent to every host. In the case of a ping flood or a denial of service attack, it
can be harmful to the reliability of a computer network.
2. Messages can become duplicated in the network further increasing the load on the networks
bandwidth as well as requiring an increase in processing complexity to disregard duplicate messages.
3. Duplicate packets may circulate forever, unless certain precautions are taken:
• Use a hop count or a time to live count and include it with each packet. This value should take
into account the number of nodes that a packet may have to pass through on the way to its destination.
• Have each node keep track of every packet seen and only forward each packet once
4. Enforce a network topology without loops
# III. DISTANCE VECTOR
In computer communication theory relating to packet-switched networks, a distance-vector
routing protocol is one of the two major classes of routing protocols, the other major class being the
link-state protocol. Distance-vector routing protocols use the Bellman–Ford algorithm, Ford–
Fulkerson algorithm, or DUAL FSM (in the case of Cisco Systems's protocols) to calculate paths.
A distance-vector routing protocol requires that a router informs its neighbors of topology

changes periodically. Compared to link-state protocols, which require a router to inform all the nodes
in a network of topology changes, distance-vector routing protocols have less computational
complexity and message overhead.
The term distance vector refers to the fact that the protocol manipulates vectors (arrays) of
distances to other nodes in the network. The vector distance algorithm was the original ARPANET
routing algorithm and was also used in the internet under the name of RIP (Routing Information
Protocol).
Examples of distance-vector routing protocols include RIPv1 and RIPv2 and IGRP.
# Method

Routers using distance-vector protocol do not have knowledge of the entire path to a destination.
Instead they use two methods:
1. Direction in which router or exit interface a packet should be forwarded.
2. Distance from its destination
Distance-vector protocols are based on calculating the direction and distance to any link in a network.
"Direction" usually means the next hop address and the exit interface. "Distance" is a measure of the
cost to reach a certain node. The least cost route between any two nodes is the route with minimum
distance. Each node maintains a vector (table) of minimum distance to every node. The cost of
reaching a destination is calculated using various route metrics. RIP uses the hop count of the
destination whereas IGRP takes into account other information such as node delay and available
bandwidth.
Updates are performed periodically in a distance-vector protocol where all or part of a router's routing
table is sent to all its neighbors that are configured to use the same distance-vector routing protocol.
RIP supports cross-platform distance vector routing whereas IGRP is a Cisco Systems proprietary
distance vector routing protocol. Once a router has this information it is able to amend its own routing
table to reflect the changes and then inform its neighbors of the changes. This process has been
described as ‗routing by rumor‘ because routers are relying on the information they receive from
other routers and cannot determine if the information is actually valid and true. There are a number of
features which can be used to help with instability and inaccurate routing information.
EGP and BGP are not pure distance-vector routing protocols because a distance-vector protocol
calculates routes based only on link costs whereas in BGP, for example, the local route preference
value takes priority over the link cost.
# Count-to-infinity problem
The Bellman–Ford algorithm does not prevent routing loops from happening and suffers from the
count-to-infinity problem. The core of the count-to-infinity problem is that if A tells B that it has a
path somewhere, there is no way for B to know if the path has B as a part of it. To see the problem
clearly, imagine a subnet connected like A–B–C–D–E–F, and let the metric between the routers be
"number of jumps". Now suppose that A is taken offline. In the vector-update- process B notices that
the route to A, which was distance 1, is down – B does not receive the vector update from A. The
problem is, B also gets an update from C, and C is still not aware of the fact that A is down – so it
tells B that A is only two jumps from C (C to B to A), which is false. This slowly propagates through
the network until it reaches infinity (in which case the algorithm corrects itself, due to the relaxation
property of Bellman–Ford). 


