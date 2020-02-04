Networks and security: study notes

Lab notes:
Clear dns cache on Mac : sudo killall -HUP mDNSResponder
ip.addr == 


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

Throughout in Computer Networks
* Throughput of client-server is min{Rc,Rs} - bottleneck link
