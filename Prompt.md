---Prompt 1
Based on api_specification.md and Readme.md,database.js act as a Senior Software Test Engineer specializing in Domain Testing (Equivalence Class Partitioning).

Focus on:
FR-03: Forgot Password and Password Reset (two-step process).

Your task is to perform ONLY the Domain Testing analysis. Do NOT perform Boundary Value Analysis and do NOT generate any test cases.

Follow this structure.

## 1. Requirement Analysis
- Summarize the functional requirements.
- Identify all user inputs.
- State any assumptions if the requirements are ambiguous.

## 2. Input Domain Identification
For each input, identify( return as list not table):
- Input name
- Data type
- Purpose
- Valid domain
- Invalid domain
- Constraints
- Dependencies with other inputs
- Assumptions


## 3. Equivalence Class Partitioning
For every input:
- Identify all valid equivalence classes.
- Identify all invalid equivalence classes.
- Assign unique IDs (EC1, EC2, ...).
- Explain why each equivalence class exists.

Present the results in a list.

## 4. Domain Testing Methodology
Provide a detailed explanation of how Domain Testing was applied step by step.

Include:
1. Study the requirements
2. Identify all inputs
3. Determine valid domains
4. Determine invalid domains
5. Partition inputs into equivalence classes
6. Verify completeness of the identified domains

Explain the reasoning behind every step.

## 5. Summary
Provide a final summary table containing:
- Input
- Valid Equivalence Classes
- Invalid Equivalence Classes
- Constraints
- Dependencies

Do NOT include boundary values.
Do NOT create any test cases.






Based on api_specification.md and Readme.md, act as a Senior Software Test Engineer specializing in Boundary Value Analysis (BVA).

Focus on:
FR-03: Forgot Password and Password Reset (two-step process).

Your task is to perform ONLY the Boundary Value Analysis. Do NOT perform Domain Testing and do NOT generate any test cases.

Follow this structure.

## 1. Requirement Analysis
- Summarize the functional requirements.
- Identify all user inputs.
- State any assumptions if the requirements are ambiguous.

## 2. Boundary Identification
For each input, identify:
- Input name
- Data type
- Validation rules
- Minimum value or minimum length (if applicable)
- Maximum value or maximum length (if applicable)
- Range constraints
- Format constraints
- Dependencies with other inputs
- Assumptions

Present the results in a table.

## 3. Boundary Value Analysis
For every input with measurable boundaries, identify:
- Just below minimum
- Minimum
- Just above minimum
- Nominal value
- Just below maximum
- Maximum
- Just above maximum

If an input has no measurable boundary (e.g., email format), explain why Boundary Value Analysis is not applicable.

Explain why each identified boundary should be tested.

Present the results in a table.

## 4. Boundary Value Analysis Methodology
Provide a detailed explanation of how Boundary Value Analysis was applied.

Include:
1. Study the requirements.
2. Identify inputs with measurable constraints.
3. Determine all lower and upper boundaries.
4. Identify representative boundary values.
5. Review completeness of boundary coverage.

Explain the reasoning behind every step.

## 5. Summary
Provide a final summary table containing:
- Input
- Constraint
- Lower Boundary
- Upper Boundary
- Boundary Values

Do NOT identify equivalence classes.
Do NOT perform Domain Testing.
Do NOT generate any test cases.









---Prompt 3.
Act as a Senior Software Test Engineer.

Using ONLY the Domain Testing analysis below, generate a comprehensive Domain Testing test suite.

Domain Testing Analysis:
[Paste the output from Prompt 1.]

Requirements:
- Cover every valid equivalence class.
- Cover every invalid equivalence class.
- Add additional test cases where necessary to achieve complete domain coverage.
- Do NOT include Boundary Value Analysis unless required to represent an equivalence class.

Generate a table with the following fields:

- Test Case ID
- Requirement
- Input(s)
- Test Data
- Equivalence Class ID
- Expected Result
- Test Type (Valid / Invalid)

Include test cases for:
- Valid inputs
- Invalid inputs
- Empty input
- Null input
- Whitespace-only input
- Incorrect data type
- Special characters
- Missing required fields
- Invalid format
- Dependency validation
- Multiple invalid inputs
- Error handling

Return test cases as table
1. Coverage Summary
2. Mapping between Equivalence Classes and Test Cases
3. Any additional recommendations to improve domain coverage.






Prompt 4
Act as a Senior Software Test Engineer specializing in Boundary Value Analysis.

Using ONLY the Boundary Value Analysis below, generate a comprehensive set of Boundary Value Analysis test cases.

Boundary Value Analysis:
[Paste the output from Prompt 2 here.]

Important rules:
- Generate test cases ONLY from the identified boundary values.
- Do NOT perform Domain Testing.
- Do NOT create or reference equivalence classes.
- Every identified boundary must be covered by at least one test case.
- Add additional boundary test cases where necessary for thorough coverage.

Generate the following table for test cases:

| Test Case ID | Input(s) | Test Data | Boundary Tested | Expected Result


If multiple inputs have boundaries, include combinations where appropriate.

