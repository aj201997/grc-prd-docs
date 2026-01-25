# ATR Module Flowcharts (SVG-safe Mermaid for GitHub)

> This file contains **all ATR flowcharts** combined into one Markdown file.
> Each flowchart is in an individual Mermaid block for GitHub preview + SVG export.

---

## 01_atr_overview_and_navigation

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;

T["ATR MODULE - OVERVIEW & NAVIGATION"]:::heading --> S0([Start])

S0 --> S1[Open ATR Module]
S1 --> S2{Select Sub Module}

S2 -->|Observations| O1[Observations List Page]
S2 -->|Sub Observations| SO1[Sub Observations List Page]
S2 -->|Management Comments| MC1[Management Comments Page]

O1 --> End([End])
SO1 --> End
MC1 --> End
```

---

## 02_atr_observations_list_and_filters

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;

T["ATR - OBSERVATIONS LIST & FILTERS"]:::heading --> S0([Start])

S0 --> S1[Open ATR Module]
S1 --> S2[Go to Observations Sub Module]
S2 --> S3[Observations List Page]

S3 --> B1["Index Counters

- Total
- By Status buckets"]:::info

S3 --> B2["Filters

- Assignee
- Status
- Type
- Date Range"]:::info

S3 --> E1["Export Options

- Export selected rows
- Export full list"]:::info

S3 --> D1[Open Observation Detail Page]

E1 --> End([End])
D1 --> End
```

---

## 03_atr_observations_manual_creation

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["ATR - OBSERVATION MANUAL CREATION"]:::heading --> S0([Start])

S0 --> S1[Open ATR Module]
S1 --> S2[Go to Observations Sub Module]
S2 --> S3[Click Add New Observation]
S3 --> F1[Observation Creation Form]

F1 --> FM1["Mandatory Fields

- Title
- Description
- Audit Type
- Engagement Name
- Financial Impact
- Management Comment
- Observation Owner
- Risk Category
- Risk Implication
- Risk Rating"]:::info

F1 --> FO1["Optional Fields

- Root Cause
- Process Mapping (Mega Process, Process, Sub Process)
- Risk and Control Mapping
- Recommendation
- Attachments"]:::info

F1 --> V1{Mandatory fields completed?}

V1 -->|No| V2["Validation Error

- Highlight missing mandatory fields"]:::error

V1 -->|Yes| SUB1[Submit Observation]

SUB1 --> OUT1["Observation Created

- Status: Final Observation
- Visible in listing"]:::action

OUT1 --> N1[Email to Observation Owner]
N1 --> End([End])
```

---

## 04_atr_observations_bulk_import

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["ATR - OBSERVATIONS BULK IMPORT"]:::heading --> S0([Start])

S0 --> S1[Open ATR Module]
S1 --> S2[Go to Observations Sub Module]
S2 --> S3[Click Bulk Import]

S3 --> P1["Import Steps

- Download template Excel
- Fill template
- Upload file
- Process validation"]:::info

P1 --> V1{File valid?}

V1 -->|No| V2["Validation Errors

- Show row and column errors
- Fix template and reupload"]:::error
V2 --> P1

V1 -->|Yes| SUB1[Submit Import]

SUB1 --> OUT1["Import Success

- Records created
- Status: Final Observation"]:::action

OUT1 --> N1[Email to Importer]
N1 --> End([End])
```

---

## 05_ia_to_atr_sync_flow

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["IA TO ATR SYNC FLOW"]:::heading --> S0([Start])

S0 --> S1[Internal Audit observation updated]
S1 --> D1{Observation status}

D1 -->|Final Observation| OK1["Eligible

- Observation can move to ATR"]:::action

D1 -->|Closed| OK1

D1 -->|Draft / Query / Draft Observation| NO1["Not Eligible

- Cannot move to ATR"]:::error

OK1 --> S2[Transfer observation to ATR Observations]
S2 --> S3["ATR Updated

- Observation visible in ATR listing"]:::action

S3 --> N1[Email to Observation Owner]
N1 --> End([End])

NO1 --> End
```

---

## 06_atr_observation_detail_and_actions

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;

T["ATR - OBSERVATION DETAIL & ACTIONS"]:::heading --> S0([Start])

S0 --> S1[Open ATR Observations List]
S1 --> S2[Open Observation Detail Page]

S2 --> V1["View Sections

- Observation details
- Attachments
- Management comments history"]:::info

S2 --> A1["Available Actions

- Create sub observation
- Add management comment
- Update status if allowed"]:::info

A1 --> End([End])
```

---

## 07_atr_sub_observations_list_and_filters

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;

T["ATR - SUB OBSERVATIONS LIST & FILTERS"]:::heading --> S0([Start])

S0 --> S1[Open ATR Module]
S1 --> S2[Go to Sub Observations Sub Module]
S2 --> S3[Sub Observations List Page]

S3 --> B1["Index Counters

- Total
- Awaiting Response
- Closed"]:::info

S3 --> B2["Filters

- Assignee
- Department
- Created By
- Date Range
- Status"]:::info

S3 --> D1[Open Sub Observation Detail Page]
D1 --> End([End])
```

---

## 08_atr_sub_observation_creation

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["ATR - SUB OBSERVATION CREATION"]:::heading --> S0([Start])

S0 --> S1[Open ATR Observation Detail Page]
S1 --> S2[Click Create Sub Observation]
S2 --> F1[Sub Observation Form]

F1 --> FM1["Mandatory Fields

- Title
- Description
- Mega Process
- Observation Owner"]:::info

F1 --> FO1["Optional Fields

- Financial Impact
- Root Cause
- Process and Sub Process
- Risk and Control
- Recommendation
- Attachments"]:::info

F1 --> V1{Mandatory fields completed?}

V1 -->|No| V2["Validation Error

- Highlight missing mandatory fields"]:::error

V1 -->|Yes| SUB1[Submit Sub Observation]

SUB1 --> OUT1["Sub Observation Created

- Status: Open
- Visible in sub observation listing"]:::action

OUT1 --> N1[Email to Sub Observation Owner]
N1 --> End([End])
```

---

## 09_atr_sub_observation_status_workflow

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["ATR - SUB OBSERVATION STATUS WORKFLOW"]:::heading --> S0([Start])

S0 --> S1["Status: Open

- Sub observation is active"]:::info

S1 --> D1{Owner action}

D1 -->|Submit Response| S2["Status: Awaiting Response

- Waiting for reviewer confirmation"]:::info

S2 --> N1[Email to Auditor or Creator]

D1 -->|Close| S3["Status: Closed

- Sub observation completed"]:::action

S3 --> N2[Email to Owner and Creator]

N1 --> End([End])
N2 --> End
```

---

## 10_atr_management_comments_flow

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;

T["ATR - MANAGEMENT COMMENTS"]:::heading --> S0([Start])

S0 --> S1[Open ATR Module]
S1 --> S2[Go to Management Comments Sub Module]

S2 --> V1["What you see

- Consolidated management comments repository
- Covers all stages"]:::info

V1 --> V2["Included Stages

- Query
- Draft Observation
- Dropped
- Final Observation
- Closed"]:::info

S2 --> A1["Actions

- Search comments
- Filter comments"]:::info

A1 --> End([End])
```

---

## 11_atr_notifications_overview

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;

T["ATR - NOTIFICATIONS OVERVIEW"]:::heading --> S0([Start])

S0 --> S1["Event Triggers

- Observation created (manual)
- Observation import success
- IA to ATR transfer
- Observation closed
- Sub observation created
- Sub observation awaiting response
- Sub observation closed
- Sub observation overdue
- New management comment added"]:::info

S1 --> O1["Notification Recipients

- Observation Owner
- Importer
- Auditor or Creator
- Sub Observation Owner
- Engagement members (as applicable)"]:::info

O1 --> End([End])
```

---

## 99_atr_full_end_to_end

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["ATR MODULE - FULL END TO END"]:::heading --> START([Start])

START --> A1[Open ATR Module]
A1 --> A2{Select Sub Module}

A2 -->|Observations| O1[Observations List Page]
A2 -->|Sub Observations| SO1[Sub Observations List Page]
A2 -->|Management Comments| MC1[Management Comments Page]

O1 --> O2["List Features

- Index counters
- Filters
- Export to Excel"]:::info

O2 --> O3["Filters

- Assignee
- Status
- Type
- Date Range"]:::info

O2 --> O4["Export

- Selected rows
- Full list"]:::info

O1 --> O5{Create Observation}

O5 -->|Manual| OM1[Manual Creation]
O5 -->|Bulk Import| BI1[Bulk Import]

OM1 --> OM2["Mandatory Fields

- Title
- Description
- Audit Type
- Engagement Name
- Financial Impact
- Management Comment
- Observation Owner
- Risk Category
- Risk Implication
- Risk Rating"]:::info

OM1 --> OM3["Optional Fields

- Root Cause
- Process mapping
- Risk and control mapping
- Recommendation
- Attachments"]:::info

OM1 --> OM4[Submit Observation]
OM4 --> OM5["Created

- Status: Final Observation
- Email to observation owner"]:::action

BI1 --> BI2["Import Steps

- Download template
- Upload file
- Process validation
- Submit import"]:::info

BI2 --> BI3{Valid file?}

BI3 -->|No| BI4["Errors

- Row and column errors
- Fix and reupload"]:::error
BI4 --> BI2

BI3 -->|Yes| BI5["Success

- Records created
- Status: Final Observation
- Email to importer"]:::action

IA1["IA Observation Status

- Final Observation
- Closed"]:::info --> IA2[Transfer to ATR Observations]

IA2 --> IA3["ATR Updated

- Observation visible in ATR list
- Email to observation owner"]:::action

O1 --> OD1[Observation Detail Page]

OD1 --> OD2["View

- Details
- Attachments
- Management comments history"]:::info

OD1 --> OD3["Actions

- Create sub observation
- Add management comment
- Update status if allowed"]:::info

SO1 --> SO2["Sub Obs List Features

- Index counters
- Filters
- Open detail"]:::info

SO2 --> SO3["Filters

- Assignee
- Department
- Created by
- Date range
- Status"]:::info

OD1 --> SC1[Create Sub Observation]

SC1 --> SC2["Mandatory Fields

- Title
- Description
- Mega process
- Observation Owner"]:::info

SC1 --> SC3["Optional Fields

- Financial impact
- Root cause
- Process and sub process
- Risk and control
- Recommendation
- Attachments"]:::info

SC1 --> SC4[Submit Sub Observation]

SC4 --> SC5["Created

- Status: Open
- Email to sub observation owner"]:::action

SC5 --> SS1{Owner Action}

SS1 -->|Submit Response| SS2["Status: Awaiting Response

- Email to auditor or creator"]:::info

SS1 -->|Close| SS3["Status: Closed

- Email to owner and creator"]:::action

SC5 --> ODUE1{Due date crossed?}

ODUE1 -->|Yes| ODUE2["Overdue Alert

- Email to sub observation owner"]:::error

ODUE1 -->|No| ODUE3[No overdue email]

MC1 --> MC2["Repository

- All management comments in one place"]:::info

MC2 --> MC3["Includes

- Query
- Draft Observation
- Dropped
- Final Observation
- Closed"]:::info

MC3 --> MC4["Actions

- Search
- Filter"]:::info

MC4 --> END([End])
```

---
