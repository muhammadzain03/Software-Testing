# SENG 438 - Software Testing and Reliability

This repository contains all assignments completed for **SENG 438 - Software Testing, Reliability, and Quality** at the University of Calgary.

## Group Members
- Muhammad Zain
- Yazin Abdul Majid
- Fateh Ali Syed Bukhari

---

## Assignments

### [Assignment 1 - Introduction to Testing and Defect Tracking](Assignment-01/)
Exploratory testing, manual functional testing (MFT), and regression testing of an ATM simulation system. Defect tracking was performed using Jira. Covers the differences between scripted and non-scripted testing approaches.

### [Assignment 2 - Requirements-Based Test Generation](Assignment-02/)
Black-box unit testing of `DataUtilities` and `Range` classes from the JFreeChart library using JUnit 5. Test cases were designed using equivalence class partitioning and boundary value analysis based solely on Javadoc API specifications.

### [Assignment 3 - Code Coverage, Adequacy Criteria, and Test Case Correlation](Assignment-03/)
White-box testing building on Assignment 2 by measuring and improving code coverage using EclEmma (JaCoCo). Includes control-flow coverage measurement, manual data-flow (DU-pair) coverage analysis, and test suite enhancement targeting statement, branch, and method coverage goals.

### [Assignment 4 - Mutation Testing and Web App Testing](Assignment%2004/)
Mutation testing using PIT (Pitest) to evaluate and strengthen JUnit test suites for JFreeChart classes, along with GUI testing of a web application using Selenium IDE. Includes mutation analysis and comparison with alternative GUI testing tools.

### [Assignment 5 - Software Reliability Assessment](Assignment-05/)
Reliability assessment using two techniques: Reliability Growth Testing with C-SFRAT for failure data modeling, and Reliability Demonstration Chart (RDC) analysis using RDC-11 to evaluate whether the system under test meets a target MTTF.

---

## Tools and Technologies
- **JUnit 5** - Unit testing framework
- **Mockito** - Mocking framework
- **EclEmma (JaCoCo)** - Code coverage measurement
- **PIT (Pitest)** - Mutation testing
- **Selenium IDE** - GUI/web application testing
- **C-SFRAT** - Reliability growth testing
- **RDC-11** - Reliability demonstration charts
- **Jira** - Defect tracking
- **Eclipse IDE** - Development and test execution
