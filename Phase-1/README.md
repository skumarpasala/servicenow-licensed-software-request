# Phase 1: Requirement Analysis & Planning

## Overview
This repository contains the planning, foundational architecture, and configuration files for the **Software Installation Request** project built on the ServiceNow platform. This project automates the end-to-end lifecycle of employee software requests, eliminating manual bottlenecks through dynamic approvals, automated task generation, and strict data validation.

## Key Modules & Breakdown

### 1. Business Objectives
* Streamline employee software and licensing requests through a centralized, user-friendly Service Portal.
* Reduce manual administrative overhead by automating approval workflows and provisioning tasks.
* Maintain compliance, data integrity, and tracking for software assets across the organization.

### 2. Functional Scope
* **Service Catalog Item:** Create a dedicated **Software Installation Request** item.
* **Form Variables:** Capture precise user requirements using specific data types (Software Name, Version Required, Business Justification, Urgency Level, and an auto-populating Requested For field).
* **Workflow & Approval:** Utilize Workflow Studio / Flow Designer to route requests dynamically (e.g., routing to the Software Asset Team for licensed software, or IT Security for elevated permissions) prior to fulfillment.
* **Data Architecture:** Map and verify record generation across the Service Catalog hierarchy: `sc_request` (Request), `sc_req_item` (RITM), and `sc_task` (Catalog Task).

### 3. Stakeholder Mapping
* **End Users / Employees:** Submit software requests and track their status via the Service Portal.
* **Approvers (Software Asset Team & IT Security):** Review, validate, and approve or reject software requests based on licensing and security policies.
* **IT Software Support Group:** Receive automatically generated and assigned tasks to process the actual software installation.
* **System Administrator:** Configure catalog forms, manage variables, design flow execution logic, and manage Update Set deployments.

### 4. Execution Roadmap
* **Phase 1:** Initialize the Local Update Set, define table schema, and outline project architecture.
* **Phase 2:** Build the catalog item, variables, choice lists, and UI layout.
* **Phase 3:** Configure the Service Portal interface, implement help text/tooltips, and test user navigation.
* **Phase 4:** Design the Flow Designer automation logic, map assignment groups, enforce data integrity (mandatory fields), and export the final Update Set.
* **Phase 5:** Finalize technical documentation, setup manuals, and prepare the end-to-end visual demonstration.
