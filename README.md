<p align="center">
<img width="338" height="190" alt="impact iq 16x9" src="https://github.com/user-attachments/assets/436670cb-9aec-4ae9-8a5c-ace341ff9283" />
  <br/>
<em><strong>Be smarter with every change</strong></em>
  <br/>
  <br/>
  <em>One-Click, Designed for Everyone</em>
</p>

# Impact Analysis and Governance for Power BI + Fabric (Tenant Admin Edition)

This repository is the **Tenant Admin edition** of Impact IQ. It follows the same core extraction and governance approach as the standard version, with added execution and permission-management options for tenant-level scenarios.

## What’s Different in This Repo

This version is designed for users who may need to run extraction beyond their existing workspace membership.

### Run Modes
The main script supports three execution paths:

1. **Normal User Mode**
   - Runs only within workspaces you can already access.

2. **Tenant Admin Mode (Existing Access Only)**
   - Uses Admin APIs for metadata on workspaces you already have access to.

3. **Tenant Admin Mode (All Workspaces)**
   - Runs across all workspaces.
   - Temporarily grants needed workspace permissions for model/report/dataflow extraction.
   - Automatically removes those temporary permissions at the end.

## Included Scripts

- **Final extraction + governance run**
  - `Final PS Script.txt`

- **Workspace membership management utility**
  - `Manage Workspace Permissions PS Script.txt`
  - Add or remove:
    - User
    - Service principal
    - Security group

- **Temporary permission cleanup utility**
  - `Remove Temp Added Tenant Permissions PS Script.txt`
  - Removes temporary permissions from prior runs.

## Built-In Safety for Tenant Admin Full Runs

When using **Tenant Admin Mode (All Workspaces)**, the process automatically outputs a list of workspaces where temporary permissions were added.

Why this matters:
- If the main script completes successfully, permissions are removed automatically.
- If the script fails mid-run, you still have a complete output list of the temporary grants.
- The cleanup script can use that output (Excel) to remove temporary access after the fact.

## Typical End-to-End Flow

1. Run `Final PS Script.txt`.
2. Choose the desired run mode.
3. If running full tenant mode, allow temporary permission assignment.
4. Review outputs and open `Power BI Governance Model.pbit`.
5. If needed (for failed/interrupted runs), run `Remove Temp Added Tenant Permissions PS Script.txt` using the generated workspace list.

## Governance Output

The solution provides:
- Visual-level impact analysis for reports and semantic model objects.
- Used/unused object visibility for model cleanup opportunities.
- Backup + metadata extraction for models, reports, and dataflows.
- A consolidated Power BI governance model output via `Power BI Governance Model.pbit`.

## Local Files in This Repo

- `Final PS Script.txt`
- `Manage Workspace Permissions PS Script.txt`
- `Remove Temp Added Tenant Permissions PS Script.txt`
- `Power BI Governance Model.pbit`
- `Config/` (supporting extraction scripts and templates)

## Notes

- Temporary permission handling is intended to minimize long-lived elevated access.
- Keep the generated temporary-access output files for audit and recovery.
- If your organization enforces strict execution policies, run according to your internal security standards.

## Core Impact IQ Features

In addition to tenant-admin execution options, Impact IQ provides the following core capabilities:

1. **Workspace & Environment Metadata Extraction**
  - Collects workspace, dataset, report, page, and app metadata.
  - Outputs structured metadata for governance review.

2. **Model Backup & Model Metadata Extraction**
  - Backs up semantic models using XMLA and non-XMLA approaches as applicable.
  - Extracts model details for documentation and impact analysis.

3. **Report Backup & Visual Metadata Extraction**
  - Backs up Power BI reports.
  - Extracts visual-layer metadata to map object usage at report/page/visual level.

4. **Dataflow Backup & Metadata Extraction**
  - Backs up dataflows and captures query-level details for lineage/governance.

5. **Model Connection Details**
  - Captures model connection information for dependency and architecture visibility.

6. **Model Refresh History & Schedule Details**
  - Extracts refresh history and refresh schedule settings for monitoring and governance.

7. **Dataflow Connection + Refresh History Details**
  - Captures dataflow connectivity and refresh history metadata.

8. **Used/Unused Object Identification**
  - Highlights actively used vs. unused tables, columns, and measures.
  - Supports safer cleanup and model optimization.

9. **Broken Visual Detection**
  - Surfaces broken visuals/filters with page-level traceability for faster remediation.

10. **Consolidated Governance Model Output**
   - Combines extracted artifacts into `Power BI Governance Model.pbit` for exploration, impact analysis, and sharing.
