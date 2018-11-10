---
layout: post
title:  "Telematik"
ref: telematik
date:   2018-10-16 07:00:00 +0100
categories: master
excerpt: Die Vorlesung behandelt Protokolle, Architekturen, sowie Verfahren und Algorithmen, die u.a. im Internet für die Wegewahl und für das Zustandekommen einer zuverlässigen Ende-zu-Ende-Verbindung zum Einsatz kommen. Neben verschiedenen Medienzuteilungsverfahren in lokalen Netzen werden auch weitere Kommunikationssysteme, wie z.B. das leitungsvermittelte ISDN behandelt. Die Teilnehmer sollten ebenfalls verstanden haben, welche Möglichkeiten zur Verwaltung und Administration von Netzen zur Verfügung stehen.
lang: de
tags: lecture
---
<div style="background-color: #EAEFF4; border: 1px solid #b5aeb1; border-radius: 3px;  padding: 10px; margin-right: 10px">
    <strong>Vorlesung:</strong> <a href="https://campus.studium.kit.edu/ev/G6hOdkEyRGaMJ98tdLHvGw">Telematik</a>, Stammmodul, 6 ECTS <br>
    <strong>Dozent:</strong> Prof. Dr. Zitterbart <br>
   <strong>ILIAS:</strong> <a href="https://ilias.studium.kit.edu/goto_produktiv_crs_880989.html">https://ilias.studium.kit.edu/goto_produktiv_crs_880989.html</a> <br>   
   <strong>Vorlesungswebsite:</strong> <a href="http://telematics.tm.kit.edu/tm.php">http://telematics.tm.kit.edu/tm.php</a> <br>   
   <strong>Klausur:</strong> 21.2.2019 11:00 - 12:30 Uhr <br>
   <strong>Einordnung:</strong> Vertiefungsfach "Telematik", Profil "Datenintensives Rechnen" <br>
</div>

## Organisatorisches

### Vorlesungen
- **17.10.2018**: Organisatorisches und Foliensatz 1-1 bis 2-20
- **18.10.2018**: Foliensatz 2-20 bis 2-63
- **24.10.2018**: Foliensatz 2-64 bis 3-12 und Besprechung Homework 1
- **25.10.2018**: Foliensatz 3-13 bis 3-53
- **31.10.2018**: Foliensatz 3-54 bis 3-100
- **07.11.2018**: Foliensatz 3-101 bis 3-135
- **08.11.2018**: Foliensatz 3-135 bis 3-154, 4-1 bis 4-

### Material
Das Material der Vorlesung besteht aus:  
- **Folien**: Folien werden im ILIAS hochgeladen, Passwort wurde in der Vorlesung mitgeteilt
- **Übungsblättern**  
Inhaltlich werden Grundlagen der Rechnernetze vorausgesetzt, Inhaltlich geht es um Technologien des Internets;
Kein spezielles Bucht auf dem VL aufbaut, da gute Standardwerke. Folien auf Englisch um Inhalt einheitlich zu
halten; VL wird durch Pingo, Kahoot und Homework interaktiv gestaltet; 
Ende der Vorlesung voraussichtlich bereits ca. 16./17.1.2019

### Übungen
Homework wird jeweils in der zweiten Hälfte der VL besprochen, das Blatt dazu gibt es in der Regele "bisschen" früher;
teilweise mit Programmieraufgaben, keine komplette Musterlösung nur Ergebnis.

### Klausur
Klausur ist schriftlich; am 21.2.2019 von 11:00 bis 12:30; Fragen in Deutsch, Antworten auf Deutsch und Englisch möglich

## Vorlesungsinhalt
### Introduction
**Internet:** largest system build by mankind; Critical Infrastructure e.g. critical infrastructures (water, electricity) depend on the internet;  
rapid development (less than 50 years):
- early 60s: vision of networked computers
- 1969: first packet-switched network with four nodes
- early 70s: architectural concept for interconnection (TCP, IP)
- since 90s: commercialization
- since around 2005: software-defined networks
- today: ubiquituous, critical infrastructure
 
**Internet of Things (Robots):** Sensors collecting data about us and environment (Eyes and Ears); Processors, Storage and Cloud processing data (Brain); 
Actuators affecting environment (Hands and Feet);

### Router
#### Basic Functionalities
**Intermediate Systems**: Forward data from input ports to output ports; Forwarding task of data path; may operate on different layers:
- *Layer 1* (Physical Layer, Bitübertragungsschicht) - *Hubs* (schicken an alle Anschlussports)
- *Layer 2* (Data Link Layer, Sicherungsschicht) - *Bridges* (entscheiden anhand MAC-Adressen)
- *Layer 3* (Network Layer, Vermittlungsschicht) - *Routers* (entscheiden anhand IP-Adressen)

**Routing**: determines path that packet follows; part of control path; requires routing algorithms and protocols;

**Forwarding table**: enthält mindestens pro Eintrag Netzadresse/Subnetzmaske (bzw. Prefixlänge), next hop, Metrik (Gewichtung, Präferenz des Weges);
Informationen welcher Value im Paket, welchem Link entspricht;

**Router**: main task: lookup in forwading table, forwart data from input to output ports; goals: forwarding in line speed (Geschw. des Links soll eingehalten werden), short queues
(da sonst hohe Latenz → schlecht bei z.B. VoIP kommt es sonst zu Verzögerungen), small tables (da sonst Speicher teuer)

**Forwarding**: part of data path; Forwarding table part of control path;  
Incoming data →  *IP-Processing*: check Headers of IP Packet (version number, valid header length, checksum); check TTL (decrement TTL); recalculate checksum) 
→ *Lookup* (determine output port for packet, Fragmentation (?), Handle IP options (?)) → *Classification* (Priorization, differentiated treatment of packets) → (Queue) → Outgoing Data

#### Challenge: Line Speed
bandwidth demand increases (32% 2015-2016); 250 Tbit/s in 2016 → Link capacity has to increase  
memory is **not** keeping up with Moore's law; network bandwidth doubles every 17-18 months; DRAM/CPU bandwidth doubles every 26-27 months;
Router needs to keep up with line-speed for **all packet sizes**

*Example:* 1 Gbit/s line-speed, 1500 byte packets: $ t_{packet} = \frac  {12000 bit}{10⁹ \frac {bit}{s}} = 12 \mu s $;
 higher requirements for smaller packets; forwarding decision is overhead for every single packet  

Regarding TCP two types of segments:
- TCP segments that transport data e.b. 1500 bytes (Ethernet)
- TCP that are purely acknowledgements (min. 40 byte)
→ e.g only 3,2ns for 40 byte in a 100 Gbit/s environment  
Problem: Small packets are quite common, 50% of IPv4 packets smaller than 100 bytes

**Router Types**:
- *Core router:* used by service provider; large amound of aggregated traffic; high speed, reliability is essential (fast lookup, redundancy to increade reliability); 
cost secondary issue (1-3 Mio. € per router) 
- *Enterprise router:* connect end systems in companies, universities,...; provide connectivity to many end systems; support VLANs, firewalls,...; low cost per post, large number
of ports, ease of maintenance
- *Edge router (access router):* at *edge* of service provider; connectivity for customer (home, small business); support PPTP, IPsec, VPNs

#### Forwarding Table Lookup
**Prefix**: Identifies block of addresses; continous blocks of addresses per output port good 
→ does not require a separate entry for each IP address (Scalability)

*Ende Vorlesung vom 17.10.2018*

**Longest Prefix Matching**: Multiple prefixes matching in the forwarding table to given destination? Select most specific prefix 
(highest number of matching bits) → *longest prefix matching*; Challenge: Lookup in Line-Speed (can be long because TTL is decreased → checksum recalculated),
 Different approaches in software:

**Efficient Data Structures for Longest Prefix Matching**  
Requirements: fast lookup; low memory; fast updates (route changes occur frequently, data structure should support >> 100 updates/second)  
Variables: N = number of prefixes; W = length of prefix (W=32 for IPv4); k = length of stride

**Binary Trie**: Trie = tree-based data structure to store and search prefix information; Idea: bits in prefix to tell algorithm what branch to take; (vgl. Abb. 02-27)
- *Lookup speed* $ O(W) $, maximum of one node per bit in prefix 
- *Memory requirement* $ O(N*W) $, prefixes stored as linked list starting from root, every prefix can have upt do W nodes
- *Updates* $ O(W) $  
Lookup speed with memory access time $ 10ns $ for 100 byte packets $ 2,5 Gbit/s $ → Optimization: Path Compression, Multibit Tries,...

**Path Compression**: one-child node waste memory → nothing stored, not required for branch decision → eliminate sequences → path compression; additional information 
of next examined index; (vgl. Abb. 02-31)
- *Lookup speed* $ O(W) $, with no one-child nodes, number of nodes to search = length of prefix
- *Memory requirement* $ O(N) $, N entries for leaf nodes, N-1 for internal nodes → max 2N-1 entries
- *Updates* $ O(W) $  

**Multibit Trie**: match multiple bits at same time; reduce number of memory accesses; fixed strides multibit tries (strides = number of bits) 
have same strides on each level, different level can have different strides; Problem: prefixes do not always match with strides → expand prefix to next available stride
(0* expands to 01* and 00*); choose prefix that is most specific; (vgl. Abb. 02-36)
- *Lookup speed* $ O(W/k) $
- *Memory requirement* $ O(2^k NW/k) $, max path length W/k, path composed of one level subtrees with $ 2^k $
- *Updates* $ O(W/k + 2^k ) $, search time $ O(W/k) $, modification $ 2^{k-1} $ entries

**Hash Tables**: goal: improve lookup speed → $ O(1) $, BUT: longest prefix match only with hash table does **not** work; use additional hash table instead (stores result of trie lookup);
check for each IP packet if entry in hash table exists if not → lookup; goof if addresses show "locality" characteristics

**Longest Prefix Matching in Hardware**  
Idea: Read information with single memory access, use destination IP as RAM address; waste of memory; required memor size grows expoentially with size of addresses;  

**Content-Addressable Memory (CAM)**: *RAM:* address → data; *CAM:* data → address (search all stored entries in single clock cycle, 
very fast address lookups with address as search input); compare search input data with stored entries, priority encoder searches "first" match
- *Binary CAM:* static lookups
- *Ternary CAM:* with *Don't Care* State; allows longest prefix matching, prefixes stored sorted by length; very fast lookups; BUT: hight energy demands
(parallelization, every core required for every lookup), high cost/ low density, requires strict ordering → severe scalability limitations

#### Router Architecture
**Generic Router Architecture**
- *Network Interfaces*: Access to attached networks; Layer 1, Layer 2 functionalities; basic functions of IP
- *Routing Processor*: Routing protocol, management functionality
- *Switch fabric*: "Backplane", realizes internal forwarding  
Conflicting Design goals: high efficiency (line speed, low delay) vs. low cost; Blocking (e.g. packets arriving at the same time, going to same port)

**Frage: TODO, irgendwas mit Blocking???** Schicht 3. Schicht 2 nicht, da IP-Paket bereits aus Schicht 2 "herausgeholt"; Indirekt aber Schicht 4, weil darin Schicht 3 Paket transportiert
**Frage: Gibt es bei Verlust eine Sendewiederholung auf Schicht 4?** Ja & Nein. Abhängig von Protokoll. TCP wird wiederholt, UDP nicht.

**Blocking**: Packets are blocking each other, prevent blocking:
- *Overprovisioning:* circuits in switch fabric faster than input ports
- *Buffering:* queue packets until resources available (network interface or switch fabric), possible buffer places (N input, output ports, storage M, speedup S, cycle time Z):   
 input buffer: FIFO at input; requirements S=1, Z= 1/2; Head-of-Line blocking (packet waiting but packet behind could be served); throughput N=2 → 75%, N → ∞ → 58,58%
 output buffer: FIFO at output; requirements: S=N, Z=1/(N+1); output buffer accepting packets N*S, input buffer at least one packet; throughput max 100%, usually 80-85%  
 distributed buffer: conflict resolution inside switch fabric, FIFO buffer per crosspoint; requirements: matrix structure, S=1, Z=1/2; no head-of-line blocking, higher memory than input/output   
 central: shared buffer for conflict resolution; Requirements: Z=1/2N, address memory for information of packets, control memory for parallelization
- *Backpressure:* signal overlaod back to input ports, input ports can reduce load
- *Parallel switch fabrics:* parallel transport of multiple packets to output ports, higher access sped required at output ports

*Ende Vorlesung vom 18.10.2018*

**Switch Fabric**: Basic Structures
- *Shared memory* 
- *Bus/ring structure:* conflict-free access through time-division multiplexing, transmission capacity bus/ring (at least sum of all input ports), 
easy support for multicast/broadcast, extensions limited, usually los number (approx. 16)
- *Crossbar:* each input connected to each output, n inputs, n outputs n² crosspoints; partial parallel switching possible, multiple packets for same output 
→ Blocking → Buffering required; especially efficient with same sized packets
- *Multi-level switching networks:* switching states can set up multilevel connections (0 → $O_1$, 1 → $O_2$); Less wiring effort than crossbar, each input
connected with each output, not all connections at same time → internal blocking possible

### Internet Routing
#### Basics
**Control Path (Control Plane)**: Routing protocols, exchange of routing messages for route calculation

**Data Path (Data Plane)**: Lookup, Forwarding of IP packets (Layer 3)

**Routing Table**: Generated by routing protocol; Entries: mapping of dest. IP prefixes to next hop (IP address); 
optimized for particular routing algorithm; Implemented in software → Performance not critical

**Forwarding Table**: Used for packet forwarding; Entries:  Mapping of IP prefixes to outgoing ports (interface ID, MAC address);
optimized for rlongest prefix matching; Uses (partially) dedicated hardware → Performance critical (Lookup in line speed)

> Anmerkung aus Vorlesung: Lookup findet in Schicht 3 statt, da es sich um IP Pakete handelt; Routing Protokolle liegen über SChicht

**Routing metric (cost, weight)**: used by router for routing decision; applied to link or overall path; e.g. Utilization, latency, data rate, number of hops
- *hop count*: distance between source and destination → number of hops on the way, limited range: 1-15 (16 = infinity); schlechte Maß, da Qualität der hops 
(= Geschwindigkeit der Links), nicht betrachtet

**Routing policy**: routing decision based on policies; defined by networrk operator/owner; e.g. prefered routes over specific neighbors

**Distributed Adaptive Routing**: most commonly used; instance of protocol per router, exchange of routing information via routing messages; path
adaptions according to current network situation; *Path computation:* Network modeled as graph, Routers are nodes; Links are edges with metric

#### Autonomous Systems
**Autonomous System (AS)**: internet divided into AS; indetification over unique number (Autonomous Systems Number - ASN: earlier 16 bit, now 32 bit); avg.
path length 3,83;    
Properties: appears as single entity to the outside, uniform routing policy, typically uniform IGP;   
Advantages: 
- *Operator autonomy:* separated administrative domains; increasing overhead with size of network
- *Scalability of routing protocols:* Routing Protocol *inside* AS, Routing protocol *between* ASes; choice of IGP, Hiding internal structure  

IANA (Internet Assigned Numbers Authority) delegates allocation to RIR (Regional Internet Registries); around 45.000 issued ASNs  

Classification of AS based on role:
- *Stub AS:* small organizations, mostly only regional, connected with exactly one provider, no transit traffic
- *Multihomed AS:* large enterprises, connected to several providers (→ Reliability), no transit traffic
- *Transit AS:* Provider, often global scope, 

Classification based on "economic position/influence", no official mapping! 
- *Tier 1:* (=Transit AS), do not buy transit, sell transit, peering with other Tier1s, e.g. Telekom
- *Tier 2:* big national and interregional AS, downstream of Tier1 ASes, sell transit to other ASes, employ peering, e.g. Vodafone
- *Tier 3:* small (regional) AS, downstream of Tier2 providers, do not sell to other ASes, sell to end customers, employ peering, e.g. Congstar

How ensure mutual reachability? Cooperation among autonomous systems?

**Transit**: Purchased connectivity, traffic exchange in both directions, only downstream AS must pay, Transit AS offers transit
- *Upstream:* provider (seller) of transit
- *Downstream:* customer (buyer)

Options for Connectivity: (Stub = Zugang)
- *Stub AS:* ein Zugang zum AS (und Rest des Internets), bei Ausfall keine Verbindung zum Internet
- *Multihomed stub AS:* zwei Zugänge, Umstieg bei Linkausfall
- *Multihomed AS:* zwei Transit Verbindungen

**Peering**: Direct connection, typically between ASes of same tier; 
- *Private Peering:* no costs for traffic exchange; mostly only data traffic between privately peered AS, no transit in other ASes 
→ Connectivity is not achieved; Advantages: benefits for both ASes (save transit costs), shorter data paths; Problems: direct connection complicated 
(geographical distance), Full mesh of n ASes more than 1 billion connections!
- *Public Peering:* through Internet Exchange Points (IXP, central public authority for interconnection): neutral traffic forwarding on layer 2, monthly 
fixed charges per port → expensive infrastructure, Different Peering policies:
    - Open
    - Selective: specific terms and conditions
    - Restrictive: no new peering relationships
    - No Peering
    
**Content Delivery Provider**: Goal: fast content delivery → locations close to Tier1 peering points

**Content delivery networt (CDN)**: connected over own routers, world wide network with own AS number, points of presence (PoP) spread over world 
(access and core routers, customer connection through access router), load balancing at access router, low latencies

**Routing Protocols**: 
- *Interior Gateway Protocol (IGP):* Routing inside an autonomous system, not visible to the outsides, different IGPs possible, metric-based
    - *Routing Information Protocol (RIP):* commonly used, distance vector algorithm
    - *Open Shortes Path First (OSPF):* commonly used, link state algorithm
    - *Intra-Domain Intermediate System to Intermediate System Routing Protocol (IS-IS):* ISO Standard, link state algorithm
    - *Enhanced Interior Gateway Routing Protocol (EIGRP):* CISCO, link state algorithm, based on RIP
- *Exterior Gateway Protocol (EGP):* Routing between autonomous systems; EGPs müssen einheitlich sein; policy-based; im Einsatz: *Border Gateway Protocol*

#### Roting Information Protocol (RIP)
**Routing Information Protocol (RIP)**: IGP, one of first routing protocols, very simple, little configuration; oberhalb von IP; application process 
implements RIP, manages forwarding table; RIP sent over UDP → *not reliable*  
*Routing Messages:* exchange messages over UDP
- *Request Message:* complete routing table (partly)
- *Response Message:* response to query, 
    - Regular Routing update: broadcasted every 30sec, not synchronized, entire routing table to neighbors, no refresh for at least 180s 
    → in case UDP messages are lost, retry, hop count 16 → route is invalidated;  
    - Triggered Update: because of route change, not complete table; rate limitation to reduce load, randomized between 1 and 5 seconds, changes during period 
    accumulated and sent in one message
    
#### OSPF: Open Shortest Path First
**Open Shortest Path First (OSPF)**: Interor Gateway Protocl, based on Link State, each router
needs to learn complete topology of network (nodes, links with costs), each router computes 
shortes path (dijkstra), every router must have identical knowledge → otherwise inconsistent
paths; OSPF on top of IP → unreliable communication

**Routing metric:** each link associated with link costs, configured value, $Cost = 
\frac{ReferenceBandwidth}{InterfaceBandwidth}, ReferenceBandwidth = 100Mbit/s (default)

**Link State Advertisement(LSA):** with information about neighbors and links; flood LSA to all 
interfaces → router must have identival copy of LSA; Lifetime: MaxAge = 1 hour, LSRefreshTime = 30 min; if nothing changes, nothing needs to be reported
→ keep quiet, LSAs refreshed every 30mins, otherwise communication only needed in case of changes; min time between two consecutive LSAs 5 secs   
Structure:
- *Header:*
    - LS Age, Options, LS Type (Hello, link state advertisement, acknowledgement)
    - Version: OSPF Version: 2 for IPv$, 3 for IPv6
    - Type: Hello, link state advertisement, acknowledgement
    - RouterID: identifier of router that originated packet
    - AreaID
    - AUType and Authentication: option authentication, verifies that sending router belongs to same network
    - LSAs: if tye is LSA
- *Body:* variable
    - (Advertising Router Flags)
    - \#Links
    - Link ID
    - Link Data: type dependent
    - Type, \#ToS, Metric
    - ToS, 0, ToS Metric
    
Flooding: Goal: Link State databases must have identical content → need to be synchronized, following actions needed:
- ensure each LSA is received by every router → reliable flooding
- ensure each router consistently store (if LSA is newer → sequence number higher) or discard each LSA → fully deterministic comparison rules
- ensure that expired LSAs are pruned from link state databases

**Link State Database:** LSAs from all routers in network stored; for topology graph and routing table

**Hello Protocol:** establish, maintain logical adjacencies, ensure bi-direction communication
→ determines identity and liveliness of neighbors

*Workflow:* Router sends hello messages (own routerID, routerID of neighbors, dest. IP of message) periodically

**Areas**: AS grow rather large, LSA flooding and route computation overhead → do not scale; Concept: Divide AS into *areas*, Link state algorithms only within area, areas exchange
summary of information, typical size in area: less than 100 router → only router within area have same link state databases; Area 0 = backbone of AS, other areas directly connected to AS 
via area border router, Inter-Area Forwarding through backbone area

**Area Border Router (ABR)**: connected to both areas, instance of OSPF for each area, generate summary LSAs, Handling summary of LSAs

On OSPF every router is pre-configured with: routerID (e.g. smallest IP address of its interfaces), Per-interface parameters (interface IP address, mask; interface output cost (metric))

**RIP vs. OSPF**

|         |     RIP       | OSPF  |
| ------------- |-------------| -----|
| **Algorithm**      | distance vector (limited metric selection and size, max path length of 15 hops | links state|
| **Messages**      | periodic updates every 30secs, even without changes     | updates only on change |
| **Resources**      | easier, less resources    | more complicate, more resources |
| **Usage** | somethimes in small networks   |  standard in large ASes, large networks divided into areas|

**ARPANET Routing Metric**: early routing metric versions based on delay; Problems: queue length can change significantly, metric may lead to routing oscillations, bandwidth not
considered  
Measuring Delay: $ t_v = (T_{out} - T_{in}) + t_a + t_s$ ; $T_{in}$: packet receiving time, $T_{}out $: sending first bit of packet, $t_a$: Ausbreitungsverzögerung (Kabelübertragungszeit), 
$t_s$ = Sendezeit (Zeit um Paket komplett zu senden)  
Problem: measured delay good indicator *after* rerouting; experienced delay ony godd in case of low load  → route oscillations, low network utilization  
Routing Oscillation: hin und her zwischen Link A und Link B  
Improvement: during heacy load better take good paths than optimal paths: $ τ = \frac{k}{C(1-ρ)} ⇒ ρ = 1 - \frac{k}{Cτ} $ and smoothed utilization value: 
$U(n + 1) = 0,5 ∗ ρ(n + 1) + 0,5 ∗ U(n)$ → damps oscillations
with: $τ$: average delay, $ρ$: measured utilization, $C$: link speed, $k$: average packet size, $U$: smoothed utilization
                                                                                                                                
**Equal Cost Multipath (ECMP)**: multiple paths with lowest cost may exist; ECMP splits traffic *equally* between paths with lowest cost; allows load balancing; OSPF supports ECMP

**Traffic Engineering**: Goal: Performance optimization for networks; determine proper link weights

**Exterior Gateway Protocol (EGP):** large networks in AS usually only have information about themselves, number of entries in routing table ans amound of exchanged routing information does not
scale, per AS at least one intermediate system with interface to another AS  
 Advantages: 
 - *Scalability:* size of routing table depends on AS size, changes in routing tables only propagated within AS
 - *Autonomy:* routing can be controlled within own network, not the same routing protocols within AS necessary

**Border Gateway Protocol (BGP)**: most important EGP, basis of today's internet routing, worldwide usage; 
Path Vector Protocol: Extension of distance vector approach, routing metric = paths (guarantee no loop exist), routing/paths are based on policies (e.g. cheapest path, not over AS xyz), 
routing not pre-determined; through smart address assignment, address ranges are summarized by single prefix → improves scalability  
*Structure:*
- *External BGP (EBGP):* between routers of *neighboring* ASs; announcement, forwarding of path information; no internal AS details exchanged
- *Internal BGP (IBGP):* between BGP routers within AS; synchronization of BGP routers; Transit AS establish transit routes  

BGP calculates routes to prefixes from **other** ASs, IGP of local AS broadcasts routes to destinations **within** AS  
Possible approaches for routing with BGP and IGP:
- IGP distributes default routes: unknown address/prefix packets to BGP router by shortest path
- Publication of external routes via IGP: BGP router responsible for specific external prefixes
- IGP router also speaks BGP (IBGP)  
Sessions: Point-to-Point (via TCP between directly connected routers = neighbors, peers); hen-eg-problem, how to establish TCP connection? 
→ IBGP: IGP of AS can be used   
→ EBGP: usually direct physical connection (no routing required), manual config  

*IBGP Connections:* 
- Simple case: BGP routers fully meshed/directly connected, but then sessions must be kept alive, bad scalability
- Alternative 1: concentragte IBGP traffic in a single router = route reflector, has to maintain sessions, forwards messages, in practice more than one reflector → reliabilty
- Alternative 2: form hierarchies from sub ASes (AS confederations), implement more complex policies, confederation appears as a single AS

*BGP Messages:* 
- OPEN: establish BGP connection to peer, TCP connection must alread exists!, authentication
- UPDATE: announcement of new / withdrawhl of outdated path; only sent if new/better paths available
- KEEPALIVE: keeps connection alive in absence of update messages, acknowledgement for OPEN request
- NOTIFICATION: error message / tear down of BGP connection 

*BGP Routing:* no predefined routing metric → policies → Routing Information Base (RIB): DB for received, dispatched routing information
- Incoming updates: Adj-RIB-In (Adjacency RIB Incoming), exists per peer, stores information received from peer
- Input Policy Engine: Filtering of information according to rules
- Decision-making Process: Selection of best route
- Loc-RIB: Local RIB, Routing Informaiton Base, actual routing table, only preferred routes, routes form *Forwarding Information Base (FIB)*
- Output Policy Engine: Filtering of information according to defined rules
- Outgoing updates: Adj-RIB-OUT (Adjacency RIB Outgoing), exists per peer, contains routes published to peer

*BGP Challenges:* maintaining scalability ( growth of routing tables, increasing dynamics), increased demands on internet, security problems

**Route Flap Damping**: Routes in routing table change more frequently → temporarily suppressing changes of unstable routes; penalty per update, penalty drops exponentially over time, can lead
to connectivity loss!

**Security Extensions for BGP**: to secure route information, authentication and authorization of senders, integrity protection and encryption, secured routing through IPSec and TCP mit MD5
- *soBGP (secure origin BGP):* from Cisco
- *S-BGP (secure BGP):* from BBN-Technologies

**Cleaning Center**: Redirect traffic to separate DDoS attack traffic and legitimate traffic, legitimate traffic routed back to AS → BUT: good position for "man in the middle" attacker

### Label Switching
#### Motivation
Issures related to IP based routing: Lookup complex, Shortest path routing, packet based

#### Flows
**Flows**: A flow is a sequence of packets traversing a network that share a set of header field values; Ip routing is special case flow based forwarding, concept also applicable to Ethernet 
switching
- *Micro-flows:* single "connection", fine grained control, high number of flows possible
- *Macro-flows:* higher level of aggregation, several "connections", lower number of flows

**Flow based forwarding**: fundamental concept, indepentent of layers (can also span multiple layers), incorporates classic routing/forwarding concepts

#### Label Switching
