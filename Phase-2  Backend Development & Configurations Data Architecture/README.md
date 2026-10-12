# Phase 2: Backend Development & Configurations Data Architecture

This repository section documents the foundational backend architecture, server-side logic, and automated workflows implemented for the **Licensed Software Request** process in ServiceNow.

---

## 1. Data Architecture & Schema Configuration

### Overview
Established a standardized, auditable data hierarchy to track software license requests across their lifecycle, ensuring data integrity from user submission through technical fulfillment.

### Schema Details & Relationships
* **Parent-Child Hierarchy:** Designed operational relationships linking the general request (`sc_request`), requested items (`sc_req_item`), and fulfillment tasks (`sc_task`).
* **Table Configurations:**
  * **Requested Item (`sc_req_item`):** Stores specific request parameters, including software title, version, business justification, license cost tier, and urgency metrics.
  * **Catalog Task (`sc_task`):** Facilitates fulfillment activities, mapping dynamic assignment groups (e.g., Software Asset Management and IT Desktop Support) based on the requested software type.
* **Data Integrity & Normalization:** Enforced strict field types, mandatory submission criteria, and reference qualifiers to prevent orphaned records and maintain consistency with CMDB software models.

---

## 2. Server-Side Business Rules

### Overview
Implemented modular Business Rules running on the `sc_req_item` table to enforce automated state management and data synchronization without requiring manual agent intervention.

### Implementation Details
* **Target Table:** `sc_req_item` (Requested Item)
* **Trigger Conditions:** State transitions into `Pending` (e.g., waiting for additional user info or external license procurement).
* **Execution Logic:**
  * Validates mandatory audit fields before state updates are committed.
  * Synchronizes state indicators downstream to open child tasks (`sc_task`), ensuring fulfillers do not work on requests currently placed on hold.
  * Generates automated work notes and audit log entries to document state transitions and rationale.

---

## 3. Automation Logic & Workflow Studio / Flow Designer

### Overview
Automated the end-to-end fulfillment pipeline using ServiceNow Flow Designer to eliminate manual handoffs, streamline approvals, and trigger task provisioning.

### Flow Execution Breakdown
* **Trigger:** Record creation via Service Catalog submission (`sc_req_item`).
* **Workflow Stages:**
  1. **Dynamic Approval Routing:**
     * Evaluates request variables to determine necessary authorization tiers.
     * Generates approval records for the designated line manager and the Software Asset Management (SAM) team.
  2. **Decision Branching:**
     * **If Approved:** Automatically advances the RITM stage to *Work in Progress* and generates fulfillment tasks (`sc_task`) assigned to the IT Software Deployment queue.
     * **If Rejected:** Updates the request state to *Closed Incomplete*, logs rejection rationale from approvers, and sends an automated email notification to the requester.
  3. **Task Completion & Closure:**
     * Monitors downstream `sc_task` records; once closed as complete, automatically sets the parent `sc_req_item` and `sc_request` states to *Closed Complete*.
