# Boundary Value Analysis - FR-03: Forgot Password and Password Reset

## 1. Requirement Analysis

FR-03 describes a two-step forgot password and password reset process.

Step 1 - Get OTP:

- The user enters the email address of an already registered account.
- The system generates a random OTP containing exactly 6 digits.
- In the demo environment, the OTP is displayed directly on screen instead of being sent through email.
- The interface must show a clear step indicator, such as "Step 1 / 2".
- The interface must provide a "Back to Login" action.

Step 2 - Reset Password:

- The user enters the OTP, a new password, and confirmation of the new password.
- The new password must follow the same strong password rule as FR-01:
  - minimum 8 characters
  - at least 1 uppercase letter
  - at least 1 lowercase letter
  - at least 1 digit
  - at least 1 special character from `@`, `$`, `!`, `%`, `*`, `?`, `&`
- The new password and confirmation password must match.
- The OTP is valid only for the email address that requested it and cannot be used for another email address.

Identified user inputs:

| Step | User input |
| --- | --- |
| Step 1 | Email address |
| Step 2 | Email address or stored email context |
| Step 2 | OTP / reset token |
| Step 2 | New password |
| Step 2 | Confirm new password |

Assumptions:

- The email field is required because the system cannot generate or validate an OTP without an account email.
- The API specification for `POST /api/reset-password` includes `email`, `resetToken`, and `newPassword`, while the system requirement also requires confirm new password. For BVA, confirm new password is treated as a required UI/input field because FR-03 explicitly states it.
- OTP is treated as a string of digits, not a numeric integer, so leading zeroes can remain valid.
- The OTP must be exactly 6 numeric digits.
- The new password has a measurable minimum length of 8 characters.
- No maximum length is specified for email, OTP, new password, or confirm new password.
- Email format, password composition, OTP ownership, and password match are validation rules, but only length or numeric limits are considered measurable BVA boundaries.

## 2. Boundary Identification

| Input name | Validation rules | Minimum value or minimum length | Maximum value or maximum length | Range constraints | Assumptions |
| --- | --- | --- | --- | --- | --- |
| Email address | Must be a registered email address and must have valid email format | Not specified | Not specified | No measurable numeric or length range is stated in FR-03 | BVA is not directly applicable unless a length limit is later specified. |
| OTP / reset token | Must be the OTP generated for the submitted/requesting email; must contain exactly 6 digits | 6 digits | 6 digits | Exact length = 6 numeric digits | Treat as a digit string so OTP values such as `000001` are possible. |
| New password | Minimum 8 characters; must contain uppercase, lowercase, digit, and allowed special character | 8 characters | Not specified | Length must be greater than or equal to 8 | Only the lower length boundary is measurable. Composition rules are not BVA boundaries. |
| Confirm new password | Must match the new password | Same effective minimum as new password when matching: 8 characters | Not specified | Must be identical to new password | Its measurable boundary is dependent on the new password length boundary. |

## 3. Boundary Value Analysis

| Input | Just below minimum | Minimum | Just above minimum | Nominal value | Just below maximum | Maximum | Just above maximum | BVA applicability and reason |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Email address | N/A | N/A | N/A | `test@eshop.com` | N/A | N/A | N/A | BVA is not applicable because FR-03 specifies format and registration status, but no measurable length or numeric boundary. |
| OTP / reset token | 5 digits, e.g. `12345` | 6 digits, e.g. `123456` | 7 digits, e.g. `1234567` | 6 digits, e.g. `654321` | N/A | 6 digits, e.g. `123456` | 7 digits, e.g. `1234567` | Applicable because OTP has an exact measurable length of 6 digits. Since minimum and maximum valid length are both 6, values immediately below and above 6 digits are boundary-adjacent invalid values. |
| New password | 7 characters, e.g. `Aa1!aaa` | 8 characters, e.g. `Aa1!aaaa` | 9 characters, e.g. `Aa1!aaaaa` | 12 characters, e.g. `Aa1!Password` | N/A | N/A | N/A | Applicable for the lower boundary because the requirement defines minimum length 8. Upper-bound BVA cannot be derived because no maximum length is specified. |
| Confirm new password | 7 characters matching a 7-character new password candidate | 8 characters matching the new password | 9 characters matching the new password | Same value as a nominal valid new password | N/A | N/A | N/A | Applicable only through dependency on the new password length boundary and match rule. It has no independent maximum boundary. |

Why each identified boundary should be tested:

| Boundary | Reason |
| --- | --- |
| OTP length = 5 digits | Verifies rejection immediately below the exact 6-digit requirement. |
| OTP length = 6 digits | Verifies acceptance at the only valid OTP length when the OTP belongs to the email. |
| OTP length = 7 digits | Verifies rejection immediately above the exact 6-digit requirement. |
| New password length = 7 characters | Verifies rejection immediately below the minimum password length. |
| New password length = 8 characters | Verifies acceptance at the minimum valid password length when composition rules are also satisfied. |
| New password length = 9 characters | Verifies acceptance immediately above the minimum password length when composition rules are also satisfied. |
| Confirm password length = 7 characters | Verifies that matching confirmation cannot make an under-length new password valid. |
| Confirm password length = 8 characters | Verifies confirmation works at the minimum valid password length when it matches the new password. |
| Confirm password length = 9 characters | Verifies confirmation works immediately above the minimum valid password length when it matches the new password. |

## 4. Boundary Value Analysis Methodology

1. Study the requirements.

FR-03 was isolated from the full system specification. The requirement was decomposed into Step 1, where the user requests an OTP by email, and Step 2, where the user resets the password using the OTP, new password, and confirmation password. UI requirements such as step indicator and back-to-login action were reviewed but excluded from BVA tables because they do not define input ranges.

2. Identify inputs with measurable constraints.

Each input was checked for numeric or length-based constraints. OTP has a measurable exact length. New password has a measurable minimum length. Confirm new password depends on the new password and therefore inherits the password length boundary. Email has format and registration constraints, but no measurable boundary in FR-03.

3. Determine all lower and upper boundaries.

OTP has both its valid minimum and valid maximum at 6 digits because it must be exactly 6 digits. New password has a lower boundary at 8 characters. Confirm new password has the same effective lower boundary when matching the new password. No upper boundary is stated for password or confirmation password, so no maximum-side password BVA values can be justified from the requirement.

4. Identify representative boundary values.

For OTP, the representative boundary values are 5, 6, and 7 digits. For password length, the representative values are 7, 8, and 9 characters. Password examples include all required character categories so the boundary analysis focuses on length rather than unrelated composition failures.

5. Review completeness of boundary coverage.

The analysis covers all measurable FR-03 boundaries: OTP exact length, new password minimum length, and confirm password length through the match dependency. Non-measurable validations, including email format, registered email existence, OTP-email association, password composition, and field matching, are noted only as validation context and are not expanded into Domain Testing, equivalence classes, or test cases.
