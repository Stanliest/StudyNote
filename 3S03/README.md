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
1. 
