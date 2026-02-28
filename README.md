<p align="center">
<img width="338" height="190" alt="impact iq 16x9" src="https://github.com/user-attachments/assets/436670cb-9aec-4ae9-8a5c-ace341ff9283" />
  <br/>
<em><strong>Be smarter with every change</strong></em>
  <br/>
  <br/>
  <em>Tenant-Admin Edidion - One-Click</em>
</p>

# Impact Analysis and Governance for Power BI + Fabric (Tenant Admin Edition)

This repository is the **Tenant Admin edition** of Impact IQ. It follows the same core extraction and governance approach as the standard version, with added execution and permission-management options for tenant-level scenarios.

## What’s Different in This Repo

This version is designed for Tenant Admins who may need to run extraction beyond their existing workspace membership.

>*If looking for the core Impact IQ's One-Click, Designed for Everyone edition that runs on any computer, provides report, model, and dataflow backups, and leverages the Power BI + Fabric Service and REST API across all Workspaces, check out: https://github.com/BeSmarterWithData/ImpactIQ*

>*Have specific Reports and/or Models downloaded you want to analyze? Don't have direct access to the Workspace but have the PBIX? Check out Impact IQ's Local edition here: https://github.com/BeSmarterWithData/ImpactIQ-Local*

### Run Modes
The main script supports three execution paths:

<img width="693" height="233" alt="image" src="https://github.com/user-attachments/assets/66c78571-eb9d-4eb2-854d-3d01baf87bb0" />




1. **Normal User Mode**
   - Runs only within workspaces you can already access.

2. **Tenant Admin Mode (Existing Access Only)**
   - Uses Admin APIs for metadata on workspaces you already have access to.

3. **Tenant Admin Mode (All Workspaces)**
   - Runs across all workspaces.
   - Temporarily grants needed workspace permissions for model/report/dataflow extraction.
   - Automatically removes those temporary permissions at the end.
  
## 🚀 Quick Start Instructions  

You’ve got **two ways** to get started:  


### 🟢 One-Click Update & Run Tool (Recommended)  
Always up-to-date and the easiest way to get started.  

➡️ [**Download Impact IQ - Tenant Admin - One-Click Update & Run Tool**](https://github.com/BeSmarterWithData/ImpactIQ-TenantAdmin/releases/download/v1.0/ImpactIQ-TenantAdmin.bat)

This automatically:  
1. Pulls the latest repo from GitHub
2. Places it into `C:\Power BI Backups`
3. Runs the **Tenant Admin Final PS Script**  
4. Opens the **Power BI Governance Model** at the end  

> 💡 **Tip:** Once downloaded, simply re-run this locally anytime to keep your **backups** and **governance details up-to-date** *and* take advantage of the **newest features**.  

> ⚠️ If security policies block the batch file, follow the manual steps below instead.


📂 **All backups and the final Power BI Governance Model will be saved to:** `C:\Power BI Backups`


---

### 🟡 Option 2 — Manual Setup  

#### ✅ Step 1: Create Folder  
> Make a folder at:  `C:\Power BI Backups`  

#### ✅ Step 2: Add Files  
> Download all repo files and place them into the newly-created `C:\Power BI Backups` folder.  

#### ✅ Step 3: Run Script  
> Open PowerShell and run the Final PS Script. You can:  
> - Copy/paste the full script, or  
> - Rename `Tenant Admin Final PS Script.txt` → `Tenant Admin Final PS Script.ps1` and run directly  
> 
> **Environment Selection**: When prompted, choose your Power BI environment:
> - Press **Enter** for Public cloud (default)
> - Or choose: `Germany`, `USGov`, `China`, `USGovHigh`, or `USGovMil` for sovereign clouds.
> - If no selection is made after 120 seconds, it will continue with the default of Public.

#### ✅ Step 4: Open the Power BI File  
> Open: `Power BI Governance Model.pbit`  
> → Let it refresh, then save as `.pbix`  

---

🎉 That’s it — enjoy! 🎉

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
- Permission extraction across the tenant scope selected for the run, including workspace, dataset, report, app, dataflow, and pipeline access.
- Inclusion of extracted permission data in the final governance outputs (Excel extract and the Power BI model/report built from it).
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

11. **Comprehensive Permission Extraction**
  - Pulls user/access-right details for every included workspace and related artifacts (datasets, reports, apps, dataflows, and deployment pipelines).
  - Included in the final output model/report for tenant-wide governance and security review.
