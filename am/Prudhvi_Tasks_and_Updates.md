# Prudhvi - Tasks & Meeting Information (July 10, 2026)

This document outlines the key updates, shared information, and pending action items for **Prudhvi** (referred to as *Prithvi* / *Pithy* in the transcript) discussed during the project progress and UI enhancements meeting.

---

## 1. Information Shared by Prudhvi (Updates)

* **Script Enhancements:** 
  * Modified the DQ generation script to automatically import custom `DQIDs` and generate the matching output SQL queries.
  * Successfully verified the script against a larger volume of records and custom DQIDs.
* **Bug Fixes:** 
  * Resolved the failure from the previous run where missing variable names caused errors. 
  * The script now checks the description and filter criteria fields to retrieve variable names dynamically.
* **Logic Validations:** 
  * Verified that percentage input formatting is handled correctly (e.g., inputting `10` successfully maps to a `<= 10` condition).
  * Confirmed that negative assertions such as `not between` and `not in` are functioning correctly with no new changes.

---

## 2. Information Shared with Prudhvi

* **UAT Sign-off:** Rachna reviewed the demo outputs and approved the current changes (`"I think I'm good with this. Yeah, this looks fine."`), opening the path for production deployment preparation.
* **Deployment Timeline:** 
  * The production deployment is scheduled for **next Wednesday**.
  * The Tuesday release window is allocated for Atharva's UI changes.
  * Sachin noted that a couple of days are required for detail review and approvals once UAT sign-off is submitted.
* **Data Access & Compliance:** 
  * Sachin highlighted strict guidelines regarding production database access, especially concerning sensitive PII (Personally Identifiable Information) records. 
  * The team is prohibited from running manual update/insert queries on ASDP or decrypting sensitive details without explicit sign-off.

---

## 3. Pending Action Items (Todo List)

| Target Date | Task Description | Dependencies / Collaborators | Status |
| :--- | :--- | :--- | :---: |
| **ASAP** | **UAT Documentation:** Prepare the test case document covering the UAT runs and screenshots (refer to Atharva's document style as a guide). | Rachna (to sign off) | `[ ]` |
| **ASAP** | **UAT Sign-off:** Send the finalized UAT test document to Rachna to receive formal business sign-off. | Rachna | `[ ]` |
| **Early Next Week** | **Release Preparation (RFC):** Once UAT sign-off is obtained, collaborate with Sachin to create the RFC to schedule the Wednesday deployment. | Sachin | `[ ]` |
| **Ongoing** | **Business Exception Validation:** Implement secondary input validation checks (e.g., throwing a business exception if task status or work basket parameter is blank). | Nirmal (Reference / guidance) | `[ ]` |
