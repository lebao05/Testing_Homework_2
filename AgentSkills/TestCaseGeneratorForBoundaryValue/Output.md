# Boundary Value Analysis Test Cases - FR-03: Forgot Password and Password Reset

| Test Case ID | Input(s) | Test Data | Boundary Tested | Expected Result |
| --- | --- | --- | --- | --- |
| BVA-FR03-001 | Email | `test@eshop.com` | Email has no measurable BVA boundary; valid nominal value used to reach OTP step | System accepts registered valid email and generates/displays a 6-digit OTP. |
| BVA-FR03-002 | Email | Empty string `""` | Required email input with no measurable boundary | System rejects the request, reports email is required/invalid, and does not generate OTP. |
| BVA-FR03-003 | Email | `null` | Null email input with no measurable boundary | System rejects the request, handles null safely, and does not generate OTP. |
| BVA-FR03-004 | Email | Whitespace only `"   "` | Whitespace-only email input with no measurable boundary | System rejects the request as missing/invalid email and does not generate OTP. |
| BVA-FR03-005 | Email | Missing `email` field | Missing required field | System rejects the request and does not generate OTP. |
| BVA-FR03-006 | Email | Number `12345` | Incorrect data type for email | System rejects the request or handles the type safely without generating OTP. |
| BVA-FR03-007 | Email | `test@@eshop.com` | Invalid format for email; no measurable BVA boundary | System rejects invalid email format and does not generate OTP. |
| BVA-FR03-008 | OTP / reset token | `12345` | Just below exact OTP boundary: 5 digits | System rejects OTP because it is shorter than exactly 6 digits. |
| BVA-FR03-009 | OTP / reset token | `123456` | Exact OTP minimum/maximum boundary: 6 digits | System accepts OTP length when the OTP matches the value generated for the submitted/requesting email. |
| BVA-FR03-010 | OTP / reset token | `000001` | Exact OTP boundary with leading zeroes | System treats OTP as a digit string and accepts the 6-digit format when it matches the generated OTP. |
| BVA-FR03-011 | OTP / reset token | `654321` | Nominal 6-digit OTP value | System accepts OTP length when the OTP matches the value generated for the submitted/requesting email. |
| BVA-FR03-012 | OTP / reset token | `1234567` | Just above exact OTP boundary: 7 digits | System rejects OTP because it is longer than exactly 6 digits. |
| BVA-FR03-013 | OTP / reset token | Empty string `""` | Empty OTP below 6-digit boundary | System rejects OTP as required and not exactly 6 digits. |
| BVA-FR03-014 | OTP / reset token | `null` | Null OTP below 6-digit boundary | System rejects OTP as required and handles null safely. |
| BVA-FR03-015 | OTP / reset token | Whitespace only `"      "` | Six characters at OTP length boundary but not digits | System rejects OTP because it is not 6 numeric digits. |
| BVA-FR03-016 | OTP / reset token | Number `123456` | Incorrect data type at 6-digit boundary | System either converts safely to a 6-digit string by explicit design or rejects with validation error; password is not reset unless OTP is valid for the email. |
| BVA-FR03-017 | OTP / reset token | `12345A` | Six-character boundary with non-numeric character | System rejects OTP because it is not 6 numeric digits. |
| BVA-FR03-018 | OTP / reset token | `12345!` | Six-character boundary with special character | System rejects OTP because it is not 6 numeric digits. |
| BVA-FR03-019 | OTP / reset token | Missing `resetToken` field | Missing required OTP field | System rejects reset request and does not change the password. |
| BVA-FR03-020 | Email + OTP / reset token | Email `other@eshop.com`, OTP `123456` generated for `test@eshop.com` | Dependency validation at valid 6-digit OTP boundary | System rejects reset because OTP is not valid for the submitted/requesting email. |
| BVA-FR03-021 | New password | `Aa1!aaa` | Just below password minimum: 7 characters | System rejects new password because it is shorter than 8 characters. |
| BVA-FR03-022 | New password | `Aa1!aaaa` | Password minimum boundary: 8 characters | System accepts password length when all required character categories are present. |
| BVA-FR03-023 | New password | `Aa1!aaaaa` | Just above password minimum: 9 characters | System accepts password length when all required character categories are present. |
| BVA-FR03-024 | New password | `Aa1!Password` | Nominal password value: 12 characters | System accepts password length when all required character categories are present. |
| BVA-FR03-025 | New password | Empty string `""` | Empty password below 8-character boundary | System rejects new password as required and shorter than 8 characters. |
| BVA-FR03-026 | New password | `null` | Null password below 8-character boundary | System rejects new password as required and handles null safely. |
| BVA-FR03-027 | New password | Whitespace only `"        "` | Eight-character password boundary with invalid content | System rejects password because composition rules are not satisfied even though length is 8. |
| BVA-FR03-028 | New password | Array/object value instead of string | Incorrect data type for password | System rejects the value or handles it safely without changing the password. |
| BVA-FR03-029 | New password | `12345678` | Eight-character password boundary with invalid composition | System rejects password because required uppercase, lowercase, and allowed special character are missing. |
| BVA-FR03-030 | New password | Missing `newPassword` field | Missing required new password field | System rejects reset request and does not change the password. |
| BVA-FR03-031 | Confirm new password | New password `Aa1!aaa`; confirm `Aa1!aaa` | Confirm password matching at invalid 7-character boundary | System rejects reset because the matching password value is still below the 8-character minimum. |
| BVA-FR03-032 | Confirm new password | New password `Aa1!aaaa`; confirm `Aa1!aaaa` | Confirm password matching at valid 8-character boundary | System accepts confirmation when OTP is valid and the new password satisfies all password rules. |
| BVA-FR03-033 | Confirm new password | New password `Aa1!aaaaa`; confirm `Aa1!aaaaa` | Confirm password matching just above valid boundary: 9 characters | System accepts confirmation when OTP is valid and the new password satisfies all password rules. |
| BVA-FR03-034 | Confirm new password | New password `Aa1!aaaa`; confirm `Aa1!aaa` | Confirmation just below password boundary and mismatch | System rejects reset because confirmation does not match the new password. |
| BVA-FR03-035 | Confirm new password | New password `Aa1!aaaa`; confirm `Aa1!aaaaa` | Confirmation just above password boundary and mismatch | System rejects reset because confirmation does not match the new password. |
| BVA-FR03-036 | Confirm new password | New password `Aa1!aaaa`; confirm empty string `""` | Empty confirmation below 8-character boundary | System rejects reset because confirmation is required and does not match. |
| BVA-FR03-037 | Confirm new password | New password `Aa1!aaaa`; confirm `null` | Null confirmation below 8-character boundary | System rejects reset because confirmation is required and handles null safely. |
| BVA-FR03-038 | Confirm new password | New password `Aa1!aaaa`; confirm whitespace only `"        "` | Eight-character confirmation boundary with mismatch/invalid content | System rejects reset because confirmation does not match the new password. |
| BVA-FR03-039 | Confirm new password | Missing `confirmNewPassword` field | Missing required confirmation field | System rejects reset request and does not change the password. |
| BVA-FR03-040 | Email + OTP + New password + Confirm new password | Email `test@eshop.com`, OTP `123456`, new password `Aa1!aaaa`, confirm `Aa1!aaaa` | Complete valid reset at OTP 6-digit boundary and password 8-character boundary | System resets password successfully when OTP belongs to the email. |
| BVA-FR03-041 | Email + OTP + New password + Confirm new password | Email `test@eshop.com`, OTP `654321`, new password `Aa1!aaaaa`, confirm `Aa1!aaaaa` | Complete valid reset with nominal OTP and password just above minimum | System resets password successfully when OTP belongs to the email. |
| BVA-FR03-042 | Email + OTP + New password + Confirm new password | Email `test@eshop.com`, OTP `12345`, new password `Aa1!aaa`, confirm `Aa1!aaa` | Multiple invalid boundary values: OTP 5 digits and password 7 characters | System rejects reset, reports validation errors, and does not change the password. |
| BVA-FR03-043 | Email + OTP + New password + Confirm new password | Email `test@eshop.com`, OTP `1234567`, new password `Aa1!aaaa`, confirm `Aa1!aaaaa` | Multiple invalid boundary values: OTP 7 digits and confirmation mismatch | System rejects reset and does not change the password. |
| BVA-FR03-044 | Email + OTP + New password + Confirm new password | Email missing, OTP missing, new password missing, confirm missing | Missing required fields | System rejects reset/request flow with validation errors and does not change the password. |
| BVA-FR03-045 | Email + OTP + New password + Confirm new password | Email `"   "`, OTP `"      "`, new password `"        "`, confirm `"        "` | Whitespace-only inputs; OTP/password character counts at boundaries but invalid content | System rejects request/reset and does not change the password. |
| BVA-FR03-046 | Email + OTP + New password + Confirm new password | Email `test@eshop.com`, OTP `12345!`, new password `Aa1!aaaa`, confirm `Aa1!aaaa` | Error handling for special-character OTP at 6-character boundary | System rejects invalid OTP format and does not change the password. |
