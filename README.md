# Test Strategy: Swag-labs E-Commerce

| Document Info | Details |
| :--- | :--- |
| **Project** | Swag-labs E-Commerce |
| **QA Lead** | Kenneth Flororita |
| **Version** | 1.0 |
| **Estimated Duration** | 8 Business Days (~64 Hours) |

---

## 1. Executive Summary
The test will focus on verification of end-to-end services together with both ends of the system (frontend (UI level of the application) as well as the backend (logic level of the application)). The test will revolve around the objective of ensuring the system delivers high quality performance while maintaining its stability throughout the test.

The project name is entitled "Test Strategy: Swag-labs E-Commerce", straightforward and concise. The test will consume a total time of 8 business days, which is approximately 64 hours. The test can go beyond the envisioned timeline for deeper analysis of the current services.

---

## 2. Scope of Testing
The test will cover end-to-end test of system stability while the user safely purchases a product.

### In Scope
#### **Authentication Module**
* **Login Functionality:**
    1. Verify successful login with valid credentials (`standard_user`).
    2. Verify access denial for locked accounts (`locked_out_user`).
    3. Verify error message appearance for invalid passwords.
* **Logout Functionality:**
    1. Verify user is redirected to the Login Page upon clicking "Logout."
    2. **Session Security:** Verify that clicking the browser "Back" button after logging out does not log the user back in.
* **Session Timeout Simulation:**
    1. Verify system timeout simulation.

#### **Product and Inventory**
* **Price Consistency:**
    1. Verify correct calculation of prices during purchase.
    2. Verify accurate price for multiple quantity of single products during purchase.
    3. Verify appropriate tax addition for prices during purchase.
* **Sorting Logic:**
    1. Verify accurate sorting for Prices (Low to High and High to Low).
    2. Verify accurate sorting for Names (A to Z and Z to A).
* **Product Details:**
    1. Verify accurate details per product.
    2. Ensure consistent product details when in different tabs.

#### **Cart and Checkout**
* **Adding and Removing items:**
    1. Verify accurate responses when products are added to cart.
    2. Verify correct responses when products are removed from cart.
* **Cart persistence:**
    1. Verify added product is still in cart even after logging out.
    2. Ensure product is truly removed by going through checkout right after pressing "Remove".
* **Checkout data validation:**
    1. Verify system response when checking out without First Name.
    2. Verify system response when checking out without Last Name.
    3. Verify system response when checking out without Postal Code.
    4. Verify order completion and "Thank You" page verification.

### Out of Scope
* **Payment gateway processing:** The environment uses a mock payment system; real credit cards are not processed.
* **Performance/Load Testing:** JMeter/LoadRunner testing is not required for this sprint.
* **Mobile Native App:** Testing is limited to Mobile Web Browsers (Chrome Responsive View), not the native APK/IPA files themselves.

---

## 3. Test Environment
* **System/App URL:** https://www.saucedemo.com/
* **Primary Browser:** Google Chrome (Latest Version)
* **Secondary Browser:** Mozilla Firefox (Latest Version)

*Please note that in mobile responsiveness testing we'll utilize the Chrome DevTools "Device Toolbar" (we'll emulate iPhone 12 and also Pixel 7).*

---

## 4. Testing Approach Utilized
The test will implement "Persona-Based Testing" to mimic real-world app usage as well as user behaviors.

| Persona | Role | Testing Objective |
| :--- | :--- | :--- |
| **standard_user** | **Happy Path** | The user will use the `standard_user` account to verify the correct flow where a user purchases an item without any errors. |
| **problem_user** | **Defect Hunting** | The user will log in the `problem_user` account to intentionally identify hidden errors ranging from UI issues to status code responses. |
| **locked_out_user** | **Security Verification** | The user will log in the `locked_out_user` account to see if the app correctly blocks the unauthorized and banned accounts. |
| **performance_glitch_user** | **Usability Specs** | The user will use the `performance_glitch_user` account to ensure that the UI remains stable even during network lag (this will be simulated). |

---

## 5. Defect Management / Bug Process
All defects found will be documented in Jira to properly handle issues. The issues found are sought to be classified in:

* **Critical (Severity 1): Complete App Block**
    * The user cannot even login or even complete checking out. This will be marked as critical because these issues will destroy the trust and usage of its users. Functional requirements aren't met.
* **High (Severity 2): Major feature breakage**
    * A workaround exists but it is difficult (e.g., "Sort by Price is broken"). Sought as High because the app does function but nowhere near enough to meet business requirements.
* **Medium (Severity 3): UI Issue**
    * Noticeable issues which require attention like product image misalignment causing UI distortion. Viewed as Medium which portrays not that heavy of an issue but can still crack the company's image.
* **Low (Severity 4): Minor Typo or QA suggestion**
    * Simple issues that can still somehow affect the company's uniformity. Might be minor Typo in footer, issues deemed as "Low" because it doesn't affect the company normally but can still be noticeable when one really seeks for issues.

---

## 6. Risks & Mitigation
The main risks lie on the usage of accounts discussed in section 4 (Testing Approach Utilized). These risks are (mitigations are also sought to be implemented to reduce the chances of present risks):

| Identified Risk | Mitigation Strategy |
| :--- | :--- |
| **Sandbox Stability** | The site "saucedemo" is public which may result in unexpected data resets. To properly mitigate the risk, the QA will implement "Atomic Tests" (or independent tests) that do not rely solely on long-term data storage. |
| **Defect Injection** | The `problem_user` account has "native" bugs that are "features" of the site. Defects found under `problem_user` will be marked as "Expected Behavior" for that specific persona but will still be documented for implementation practice. |
---

## 7. Entry & Exit Criteria
### Entry Criteria (Start)
1. Make sure that test environment discussed in section 3 is accessible.
2. Test Cases/Checklists are properly reviewed as well as approved.

### Exit Criteria (Stop)
1. A solid 100% of "Critical" as well as "High" Priority Test Cases are thoroughly executed.
2. Absence of "Severity 1 (Blocker)" bugs that stay open.
3. Test summary report is completed and generated.
