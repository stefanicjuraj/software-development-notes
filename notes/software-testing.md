# Testing in Software Development

Software Testing is the process of identifying the accuracy and quality of the software product. It checks whether the developed software meets the specified requirements and identifies any defect in the software in order to produce a quality product.

There are many different types of software testing, and those software testing approaches can be categorized in different ways, depending on **how** the tests are being conducted and **what** is being tested.

## Types of Software Testing

![[types-of-software-testing.png]]

### Manual Testing

The software is tested manually, without using any automated tool or script. The tester takes over the role of an end-user and tests the software to identify any unexpected behavior.

### Automated Testing

This type of testing requires writing scripts and uses another software or tool to test the product. This process automates the manual testing process.

## Stages of Software Testing

Software testing is usually broken down into 4 different stages and executed in this order: **Unit Testing**, **Integration Testing**, **System Testing**, and **User Acceptance Testing**.

Testers use **test plans**, **test cases**, or **test scenarios** to test a software to ensure the completeness of testing.

![[stages-of-software-testing.png]]

### Unit Testing

**Individual methods and classes** are being tested, but not larger configurations of the program/system. The developer who does the unit testing knows all the method signatures and the data being used. This type of testing is also known as white-box testing because the tester sees all the details of the code being tested.

**The traditional approach** assumes writing your code first, get it to compile, so you have eliminated the syntax errors, and then write your tests and do the unit testing. In this strategy testing and debugging occur pretty much simultaneously: you find an error, fix it, and then re-run the failed test right away.

**A newer strategy** is found in the [agile methodologies](agile-model), especially in Extreme Programming which is called development **test-driven development (TDD)**. In TDD, your unit tests are written before any code is implemented. The goal in this strategy is to get all the tests to pass as you write the code.

**What to Test in Unit Testing?**

Every **line of code** with good and bad **data**

**Code coverage** is a measure which describes the degree which the source code of the program has been tested. Code coverage testing requires executing every line of code in program at least once with representative data to assure that all the code functions correctly.

**The objective is to test every statement in the program.**

Sequential statements normally require one test per different data type.

Branch coverage requires testing if-else and switch statements, and every complex conditional expression (those that contain AND and OR operators).

- For every if statement you’ll need two tests – one for when the conditional expression is true and one for when it’s false.
- For every switch statement in your method you’ll need a separate test for each case clause in the switch.
- The logical and (_&&_) and or (_||_) operators add more complexity to your conditional expressions - you need extra test cases for those.

**Loop coverage** requires testing the for, while, or do-while loops. There are different test that need to be done:

- Introduce and test the off-by-one error (OBOE).
  - It occurs when a loop iterates one time too many or too few. This problem arises when a programmer makes mistakes such as using _<=_ where _<_ should have been used in a comparison, or fails to take into account that a sequence starts at zero rather than one.
- Test for a normal run through the loop.
- Pre-test loops so that the loop body is never entered – the loop conditional expression fails the very first time.
- Test for an infinite loop – the conditional expression never becomes false.
- For loops that read files, test for the end-of-file marker (EOF).

**Test the return values.**

**Data coverage** is a measure which describes the degree to which representative samples of good and bad data (both input & output) are being used in testing to assure that the program handles data and particularly data errors correctly.

**Test Good Data**. It requires testing if the data is of the correct type and within the **correct type** and **within the correct ranges**. Aside of these, following special cases also need to be tested:

- Test boundary conditions.
  - This requires testing data near the edges of the range of your valid data. For example, if your data values fall between _0_ and _100_ inclusive, you should test values at _0_, _1_, _99_, and _100_, as well as invalid values at _-1_, and _101_.
- Test typical data values.
  - This requires testing valid data values - the ones you expect to get. Following the previous example, you might check _30_, _50_, _75_, _83_, and so on.
- Test pre- and post-conditions.
  - Entering OR leaving a control structure or a method call is based on an assumption either about:
    - data values and the state of the computations (pre-conditions). A pre-condition is a statement or set of statements that describe a condition that should be true right before a function is called.
    - exit/return values (post-conditions). A post-condition is a statement or set of statements describing the outcome of the code execution - what needs to be true when the execution finishes its task.

**Test Dad Data**.

- Illegal data values.
  - You should test data that is offensively illegal to make sure that your data validation code is working.
- No data.
  - Test the case where data are expected but nothing is provided in return.
- Uninitialized variables.
  - Most language systems provide default initial values for any variable that is declared. Regardless, you should test that the variables are initialized correctly and not depend on the system's default values.

### Integration Testing

This is the testing of a **collection of classes** that interact with each other, and is performed after the unit tested code is integrated into the source code base. Its purpose is to test interface between modules or classes and the interactions between the modules. Testers know about the interfaces but they are not aware of how each module is implemented. This type of testing is also called gray-box testing.

### System Testing

This is the **testing of the entire program** (the system). The testers do not know anything about how the program is designed or written. Testers only know the inputs the system takes and the outputs it produces. This type of testing is also known as black-box testing.

### User Acceptance Testing

Tests that the software meets the requirements described in the business users’ requirements document. Business users usually participate in this testing.

## Developers & Testers

Based on the requirements, developers produce a design and write the code that implements the design. Developers are focused on getting the code to work.

Based on the requirements and the code developers have implemented, a tester’s job is to get the code to break, to expose the errors.

The developer then needs to fix those errors.

Most software development organizations have a separate testing team, particularly for integration and system testing.

_Unit testing is usually the developer's responsibility._
