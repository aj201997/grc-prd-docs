# Internal Audit Module Flowcharts (SVG-safe Mermaid for GitHub)

> This file contains **all Internal Audit flowcharts** combined into one Markdown file.
> Each flowchart is in an individual Mermaid block for GitHub preview + SVG export.

---

## 01_engagement_creation

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["IA - ENGAGEMENT CREATION"]:::heading --> S0([Start])

S0 --> S1[Login to GRC Tool]
S1 --> S2[Open Internal Audit Module]
S2 --> S3[Engagement Listing Page]

S3 --> F0["Filters

- Audit Plan
- Date Range
- Audit Type
- Audit Sub-type
- Created By"]:::info

S3 --> S4[Click Add New]
S4 --> F1[Engagement Creation Form]

F1 --> FM1["Mandatory Fields

- Engagement Name
- Audit Plan
- Audit Start Date
- Audit End Date
- Coverage Period
- Auditor type (Internal or External)"]:::info

F1 --> FO1["Optional Fields

- Requested By section (conditional)
- Attachments (conditional)"]:::info

FM1 --> V1{Engagement name unique?}

V1 -->|No| V2["Validation Error

- Engagement name already exists"]:::error

V1 -->|Yes| A1{Auditor type selected}

A1 -->|Internal| A2["Internal Auditor

- Audit Firm field hidden"]:::info

A1 -->|External| A3["External Auditor

- Audit Firm dropdown enabled"]:::info

A2 --> RB1{Requested By added?}
A3 --> RB1

RB1 -->|No| T1[Add Team Members]

RB1 -->|Yes| RBF["Requested By Fields

- Department mandatory (single or multiple)
- Request Date mandatory
- Attachment (optional)"]:::info

RBF --> T1

T1 --> T2[Click Add New Team Member]
T2 --> T3["Team Modal

- Select users
- Assign predefined roles"]:::info

T3 --> T4[Save Team]
T4 --> SUB1[Submit Engagement]

SUB1 --> OUT1["Engagement Created

- Redirect to listing
- New engagement shown on top"]:::action

OUT1 --> End([End])
```

---

## 02_engagement_details_tab

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;

T["IA - ENGAGEMENT DETAILS TAB"]:::heading --> S0([Start])

S0 --> S1[Open Internal Audit Module]
S1 --> S2[Open Engagement from Listing]
S2 --> S3[Engagement Details Tab]

S3 --> V1["What you see

- All engagement fields entered during creation
- Team member list with roles"]:::info

S3 --> A1["Actions (Audit Owner Only)

- Update details
- Add team member
- Remove team member"]:::info

S3 --> L1["Audit Logs

- Creation log
- All edits with user and timestamp"]:::info

A1 --> End([End])
```

---

## 03_audit_planning_tab

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["IA - AUDIT PLANNING TAB"]:::heading --> S0([Start])

S0 --> S1[Open Engagement]
S1 --> S2[Open Audit Planning Tab]

S2 --> FM1["Mandatory Sections

- Audit Objective (text)
- Audit Scope (text)
- Audit Background (text)
- Audit Limitation (Yes/No)"]:::info

S2 --> FO1["Optional Attachments

- File attachment for Objective
- File attachment for Scope
- File attachment for Background"]:::info

FM1 --> L1{Audit limitation selected Yes?}

L1 -->|No| L2[No limitation details required]

L1 -->|Yes| L3["Limitation Details

- Limitation text mandatory
- Attachment (optional)"]:::info

L2 --> A1["User Actions

- Save as Draft
- Submit for Review"]:::info

L3 --> A1

A1 -->|Save as Draft| D1["Saved as Draft

- Editable by user"]:::action

A1 -->|Submit for Review| S3["Status: Submitted for Review

- Fields locked"]:::action

S3 --> N1[Email notification to Reviewer]
N1 --> R1[Reviewer opens Audit Planning]
R1 --> R2{Approve or Reject?}

R2 -->|Approve| AP1["Approved

- Planning approved
- Engagement becomes In Progress
- Other tabs unlock"]:::action
AP1 --> End([End])

R2 -->|Reject| RJ1["Rejected

- Remarks mandatory
- Attachment (optional)"]:::error

RJ1 --> RJ2[Status set to Rejected]
RJ2 --> RJ3[User can view rejection remarks]
RJ3 --> RJ4[User edits planning and resubmits]
RJ4 --> S3
```

---

## 04_tab_unlocks_and_engagement_status

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;

T["IA - TAB UNLOCKS & ENGAGEMENT STATUS"]:::heading --> S0([Start])

S0 --> S1[Engagement Created]

S1 --> S2["Initial Tabs Available

- Engagement Details
- Audit Planning"]:::info

S2 --> S3{Audit Planning approved?}

S3 -->|No| S4["Locked Tabs

- Audit Procedures
- DRL
- Working Papers
- Query & Observations
- Report Generation
- MoM & Recordings"]:::info
S4 --> End([End])

S3 -->|Yes| S5["Unlocked Tabs

- Audit Procedures
- DRL
- Working Papers
- Query & Observations
- Report Generation
- MoM & Recordings"]:::info

S5 --> S6["Engagement Workflow Status

- Planned (before approval)
- In Progress (after planning approval)
- Draft Report (when draft report issued)
- Final Report (after final report uploaded)"]:::info

S6 --> End([End])
```

---

## 05_audit_procedures_bulk_import

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["IA - AUDIT PROCEDURES BULK IMPORT"]:::heading --> S0([Start])

S0 --> S1[Open Engagement]
S1 --> S2[Open Audit Procedures Tab]
S2 --> S3[Click Import]

S3 --> P1["Import Steps

- Download sample template (Excel)
- Fill Audit Procedures and DRL sheet
- Attach file
- Click Process to validate"]:::info

P1 --> V1{Data valid?}

V1 -->|No| V2["Import Errors

- Template data incorrect
- Fix file and reupload"]:::error
V2 --> P1

V1 -->|Yes| SUB1[Submit Import]
SUB1 --> OUT1["Imported

- Procedures visible in list view"]:::action
OUT1 --> End([End])
```

---

## 06_audit_procedures_manual_creation

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["IA - AUDIT PROCEDURE MANUAL CREATION"]:::heading --> S0([Start])

S0 --> S1[Open Engagement]
S1 --> S2[Open Audit Procedures Tab]
S2 --> S3[Click Add New]
S3 --> F1[Audit Procedure Form]

F1 --> FM1["Mandatory Fields

- Department (single or multiple)
- Procedure Title
- Procedure Description"]:::info

F1 --> FO1["Optional Fields

- Attachment (Excel / PDF / Word)
- Max size 100 MB"]:::info

F1 --> SYS1["System Field

- Automated Procedure ID"]:::action

SYS1 --> V1{Mandatory fields completed?}

V1 -->|No| V2["Validation Error

- Highlight missing mandatory fields"]:::error

V1 -->|Yes| SUB1[Create Procedure]
SUB1 --> OUT1["Created

- Procedure shown in list view"]:::action
OUT1 --> End([End])
```

---

## 07_drl_raise_and_response_workflow

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["IA - DRL RAISE & RESPONSE WORKFLOW"]:::heading --> S0([Start])

S0 --> S1[Open Audit Procedures Tab]
S1 --> S2[Locate Procedure Row]
S2 --> S3[Click DRL Column]
S3 --> P1[Left DRL Panel opens]

P1 --> P2["DRL Panel

- Shows past DRLs (if any)
- Click + to raise new DRL"]:::info

P2 --> F1[Raise DRL Modal]

F1 --> FM1["Mandatory Fields

- Audit Requirement
- Assigned User
- Due Date"]:::info

F1 --> FO1["Optional Fields

- Remarks"]:::info

F1 --> SUB1[Submit DRL]
SUB1 --> OUT1["DRL Created

- Listed in left panel
- Email to assignee"]:::action

OUT1 --> A1[Assignee replies with attachment]
A1 --> N1[Email to DRL Creator]
N1 --> R1[Creator reviews reply]

R1 --> ST1{Set status}

ST1 -->|Close| C1["Status: Closed

- Visible to assignee as Closed"]:::action

ST1 -->|Drop| D1["Status: Dropped

- Visible to assignee as Dropped"]:::action

C1 --> End([End])
D1 --> End
```

---

## 08_drl_tab_list_filters_export

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;

T["IA - DRL TAB (LIST, FILTERS, EXPORT)"]:::heading --> S0([Start])

S0 --> S1[Open Engagement]
S1 --> S2[Open DRL Tab]

S2 --> V1["DRL List Columns

- DRL ID (auto)
- Audit Requirement
- Status (Open / Dropped / Closed)
- Assignee
- Due Date
- Attachment"]:::info

S2 --> F1["Filters

- Status
- Assignee
- Date Range"]:::info

S2 --> E1["Export

- Excel
- Word
- PDF"]:::info

E1 --> End([End])
```

---

## 09_working_papers_folders_upload

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["IA - WORKING PAPERS (FOLDERS & UPLOAD)"]:::heading --> S0([Start])

S0 --> S1[Open Engagement]
S1 --> S2[Open Working Papers Tab]

S2 --> A1["Actions

- Create folder
- Create subfolder
- Upload files"]:::info

A1 --> F1[Click Add Folder]
F1 --> F2["Folder Modal

- Folder name
- Submit"]:::info

F2 --> OUT1[Folder Created]

OUT1 --> SF1[Open Folder]
SF1 --> SF2[Click Add Subfolder]

SF2 --> SF3["Subfolder Modal

- Subfolder name
- Submit"]:::info

SF3 --> OUT2[Subfolder Created]

OUT2 --> UP1["Upload Files

- Attach multiple files
- Excel / Word / PDF"]:::action

UP1 --> End([End])
```

---

## 10_observation_creation_from_procedure

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["IA - OBSERVATION CREATION FROM PROCEDURE"]:::heading --> S0([Start])

S0 --> S1[Open Audit Procedures Tab]
S1 --> S2[Click Observation Button]
S2 --> P1[Right Observation Panel opens]

P1 --> P2["Panel Features

- View existing observations
- Click + to create new observation"]:::info

P2 --> F1[Observation Form]

F1 --> FM1["Mandatory Fields

- Observation Title
- Observation Description
- Financial Impact
- Management Comment
- Observation Owner
- Risk Category
- Risk Implication
- Risk Rating"]:::info

F1 --> FO1["Optional Fields

- Root Cause
- Mega Process
- Process
- Sub Process
- Risk
- Control
- Recommendation
- Attachments"]:::info

F1 --> ACT1{Save Draft or Submit?}

ACT1 -->|Save Draft| D1["Saved as Draft

- Status: Draft
- No email triggered"]:::action

ACT1 -->|Submit| Q1["Submitted

- Status: Query
- Email to Observation Owner"]:::action

D1 --> End([End])
Q1 --> End
```

---

## 11_observation_lifecycle_workflow

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["IA - OBSERVATION LIFECYCLE"]:::heading --> S0([Start])

S0 --> S1["Draft

- Saved as draft
- No notifications"]:::info

S1 --> S2{Submit Observation?}

S2 --> S3["Query

- Email to observation owner
- Drop option available"]:::info

S3 --> D1{Drop?}

D1 -->|Yes| DR1["Dropped

- Evidence satisfactory
- Observation removed from report path"]:::action

D1 -->|No| S4["Draft Observation

- Drop option available
- Eligible for draft report"]:::info

S4 --> D2{Drop?}

D2 -->|Yes| DR1
D2 -->|No| S5["Final Observation

- Move to ATR eligible"]:::action

S5 --> S6["Closed

- If satisfactory evidence received
- Move to ATR eligible"]:::action

DR1 --> End([End])
S6 --> End
```

---

## 12_query_observations_tab_list_export_add

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["IA - QUERY & OBSERVATIONS TAB"]:::heading --> S0([Start])

S0 --> S1[Open Engagement]
S1 --> S2[Open Query & Observations Tab]

S2 --> V1["What you see

- List view of observations in Query or higher status"]:::info

S2 --> E1["Export

- Export selected observations to Excel
- Export full list to Excel"]:::info

S2 --> A1[Click Add New Observation]

A1 --> NOTE1["Note

- Standalone observation
- Not linked to any audit procedure"]:::info

NOTE1 --> F1[Observation Form]

F1 --> FM1["Mandatory Fields

- Observation Title
- Observation Description
- Financial Impact
- Management Comment
- Observation Owner
- Risk Category
- Risk Implication
- Risk Rating"]:::info

F1 --> FO1["Optional Fields

- Root Cause
- Process mapping fields
- Risk control mapping
- Recommendation
- Attachments"]:::info

F1 --> SUB1[Submit Observation]
SUB1 --> OUT1["Created

- Status: Query
- Email to owner"]:::action

OUT1 --> End([End])
```

---

## 13_report_generation_draft_report

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["IA - REPORT GENERATION (DRAFT REPORT)"]:::heading --> S0([Start])

S0 --> S1[Open Engagement]
S1 --> S2[Open Report Generation Tab]

S2 --> C1{All observations at Draft Observation or higher?}

C1 -->|No| B1["Blocked

- Draft report cannot be issued
- If any observation is Draft or Query"]:::error
B1 --> End([End])

C1 -->|Yes| I1[Click Issue Draft Report]

I1 --> R1["Draft Report Includes

- Audit scope
- Audit objective
- Audit background
- Audit limitation (optional)
- Engagement details
- Draft observations with risk"]:::info

R1 --> REQ1["Request Issuance

- Auditor requests issuance
- Email to Audit Owner"]:::info

REQ1 --> AO1[Audit Owner reviews Draft Report]
AO1 --> D1{Accept or Reject?}

D1 -->|Accept| A1["Accepted

- Email to all engagement team
- Auditor can download report
- Engagement status: Draft Report"]:::action

D1 -->|Reject| RJ1["Rejected

- Rejection remarks mandatory
- Attachment optional
- Auditor download blocked"]:::error

RJ1 --> REQ1

A1 --> LOG1["Logging Rule

- Every draft issuance overrides previous
- Audit log records user and timestamp"]:::info

LOG1 --> End([End])
```

---

## 14_report_generation_final_draft_and_final_upload

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["IA - FINAL DRAFT REPORT & FINAL UPLOAD"]:::heading --> S0([Start])

S0 --> S1[All observations in Final Observation or Closed]
S1 --> S2[Open Report Generation Tab]
S2 --> S3[Click Issue Final Draft Report]

S3 --> F1["Audit Conclusion

- Free text mandatory"]:::info

F1 --> SUB1[Submit Final Draft Request]
SUB1 --> N1[Email to Audit Owner]
N1 --> AO1[Audit Owner reviews Final Draft Report]

AO1 --> D1{Accept or Reject?}

D1 -->|Reject| RJ1["Rejected

- Rejection remarks mandatory
- Attachment optional
- Auditor download blocked"]:::error
RJ1 --> S3

D1 -->|Accept| AC1["Accepted

- Email to assigned auditor
- Auditor can download final draft report"]:::action

AC1 --> UP1[Auditor clicks Upload Final Report]

UP1 --> UP2["Upload Modal

- Attach Final Report
- Final Issuance Date (present or back-dated)"]:::info

UP2 --> UP3[Submit Upload]
UP3 --> N2[Email to Audit Owner for Approval]

N2 --> AO2[Audit Owner approves Final Report]

AO2 --> OUT1["Final Report Approved

- Email to all engagement members
- Engagement status: Final Report"]:::action

OUT1 --> End([End])
```

---

## 15_atr_transfer_rule

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["IA - TRANSFER TO ATR RULE"]:::heading --> S0([Start])

S0 --> S1["Observation Status Check

- Only Final Observation or Closed"]:::info

S1 --> D1{Eligible?}

D1 -->|No| N1["Not Eligible

- Draft / Query / Draft Observation not transferred"]:::error
N1 --> End([End])

D1 -->|Yes| T1["Transfer Action

- Move to ATR module under Observations tab"]:::action

T1 --> OUT1["ATR Updated

- Observation visible in ATR listing"]:::action
OUT1 --> End([End])
```

---

## 16_mom_and_recordings_create_edit

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["IA - MOM & RECORDINGS (CREATE & EDIT)"]:::heading --> S0([Start])

S0 --> S1[Open Engagement]
S1 --> S2[Open MoM & Recordings Tab]

S2 --> V1["Tabs

- MoM tab
- Recording tab"]:::info

S2 --> L1["MoM List Columns

- Title
- Description
- Date
- Created By
- Attachment
- Timestamp
- Edit icon"]:::info

S2 --> L2["Recording List Columns

- Title
- Description
- Date
- Created By
- Link
- Attachment
- Timestamp
- Edit icon"]:::info

S2 --> A1[Click Add New]
A1 --> F1[Create Entry Modal]

F1 --> FM1["Mandatory Fields

- Type (MoM or Recording)
- Title
- Date (MoM)
- Submit"]:::info

F1 --> FO1["Optional Fields

- Description
- Attachment
- Recording link (Recording type)"]:::info

F1 --> D1{Type selected}

D1 -->|MoM| M1["MoM Fields

- Title mandatory
- Date mandatory
- Description optional
- Attachment optional"]:::info

D1 -->|Recording| R1["Recording Fields

- Title mandatory
- Description optional
- Recording link optional
- Attachment optional"]:::info

M1 --> SUB1[Submit Entry]
R1 --> SUB1

SUB1 --> OUT1["Created

- Entry visible in list view
- Click title to view"]:::action

OUT1 --> E1[Edit entry using Edit icon]
E1 --> E2["Edit Flow

- Update fields
- Save changes"]:::info

E2 --> End([End])
```

---

## 99_ia_full_end_to_end

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["INTERNAL AUDIT - FULL END TO END"]:::heading --> START([Start])

START --> A1[Open Internal Audit Module]
A1 --> A2[Engagement Listing Page]
A2 --> A3[Create New Engagement]

A3 --> A4["Engagement Creation

- Mandatory engagement fields
- Conditional external auditor fields
- Team assignment modal"]:::info

A4 --> A5[Engagement Created]

A5 --> D1[Engagement Details Tab]
D1 --> D2["Actions

- Update details (Audit Owner)
- Manage team members
- View audit logs"]:::info

A5 --> P1[Audit Planning Tab]
P1 --> P2["Mandatory Sections

- Objective
- Scope
- Background
- Limitation (Yes/No)"]:::info

P1 --> P3["User Actions

- Save as Draft
- Submit for Review"]:::info

P3 --> P4[Reviewer approval loop]
P4 --> P5{Approved?}

P5 -->|No| P6["Rejected

- Remarks mandatory
- Resubmit"]:::info
P6 --> P4

P5 -->|Yes| UN1["Tabs Unlocked

- Audit Procedures
- DRL
- Working Papers
- Query & Observations
- Report Generation
- MoM & Recordings"]:::action

UN1 --> AP1[Audit Procedures]
AP1 --> AP2["Create Procedures

- Manual entry
- Bulk import"]:::info

AP1 --> DRL1["DRL Workflow

- Raise DRL
- Assignee response
- Close or drop"]:::info

AP1 --> OBS1["Observations

- Create from procedure
- Save draft or submit to Query"]:::info

UN1 --> WP1["Working Papers

- Folder and subfolder
- Upload multiple files"]:::info

UN1 --> QO1["Query & Observations

- List Query or higher
- Export to Excel
- Add standalone observation"]:::info

OBS1 --> LC1["Observation Lifecycle

- Draft → Query → Draft Observation → Final Observation → Closed"]:::info

LC1 --> REP1[Report Generation]

REP1 --> REP2["Draft Report

- Only when all obs ≥ Draft Observation
- Approval loop by Audit Owner"]:::info

REP1 --> REP3["Final Draft + Final Upload

- Only when all obs Final or Closed
- Approval and final issuance"]:::info

LC1 --> ATR1["Transfer to ATR

- Only Final Observation and Closed transferred"]:::info

UN1 --> MOM1["MoM & Recordings

- Create and edit entries
- Separate MoM and Recording tabs"]:::info

MOM1 --> END([End])
```

---
