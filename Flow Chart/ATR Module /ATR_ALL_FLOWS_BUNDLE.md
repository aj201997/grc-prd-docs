# ATR Module Flowcharts (GitHub Mermaid)

## 01_atr_overview_and_navigation.md

```mermaid
flowchart TD

%% ======================================
%% ATR MODULE - OVERVIEW AND NAVIGATION
%% ======================================

S0([Start]) --> S1[Open ATR Module]
S1 --> S2{Select Sub Module}

S2 -->|Observations| O1[Observations List Page]
S2 -->|Sub Observations| SO1[Sub Observations List Page]
S2 -->|Management Comments| MC1[Management Comments Page]

O1 --> End([End])
SO1 --> End
MC1 --> End

```

## 02_atr_observations_list_and_filters.md

```mermaid
flowchart TD

%% ======================================
%% ATR - OBSERVATIONS LIST AND FILTERS
%% ======================================

S0([Start]) --> S1[Open ATR Module]
S1 --> S2[Go to Observations Sub Module]
S2 --> S3[View Observations List]

S3 --> S4[View Status Index Counters]
S3 --> S5[Apply Filters]
S5 --> S5A[Filter by Assignee]
S5A --> S5B[Filter by Status]
S5B --> S5C[Filter by Type]
S5C --> S5D[Filter by Date Range]

S3 --> S6[Select Rows Optional]
S6 --> S7{Export Action}
S7 -->|Export Selected| S8[Export Selected to Excel]
S7 -->|Export Full List| S9[Export Full List to Excel]

S3 --> S10[Open Observation Details Page]

S8 --> End([End])
S9 --> End
S10 --> End

```

## 03_atr_observations_manual_creation.md

```mermaid
flowchart TD

%% ======================================
%% ATR - OBSERVATION MANUAL CREATION FLOW
%% ======================================

S0([Start]) --> S1[Open ATR Module]
S1 --> S2[Go to Observations Sub Module]
S2 --> S3[Click Add New Observation]

S3 --> F1[Observation Creation Form]

F1 --> F2[Enter Title Mandatory]
F2 --> F3[Enter Description Mandatory]
F3 --> F4[Select Audit Type Mandatory]
F4 --> F5[Select Engagement Name Mandatory]
F5 --> F6[Enter Financial Impact Mandatory]
F6 --> F7[Enter Management Comment Mandatory]
F7 --> F8[Select Observation Owner Mandatory]
F8 --> F9[Select Risk Category Mandatory]
F9 --> F10[Enter Risk Implication Mandatory]
F10 --> F11[Select Risk Rating Mandatory]

F11 --> F12[Optional Root Cause Process Mapping Recommendation Attachment]

F12 --> V1{Mandatory Fields Completed}
V1 -->|No| V2[Show Validation Errors]
V1 -->|Yes| S4[Submit Observation]

S4 --> S5[Observation Created]
S5 --> S6[Status Final Observation]
S6 --> N1[Notify Observation Owner by Email]

N1 --> End([End])

```

## 04_atr_observations_bulk_import.md

```mermaid
flowchart TD

%% ======================================
%% ATR - OBSERVATIONS BULK IMPORT FLOW
%% ======================================

S0([Start]) --> S1[Open ATR Module]
S1 --> S2[Go to Observations Sub Module]
S2 --> S3[Click Bulk Import]

S3 --> S4[Download Import Template Excel]
S4 --> S5[Fill Template and Upload File]
S5 --> S6[Click Process Validation]

S6 --> V1{File Valid}
V1 -->|No| V2[Show Row and Column Errors]
V2 --> S5

V1 -->|Yes| S7[Submit Import]
S7 --> S8[Records Created]
S8 --> S9[All Imported Observations in Final Observation Status]
S9 --> N1[Notify Importer on Success]

N1 --> End([End])

```

## 05_ia_to_atr_sync_flow.md

```mermaid
flowchart TD

%% ======================================
%% IA TO ATR SYNC FLOW
%% ======================================

S0([Start]) --> S1[Internal Audit Observation Updated]
S1 --> S2{Observation Status}

S2 -->|Final Observation| S3[Eligible for ATR Transfer]
S2 -->|Closed| S3
S2 -->|Draft or Query or Draft Observation| S4[Not Eligible for ATR Transfer]

S3 --> S5[Move Observation to ATR Observations Tab]
S5 --> S6[Observation Listed in ATR]
S6 --> N1[Notify Observation Owner by Email]

S4 --> End([End])
N1 --> End

```

## 06_atr_observation_detail_and_actions.md

```mermaid
flowchart TD

%% ======================================
%% ATR - OBSERVATION DETAIL PAGE AND ACTIONS
%% ======================================

S0([Start]) --> S1[Open ATR Observations List]
S1 --> S2[Open Observation Detail Page]

S2 --> S3[View Observation Details and Attachments]
S2 --> S4[View Management Comments History]

S2 --> S5[Create Sub Observation]
S2 --> S6[Add Management Comment]
S2 --> S7[Update Observation Status if Allowed]

S5 --> End([End])
S6 --> End
S7 --> End

```

## 07_atr_sub_observations_list_and_filters.md

```mermaid
flowchart TD

%% ======================================
%% ATR - SUB OBSERVATIONS LIST AND FILTERS
%% ======================================

S0([Start]) --> S1[Open ATR Module]
S1 --> S2[Go to Sub Observations Sub Module]
S2 --> S3[View Sub Observations List]

S3 --> S4[View Index Counters Total Awaiting Response Closed]
S3 --> S5[Apply Filters]
S5 --> S5A[Filter by Assignee]
S5A --> S5B[Filter by Department]
S5B --> S5C[Filter by Created By]
S5C --> S5D[Filter by Date Range]
S5D --> S5E[Filter by Status]

S3 --> S6[Open Sub Observation Details Page]

S6 --> End([End])

```

## 08_atr_sub_observation_creation.md

```mermaid
flowchart TD

%% ======================================
%% ATR - SUB OBSERVATION CREATION FLOW
%% ======================================

S0([Start]) --> S1[Open ATR Observations List]
S1 --> S2[Open Observation Detail Page]
S2 --> S3[Click Create Sub Observation]

S3 --> F1[Sub Observation Form]

F1 --> F2[Enter Title Mandatory]
F2 --> F3[Enter Description Mandatory]
F3 --> F4[Select Mega Process Mandatory]
F4 --> F5[Select Observation Owner Mandatory]

F5 --> F6[Optional Financial Impact Root Cause Process Sub Process Risk Control Recommendation Attachment]

F6 --> V1{Mandatory Fields Completed}
V1 -->|No| V2[Show Validation Errors]
V1 -->|Yes| S4[Submit Sub Observation]

S4 --> S5[Sub Observation Created]
S5 --> S6[Status Open]
S6 --> N1[Notify Sub Observation Owner by Email]
N1 --> End([End])

```

## 09_atr_sub_observation_status_workflow.md

```mermaid
flowchart TD

%% ======================================
%% ATR - SUB OBSERVATION STATUS WORKFLOW
%% Open -> Awaiting Response -> Closed
%% ======================================

S0([Start]) --> S1[Sub Observation Status Open]
S1 --> S2{Owner Action}

S2 -->|Submit Response| S3[Status Awaiting Response]
S3 --> N1[Notify Auditor or Creator]
S2 -->|Close Sub Observation| S4[Status Closed]
S4 --> N2[Notify Owner and Creator]

N1 --> End([End])
N2 --> End

```

## 10_atr_management_comments_flow.md

```mermaid
flowchart TD

%% ======================================
%% ATR - MANAGEMENT COMMENTS FLOW
%% ======================================

S0([Start]) --> S1[Open ATR Module]
S1 --> S2[Go to Management Comments Sub Module]

S2 --> S3[View Consolidated Management Comments]
S3 --> S4[Includes Query Draft Observation Dropped Final Observation Closed]
S4 --> S5[Search and Filter Comments]

S5 --> End([End])

```

## 11_atr_notifications_overview.md

```mermaid
flowchart TD

%% ======================================
%% ATR - NOTIFICATION OVERVIEW
%% ======================================

S0([Start]) --> S1{Event Trigger}

S1 -->|New Observation Manual Creation| N1[Email to Observation Owner]
S1 -->|Observation Bulk Import Success| N2[Email to Importer]
S1 -->|IA to ATR Transfer| N3[Email to Observation Owner]
S1 -->|Observation Closed| N4[Email to Owner and Auditor]
S1 -->|Sub Observation Created| N5[Email to Sub Observation Owner]
S1 -->|Sub Observation Awaiting Response| N6[Email to Auditor or Creator]
S1 -->|Sub Observation Closed| N7[Email to Owner and Creator]
S1 -->|Sub Observation Overdue| N8[Email to Sub Observation Owner]
S1 -->|New Management Comment Added| N9[Email to Assigned Auditor]

N1 --> End([End])
N2 --> End
N3 --> End
N4 --> End
N5 --> End
N6 --> End
N7 --> End
N8 --> End
N9 --> End

```

## 99_atr_full_end_to_end.md

```mermaid
flowchart TD

%% ==========================================================
%% ATR MODULE - FULL END TO END FLOW
%% GitHub Mermaid Compatible
%% ==========================================================

START([Start]) --> A1[Open ATR Module]
A1 --> A2{Select Sub Module}

A2 -->|Observations| O1[Observations List Page]
A2 -->|Sub Observations| SO1[Sub Observations List Page]
A2 -->|Management Comments| MC1[Management Comments Page]

%% ----------------------------------------------------------
%% OBSERVATIONS LIST
%% ----------------------------------------------------------
O1 --> O2[View Status Index Counters]
O1 --> O3[Apply Filters]
O3 --> O3A[Assignee]
O3A --> O3B[Status]
O3B --> O3C[Type]
O3C --> O3D[Date Range]
O1 --> O4[Export to Excel]
O4 --> O4A[Export Selected]
O4 --> O4B[Export Full List]

O1 --> O5{Create New Observation}
O5 -->|Manual| OM1[Add New Observation]
O5 -->|Bulk Import| BI1[Bulk Import Observations]

%% Manual observation creation
OM1 --> F1[Fill Mandatory Fields]
F1 --> F2[Title Description Audit Type Engagement Name]
F2 --> F3[Financial Impact Management Comment Owner]
F3 --> F4[Risk Category Risk Implication Risk Rating]
F4 --> F5[Optional Root Cause Process Mapping Recommendation Attachment]
F5 --> V1{Validation Pass}
V1 -->|No| VE1[Show Validation Errors]
V1 -->|Yes| OM2[Submit Observation]
OM2 --> OM3[Observation Created in Final Observation Status]
OM3 --> OM4[Email to Observation Owner]

%% Bulk import creation
BI1 --> BI2[Download Template Excel]
BI2 --> BI3[Upload File]
BI3 --> BI4[Process Validation]
BI4 --> BV1{Valid File}
BV1 -->|No| BV2[Show Row and Column Errors]
BV2 --> BI3
BV1 -->|Yes| BI5[Submit Import]
BI5 --> BI6[Imported Observations in Final Observation Status]
BI6 --> BI7[Email to Importer]

%% ----------------------------------------------------------
%% IA TO ATR SYNC
%% ----------------------------------------------------------
IA1[Internal Audit Observation Final or Closed] --> IA2[Transfer to ATR Observations]
IA2 --> IA3[Observation Listed in ATR]
IA3 --> IA4[Email to Observation Owner]

%% ----------------------------------------------------------
%% OBSERVATION DETAIL PAGE
%% ----------------------------------------------------------
O1 --> OD1[Open Observation Detail Page]
OD1 --> OD2[View Observation Details]
OD1 --> OD3[View Management Comments History]
OD1 --> OD4[Create Sub Observation]
OD1 --> OD5[Add Management Comment]

%% ----------------------------------------------------------
%% SUB OBSERVATIONS
%% ----------------------------------------------------------
SO1 --> SO2[View Index Counters Total Awaiting Response Closed]
SO1 --> SO3[Apply Filters Assignee Department Created By Date Range Status]
SO1 --> SO4[Open Sub Observation Detail]

OD4 --> SC1[Sub Observation Form]
SC1 --> SC2[Mandatory Title Description Mega Process Owner]
SC2 --> SC3[Optional Fields Financial Impact Root Cause Risk Control Recommendation Attachment]
SC3 --> SV1{Validation Pass}
SV1 -->|No| SV2[Show Validation Errors]
SV1 -->|Yes| SC4[Submit Sub Observation]
SC4 --> SC5[Sub Observation Created Status Open]
SC5 --> SC6[Email to Sub Observation Owner]

%% Sub observation status flow
SC5 --> SS1[Status Open]
SS1 --> SS2{Owner Action}
SS2 -->|Submit Response| SS3[Status Awaiting Response]
SS3 --> SS4[Email to Auditor or Creator]
SS2 -->|Close| SS5[Status Closed]
SS5 --> SS6[Email to Owner and Creator]

%% Overdue notification
SS1 --> ODUE1{Due Date Crossed}
ODUE1 -->|Yes| ODUE2[Send Overdue Email to Sub Observation Owner]
ODUE1 -->|No| ODUE3[No Overdue Email]

%% ----------------------------------------------------------
%% MANAGEMENT COMMENTS
%% ----------------------------------------------------------
MC1 --> MC2[View Consolidated Comments Repository]
MC2 --> MC3[Includes Query Draft Observation Dropped Final Observation Closed]
MC3 --> MC4[Search and Filter]

%% Notification on new comment
OD5 --> MCN1[Email to Assigned Auditor]

END([End])

```

