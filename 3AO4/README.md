# Final exam review for 3AO4 Software Design III: Large System Design
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
