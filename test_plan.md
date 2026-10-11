# Test Plan: Sauce Demo (Swag Labs) E-commerce Web Application

| **Item** | **Detail** |
| :-: | :-: |
| Project | QA Portfolio – Sauce Demo |
| Application under test | https://www.saucedemo.com |
| Author | Patrick Hui |
| Version | 1.0 |
| Date | October 2026 |

## **1. Introduction**

### **1.1 Purpose**

This document defines the scope, approach, resources and schedule for testing the Sauce Demo web application, a public practice e-commerce site. The goal is to verify that core user flows (login, product browsing, cart, checkout) work as expected, and to demonstrate a structured QA process from planning through automation and CI.

### **1.2 Objectives**

- Verify functional correctness of login, inventory, cart and checkout flows. 

- Identify and document defects with clear reproduction steps. 

- Automate the core regression suite using Playwright. 

- Run the automated suite automatically through GitHub Actions. 

## **2. Scope**

### **2.1 In Scope**

| **Module** | **Features** |
| :-: | :-: |
| Login / Logout | Valid and invalid login, account locked, empty fields, logout via menu, close browser session |
| Inventory page | Product list display, product detail page, sorting (name and price) |
| Shopping cart | Add / remove items, cart items count, cart status while navigating |
| Checkout | Customer information form validation, order overview, price calculation, order completion |
| Navigation | Burger menu, Reset App State, About link, back/continue navigation |
| Cross-browser | Chromium, Firefox, WebKit (via Playwright) |

### **2.2 Out of Scope**

- Performance and load testing of the hosting server 

- Security / penetration testing 

- Native mobile apps 

- Payment gateway integration (not present in the demo) 

## **3. Test Items and Test Data**

### **3.1 Test Users (provided on the login page)**

| **Username** | **Expected behaviour** |
| :-: | :-: |
| standard\_user | Normal behaviour |
| locked\_out\_user | Login rejected with locked-out message |
| problem\_user | Known UI/functional issues (e.g. broken images, cart problems) |
| performance\_glitch\_user | Slow responses on login/actions |
| error\_user | Errors during certain actions |
| visual\_user | Visual/layout differences |

All users share the password listed on the login page.

### **3.2 Test Data**

- Valid checkout info: First Name, Last Name, Postal Code 

- Invalid checkout info: blank fields, one field missing at a time 

- Product set: all 6 inventory items 

## **4. Test Approach**

| **Test Type** | **Description** | **Tool** |
| :-: | :-: | :-: |
| Functional (manual) | Execute test cases against each module; record results | Google Sheets / Browser |
| Exploratory | Time-boxed sessions (30 min per module) to find unscripted defects | Browser DevTools |
| Negative testing | Invalid inputs, boundary cases, unauthorized URL access | Manual |
| Regression (automated) | Core scenarios automated for repeatable runs | Playwright (Python) |
| Cross-browser | Run automated suite on Chromium, Firefox, WebKit | Playwright |
| Compatibility / Responsive | Check layout at desktop, tablet, mobile viewports | Browser DevTools |
| CI execution | Run suite on every push / pull request | GitHub Actions |

### **4.1 Test Case Prioritization**

- **P1 (Critical):** Login, add to cart, complete checkout 

- **P2 (High):** Sorting, remove from cart, checkout validation, logout 

- **P3 (Medium):** Navigation links, menu, UI consistency 

### **4.2 Automation Strategy**

- Use Page Object Model: separate page classes (LoginPage, InventoryPage, CartPage, CheckoutPage) from test logic. 

- Automate P1 and selected P2 cases (target: 8–10 cases). 

- Generate an HTML report after every run. 

## **5. Entry and Exit Criteria**

### **5.1 Entry Criteria**

- Test environment (saucedemo.com) is accessible. 

- Test plan and test cases are reviewed. 

- Test users and test data are available. 

### **5.2 Exit Criteria**

- 100% of P1 test cases executed and passed (or defects logged). 

- At least 90% of all planned test cases executed. 

- No open Critical or High defects without documentation. 

- Automation suite runs successfully in CI. 

### **5.3 Suspension / Resumption**

- Suspend testing if the site is unavailable or login is blocked for all users; resume when access is restored. 

## **6. Test Environment**

| **Item** | **Detail** |
| :-: | :-: |
| Application | https://www.saucedemo.com (public, hosted) |
| OS | Windows 11 / macOS (local), Ubuntu (GitHub Actions) |
| Browsers | Latest Chrome, Firefox, Safari (WebKit) |
| Automation | Python 3.x, Playwright, pytest |
| API testing (separate module) | Postman, Restful-Booker |
| Defect tracking | GitHub Issues (or JIRA Free) |
| Version control / CI | GitHub, GitHub Actions |

## **7. Deliverables**

- Test plan (this document) 

- Test cases (30+) with expected and actual results 

- Defect reports (minimum 2–3 with screenshots) 

- Playwright automation source code 

- HTML test execution report 

- Test summary report 

- README with setup and run instructions 

## **8. Defect Management**

### **8.1 Severity Levels**

| **Severity** | **Definition** |
| :-: | :-: |
| Critical | Core flow blocked (e.g. cannot log in or check out) |
| High | Major feature broken, no workaround |
| Medium | Feature issue with workaround |
| Low | Cosmetic or minor usability issue |

### **8.2 Defect Report Template**

- ID, Title, Severity / Priority 

- Environment (browser, OS, user) 

- Steps to reproduce 

- Expected result 

- Actual result 

- Screenshot / video 

- Status (New, Open, Fixed, Retest, Closed) 

## **9. Risks and Mitigation**

| **Risk** | **Impact** | **Mitigation** |
| :-: | :-: | :-: |
| Public site may change or go down | Tests fail unexpectedly | Re-verify manually; version-pin test data; keep screenshots as evidence |
| Intentionally buggy users (problem\_user etc.) | Many failures | Document as expected known issues; separate from standard\_user results |
| Flaky automated tests (timing) | Unreliable CI | Use Playwright auto-wait; avoid fixed sleeps |
| Limited time (part-time effort) | Delays | Prioritize P1 first; time-box exploratory testing |

## **10. Schedule**

| **Week** | **Activity** |
| :-: | :-: |
| 1 | Test plan, test cases, manual execution, defect reports |
| 2 | API testing (Postman, Restful-Booker) |
| 3–4 | Playwright UI automation, HTML reporting |
| 5 | GitHub Actions CI, README, test summary report |

## **11. Roles and Responsibilities**

| **Role** | **Responsibility** |
| :-: | :-: |
| QA Analyst (Patrick Hui) | Plan, design, execute, automate, report |

## **12. Test Cases Overview (high-level)**

| **ID** | **Module** | **Scenario** | **Priority** |
| :-: | :-: | :-: | :-: |
| TC-001 | Login | Valid login with standard\_user | P1 |
| TC-002 | Login | Login with locked\_out\_user shows error | P1 |
| TC-003 | Login | Invalid password shows error | P2 |
| TC-004 | Login | Empty username / password validation | P2 |
| TC-005 | Login | Logout returns to login page | P2 |
| TC-006 | Inventory | All 6 products displayed with name, price, image | P2 |
| TC-007 | Inventory | Sort by price low to high | P2 |
| TC-008 | Inventory | Sort by name Z to A | P3 |
| TC-009 | Cart | Add single item updates cart badge | P1 |
| TC-010 | Cart | Add multiple items | P1 |
| TC-011 | Cart | Remove item from cart page | P2 |
| TC-012 | Checkout | Complete purchase with valid info | P1 |
| TC-013 | Checkout | Missing first name shows error | P2 |
| TC-014 | Checkout | Missing postal code shows error | P2 |
| TC-015 | Checkout | Item total, tax and total calculated correctly | P1 |
| TC-016 | Navigation | Direct URL access to inventory without login is blocked | P2 |
| TC-017 | Navigation | Reset App State clears cart | P3 |
| TC-018 | UI | problem\_user: verify product images and cart behaviour | P3 |
| TC-019 | Performance | performance\_glitch\_user login completes within acceptable time | P3 |
| TC-020 | Cross-browser | Core checkout flow on Chromium, Firefox, WebKit | P2 |

*(Detailed steps and expected results are documented in the test case spreadsheet.)*

## **13. Approval**

| **Name** | **Role** | **Date** |
| :-: | :-: | :-: |
| Patrick Hui | QA Analyst |  |

