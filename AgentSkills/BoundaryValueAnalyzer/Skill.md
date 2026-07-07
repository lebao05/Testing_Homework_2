Based on Context.md act as a Senior Software Test Engineer specializing in Boundary Value Analysis (BVA).

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
- Validation rules
- Minimum value or minimum length (if applicable)
- Maximum value or maximum length (if applicable)
- Range constraints
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
And Write output into file Output.md

Do NOT identify equivalence classes.
Do NOT perform Domain Testing.
Do NOT generate any test cases.