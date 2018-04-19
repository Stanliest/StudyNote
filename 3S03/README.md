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
Total number of pikes originally in lake soft is: (M-M')*(N/M')
