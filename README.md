# Guru99 Bank: Manual Testing Case Study

Manual functional testing of the Guru99 Bank demo banking application, focused on form validation. 237 test cases written, 127 executed, 34 bugs documented.

By Deborah Dan-Jumbo

## Project summary

| Item | Details |
|---|---|
| Application | Guru99 Bank (demo banking app) |
| Testing type | Manual functional testing, form validation |
| User role | Manager |
| Test cases | 237 across 13 modules |
| Executed | 127 (93 passed, 34 failed) |
| Bugs documented | 34 |
| Browser and version | Google Chrome 157.0.8103.39 (64-bit) |
| Operating system | Windows 11 Pro |
| Dates tested | October 2026 |
| Tools | Microsoft Excel, Git and GitHub |

## Overview

The focus of this project was form validation: what each field accepts, what it should reject, and whether the error message makes sense to the person using the screen. Every failed test case was written up as a bug report with steps to reproduce, the expected result, the actual result and a priority.

## Repository structure

```
guru99-bank-manual-testing
│
├── README.md
├── Guru99_Bank_Test_Cases_and_Bug_Report.xlsx
├── test-cases/        Test case register (CSV)
├── bug-report/        Bug report (CSV)
└── screenshots/       Evidence for each bug
```

| Item | What it is |
|---|---|
| [Test case register](test-cases/Guru99_Test_Case_Register.csv) | All 237 test cases with execution status |
| [Bug report](bug-report/Guru99_Bug_Report.csv) | The 34 failed cases, one bug each |
| [Excel workbook](Guru99_Bank_Test_Cases_and_Bug_Report.xlsx) | Both sheets in one file |
| [Screenshots](screenshots/) | Evidence for each bug, named by bug ID |

## What I tested

The register covers 13 modules: New Customer, Edit Customer, New Account, Edit Account, Delete Account, Delete Customer, Mini Statement, Customized Statement, Balance Enquiry, Fund Transfer, Withdrawal, Deposit and Change Password.

Eight of these were executed. The other five (Balance Enquiry, Fund Transfer, Withdrawal, Deposit and Change Password) are written up but not yet run. See Limitations below.

## How I approached it

Every test case in the register has the same columns: ID, module, scenario, preconditions, objective, steps, test data, expected result, actual result, status and priority. Each one checks a single thing, so when it fails there is no doubt about the cause.

For each field I tried the same kinds of input:

- a valid value
- a blank field
- a field with only spaces
- a leading space
- special characters
- letters in a number field and numbers in a text field
- a single character
- boundary values, for example an initial deposit of 499 and 0 against a minimum of 500, and a PIN that must be exactly 6 digits

Execution status is Pass, Fail, Blocked or not run. Only Fail cases went into the bug report.

## Bug report fields

Each bug has: Bug ID, Title, Module, Steps to Reproduce, Expected Result, Actual Result, Severity, Priority, Environment, Linked Test Case and Status.

## Results

| Status | Test cases | Share of 237 |
|---|---|---|
| Pass | 93 | 39% |
| Fail | 34 | 14% |
| Blocked | 66 | 28% |
| Not run | 44 | 19% |
| **Total** | **237** | **100%** |

Of the 127 cases I executed, 93 passed, which is a pass rate of about 73%.

### Results by module

| Module | Total | Pass | Fail | Blocked | Not run |
|---|---|---|---|---|---|
| New Customer | 62 | 43 | 17 | 0 | 2 |
| Edit Customer | 59 | 2 | 0 | 57 | 0 |
| New Account | 11 | 3 | 8 | 0 | 0 |
| Edit Account | 27 | 18 | 0 | 9 | 0 |
| Delete Account | 5 | 5 | 0 | 0 | 0 |
| Delete Customer | 7 | 7 | 0 | 0 | 0 |
| Mini Statement | 5 | 5 | 0 | 0 | 0 |
| Customized Statement | 19 | 10 | 9 | 0 | 0 |
| Balance Enquiry | 10 | 0 | 0 | 0 | 10 |
| Fund Transfer | 11 | 0 | 0 | 0 | 11 |
| Withdrawal | 11 | 0 | 0 | 0 | 11 |
| Deposit | 5 | 0 | 0 | 0 | 5 |
| Change Password | 5 | 0 | 0 | 0 | 5 |
| **Total** | **237** | **93** | **34** | **66** | **44** |

### Where the 34 bugs are

| Module | Area | Bugs |
|---|---|---|
| New Customer | Address | 5 |
| New Account | Customer ID | 5 |
| New Customer | Customer Name | 4 |
| Customized Statement | Amount Lower Limit | 4 |
| Customized Statement | Number of Transactions | 4 |
| New Customer | State | 3 |
| New Account | Initial Deposit | 3 |
| New Customer | City | 2 |
| New Customer | PIN | 1 |
| New Customer | Telephone | 1 |
| New Customer | Email | 1 |
| Customized Statement | Transaction date | 1 |

By priority, 3 bugs are High (all three are in Initial Deposit) and 31 are Medium.

## Key findings

**1. The wrong error message appears on valid input (9 bugs).**
In New Customer, the message "Numbers are not allowed" appears when the input has no numbers at all. It shows up for a name with a space in it ("Anita John", NC7), a city with a space ("Port Harcourt", NC27) and a state with a space ("Rivers State", NC34). It also shows up when a field starts with a space, where the expected message was "First character cannot have space" (NC10, NC24, NC32), and when a field holds only spaces, where a blank-field message was expected (NC12, NC33). A name with a trailing space is rejected with the same message instead of being trimmed or accepted (NC11). A real user typing a normal city name would be told they entered a number.

**2. The minimum initial deposit is not enforced (3 bugs, High priority).**
In New Account, entering 499 (NA11 and NA13) or 0 (NA14) in Initial Deposit gives no minimum-deposit error. The expected message was "Initial deposit must be at least 500". This is a money rule, which is why I rated these High.

**3. Customer ID in New Account is not validated (5 bugs).**
A blank value (NA2), spaces only (NA3), special characters ("123@45", NA6), letters ("123AB", NA7) and a leading space (" 1234", NA8) all fail to produce the expected error message.

**4. Leading spaces get through in other fields (5 bugs).**
The New Customer form accepts a leading space in Address (NC16), PIN (" 12345", NC43), Telephone Number (NC47) and Email (NC52) with no error. Address also accepts spaces only (NC18). The PIN case matters because the expected rule is exactly 6 digits.

**5. Address accepts content it should not (3 bugs).**
Address accepts a special character at the start ("@15 Peter Odili Road", NC17), a single letter "A" (NC19) and a single digit "1" (NC20), with no error shown.

**6. Customized Statement has missing validation messages (9 bugs).**
Amount Lower Limit and Number of Transactions do not show the expected message for special characters, letters or spaces only (CS7, CS10, CS12, CS15, CS17, CS18), and a blank value in either field shows no message (CS9 for Amount Lower Limit, CS16 for Number of Transactions). The system also accepts a From Date later than the To Date (15/01/2026 to 10/01/2026, CS21).

## Limitations

- **66 cases are blocked.** 57 in Edit Customer and 9 in Edit Account could not be run because of a connection issue.
- **44 cases have not been run.** 42 of them are in five modules (Balance Enquiry 10, Fund Transfer 11, Withdrawal 11, Deposit 5, Change Password 5) and 2 are in New Customer (NC53 and NC60).
- This is practice work on a public demo application, not a live system.

## Next steps

- Re-run the blocked Edit Customer and Edit Account cases once the connection is stable.
- Run the five modules that are still untested.
- Automate the repeatable field-validation checks with Python and Selenium.

## Author

Deborah Dan-Jumbo

- LinkedIn:
- GitHub: 
