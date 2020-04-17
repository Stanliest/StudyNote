Networks and security: study notes

Lab notes:
Clear dns cache on Mac : sudo killall -HUP mDNSResponder

Chapter 1: Computer networks and the internet

Internet: computer network connected thought end systems(client, server)
* Use packets to communicate between end systems
* Packet switch: routers, link-layer switches
* End systems access the internet through ISP (internet service providers)

DSL (digital subscriber line) internet- access to internet
* Internet and telco(telephone company)

Network edge: 
End systems (or host) connect to ISP (internet)
* FTTH (fiber to the home)
* HFC (hybrid fiber coax) - consist of both fiber and coaxial cables

* Physical media:
    * Twisted-pair Copper wire
        * telephone networks, DSL and ethernet use copper wire
    * Coaxial cable
        * Cable television system, shared medium
        * Higher transmitting rate 
    * Fiber optics
        * Overseas links
        * High cost
    * Terrestrial radio channels
        * Mobile network
        * Three groups: short distance, local area, wide area
    * Satellite radio channels

Network core:
The mesh of packet switches and links that interconnects the internet’s end systems
* Packet switching
    * Time to transmit a packet = L bits packet / R bits/sec transmission rate = L / R sec
    * Store-and-forward transmission (delay)
        * Packet switch must receive the entire packet before it can transmit to outbound link
    * Output buffer in packet switch - queueing delays
        * If the buffer is full, incoming packet is lost
    * End-to-end routing process:
        * Router uses packet’s destination address to index a forwarding table and determine the outbound link
    * Deliver in a timely manner, but does not make any guarantees
* Circuit switching
    * Like traditional telephone, need to maintain a connection first, this connection is called a circuit
    * Guaranteed constant data transmission rate
    * Multiplexing in circuit-switched networks
        * Frequency-division multiplexing (FDM)
            * Frequency is divided among the connections across the link
            * The link dedicates a frequency band to each connection for the duration of connection
            * The width of the band is call bandwidth
            * Telephone networks, FM radio stations
            * Each circuit continuously gets a fraction of the bandwidth
            * Advantages: lower latency - all channels can transmit at anytime.
        * Time-division multiplexing (TDM)
            * Time is divided into frames of fixed duration, each frame is divided into a fixed number of time slots
            * Each circuit gets all of the bandwidth periodically(alternatively) during brief intervals of time
            * Advantages: Greater flexibility and efficiency. Allocate more time periods to the signals that need more bandwidth. But only one channel can transmit at a time.
* Packet switching vs. Circuit switching
    * Packet switching:
        * Offers better sharing of transmission capacity, efficient and less costly
            * Users will have idle time
* A network of networks
    * ISPs themselves are interconnected
    * Network structure 1 (access ISP): Interconnects all of the access ISPs with a single global transit ISP
    * Network structure 2 (regional ISP): multiple global transit ISPs, themselves must interconnect too (economically more desired)
    * Network structure 3: multi-tier hierarchy, ISP in each city, connect to provincial, then connect to national (China)
    * Network structure 4: ecosystem that consist of access ISPs, regional ISPs, tier-1 ISPs, PoPs, multi-homing, peering, and IXPs
    * PoPs: points of presence - a group of routers in the provider’s network where customer ISPs can connect into the provider ISP
    * Peering: ISP pair can directly connect their networks together 
    * Network structure 5: Today’s internet
        * Builds on top of 4 by adding content-provider networks(eg. Google data centres)

Delay, loss, and throughput in packet-switched networks
Delay
* Processing Delay
    * Examine the packet’s header and determine where to direct the packet
* Queueing delay
    * Packet waits to be transmitted onto the link
* Transmission delay
    * L/R = length of he packet / transmission rate of the link
    * Depends on the physical medium of link
* Propagation delay
    * Time required to propagate from beginning of link to router B
    * Depends on the length of physical medium of the link
    * D/s = distance between router A and B / propagation speed of the link
* Transmission vs propagation delay
    * Packets length vs distance between routers
* dnodal = dproc + queue + dtrans + dprop

Queueing delay and packet loss
* La/R: arrival rate of data (traffic intensity)
* La/R > 1 means arrival rate exceeds transmitting capacity
* La/R <= 1 
* When traffic intensity is close to 1, queue gets built up
* Packet loss:
    * When a packet arrive to a full queue, the router will drop that packet - lost 

End-to-End delay
* dend-end = N(dproc + dtrans + dprop) given N-1 routers
* No queueing delay

Throughout in Computer Networks
* Throughput of client-server is min{Rc,Rs} - bottleneck link

Protocol layers and their service models
Protocol layers
* Each layer has a service model that provides service to the layer above
* Modularity makes it easier to update system components
* Drawback:
    * One layer may duplicate lower-layer function
    * One layer might need info that only present in another layer

* ISO/OSI reference model (7 layers)
* Example: Skype: person 1 application layer -> … -> physical layer -> person 2 physical layer -> … -> application layer
* Internet protocol stack (5 layers)
* Application layer
    * HTTP, SMTP, FTP protocol
* Transport layer 
    * Transport application-layer messages between application endpoints
    * TCP, UDP protocol
* Link layer 
    * Routes datagram through routers between source and destination
    * Link-layer protocol example: Ethernet, WiFi, cable access
* Physical layer
    * Move individual bits within the frame from one node to the next
    * Example: Ethernet has many physical0layer protocols: one for twisted-pair copper wire, another for coaxial cable, another for fiber..
* Encapsulation: 
Application: take <message> M
Transport: add header <segment>, add more information Ht, M
Network: <datagram> Hn, Ht, M
Link: <frame> Hl, Hn, Ht, M
Physical: transmit the message

* Link-layer switch: link, physical
* Router: network, link, physical
* Advantages: 1. Processing will be quicker; 2. Provide security
* Host: all 5 layers



Chapter 2: Application Layer

Principles of network applications
Network application architecture
* Two model: 1. Client-server 2. Peer-to-peer (P2P)
* P2p:
    * Peers(connected hosts) request service from other peers, provide service in return to other peers
    * Peers are intermittently connected and change IP addresses
    * A list of active nodes
    * Traffic intensive applications: file sharing (bitTorrent), Xunlei, Skype
    * Advantage: self-scalability, cost efficient
    * Challenges: security, performance, reliability 

Process communicating
* Process: program running within a end system(host)
    * Client process: initiates communication
    * Server process: waits to be contacted

Socket (door of the house)
* Process sends/receive messages to/from its socket
* Always bind with some port
* Application layer - socket (used to communicate) - transport layer(OS)
* Identifier
    * Include both IP address and port numbers

App-layer protocol:
1. Types of messages exchanged
2. Message syntax
3. Message semantics
4. rules
* Open protocols: 
    * defined in text doc called RFCs
    * Eg: HTTP(web), SMTP(mail)

Different application have different requirement - eg for file transfer, no data loss
* Data integrity
* throughput
* Timing
* Security

Internet transport protocols:
* TCP: 
    * have some service guarantees, reliable data transfer
    * Connection oriented service - handshaking
    * Congestion-control
    * Email, file transfer, streaming 
* UDP: 
    * does not have service guarantee, lightweight, connectionless
    * Why do we need this? When objective is very simple, no restrictions, can send huge amount of data as fast as possible
    * Steaming, internet telephony(skype)
SSL
* Always runs over TCP
* Between app-layer and transport-layer
* Securing TCP
* End-point authentication

The web and HTTP
HTTP overview:
* Client/server model
    * Client: browser that requests, receives, and display web objects 
    * Server: web server sends objects in response to request
        * Stateless protocol: server don’t store any state info about the clients
* Uses TCP:
    * Web server always runs on port 80
    * Client initiates TCP connection to server, port 80, then server accepts TCP connection from client; HTTP messages exchanged between browser and web server, then TCP connection closes

HTTP connections
* Non-persistent HTTP: each object sent over one TCP connection 1-1, connection does not persist for other objects
    * RTT (round trip time): time for a small packet to travel from client to server and back
    * Response time = 2RTT + file transmission time
    * 1 RTT for TCP connection, 1 RTT for HTTP request, assume both have same length of time
* Persistent HTTP: multiple objects can be sent over single TCP connection 1-M
    * default

HTTP message format: see textbook

Telnet (slide 28)
* Remotely connect to another machine 
* Network based utility
* telnet <address> <port>
* Not using HTTP protocol, but the telnet protocol

Cookies
* Four components:
    * Header line in http request message
    * Header line in http response message
    * A cookie file kept at user’s end system, managed by user’s browser
    * A backend database at the website 
* Browser save a text file(cookie file)
* Next time hitting the url, browser look for the file along with the HTTP request

Web cache (Proxy server)
* Goal: satisfy client request without involving origin server
    * Faster, reduce traffic to origin server
* Cache: store copy of data locally, fast to access
    * Local cache on computer
    * Web cache in router
    * ISP
* Refreshing the page fetch a fresh copy, update the cache(proxy server) on the way
* To improve performance:
    1. Increase bandwidth of access link
    2. Install local cache

Electronic mail
* User agent: client, email apps
    * Generate email
    * Receive email
* Mail server
    * Sending email for user agent
    * Receive email for user agent
* SMTP protocol: transfer email from one mail server to another mail server
    * Email app -> mail server(McMaster) -> SMTP client -> SMTP server -> receiver mail server(gmail) -> receiver mail app
    * Mail server has two queues: outgoing and incoming mail queue
    * Port: Email app -> mail server(McMaster):25 -> another mail server(gmail):25 -> another mail app
    * SMTP interaction: communicate using command and response
    * Multiple objects sent in multiple messages
* HTTP vs SMTP:
    * http is a pulled protocol, server who wants to receive initiate the TCP connection, (text, images) can be sent separately with calls
    * Smtp is a pushed protocol, server who wants to send initiate the TCP connection, 7-bit ASCII, everything in one message
* Mail message format: header(from, to, subject), blank line, body
* Mail access protocol
    * User agent -smtp-> sender’s mail server -smtp-> receiver’s mail server -mail access protocol(eg.POP, IMAP)-> user agent
    * POP3 protocol (authorization, download) - easy and small
        * Authorization phase
        * Transaction phase
        * Download and keep/delete, copies of messages on different client
        * Stateless across sessions
        * Download-and-delete mode:
            * User cannot read message from multiple devices
    * IMAP 
        * Keeps all messages in one place: at server
        * Allow user to organize messages in folder
        * Keeps user state across sessions
DNS
How to map between IP address and name, and vice versa?
* Domain name system
    * Distributed database
    * Application-layer protocol
* Centralize DNS(bad): single point of failure, traffic volume, distant centralized database, doesn’t scale
* Client want IP for www.amazon.com(name)
    * Queries root DNS server, then .com(TLD) DNS server, then amazon.com DNS server
* TLD (top level domain) servers
    * Eg. Uk, fr, ca, jp, top-level country domains. Com, org, net, edu, aero, jobs, museums - maintained by network solutions
    * Authoritative DNS servers: organization’s own DNS servers
* Local DNS name server
    * Each ISP (residential ISP, company, university) has one
    * When host makes DNS query, it’s sent to its local DNS server
        * Has local cache of recent translation pairs
        * Acts as proxy, forwards query into hierarchy
* Example on slide 63, 64
    * Iterated query
    * Recursive query
* Caching, updating records
    * TLD servers cached in local name servers
    * Cache may be out-of-date, if name host changes IP address, may not be known until all TTLs expires
    * Update/notify IETF standard: RFC 2136
* DNS records
    * Distributed database storing resource records(RR)
* DNS protocol, messages
    * Query and reply messages, both with same format
    * Message header: identification 16 bit, flags
* Attaching DNC
    * DDoS attacks: Bombard root servers with traffic, not successful now - local DNS servers cache IPs of TLD servers, allowing root server bypass
    * Bombard TLD servers, more dangerous
    * Redirect attack
        * Intercept queries
        * DNS poisoning: send bogus relies to DNS server, which caches
    * Exploit DNS for DDoS: send queries with spoofed sources address: target IP

P2P Application
Peer-2-peer application
* No always-on server
* File distribution time: client-server
    * F: size of file; us: upload rate; time to send one copy = F/us (server)
    * dmin = minimum download rate; time to download F/d (client)
    * Bottleneck, server or client whichever has slower rate
    * Time to distribute F to N clients: 
        * Dc-s >= max { NF/u, F/d }
* Dp2p >= max { F/us, F/dmin, NF/(us + sum ui) }
* Example: first time need a file, go to server and look for it (torrent movie file - containing trackers and clients), use your software to connect to all those trackers and download the file
Video streaming and CDNs: context
* Solution 1: Distributed server to solve single mega-video server
* CDN (content distribution network) - store the content nearby so easily accessible 
* Solution 2: store/serve multiple copies of videos at multiple geographically distributed server
Socket programming
* Socket: door between application process and end-end-transport protocol
* Example in the book

Assignment 2
Sequence of execution:
* Run the proxy server
    * It is accepting connections on some port #
* Run the client
* Enter command at client: ftp ftp.cdc.gov
    * To connect with the proxy server, proxy server port may be hardcoded
    * Client screen should show some response (ok message)
Syntax of FTP command (need to google to implement)

Chapter 3: Transport Layer
Implement reliable delivery of data

Protocols
* Run between app processes, take care of individual process (TCP, UDP ..etc)
* Send side: Breaks app messages into segment
* Rcv side: reassembles segments into messages, passes to app layer
* TCP - in-order, reliable, data not lost on the way; UDP - unordered, unreliable, transmit data at higher rate (no restriction)

Multiplexing/demultiplexing
* For every process, there are always a TCP and UTP process running
* Multiplexing at sender: handle data from multiple sockets, add transport header
* Demultiplexing at receiver: use header info to deliver received segments to correct socket 
* Example: multiple sockets —> multiplexing/demultiplexing —> either process

Tunnelling:
* Client to proxy server: inside HTTP GET/POST query message
* Proxy server to client: inside HTTP response message
* Client to proxy server: slide 2 - 29, uploading form input

UDP protocol
* UDP segments may be lost or delivered out-of-order to app
* Use: DNS, Video streaming buffer(receive first 50 segments, deliver to application layer)
* Connectionless: no establishing connections, each segment handled independently
* UDP Segment header
    * Checksum: detect errors (flipped bits) in transmitted segment (transport layer, network layer)

Reliable data transfer:
* Reliable data transfer protocol (rdt protocol)
* rdt2.0
    * Underlying channel may flip bits - checksum will detect bit errors
    * FSM specification: sender receiver slide 3-25
        * Acknowledgment and negative-acknowledgment packets (confirmation)
    * Sequence number for duplicate identification
* rdt3.0
    * Packet loss on the way from sender to receiver <- acknowledgement not received from receiver 
        * If loss(using timer), resend
    * If acknowledgement is lost, receiver send again, duplicate packets(with sequence number)
* Pipeline protocols
    * Go-back-n 
        * Sender can have up to n unpacked packages in pipeline 
        * Receiver sends cumulative acknowledgment 
    * Selective repeat
        * Receiver sends individual acknowledgment 

Connection-oriented transport: TCP
* Point to point, reliable, pipelined, full-duplex data, connection-oriented(handshaking)
* RTT (round-trip time)
* TCP timeout = estimatedRTT + safety margin
* Only retransmit the oldest packet
    * No matter timed out or not, receiver always send the newest acknowledgment number
* cumulative acknowledgment fulfill the lost of data
* Acknowledgment generation:
        * Lower end of gap: eg. 3 sec and 5 sec gaps, send to the one that starts with 3 sec gap
* Fast retransmission: retransmission before the timeout ends
* TCP flow control: receiver control sender, tell sender the buffer size, avoid overflow
* Connection management:
    * Three-way handshake: SYN msg(SYNbit) used to establish connection
    * Closing connection can be initiated on either side (FINbit)
        * If there’s a pending segment, delay the closing
* Principle of congestion control READ 
* Congestion control 
    * To slow down the sender
    * MSS - maximum segment size - based on data network layer (wifi,..)
        * 1 MSS - how much data can be transmitted in one 
        * cwnd - tcp sender congestion window size
    * Additive increase: for every acknowledgement, add one more
    * Multiplicative increase: cut down to half
    * Detecting loss:
        * By timeout -> cwnd set to 1 MSS, then grow exp
        * Duplicate acknowledgement -> cwnd set to half, then grow linearly 
        * Tcp throughput - not tested
    * Bandwidth share among connections - fair

Chapter 4 Network Layer: The data plane
Protcols: IPv4, IPv6
Overview
* Not implemented on switch
* Two key network-layer functions
    * forwarding: move packets in and out of router
    * Routing: determine route taken by packets (Both are bi-directional)
* Data plane: where actions are taken, forwarding function (has the forwarding/routing table)
* Control plane: determine how datagram is routed, where router computes the routing table
    * Traditional: Individual routing algo components in every router, figure out which port 
    * Software defined networking (SDN): a remote controller that calculates the routing tables for each router
Router
* At least two ports(ISP and enterprise)
* Routing bus (shared): only one port is used at a time
* Input port structure: line termination -> link layer protocol -> lookup, forwarding queueing -> switch fabric
    * Destination based forwarding
        * Destination address rage 2^32 ip addresses
        * Longest prefix matching: look for the longest matching bits
    * Generalized forwarding 
* Input port queueing
    * Head-of-the-line (HOL) blocking
* Output port structure: datagram buffer queueing -> link layer protocol -> line termination
* Output port queueing:
    * Queue delay and lost due to output port buffer overflow
    * Datagram (packet) can be lost due to congestion
* Scheduling 
    * FIFO
    * Priority scheduling: send highest priority packet first
    * Round robin
    * Weighted fair queueing (WFQ)

IP internet protocol
NAT: network address translation
* Scalability of network ip addresses
* Translation process
    * Datagram request generated from inside network, send to gateway router
    * Router change IP address, port number, updates NAT translation table
    * The reply comes back, look in the table and return to original source address
    * If it can’t find the address, it drops the reply packet
* Local IP address use reserved IP address range (class A: 10.x.x.x, class B: 198.x.x.x, class c…class d…)

Generalized forward and SDN
* OpenFlow data plain abstraction
    * Flow: defined by header fields
    * Generalized forwarding
        * pattern: for matching values in packet header fields
        * actions: for matched packet: drop, forward, modify
        * Priority 
        * Counters 

Routing algorithm
* Centralized and decentralized 
* Static and dynamic 
* Link-state algorithm
* Distance-vector algorithm
* Dijkstra’s algorithm

Routing protocols categories
* Intra-AS(autonomous system, aka domains) routing:
    * Algorithms routing inside the AS
* Inter-AS routing
    * Algorithms routing among AS'es
OSPF (open shortest path first) - single AS
* Open: publicly available 
* Using Dijkstra 
* Packet carried over IP, not on top of TCP or UDP
* Multiple same-cost paths allowed
* Backbone area connects sub areas together (backbone router - area border routers - internal routers, boundary routers connects to other routers)
    * So not only used as intra-AS but also inter-AS


Chapter 5: Network layer, the Control panel

Forwarding was data plane
Routing is control plane

* Per-router: routing algo in each router
* Logical centralized control plane: remote controller interact with each local control agent (CA) in each router
* Routing algo classification:
    * Global: all routers have complete topology
    * Decentralized: each router knows connected neighbours
    * Static: routes change slowly over time
    * Dynamic: routes change more quickly
* Link state: Dijkstra algo
* Distance vector(DV): bellman-ford algo
    * Each node sends its own estimate distance vector to neighbours 
    * Dx(y) ← minv{c(x,v) + Dv(y)}  for each node y ∊ N
    * Detect link cost change, then recalculate distance vector, if changed, notify neighbours 
    * Comparison of Link state vs Distance vector
        * 5-29
    * To scale routing: aggregate routers into regions known as “autonomous systems” (AS) (aka domains)
* Forwarding table configured by intra-AS and inter-AS routing algo
    * Intra-AS determine entries for destinations within AS
    * intra-AS and inter-AS determine entries for external destinations
    * 
    * Inter-AS: propagate reachability
    * Intra-AS: (interior gateway protocol) 
        * Most common ones:
            * RIP: routing information protocol
            * OSPF: open shortest path first (IS-IS routing nearly the same as this)
                * 5-36
                * Hierarchy OSPF:
                    * Boundary router - backbone routers - area boarder routers - internal routers
            * IGRP: interior gateway routing protocol
* Routing among ISPs: BGP
    * Internet inter-AS routing: BGP
        * Border gateway protocol: glue that holds internet together
        * eBGP: connect ASs
        * iBGP: connect AS-internal routers
    * BGP path advertisement 
        * 5-45
    * BGP route selection:
        * Based on local preference value attribute: policy decision
        * Shortest AS-path
        * Closest next-stop router: hot potato routing
    * Difference between inter and intra-AS routing?
        * Policy:
            * Inter-AS: admin wants control over how its traffic routed, who routes through its net
            * Intra-AS: single admin, so no policy decision needed
        * Performance:
            * Inter-AS: policy may dominate over performance
            * Intra-AS: can focus on performance 
* ICMP: Internet control message protocol
    * Used by hosts and routers to communicate network level info: error reporting, echo request/reply
    * ICMP messages carried in IP datagrams
    * Tranceroute and ICMP
* Network management and SNMP
    * Deployment, integration and coordination of hardware, software, and human element to test, poll, configure the network to meet the requirements and quality at a reasonable cost
    * Infrastructure: Managed devices contain managed objects those data is gathered into a Managed Information Base (MIB)
    * SNMP protocol: two ways to convey MIB info:
        * Request/response mode
        * Trap mode

Chapter 6: The Link Layer and LANs

* Introduction, services
    * Data-link layer is responsible for transferring datagram from one node to physically adjacent node over a link
    * Links: wired link, wireless link, LANs;
    * Nodes: hosts and routers
    * Framing, link access: 
        * Encapsulate datagram into frames, add header, trailer
        * MAC address
    * Reliable delivery between adjacent nodes
    * Error detection/correction
    * Link layer is implemented in each and every host 
        * In “adaptor” network interface card (NIC) or a chip
    * Adaptors communication:
        * Sending side: encapsulate datagram into frame, add error checking bits, flow control etc.
        * Receiving side: looks for error, rdt, flow control etc, extract datagram and pass to upper layer at receiving end
* Error detection, correction 
    * EDC: error detection and correction bits
    * D : data protected by error checking, may include header fields
    * Not 100% reliable: larger EDC yields better detection
    * Internet checksum: detect error in transmitted packets (used at transport layer only)
    * Cyclic redundancy check (CRC) : binary, calculate reminder
        * If non-zero remainder, error detected
        * R = remainder[(D*2^r)/G]
* Multiple access protocols
    * Two types of links:
        * Point to point
            * Ppp for dial up
            * Point to point link between ethernet switch, hosts
        * Broadcast (shared wire or medium)
            * Old-fashioned ethernet
            * Upstream HFC
            * 802.11 wireless LAN (local area network)
    * Multiple access protocols
        * Distributed algo that determine how nodes share channel
        * Communication about channel sharing must use channel itself
    * MAC protocols
        * Channel partitioning
            * FDMA: frequency division multiple access
        * Ramdom access
            * Slotted ALOHA, ALOHA
            * CSMA, CSMA/CD, CSMA/CA
        * “Taking turns"
            * polling with slave nodes
            * Token passing
* LANs
    * MAC addresses and ARP
        * Mac address: used “locally"
        * Each adaptor on LAN has unique LAN address
        * Address resolution protocol (ARP)
            * ARP table: each IP node on LAN has a table
            * IP/MAC address mapping for some LAN nodes
            * Same LAN: broadcast query to all nodes on LAN
            * Routing to another LAN
    * Ethernet 
        * Wired LAN technology (10 mbps - 10 gbps)
        * Physical topology: 
            * bus: coaxial cable
            * Star: active switch in center
        * Ethernet frame structure: preamble, dest address, source address, type, data(payload), CRC
            * 6-56
        * Connectionless, unreliable 
        * 802.3 ethernet standard
    * Switches
        * Ethernet switch: 
            * Store, forward ethernet frames
            * Use CSMA/CD to access segment, selectively forward frame
            * Transparent: host doesn’t know about switches; self-learning: no need configuration
            * Switches buffer packets
            * Hosts link to switch, each link has its own collision domain, so no collisions 
        * Switch forwarding table
            * It learns which hosts can be reached through which interfaces
            * Records sender/location(incoming LAN segment) pairs in switch table
            * Logic:
                * If entry found for destination
                    * Then if destination on segment from which frame arrived
                    * Then drop frame
                    * Else forward frame on interface indicated by entry
                * Else flood (forward on all interfaces except arriving interface)
    * Switches vs routers
        * Both and store-and-forward
        * Both have forwarding table
    * VLAN: virtual local area network
        * Switches supporting VLAN capabilities 
        * Portable based VLAN
    * 802.1Q VLAN
* Link visualization: MPLS
    * MPLS: MultiProtocol label switching
    * MPLS capable routers 
    * MPLS vs. IP paths
        * IP routing: path to destination determined by destination address alone
        * MPSL routing: path to destination determined by destination address alone
            * fast reroute: precompute backup routes in case of link failure
    * MPLS signalling 
    * MPLS forwarding table
* Data center Networking
    * * e-business (e.g. Amazon)
    * * content-servers (e.g., YouTube, Akamai, Apple, Microsoft)
    * * search engines, data mining (e.g., Google)
    * Load balancer: application layer routing
* A day in life of a web request
    * 6-89

Chapter 7: Wireless and Mobile Networks

* Intro
    * Elements:
        * Base station (eg. Cell towers, 802.11 access points)
        * Wireless link
            * Infrastructure mode
            * Ad hoc mode (no base station)
* Wireless links, characteristics
    * Comparing to wired link
        * Decreased signal strength
        * Interference from other sources
        * Multiple propagation
    * SNR - signal-to-noise ratio
        * The larger, the easier to extract signal from noise, the better
        * Increase SNR -> decrease BER
    * CDMA - code division multiple access
        * Each user has same frequency, but each has a unique code to encode data
        * Encode signal = original data x chipping sequence
        * Decode = inner product of encoded signal and chipping sequence
* IEEE 802.11 wireless LAN
    * BBS - basic service set (aka “cell”)
    * Collision avoidance (RTS-CTS exchange) - request-to-send, clear-to-send
    * addressing
    * Beacon frame
* Cellular internet access
    * Base station: 802.11 AP
    * 2G, 3G, 4G-LTE
    * Difference of 4G-LTE from 3G
        * * all IP core: IP packets tunneled (through core IP network) from base station to gateway
        * * no separation between voice and data – all traffic carried over IP core to gateway

Chapter 8: Security

* What is network security?
    * confidentiality
    * authentication
    * Message integrity 
    * Access and availability
    * Accountability 
* Principle of cryptography
    * The language: 
        * m plaintext message
        * KA(m) ciphertext, encrypted with key KA
        * m = KB(KA(m))
    * Symmetric key: sender and receiver share same key Ks
        * Fast, convenient to process 
        * The sharing and producing of the key is an limitation 
    * Simple encryption scheme
        * Substitution cipher 
    * Symmetric key crypto: DES
        * DES - Data Encryption Standard
            * * US encryption standard [NIST 1993]
            * * 56-bit symmetric key, 64-bit plaintext input
            * * block cipher with cipher block chaining
        * DES operation: permutations
    * AES - Advanced Encryption Standard
        * * symmetric-key NIST standard, replaced DES (Nov 2001)
        * * processes data in 128 bit blocks
        * * 128, 192, or 256 bit keys
        * * brute force decryption (try each key) taking 1 sec on DES, takes 149 trillion years for AES
    * Public key crypto
        * * sender, receiver do not share secret key
        * * public encryption key  known to all
        * * private decryption key known only to receiver
    * RSA: Rivest, Shamir, Adelson algorithm
        * In practice: the asymmetric key (public key) is used to share the symmetric key, then the symmetric key is used to encrypt or decrypt the message
* Authentication
    * Nonce: number (R) used only once-in-a-lifetime
    * ap5.0: still cannot avoid the middle man attack
* Message Integrity
    * Digital signature
        * Bob encrypt with his private key, if Alice can decrypt with bob’s public key, she can verify it’s bob
        * However, everyone that has bob’s public key, can see the message
    * Message digests
        * Use hash function H to convert large message m to small message digests H(m)
        * Used like a checksum to verify if the message has been modified, or integrity
        * Not used for confidentiality, because it’s one-way function
        * Hash function algo: MD5, SHA-I
        * What if someone sends her public key, and say it’s bob’s public key? Solved below
    * Certification authorities (CA)
        * Binds public key to particular entity, E
        * E(person, router)
        * Alice apply CA’s public key to bob’s certificate, gets bob’s public key
* Securing email
    * Send confidential email with Ks(m) and Kb+(Ks), where Ks=symmetric private key, Kb=bob’s public key
    * Provide authentication message integrity with Ka-(H(m))
        * First hash the message, then it’s digitally signed with private key of alice
    * The hash/message digest is what ensures the message integrity
        * Recipient computes the hash and match with the hashed message
* Securing TCL connectionless: SSL
    * SSL - secure sockets layer (security protocol)
    * Provides: confidentiality, integrity, authentication
    * Used for: web e-commerce transactions, encryption, merchant business
    * Available for all TCP apps
    * SSL cypher suite
        * cipher suite
            * * public-key algorithm
            * * symmetric encryption algorithm
            * * MAC  algorithm
        * Client offer several suites, server picks one
* Network layer security: IPsec
    * VPN - Virtual private networks: encrypted inter-office traffic is sent over public internet instead
    * IPsec services:
        * * data integrity
        * * origin authentication
        * * replay attack prevention
        * * confidentiality
    * Two protocols: AH, ESP
    * AH - authentication header: provides authentication and data integrity, but not confidentiality
    * ESP - encapsulation security protocol: provides all (more widely used)
    * SAs - security associations
        * * before sending data, “security association (SA)”  established from sending to receiving entity
    * IKE - internet key exchange
        * PSK and PKI
        * Automatically establish IPsec SAs
* Operational security: firewalls and IDS
    * Firewalls:
        * Isolate organization’s internal net from larger internet, allowing some packets to pass, block others
        * Three types: 8-100
            * Stateless packet filtering: router filters packet by packet
                * ACL: access control lists: table of rules - what to block, what to allow
                * But it’s heavy handed tool, admits packets with no sense
            * Stateful packet filtering: track status of every TCP connection
                * Accept packet that make sense
            * Application gateways: filter packets on application data as well as on IP/TCP/UDP fields.
                * Example: allow select internal users to telnet outside
    * IDS - Intrusion Detection Systems
        * Deep packet inspection, examine correlation between multiple packets
        * Multiple IDSs: different types of checking at different locations















