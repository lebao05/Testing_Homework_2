---Prompt 1
Based on Context.md act as a Senior Software Test Engineer specializing in Domain Testing (Equivalence Class Partitioning).

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

Write output into file Output.md

Do NOT include boundary values.
Do NOT create any test cases.

