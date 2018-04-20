Last lecture:  
"Estimating defects will be on the exam."  
  
# Final review starts here  
just going through lecture slides and listing some key points
## slide 1 test principles
### Principles
1. a necessary part of a test case is a definition of the expected output or result.  
2. a programmer shoud avoid attempting to test his or her own program.  
3. a programming organization should not test its own programs.
4. thoroughly inspect the results of each test.
5. test cases must be written for input conditions that are invalid and unexpected, as well as for valid and expected.
6. avoid throwaway test cases unless the program is truly a throwaway program.
7. do not plan a testing effort under the tacit assumption that no errors will be found.
8. prob of existence of more errors in a section of program is proportional to the # of errors already found in that section.
9. testing is an extremely creative and intelectually challenging task. (i know)
10. no 10

* Testing is the process of executing a program with the intent of finding errors.  

## slide 2 testing strategies and plans
### errors defects, failures
1. errors lead to defects
2. defects lead to failure
3. risk is a condition that can result in a loss
4. cannot eliminate risks, but we can take countermeasures to reduce
5. risk of undertesting: directly translated into system defects
6. risk of overtesting: unnecessary use of resources

### test stragety
This is in assignment 1 -> look at assignment 1!!  
1. testing objective
2. stragety: 
* test factor: correctness, data integrity, authorization... (select and rank test factors)
* test phase: system development methodology
* identigy business risks associated with system under development
* place risks in test factor/ test phase matrix
* NOTE: matrix: test phases: require, arch. design, design, coding, unit testing, integration testing, sys./accp. testing, maintenance  
3. test plan: is the roadmap that will be followed in conducting testing
* general info
* plan: software des, test team, milestones, budgets, testing (schedule, require, testing materials, training, test to be conducted)
* specifications and evaluation (specifications, methods and constraints, evaluation)
* test decriptions (test: control, inputs, outputs, procedures)

### develop a unit testing plan
1. units have its own test plan - complexity based on quality expectations
2. unit testing structure a little different

## slide 3 determining your software testing techniques
Three categories: functional, structural, and unit testing techniques.  
This was also in assignment 1 (functional and structural)  

### fault seeding
estimate the # of pikes in lake soft:  
1. catch a number of pikes  in lake seed
2. mark and throw them into lake soft
3. catch a # of pikes, M in lake soft
4. suppose that M' out of M pikes are found to be marked:  
#### Total number of pikes originally in lake soft is: (M-M')(N/M')  
if we find many seeded faults and relatively few other, the result can be trusted. Opposite not true.  

Different testing comparison:  
Functional testing: focus on what, the results of processing behaviour  
structural testing: focus on the how, implementation algorithms  
dynamic: execute code, stage is validation, implementation testing  
static: by inspection, stage is verification, requirements and design  
exhustive testing: a complete verification, test on every possible condition; this is not practical..   
static testing: criteria for choosing representative test cases, reasonable test cases.  
automated testing: the more automated the development process, the easier to automate the test process  
manual testing: for the project that has greater reliance on people to analyze, document, and develop computer systems manually  

### select techniques/tools
Steps:  
1. begin with selecting test factor
2. functional or structural test
3. dynamic or static
4. manual or automated

## slide 4 Functional testing techniques
functional testing is to ensure that the system requirements and specification are achieved, create test conditions for use in evaluting 
the **correctness** of the application.  
1. regression: test previous tested segments, use when there is high risk when new changes may affect unchanged areas
2. error-handling testing: determine the ability to process incorrect transactions
3. manual-support testing: evaluate functions performed by people while preparing data
4. intersystem testing: ensures that the integration between systems functions correctly, use when there is a change in parameters
5. parallel testing: determine the results of the new app are consistent with the previous app or version

## slide 5 Structural testing techniques
structural testing is to ensure that the product designed is structrually sound and the tech is used properly, focus on process, not 
too much on the correctness.
1. stress testing: determines if the system can handle heavy loads.
2. execution testing: determines if the system achieves the desired level of proficiency in a production status (respond time, design performance)
3. recovery testing: determines the ability to **restart** operations after the integrity has been  lost, revert to a point
4. operations testing: to verify the operating procedures and staff can properly execute the app
5. compliance testing: verifies that the app is develped according to standards, procedures and guidelines
6. security testing: ensure confidential info and for competitive purposes to assure third parties that their data will be protected

## slide 6 Unit testing in java with JUnit
1. assertion: the code for an assumption
2. turn on assertions by "-ea" flag
3. if JUnit not integrated into the IDE, can use the TestRunner manually
4. when running test, a failure or error occurs, current test is aborted, other tests in the same test class will still be executed.
5. specify the tolerance when assertion has floating point
6. all method name start with "test" will be auto run by JUnit
7. setup and teardown for every method

## slide 7 Unit Testing
### theoretical funcdations of unit testing
1. Theoretical fundations of unit testing (tbh don't think this is on the exam, hopefully)
2. T is successful for P: P is correct for T if it is correct for all elements in T
3. test set T is ideal: if whenever P is **incorrect**, there exists a (d in T) such that P is incorrect for d
* an ideal test set always shows the existence of an error in a program
4. Conclusion:\
It is impossible to decide whether:
* a test is ideal,
* a criterion is consistent or complete, etc.

### Empirical unit testing principles
#### complete coverage principle
1. divide input domain into classes (for ex: {n<0}, {n=0}, 0<n<20, etc)
2. if classes disjoint, possibility to choose a representitives to minimize # of test cases
3. basically choose a test set that covers each representitive of sub domain
4. black-box testing: test without relying on any knowledge of the code or design, only has basis of specification
5. white-box testing: using the info about the internal structure, maybe ignore specification.

#### statement coverage criterion (white-box)
* weakness: executing some statement once and oberve it behaves properly is no guarantee that it is correct.
* each statement in the program is executing at least once
#### edge coverage criterion (white)
* some if else then while --> graphfla
#### other testing criteria
* condition coverage
* path coverage: include all the path (if else, loops...)
* major source of complexity is nested loops

## slide 8 Security testing
1. software security vulnerabilities:
* design vulnerabilityes: mistakes in the design that precludes the program from operating securely, no matter how perfectly is is implemented. Found in software's security features.
* implementation vulnerabilities: caused by security defects in the actual coding (sloppy coding) of the software.
2. good secure software use principles and techniques:
* compartmentalization: srong abstractions and interface validations
* least privilege: granting a user the fewest privileges possible
* separation of privileges: ensure multiples keys are needed to complete sensitive transactions
* attack surface reduction: eliminates interfaces that are not necessary to complete its work
* cryptography: protects data so if one security mechanism falis, the data needs decryption
3. cryptography: essential
* communication over an insecure channel
* securely store password
* enable session to be securely maintained  
pitfall: 陷阱  
4. input validation (design flaw): buffer overflow, SQL injection, cross-site scripting
5. structural security (design flaw): large attack surface, running a process at too high a privilege level, no defense in depth, not failing securely  
idiosyncrasy: 特质, notorious: 臭名昭著  
6. c/c++ is notorious in security vulnerabilities, program does not keep track of size --> buffer overrun/ overflow
7. to prevent buffer overflow: limit size of inputs to xxx bytes
8. scripting languages are less of a risk because they are high level
9. unix and window shell scripts: often used as quick and easy interfaces
10. java and c# compile into bytecode and require a virtual machine, MUCH SAFER
11. however, when managed code calls into NATIVE code using a NATIVE method, the virtual machines can no longer enfore security
12. plateform: the environment that a program (mainly os) runs inside
* symbolic linking: files in a file system that point to other files, attacker can create same filename the program is running;
* directory traversal: allow access to dir that are not below the share dir by using the .. notation to go up a level in the file system
* there are more pitfalls

## slide 9 The basics of measurement
### empirical relations
* data we obtain as measures should represent attributes of the entities
* empirical (binary) relation: a reasonable consensus about which pairs are in the relation
* empirical relations NEED NOT be binary
* Measurement: mapping from the empirical world to the formal world (specify domain, range, rule to perform mapping)
* Measurement mapping: surjective (could be), neither injective nor surjective (the most of the meas. mapping)
### representation condition of measurement
each relation represented by mathematical element or model (entity, attribute, measure)
### models
* danger: focus too much on the mathematical system, not enough on empirical one.
* **Direct measurement** of attribute of an entity involves no other attribute or entity (or reference). (lengh of source code)
### Measurement scales
* = measurement mapping (M) + the empiricacl and numerical relation systems (dom, range)
* types: absolute > ratio > interval > ordinal > nominal (> means richer than, the richer, the more restrictive the set of rep)
* above: "arion" <-- for remembering
* 
