# Final exam review for 3AO4 Software Design III: Large System Design
He said the slides are not substitudes for attending class

## slide 1 Introduction
1. design entity: objective and subjective, mathematics(dft) and art
2. what is design??
* an activity that translates an idea/goal/wish into a blueprint for an artifact or process that fit the environment
3. wait do we get a cheat sheet for exam?

## slide 2 Architecture Design Space
So much content...
### software architecture
Three perspectives: software code units, project's runtime structure, allocation structure
#### software code structure
1. main software element: code modules or files
2. modules are assigned to: func and non-func attributes, public APIs
3. some dependency relations between modules (contains, follows, uses, etc.)
4. "call graph" for method call and information flow between modules
5. **Connector**: both directions, asynchronous and synchronous operation, sequence: connectors used in particular sequence
* asynchronous: a process runs independent from other processes
* synchronous: a process runs only as a result of other processes complete or hand off operation
#### runtime structure
1. client-server application
2. Connector: (multiplicity) one element can invoke methods of multiple element at runtime
3. Two connected element can communicate through same thread/process/computer/network
4. universal invokable, self-descriptive(bluetooth of different companies disconver each other)
#### software manangement structure
1. used for project resources allocatioin
#### software element
1. elements are connected through conncectors into dependency graphs
2. element is reentrant (can be safely executed concurrently), it can be implemented by any thread or process
3. element is not reentrant, must be run on separate thread to be thread-safe
4. element with high multiplicity, use an application server for implementation
5. heavy computation for deployment in an element, use a cluster of processors
6. element is assigned well-defined complex functions, use off-the-shell solutions
7. complex element --> sequence of layered elements, sequence of tiered elements
#### software connectors
