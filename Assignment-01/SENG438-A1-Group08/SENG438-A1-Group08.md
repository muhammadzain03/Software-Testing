# SENG 438 - Software Testing, Reliability, and Quality

## Lab Report #1 - Introduction to Testing and Defect Tracking

**Group: 08**

- Muhammad Zain 
- Yazin Abdul Majid 
- Fateh Ali Syed Bukhari 

## Table of Contents

- [Introduction](#introduction)
- [High-level Description of the Exploratory Testing Plan](#high-level-description-of-the-exploratory-testing-plan)
- [Comparison of Exploratory and Manual Functional Testing](#comparison-of-exploratory-and-manual-functional-testing)
- [Notes and Discussion of the Peer Reviews of Defect Reports](#notes-and-discussion-of-the-peer-reviews-of-defect-reports)
- [How the Pair Testing Was Managed and Team Work/Effort Was Divided](#how-the-pair-testing-was-managed-and-team-workeffort-was-divided)
- [Difficulties Encountered, Challenges Overcome, and Lessons Learned](#difficulties-encountered-challenges-overcome-and-lessons-learned)
- [Comments/Feedback on the Lab and Lab Document Itself](#commentsfeedback-on-the-lab-and-lab-document-itself)
- [Use of Generative AI Tools](#use-of-generative-ai-tools)
- [References](#references)

---

## Introduction

Prior to this lab, our team had primarily theoretical knowledge of software testing concepts gained through lectures and course materials. We understood that **exploratory testing** is an informal, flexible approach where testers simultaneously learn about the system, design tests, and execute them without predetermined scripts. This method relies heavily on tester creativity, domain knowledge, and intuition to discover defects that might not be captured by formal test cases.

Regarding **manual functional testing**, we knew it involved executing predefined test cases that verify whether a system meets its specified functional requirements. These scripted tests typically include detailed steps, expected outcomes, and are designed based on requirements documentation or use case specifications. We understood that this approach ensures comprehensive coverage of known requirements and provides repeatability across testing cycles.

However, our understanding was largely conceptual. We had not yet experienced the practical differences in test execution, defect discovery patterns, or the challenges of maintaining test documentation in a real testing environment. This lab provided our first hands-on opportunity to apply both testing methodologies to an actual software system through black-box testing of the ATM simulation JAR file. With no source code access, we relied entirely on observable system behavior, documented requirements, and industry-standard defect tracking (Jira) to identify and report issues.

---

## High-level Description of the Exploratory Testing Plan

Our exploratory testing approach for the ATM simulation system was designed as a **manual, non-scripted testing phase** conducted after initial system familiarization. This phase allowed testers to freely explore system functionality without predetermined test cases, leveraging domain knowledge and intuition to uncover defects that might not be captured through formal scripted testing.

### Testing Methodology

Exploratory testing was conducted as an informal, session-based activity where test design, test execution, and defect investigation happened simultaneously. Unlike scripted testing, which follows predefined procedures, our exploratory approach relied on tester creativity, critical thinking, and real-time decision-making. This method was informed by our prior familiarization with the ATM system's basic operations, interface, and documented requirements (Appendix B), which helped us form hypotheses about where defects might occur.

### Time-Boxing and Session Structure

The exploratory testing phase was time-boxed to approximately **30 minutes per testing pair**, as specified in the lab instructions. This constraint encouraged focused exploration rather than aimless testing. Within this timeframe, we tried to balance breadth (covering multiple functional areas) with depth (thoroughly investigating suspicious behaviors or complex interactions).

### Focus Areas and Testing Objectives

Our exploratory testing plan targeted the following high-level focus areas, selected based on their criticality to ATM functionality and potential for state-dependent defects:

1. **Transaction Correctness**: Exploring the accuracy and completeness of withdrawal, deposit, transfer, and balance inquiry transactions across different account types (checking, savings, money market) and various operational conditions.

2. **Balance and Available Balance Consistency**: Investigating whether account balances and available balances are correctly maintained and displayed throughout transaction sequences, particularly after multiple consecutive operations or interrupted transactions.

3. **Account Type Validation**: Testing the system's ability to correctly distinguish between different account types, enforce account-specific rules, and handle transactions involving accounts that share common properties (e.g., both cards accessing the same checking account).

4. **Error Handling and Recovery**: Examining system responses to invalid inputs, boundary conditions, insufficient funds, insufficient cash on hand, and exceptional scenarios not fully specified in requirements documentation.

5. **Transaction Cancellation and State Management**: Exploring the correctness of cancellation functionality at various stages of each transaction type, and verifying that cancelled transactions do not leave the system in inconsistent or incorrect states.

6. **State-Dependent System Behavior**: Investigating how the system handles sequences of transactions that modify system state (cash availability, account balances), particularly focusing on transitions between states and potential race conditions or state corruption.

### Rationale for Exploratory Testing

Exploratory testing was particularly appropriate for the ATM simulation system for several reasons:

- **Complex State Space**: The ATM system maintains dynamic state (account balances, cash on hand, transaction history) that changes with each operation. Exploratory testing enables testers to investigate state-dependent defects that emerge only under specific sequences of operations, which may not be anticipated in predefined test scripts.

- **Uncovering Logic Defects**: Manual exploration allows testers to question assumptions, test boundary conditions creatively, and pursue anomalies that scripted tests might overlook. This is valuable for discovering logical errors in transaction processing, balance calculations, and validation rules.

- **Real-World Usage Patterns**: Exploratory testing encourages testers to simulate realistic user behaviors, including mistakes, unusual input patterns, and edge cases that occur in actual ATM usage but may not be formally specified in requirements.

- **Rapid Feedback on System Quality**: The non-scripted nature of exploratory testing allows for quick initial assessment of system stability and identification of high-severity defects early in the testing process.

### Results and Documentation

Our exploratory testing session identified significant defects affecting core ATM functionality. Key categories of defects discovered included:

- **Incorrect transaction amounts**: System dispensing or transferring amounts that did not match user input
- **Balance inconsistencies**: Account balances not reflecting completed transactions accurately
- **State-dependent failures**: Defects that manifested only under specific sequences of operations or system states
- **Authentication flow issues**: PIN validation and re-entry behavior not functioning as specified
- **Menu and interface defects**: Incomplete account selection menus and unexpected system responses

All defects were documented immediately upon discovery in Jira. Each report captured the function tested, initial system state, detailed reproduction steps, expected outcomes (based on Appendix B requirements), and actual outcomes, ensuring exploratory findings were reproducible and actionable. Some defects discovered during exploratory testing were later validated during Manual Functional Testing, confirming their systematic nature and reproducibility through scripted test cases.

---

## Comparison of Exploratory and Manual Functional Testing

Based on our experience conducting both exploratory and Manual Functional Testing (MFT) on the ATM simulation system, we observed several significant differences between these two approaches across multiple dimensions. Our testing identified **10 distinct defects total** across both phases, with several defects discovered through both methods and others unique to each approach. All defects are tracked in Jira with clear indication of which testing phase(s) identified them.

### Comparison Summary

| **Aspect** | **Exploratory Testing** | **Manual Functional Testing (MFT)** |
|------------|-------------------------|-------------------------------------|
| **Structure** | Flexible, adaptive strategy in real-time | Highly structured with predefined test cases |
| **Coverage** | No predefined checklist; coverage uncertain | Systematic coverage of documented requirements |
| **Approach** | Creative test design based on intuition | Follow step-by-step instructions from Appendix C |
| **Strength** | Discovers unexpected defects and edge cases | Verifies compliance with specified requirements |
| **Limitation** | Difficult to ensure comprehensive coverage | Limited ability to explore beyond scripted paths |

### Defect Discovery Effectiveness

| **Testing Phase** | **Time/Effort** | **Test Cases** | **Results** | **Key Strengths** |
|-------------------|-----------------|----------------|-------------|-------------------|
| **Exploratory Testing** | ~30 minutes | Non-scripted exploration | Discovered significant defects | Transaction errors, state corruption, authentication issues, edge cases not in formal requirements |
| **Manual Functional Testing** | Extended execution | 40 test cases (Appendix C) | 32 passed, 8 failed (7 distinct defects) | Systematic requirement verification, repeatable scenarios, measurable coverage |
| **Total** | Combined phases | - | **10 distinct defects** | Complementary discovery: some defects found by both methods, others unique to each |

The creative freedom in exploratory testing enabled testers to think like end users and attempt operations that formal requirements might not have anticipated. Notably, several defects initially discovered through exploratory testing were later validated through MFT, demonstrating overlap between the two approaches.

**Total Defect Count**: Across both testing phases, our team identified **10 distinct defects** tracked in Jira. The overlap between exploratory and manual functional testing confirmed that several critical defects could be discovered through both approaches, while some defects were unique to each method. Each Jira defect entry indicates which testing phase(s) identified it, providing traceability and demonstrating the complementary nature of both approaches.

### Execution, Repeatability, and Coverage

| **Dimension** | **Exploratory Testing** | **Manual Functional Testing (MFT)** |
|---------------|-------------------------|-------------------------------------|
| **Cognitive Effort** | High; simultaneous design, execution, observation, documentation | Lower; follow predefined step-by-step instructions |
| **Learning Curve** | Steeper; effectiveness varies with tester skill | Accessible to novice testers |
| **Repeatability** | Challenging; requires detailed documentation of exploration path | Excellent; permanent test suite record (Appendix C) |
| **Regression Testing** | Difficult; exploratory sessions inherently unique | Easily repeatable for validating bug fixes |
| **Efficiency** | Rapid defect discovery (~30 minutes) | Time-intensive but thorough |
| **Coverage Measurement** | Difficult without predefined checklist | Measurable: 80% pass rate (32/40 tests passed) |
| **Suitability** | Quick initial assessment, high-severity defects | Systematic verification, baseline for regression |

### Complementary Nature

In practice, these approaches proved highly complementary. Exploratory testing enabled rapid discovery of state-dependent issues and edge cases that might not have been anticipated in predefined test cases. Manual Functional Testing's systematic execution of 40 test cases ensured no documented requirement was missed, validated exploratory findings through repeatable scenarios, and provided a baseline for regression testing. Together, the **10 distinct defects** discovered and tracked in Jira through both methods provided comprehensive quality assessment of the ATM system. The overlap between methods confirmed the reproducibility of critical defects, while unique findings from each approach demonstrated the value of employing multiple testing strategies.

---

## Notes and Discussion of the Peer Reviews of Defect Reports

The peer review process was a critical component of ensuring high-quality defect documentation. After we completed the testing sessions (both exploratory and Manual Functional Testing), we conducted systematic peer reviews of all recorded defect reports before finalizing them in the defect tracking system.

### Peer Review Process

Our peer review workflow consisted of the following steps:

1. Since we were three in a group, only one pair independently conducted testing and documented defects in draft form
2. Pairs exchanged defect reports for cross-review
3. Reviewers evaluated each defect report against established quality criteria
4. Feedback was provided through comments in the tracking system
5. Original reporters revised defect reports based on feedback
6. A final group discussion resolved any disagreements or ambiguities

### Common Issues Identified During Review

Through the peer review process, we identified several recurring issues in initial defect reports:

| **Issue Type** | **Problem** | **Resolution** |
|----------------|-------------|----------------|
| **Missing Reproduction Steps** | Reports omitted critical details (e.g., "withdrawal fails" without initial balance, amount, or cash loaded) | Ensured steps were detailed enough for unfamiliar developers to recreate exact conditions |
| **Unclear Expected vs. Actual Results** | Lacked clear distinction between requirements and observed behavior | Emphasized citing specific Appendix B requirements when stating expected behavior |
| **Severity Misclassification** | Inconsistent severity ratings (cosmetic issues as high, functional defects as medium) | Developed shared criteria: severity based on functional impact and requirement alignment |
| **Duplicate Defects** | Same defects found by different pairs or across testing phases (PIN validation, transaction errors) | Consolidated into single Jira entries with phase tags, preserving unique observations |
| **Insufficient Environmental Info** | Missing system configuration details (starting cash, initial balances) | Ensured contextual details captured for reliable reproduction |
| **Vague Titles** | Generic titles (e.g., "Transfer doesn't work") | Required specific, searchable titles indicating function, condition, and symptom |

### Quality Improvements from Peer Review

The peer review process substantially improved defect report quality:

- **Reproducibility**: Reports became much more reproducible, with step-by-step instructions that a developer could follow without ambiguity
- **Consistency**: Severity classifications and formatting became more consistent across all defects, making prioritization easier
- **Completeness**: Reviews ensured all mandatory fields (function tested, initial state, steps, expected output, actual output) were thoroughly populated
- **Clarity**: Descriptions became more concise and focused, eliminating unnecessary details while retaining essential technical information

### Defect Tracking Integration and Jira Usage

All **10 distinct defects** identified across both Exploratory Testing and Manual Functional Testing (MFT) phases were consolidated and tracked in Jira as the single source of truth for defect management. The peer review process ensured that every defect in Jira contained complete, accurate information. Each Jira entry indicates which testing phase(s) identified the defect:
- Defects marked "Exploratory" were discovered during exploratory testing
- Defects marked "MFT" were discovered during Manual Functional Testing  
- Defects marked with both tags were independently discovered through both approaches, confirming their reproducibility

No defects exist only in external documentation-all identified issues are properly tracked in Jira with full reproduction steps, expected vs. actual outcomes, and severity classifications.

**Regression Testing in Jira**: During regression testing with Version 1.1, all 10 defects were retested. Jira status fields were updated to "Resolved" for fixed defects or remained "In Progress" with comments noting "Still exists in version 1.1" for unresolved defects. This provided complete defect lifecycle traceability across both system versions.

The peer review experience taught us that defect reporting is both a technical and communication skill. Even when a defect is clearly observed, communicating it effectively to developers requires careful attention to detail, clear writing, and understanding of what information is necessary for debugging.

---

## How the Pair Testing Was Managed and Team Work/Effort Was Divided

Our team of three members adopted a flexible and pragmatic approach to testing and workload distribution. While the lab instructions emphasized pair testing, the majority of work was conducted independently due to team availability, with collaboration occurring through discussion, cross-checking, and review to maintain quality standards.

### Pair Formation and Rotation

Our team consisted of three members: Muhammad Zain, Yazin Abdul Majid, and Fateh Ali Syed Bukhari. Due to availability constraints during the lab timeline, the primary active collaboration occurred between Muhammad Zain and Yazin Abdul Majid. Work was not carried out as strict pair programming; instead, both members worked independently and coordinated as needed through discussions, clarification of findings, and mutual review of test results and defect reports.

Fateh Ali Syed Bukhari had limited availability for much of the lab period as he was out of the country due to personal commitments. As a result, responsibilities were adjusted accordingly to ensure steady progress and timely completion of the assignment. All team members remain listed and acknowledged as part of the group submission.

### Division of Testing Responsibilities

**Exploratory Testing Phase**:
- Muhammad Zain and Yazin Abdul Majid each conducted exploratory testing independently, alternating between system operation and defect documentation
- Different functional areas were explored to maximize overall system coverage
- Findings were discussed and cross-checked to consolidate defects and avoid duplication

**Manual Functional Testing Phase**:
- All 40 test cases from Appendix C were systematically executed by dividing them into subsets based on use case grouping
- Muhammad Zain executed System Startup, System Shutdown, Session, and Withdrawal test cases (tests 1-18)
- Yazin Abdul Majid executed Deposit, Transfer, Inquiry, and Invalid PIN Extension test cases (tests 19-40)
- This division ensured comprehensive coverage while maintaining manageable individual workloads
- All test results (32 passed, 8 failed) were documented independently
- The 8 failing test cases represented 7 distinct defects, several of which had already been identified during exploratory testing
- Defects were logged in Jira with appropriate phase tags indicating discovery through exploratory testing, MFT, or both

**Regression Testing Phase (Version 1.1)**:
- All 10 Jira-tracked defects from version 1.0 were retested against version 1.1
- Regression testing responsibilities were divided between Muhammad Zain and Yazin Abdul Majid
- All 40 Manual Functional Testing test cases from Appendix C were re-executed using version 1.1
- Test case assignments remained consistent with the initial MFT phase
- Focus was placed on verifying defect fixes, identifying persistent issues, and updating Jira status fields and comments accordingly

### Communication and Coordination

Communication was maintained through periodic synchronization and review:

- **Shared Documentation in Jira**: Defect reports were entered and updated centrally, allowing visibility into discoveries and preventing duplicate submissions
- **Periodic Synchronization Points**: Discussions were held after major testing phases to compare findings and coordinate next steps
- **Peer Review Sessions**: Defect reports were cross-reviewed to ensure clarity, completeness, and consistency before finalization
- **Testing Log**: Execution of the 40 test cases was tracked to ensure full coverage and accountability

### Ensuring Consistency in Defect Reporting

To maintain consistency across defect reports:

- A shared reporting template was established at the outset, specifying required fields and formatting conventions
- Severity and priority classifications were agreed upon before testing began
- All defects underwent peer review as described in Section 4
- Consistent naming conventions were used for defect titles (e.g., "[Component] - [Symptom] under [Condition]")
- Expected outcomes were justified by referencing requirements from Appendix B

### Workload Balance

Workload distribution was managed based on availability and task complexity:

- Testing responsibilities were divided according to test suite structure and estimated effort
- Primary testing, defect tracking, and regression verification activities were handled by Muhammad Zain and Yazin Abdul Majid
- Report sections were drafted based on individual testing experience and observations, with cross-review for consistency

This flexible and adaptive approach ensured successful completion of the lab while accommodating differing levels of availability among team members.

---

## Difficulties Encountered, Challenges Overcome, and Lessons Learned

Throughout this lab, our team encountered several challenges that provided valuable learning experiences in software testing practices.

### Challenges with Exploratory Testing

**Challenge**: Initially, our exploratory testing felt aimless and inefficient. Without a predefined script, we found ourselves uncertain about what to test next and concerned about whether we were achieving adequate coverage.

**Solution**: We addressed this by developing a lightweight charter-based approach. Before beginning exploratory testing, we listed major functional areas on a whiteboard and committed to spending at least 5 minutes on each area. This gave us enough structure to ensure we covered different parts of the system while still allowing flexibility to pursue interesting observations.

**Lesson Learned**: Effective exploratory testing requires discipline and structure, not complete freedom. A high-level test plan or charter that defines goals and scope is essential for productive exploratory sessions.

### Defect Report Quality and Consistency

**Challenge**: Our initial defect reports varied significantly in quality, detail, and format. Some reports were too verbose, while others lacked sufficient detail for reproduction. This inconsistency would have created confusion for developers attempting to fix the defects.

**Solution**: After the first few defects were reported, we paused to establish a team-wide template and standards. We defined mandatory fields, created examples of well-written reports, and started the peer review process. This upfront investment in standards improved our report quality significantly.

**Lesson Learned**: Defect reporting standards should be established before testing begins, not reactively after problems emerge. Consistent, high-quality defect reports are as important as finding defects in the first place.

### Defect Duplication

**Challenge**: Both testing groups independently discovered several of the same defects, particularly obvious ones in high-traffic functionality like PIN validation. This duplication represented wasted effort and created confusion when both reports appeared in the tracking system.

**Solution**: We implemented a practice of checking the defect tracking system every 10-15 minutes during active testing. Before logging a new defect, we performed a quick search to verify it hadn't already been reported. For similar but not identical defects, we added notes to existing reports rather than creating new ones.

**Lesson Learned**: Regular synchronization and communication during parallel testing efforts is crucial. In a larger team or longer testing cycle, more sophisticated defect tracking workflows (e.g., triage meetings, designated defect coordinators) would be necessary.

### State Management and Test Independence

**Challenge**: The ATM system's stateful nature made it difficult to ensure test independence. Several discovered defects were state-dependent, manifesting only after specific transaction sequences. For example, balance discrepancies in deposits and transfers became apparent only when carefully tracking account balances across multiple operations.

**Solution**: We learned to restart the ATM system between major test sequences to restore initial conditions. We became more diligent about documenting the exact starting state (initial balances, cash loaded) in defect reports. This discipline was essential for reliably reproducing all 10 distinct defects identified across both testing phases.

**Lesson Learned**: Understanding system state and ensuring test independence is critical for reliable testing, especially when testing transactional systems where defects may only appear after specific operation sequences.

### Regression Testing Complexity

**Challenge**: During regression testing with version 1.1, we retested all 10 previously identified defects from version 1.0. Some defects appeared fixed while others persisted, requiring careful verification and Jira status updates. We also needed to execute the complete Manual Functional Testing suite again to identify any new defects introduced by fixes.

**Solution**: We expanded our regression testing beyond simply re-executing original reproduction steps. For each of the 10 defects, we tested related functionality and boundary cases to detect potential side effects or incomplete fixes. We updated Jira entries with regression test results: marking defects as "Resolved" when fixed in version 1.1, or adding comments stating "Still exists in version 1.1" for persistent defects. We also re-executed all 40 Appendix C test cases to check for regression defects.

**Lesson Learned**: Regression testing must verify both that reported defects are fixed and that fixes did not introduce new issues. The systematic retesting of all Jira-tracked defects against version 1.1, combined with full test suite re-execution, ensured accurate defect lifecycle tracking and detection of any regression issues. Jira served as the single source of truth for tracking defect status across both system versions.

### Time Management and Scope

**Challenge**: Completing all 40 Appendix C test cases, conducting exploratory testing, logging all defects in Jira, and performing peer reviews created significant time pressure.

**Solution**: We balanced thoroughness with efficiency by adopting a "capture now, refine later" approach-logging essential details immediately in Jira and enhancing reports during peer review. We also divided the test suite strategically to ensure all 40 test cases were executed without duplication of effort.

**Lesson Learned**: Effective time management in testing requires both upfront planning (clear task division) and adaptive prioritization (focusing on high-severity defects first during review and refinement).

### Tool Learning Curve

**Challenge**: Learning Jira while simultaneously conducting testing created initial overhead. We needed to understand how to properly structure defect reports, assign severity levels, track which testing phase(s) identified each defect, and maintain consistency across all team members' submissions.

**Solution**: We invested time upfront to establish templates and conventions, which proved worthwhile as we logged all defects from both exploratory and manual functional testing phases consistently into the system. We also established a tagging system to indicate whether defects were found during exploratory testing, MFT, or both.

**Lesson Learned**: Familiarity with defect tracking tools is essential. The time we spent learning Jira upfront was worthwhile because it helped us document all 10 distinct defects consistently, making them traceable and clearly linked to their discovery phase(s).

### Key Takeaways

This lab reinforced several fundamental testing principles:

1. **Testing is both systematic and creative**: The 10 distinct defects discovered demonstrate that effective testing requires both disciplined processes (systematic execution of 40 scripted tests) and creative exploration (uncovering state-dependent issues and edge cases)
2. **Documentation and traceability are critical**: All 10 defects required complete, accurate Jira reports to be actionable, with clear indication of discovery phase(s)
3. **Testing methodologies complement each other**: Some defects were discovered through both exploratory and manual functional testing, confirming their reproducibility; others were unique to each approach, demonstrating the value of employing multiple strategies
4. **Black-box testing is viable**: Without source code access, observable behavior and requirements were sufficient to identify 10 significant system defects affecting core functionality
5. **Collaboration amplifies effectiveness**: Pair testing and peer review prevented duplicate defects, consolidated findings across phases, and improved report quality

---

## Comments/Feedback on the Lab and Lab Document Itself

### Positive Aspects

**Realistic Testing Experience**: The lab provided an excellent simulation of real-world testing practices. The ATM system was sufficiently complex to present genuine testing challenges while remaining manageable within the lab timeframe. The progression from exploratory to scripted to regression testing mirrors the typical software development lifecycle and gave us practical insight into how testing evolves throughout a project.

**Clear Structure and Instructions**: The lab document was well-organized with clear objectives, step-by-step instructions, and comprehensive appendices. Appendix C's test suite was particularly valuable, providing a concrete example of professional test case documentation that we could use as a reference for our own test design.

**Hands-on Tool Experience**: Using Jira to track all 10 distinct defects across both testing phases provided valuable experience with industry-standard defect management. Learning to create consistent, professional defect reports, track defect lifecycle through regression testing, and indicate discovery phase(s) was highly practical and directly applicable to future work.

**Pair Testing Methodology**: The pair testing approach was highly effective. Having two sets of eyes on the system simultaneously improved defect detection and provided immediate peer learning opportunities. The collaborative nature also made the testing process more engaging.

### Areas for Improvement

**System Limitations and Known Issues**: It would be helpful if the lab document explicitly stated which system behaviors are intentional and which are known defects. We occasionally debated whether an observed behavior was a bug or a design decision, which consumed time during testing and defect reporting.

**Test Suite Ambiguities**: Some test cases in Appendix C had ambiguous expected results or required assumptions about system behavior not explicitly stated in Appendix B's requirements. For example, specific error messages expected by the system were not documented in requirements, making it difficult to determine if actual messages were correct. Additional clarity in test cases would reduce uncertainty.

**Regression Testing Guidance**: The regression testing section could benefit from more detailed guidance on how to interpret partial fixes or fixes that introduce new issues. We were uncertain about the appropriate defect tracking workflow when a fix resolved one problem but created another.

**Time Allocation**: While the lab was completable in the allocated time, the workload was substantial, particularly when combined with defect report peer review and final report preparation. Either extending the allocated time or reducing the scope slightly (perhaps fewer test cases in Appendix C) would reduce time pressure and allow for more thorough reflection on the testing process.

**Group Size Flexibility**: The lab instructions assumed groups of 5 members, but our group had 3 members. While we adapted successfully, explicit guidance for smaller group sizes would be helpful, including suggestions for workload adjustment or modified pair testing structures.

### Suggestions for Enhancement

1. **Add a defect reporting tutorial**: A brief tutorial or example walkthrough demonstrating how to write a high-quality defect report before testing begins would improve report consistency and quality from the start.

2. **Include test metrics**: Providing guidance on capturing simple test metrics (e.g., number of test cases executed, pass/fail rates, defect density) would add an analytical dimension to the lab and introduce students to test measurement practices.

3. **Expand requirements documentation**: Adding more detail to Appendix B, particularly regarding expected error messages and boundary condition behaviors, would reduce ambiguity during testing and defect reporting.

4. **Provide a sample defect lifecycle**: Walking through one defect from discovery through fix verification in detail would help students understand the complete defect management process.

5. **Add discussion of test automation**: While this lab appropriately focused on manual testing, a brief discussion or appendix about how these tests might be automated in practice would provide valuable context about testing evolution.

### Overall Assessment

Overall, this lab was a valuable and practical introduction to software testing. The hands-on nature, realistic system, and emphasis on both testing execution and defect documentation provided comprehensive exposure to fundamental testing concepts. The challenges we encountered were appropriate for a learning environment-difficult enough to require problem-solving and collaboration, but not so overwhelming as to be discouraging. The lab successfully achieved its stated objectives of providing practical testing experience, demonstrating differences between testing approaches, and familiarizing us with industrial defect tracking practices.

We appreciate the opportunity to apply theoretical testing concepts to a concrete system and look forward to building on these foundational skills in subsequent labs and assignments.

---

## Use of Generative AI Tools

ChatGPT (GPT-5.2 / GPT-5.x by OpenAI) was used by our team to support various aspects of lab documentation and clarification, but not for actual testing execution or defect discovery. Specifically, ChatGPT was used in the following ways:

- To clarify assignment instructions, rubric expectations, and the sequencing of testing phases (exploratory testing, manual functional testing, regression testing)
- To ask conceptual questions about testing methodology, such as what constitutes a bug, how to handle overlap between testing phases, and how to report defects correctly in Jira
- To help structure and refine Jira defect report fields, including descriptions, initial system state, steps to reproduce, and expected vs. actual results
- To help document the overlap between exploratory testing and manual functional testing, including how to phrase comments indicating whether a bug was identified during exploratory testing, MFT, or both
- To help interpret test logs and confirm whether defects were fixed or still present during regression testing of version 1.1
- To review the written lab report for clarity, consistency, and alignment with assignment requirements

**Examples of Prompts Used**

The following are representative examples of prompts used during this project (paraphrased for clarity):

- "How should we phrase Jira comments to indicate whether a defect was found during exploratory testing, manual functional testing, or both?"
- "Does this Jira issue represent a new defect or does it overlap with one already reported?"
- "Given these ATM test logs, can we conclude whether the defect is resolved or still present in version 1.1?"
- "How should regression testing results be reflected in Jira status fields and comments?"
- "How can we clearly explain the difference between exploratory testing and manual functional testing using our actual findings?"
- "How should we revise the report to correctly state that there are 10 total distinct bugs across all testing phases, considering some bugs were found in both phases?"

These prompts were used exclusively for clarification, structuring, wording, and reporting guidance. They did not involve ChatGPT performing any testing, analysis, or defect discovery activities.

**Important clarifications:**
- ChatGPT was **NOT** used to execute tests, discover bugs, or generate test results or observations
- All testing activities, defect identification, execution, verification, and Jira updates were performed manually by team members
- ChatGPT served only as a clarification and documentation support tool

---

## References

- ChatGPT (GPT-5.2 / GPT-5.x), OpenAI. Used for clarification of testing concepts, report structuring guidance, and wording refinement only.

- SENG438-Assignment01 (slides).pdf

- SENG438-A1-Instructions.md

- [Ultimate Jira Tutorial for Beginners | Free Agile Project Management Tool](https://www.youtube.com/watch?v=8jWKwiIcWPI) - YouTube
