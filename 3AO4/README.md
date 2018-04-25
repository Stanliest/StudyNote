# Exam review: 3AO4 Software Design III: Large System Design
Look over slides and take notes of key points\
He said the slides are not substitudes for attending class

## slide 1 Introduction
1. design entity: objective and subjective, mathematics(dft) and art
2. what is design??
* an activity that translates an idea/goal/wish into a blueprint for an artifact or process that fit the environment
3. wait do we get a cheat sheet for exam?

## slide 2 Architecture Design Space
### software architecture
Three perspectives: software code units, project's runtime structure, allocation structure
### software code structure
1. main software element: code modules or files
2. modules are assigned to: func and non-func attributes, public APIs
3. some dependency relations between modules (contains, follows, uses, etc.)
4. "call graph" for method call and information flow between modules
5. **Connector**: both directions, asynchronous and synchronous operation, sequence: connectors used in particular sequence
* asynchronous: a process runs independent from other processes
* synchronous: a process runs only as a result of other processes complete or hand off operation
### runtime structure
1. client-server application
2. Connector: (multiplicity) one element can invoke methods of multiple element at runtime
3. Two connected element can communicate through same thread/process/computer/network
4. universal invokable, self-descriptive(bluetooth of different companies disconver each other)
### software manangement structure
1. used for project resources allocatioin
### software element
1. elements are connected through conncectors into dependency graphs
2. element is reentrant (can be safely executed concurrently), it can be implemented by any thread or process
3. element is not reentrant, must be run on separate thread to be thread-safe
4. element with high multiplicity, use an application server for implementation
5. heavy computation for deployment in an element, use a cluster of processors
6. element is assigned well-defined complex functions, use off-the-shell solutions
7. complex element --> sequence of layered elements, sequence of tiered elements
### software connectors
1. for one element to send a message to another
2. two elements are mapped to the single process, two diferent process and two different computers
3. types of connectors based on attribute(synchronization mode, initiator, implementation type, active time, span, fan-out, etc.)
4. Initiator: an incident element of a connector that can make a request to its partner
5. two subsystems must be connected by a two-initiator connector
### Iterative refinement of an architecture
Steps:  
1. standalone
2. network
3. HTML and HTTP based
4. layered architecture

## slide 3: Models for software architecture
### intro
1. describe software archi. formally(ADL: archi. description lang) or informally(UML: objecte-oriented solution)
2. block diagrams (box and line)
3. "4+1" view model (UML)
* logical view
* process view
* development view
* physical view
* user interface view
### UML 
1. structural(static) and behavioral(dynamic)
2. structural
* static structure, class hierarchy, relationships between classes
* control flow between elements
* **class diagram, component diagram, deployment diagram, etc.** all independent from time
* (Structural)Object diagram: based on class diagram, present an overview of a particular instance of a class diagram, specific case
* composite structural diagram: inner structure of a component
* component diagram: all components of a system, interrelationships between components
* deployment diagram: system hardware, software and network connections
3. behavioral
* behaviors of objects
* object collaboration, interaction, activity and concurrency
* **use case diagram, state machine diagram, sequence diagram, collaboration diagram, activity diagram**
* use case: the little person figure must be an **ACTOR**!!
* activity diagram: outline of activity's data and control flow, work-flow oriented
* state machine diagram: life cycle of an object
* sequence diagram: shows chronological sequence of messages between objects, one diagram corresp. to one use case
* collaboration/communication diagram: is basically sequence, but has indices for messages
4. public: +, private: -, protected: #

## slide 4: General Design Principles
Design principles build on simplicity and restriction  
1. Low coupling and high cohesion principle (where we improve **information hiding**)
* coupling: degree of modules depending directly on other modules
* cohesion: degree of communication among module's element
* tight coupling between classes is hard to maintain, improve by new class or inheritance
* lack of cohesion: a class perform more than one non-related functions, hard to manage
2. Open-closed principle
* open to extension: extend to meet new requirements
* closed to modification: existing implementation should not be modified as a result of system expansion
3. Liskov substitution principle
* Substitution for same type or subtype still true.
4. Dependency inversion principle
* high level not depend on low level, both levels and details depend on abstraction
* design to an interface, not to implementation
* package that is max stable should be max abstract
5. interface segregation principle
* if there are two non-cohesive functionalities, keep them separate
6. law of demeter
* a method should have limited knowledge of an object model
7. least privilege (for security, and the following)
* subject only given privilege it needs to complete its task
8. fail-safe defaults
* subject cannot access object without given access
9. economy of mechanism
* security mechanism should be as simple as possible
10. complete mediation
* all access to objects need to be check to ensure they are allowed
11. open design
* security of mechanism should not depend on secrecy of its design or implementation
12. separation of privilege
* system should not grant permission based on a single condition
13. least common mechanism
* mechanism used to access resources should not be shared
14. psychological acceptability
* security mechanisms should not make the resource more difficult to access than if the security mechanisms were not present

## slide 5: Data flow architecture
### overview
* software system decomposed into modules(aka. sub-systems), each module transforms its input data to output data  
* there is only data connection between modules
* modifiability and reusability are the property attributes of data flow archi.
* execution sequence: Batch sequential, pipes, filters
* pipes are special case of filters

### batch sequential
* data flow carries a batch of data as a whole to move from one element to another
* typical application: business data processing (usually shell script)
* no message on the arrow
* **benefits**: simple divisions between modules, each module can be stand-alone working on input and output data
* **limitation**: require external control, low throughput

### pipe and filter
* flow is directed by data: data source, filters, pipes, data sink
* connection between components are **data streams**(fifo buffer type)
* **filter**: independent data stream transformer, write transformed data through pipe to next filter. Does not need to wait for batched data, just working in a local incremental mode
* **ex**: data(input) --> GZIPOutputStream --compressed data--> CryptOutputStream --compressed and encrypted data--> fileOutputStream --> file(output)
* **Pipe**: a stateless conduit that moves data stream from one filter to another, can carry binary or character stream. Object type must be serialized (serialization/defalting/marshalling, opposite is deserialization)
* push only(write only), pull only(read only), pull/push(read|write)
* active filter, passive filter
* **benefits**: concurrency, reusability, modifiability(low coupling between filters), simplicity, flexibility
* **limitation**: not for dynamic interactions, parsing overhead in two consecutive filters, error-handling issues

### process-control architecture
1. mainly for embedded system software design
2. two parts:
* executor processor unit for changing process control variables
* controller unit for calculating the amounts of the changes
3. process control data: controlled variable(speed of a cruise), input variable(measured data), manipulated variable(can be adjusted by controller)
4. Application domain: maintain a stable level for output data
5. **beneifits**: no precise formula can be used to decide the manipulated variable, software can be completely embedded in the devices
6. **limitations**: can be unstable and requires a thorough mathematical analysis

## slide 6: data centered software architecture
### overview
1. data store is shared by all related software components
2. system has two parts: data store and software components
3. two categories: repository and blackboard

### Repository
1. data store is **passive**, clients of data store is active
2. widely used in database management system, **library**, computer aided software engineering
3. clients get data from data store and put data in the store
4. **Benefits**: 
* data integrity: easy to backup and restore
* easy to add new software component(scalability and reusability)
* reduce overhead of transiend data between software components
5. **limitations**: 
* data store reliability & availability are important issues
* centralized repo is vulnerable to failure
* high dependency between data structure of data store and its agents
* change of data has significant impact on agents

### Blackboard
1. data store is **active**, clients are passive(clients are called knowledge source)
2. most of software are **knowledge based systems**: voice and image recognition system, security system
3. two parts: blackboard data store and knowledge sources.
4. the data change triggers a matched knowledge source
5. each knowledge source is independent, they collaborate together to solve complex problem with uncertainties
6. **benefits**: 
* scalability: easy to add new knowledge source
* concurrency: all knowledge can work in parallel
7. **limitations**: 
* tight dependency between knowledge and blackboard
* difficult to make a decision when to terminate reasoning
* synchronization of multiple agents is an issue
* debugging is challenging

## slide 7: Hierarchy architecture
### overview
1. modules at different levels are connected by explicit method invocations
2. three layers:
* lower level: provides more specific fundamental utility service
* middle layer: all business logic or core processing services
* upper layer: provides interface
* (Each layer is supported by its lower layer and provides service interface to its upper layer)
3. HA is characterized by explicit method invocation (call-and-return) connection styles

### Main/subroutine software architecture
1. purpose: max reuse of subroutines and make individual subroutine be developed independently
2. system decomposition depends on secrets (... hiding)
3. **benefits**: easy to decompose, can still be used in a sub-system of OO design
4. **limitation**: 
* globally shared data are vulnerable
* tight coupling cause ripple impacts

### Master/slaves software architecture
1. a variant of main/subroutine, supports fault tolerance and **system reliability**
2. suitable for **parallel computing**, and accuracy of computing, slaves executed in parallel

### layered architecture
1. higher and lower layers of classes and modules
2. request from higher layer to lower layer via method invocation, goes back via method return
3. each layer: up interface (provide services to its upper layer) and low interface(..)
4. higher layer provides more generic and abstract service
5. lower layer provides more specific
6. jar file includes all service classes from all layers
7. a simple software system has two layers:
* interaction layer(interface)
* processing layer(business logic)
8. **benefits**:
* increamental software dev based on increaing levels of abstraction
* enhanced independence of layers
* enhanced reusability
9. **limitaions**:
* lower runtime performance (a request go through many layers)
* overhead on data
* many app don't fit this archit.
* exception and error handling is an issue
10. **related archit.**: repository, client/server

### virtual machine
1. **benefits**: 
* portability and machine plateform independence
* simplicity of software development
* simulation for non-native model
2. **limitations**:
* slow execution of the interpreter
* additional overhead
3. related archit: interpreter, repository, layered archit.

## slide 8: interaction oriented software architecture
### overview
1. three partitions:
* data module
* flow control module
* view presentation module
2. two categories:
* presentation-abstraction-control (PAC)
* model-view-controller (MVC)

### PAC
1. system decomposed into many cooperating **agents**, developed from MVC
2. each agent has three components(presentation, abstraction, and control)
3. no direct connections between abstraction component and presentation component, controll component do the communication
4. each agent has its specific job
5. **benefits**: 
* support multi-tasking/viewing
* support agent reusability and extensibility
* easy to plug in new agent or replace
* support concurrency
6. **limitations**:
* overhead due to control bridge and communications between many agents
* hard to determine # of agents
* development complexivity
7. related archit: layered, multi-tier, MVC

### MVC
1. most web application(online shopping, online survey, etc)
2. summary:
* controller: control sequence of user interaction, manages initialization and registration
* model module: DOES NOT depend on other modules, provides core functional services
* view module: displays data, updates interface
3. Suitable for interactive app(multiple views), clear division between M, V, and C
4. **benefits**: 
* many MVC vendor frameworks available
* multiple view synchronized with same data model
* easy to update views and interfaces
* very effective for development
5. **limitations**:
* does not fit agent-oriented app
* multiples views and controllers make data model expensive
* division between view and controller is not very clear in some case
6. related archit: PAC, implicit invocation archit.
#### MVC-I
* simple version: two modules: controller/view, and model
* diagram: controller/view --subscribes--> model
#### MVC-II
* view and controller subscribe to model
* can have multiples of controller and views, each controller can have many views
* **model connects to database**

## slide 9: distributed architecture
### overview
1. data, software, user are distributed
2. Topology, mode

### client/server
1. advantages:
* separation of responsibilities
* reusability of server components
2. disadvantages:
* lack of heterogeneous structure to deal with changes
* security complications
* server availability
* testability
* fat/thin client

### multi-tier
1. front tier(UI), middle tier(business logic), back tier(database)
2. advantages: reusability, scalability, reduces traffic on network
3. disadv: complex testability

### broker architectual style
1. middleware, for communication
2. brokering, forwarding requests
3. **better decoupling between clients and servers**
4. proxy-based system. Proxy handles communication
5. stub(client-proxy), skeleton(server-proxy), broker, and bridges(optional, connect brokers)
6. advan:
* server location transparancy
* changability and extensibility
* simplicity for client access server
* reusability
7. disadv:
* inefficiency due to overhead of proxies
* low fault-tolerance
* difficault in testing

### Service-oriented architecture (SOA)
1. advan: 
* loosely-coupled connection
* each service component is independent
* interoperability
* reusability: any service can be reused by any other services
* scalability

### enterprise service bus (ESB)
1. enterprise info system requires highly adaptable and highly flexible system architecture
2. strong demand for low cost and quick system
3. SOA integration technology that provides a unified archit. for high reusability

## slide 10: heterogeneous architecture
1. large scale project need multiple architecture styles
2. depending on requirements and their priorities, and constraints, to choose the "optimal"
3. system quality attributes: score of a design: +(score * weightOfAttribute)
4. SAAM

## slide 11: software product families and product families algebra
1. product family: a set of products that share common hardware or software artefacts such as requirements, properties, middleware, or code (both hardware and software)
2. feature modelling:
* G = (V, E)
* FODA: a tree
* FORM: a tree with AND/OR
* FeatuRSEB: a tree with XOR (mutual exclu. constraint)
* generative programming: parent-children with filled circle(mandatory)
* ...
3. product family algebra: 
* monoid: (S,+,0)
* semiring: (S,+,0,.,1)
* an idempotent commutative is semiring --> and this is a product family algebra..
* +: choice between optionalities of products and features
* .: mandatory presence
* LOL this is too complicated
* F = a * b * (c + 1) --> +1 expresses optinality of c
* above becomes F = a * b * c + a * b, so there are two products/features
