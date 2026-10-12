# Phase 2: Backend Development & Configurations Data Architecture

This folder contains all documentation, configurations, and deliverables completed for Phase 2 tasks in ServiceNow.

---

## 1. Data Architecture

### Description
* Defined foundational data architecture and schema configurations required for the licensed software request process.
* Configured core fields, data types, and table relationships across `sc_req_item` (Requested Item) and `sc_task` (Catalog Task) to support request tracking, approvals, and assignment groups.

---

## 2. Business Rules Configuration

### Description
Configured server-side Business Rules on the Requested Item (`sc_req_item`) table to automatically execute updates when a request enters the `Pending` state.

---

## 3. Automation Logic

### Description
Configured process automation in ServiceNow Flow Designer to handle end-to-end request logic upon catalog item submission:
* **Trigger:** Service Catalog
* **Actions:** 
  1. **Ask For Approval:** Routes approval request to the designated manager.
  2. **If Approved:** Automatically creates a Catalog Task (`sc_task`) assigned to the fulfillment team.
