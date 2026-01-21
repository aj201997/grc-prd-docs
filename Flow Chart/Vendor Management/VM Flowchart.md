# Vendor Management Module Flowcharts (GitHub Mermaid)

## 01_budget_listing_and_creation.md

```mermaid
flowchart TD

%% ==========================================================
%% VENDOR MANAGEMENT - BUDGET LISTING AND CREATION
%% ==========================================================

S0([Start]) --> S1[Login to System]
S1 --> S2[Open Vendor Management Module]
S2 --> S3[Open Budget Creation Module]
S3 --> S4[Budget Listing Page]

S4 --> S5[Use Global Search Optional]
S4 --> S6[Select Financial Year Filter Optional]
S4 --> S7[View Budget List Columns]
S7 --> S7A[Budget Details]
S7A --> S7B[Financial Year]
S7B --> S7C[Budget Code]
S7C --> S7D[Unique Budget Code]
S7D --> S7E[Budget Amount]
S7E --> S7F[Status]

S4 --> S8[Click Add New Budget]
S8 --> F1[Budget Creation Form]

F1 --> F2[Select Budget Details Mandatory]
F2 --> F3{Budget Details is Other}
F3 -->|Yes| F4[Enter Budget Details Free Text Mandatory]
F3 -->|No| F5[Continue]

F4 --> F6[Select Financial Year Mandatory]
F5 --> F6
F6 --> F7[Enter Reference Number Mandatory]
F7 --> F8[Enter Budget Amount Mandatory Numeric Only]
F8 --> F9[Budget Amount Validation No Negative Excluding Tax]

F9 --> F10[System Generates Budget Code Using FY and Reference]
F10 --> V1{Mandatory Fields Completed}
V1 -->|No| V2[Show Validation Errors]
V1 -->|Yes| F11[Submit Budget]

F11 --> S9[Budget Created and Visible in Listing]
S9 --> End([End])

```

## 02_budget_approval_workflow.md

```mermaid
flowchart TD

%% ==========================================================
%% VENDOR MANAGEMENT - BUDGET APPROVAL WORKFLOW
%% ==========================================================

S0([Start]) --> S1[Budget Submitted by Audit Owner]
S1 --> S2[Notify Head Audit by Email]
S2 --> S3[Head Audit Reviews Budget]

S3 --> D1{Approve or Reject}
D1 -->|Approve| A1[Budget Approved]
A1 --> A2[Status Approved]
A2 --> A3[Budget Available for PO and Invoice Validation]
A3 --> End([End])

D1 -->|Reject| R1[Head Audit Adds Rejection Remarks Mandatory]
R1 --> R2[Reject Budget]
R2 --> R3[Status Rejected]
R3 --> R4[Notify Audit Owner]

R4 --> U1[Audit Owner Edits Budget Details]
U1 --> U2[Resubmit Budget for Approval]
U2 --> S2

S2 --> REM1[System Sends Reminder Every 15 Days Until Approved]
REM1 --> S3

```

## 03_vendor_listing_and_creation.md

```mermaid
flowchart TD

%% ==========================================================
%% VENDOR MANAGEMENT - VENDOR LISTING AND CREATION
%% ==========================================================

S0([Start]) --> S1[Login to System]
S1 --> S2[Open Vendor Management Module]
S2 --> S3[Open Vendor Creation Module]
S3 --> S4[Vendor Listing Page]

S4 --> S5[Search Vendor Optional]
S4 --> S6[Sort Any Column by Clicking Header]
S4 --> S7[Click Add New Vendor]
S7 --> F1[Vendor Creation Form]

F1 --> F2[Enter Vendor Name Mandatory]
F2 --> F3[Enter PAN Mandatory]
F3 --> V1{PAN Already Exists}
V1 -->|Yes| V2[Show Error PAN Must be Unique]
V1 -->|No| F4[Select MSME Yes or No Mandatory]
F4 --> F5[Attach KYC Documents Mandatory]
F5 --> V3{Mandatory Fields Completed}
V3 -->|No| V4[Show Validation Errors]
V3 -->|Yes| F6[Submit Vendor]

F6 --> S8[Vendor Created and Visible in Listing]
S8 --> S9[KYC Documents Download Link Available]
S9 --> End([End])

```

## 04_po_listing_and_creation.md

```mermaid
flowchart TD

%% ==========================================================
%% VENDOR MANAGEMENT - PO LISTING AND PO CREATION
%% ==========================================================

S0([Start]) --> S1[Login to System]
S1 --> S2[Open Vendor Management Module]
S2 --> S3[Open PO Creation Module]
S3 --> S4[PO Listing Page]

S4 --> S5[Search PO Optional]
S4 --> S6[Sort Any Column by Clicking Header]
S4 --> S7[Click Add New PO]
S7 --> F1[Record New PO Form]

F1 --> F2[Select Vendor Name Mandatory]
F2 --> F3[System Auto Populates PAN from Vendor Master]
F3 --> F4[Enter PO Reference Number Mandatory]
F4 --> V1{PO Reference Unique}
V1 -->|No| V2[Show Error PO Reference Already Exists]
V1 -->|Yes| F5[Select Unique Budget Code Mandatory]
F5 --> F6[Enter Service Description Mandatory]
F6 --> F7[Enter PO Amount Mandatory Numeric Only]
F7 --> F8[PO Amount Validation No Negative Excluding Tax]

F8 --> F9[Attach Final PO Agreement Rate Contract Mandatory]
F9 --> F10[Attach Approval Note Mandatory]
F10 --> F11[Add Remarks Optional]

F11 --> CHK1{All Mandatory Attachments Added}
CHK1 -->|No| POP1[Popup Missing Attachments Proceed Yes or No]
POP1 -->|No| F9
POP1 -->|Yes| CHK2[Continue Submission]

CHK1 -->|Yes| CHK2

CHK2 --> CHK3{PO Amount Exceeds Budget}
CHK3 -->|Yes| POP2[Popup PO Amount Exceeds Budget Proceed Yes or No]
POP2 -->|No| F7
POP2 -->|Yes| CHK4[Continue Submission]
CHK3 -->|No| CHK4

CHK4 --> F12[Submit PO]
F12 --> S8[PO Created and Visible in Listing]
S8 --> End([End])

```

## 05_po_approval_workflow_and_status_logic.md

```mermaid
flowchart TD

%% ==========================================================
%% VENDOR MANAGEMENT - PO APPROVAL WORKFLOW AND STATUS LOGIC
%% ==========================================================

S0([Start]) --> S1[PO Submitted by Audit Owner]
S1 --> S2[Notify Head Audit by Email]
S2 --> S3[Head Audit Reviews PO]

S3 --> D1{Approve or Reject}
D1 -->|Approve| A1[PO Approved]
A1 --> A2[Notify Audit Owner and Head Audit]
A2 --> A3[PO Status Set to Open]
A3 --> L1[PO Available for Invoice Recording]
A3 --> End([End])

D1 -->|Reject| R1[Head Audit Adds Rejection Remarks Mandatory]
R1 --> R2[Reject PO]
R2 --> R3[Notify Audit Owner]
R3 --> U1[Audit Owner Updates PO]
U1 --> U2[Resubmit PO]
U2 --> S2

L1 --> ST1[System Calculates Total Invoice Basic Amount]
ST1 --> ST2{PO Amount Greater Than or Equal Total Invoice Basic}
ST2 -->|Yes| ST3[PO Status Closed]
ST2 -->|No| ST4[PO Status Open]

```

## 06_po_short_closure_workflow.md

```mermaid
flowchart TD

%% ==========================================================
%% VENDOR MANAGEMENT - PO SHORT CLOSURE WORKFLOW
%% ==========================================================

S0([Start]) --> S1[Open PO Listing]
S1 --> S2[Open PO Details]

S2 --> D1{PO Status is Open}
D1 -->|No| E1[Short Closure Not Allowed]
E1 --> End([End])

D1 -->|Yes| S3[Click Short Closure]
S3 --> F1[Short Closure Form]

F1 --> F2[System Shows Pending PO Amount]
F2 --> F3[Enter Short Closure Amount Mandatory]
F3 --> F4[Enter Reason Mandatory]

F4 --> V1{Short Closure Amount Less Than or Equal Pending}
V1 -->|No| V2[Show Validation Error]
V2 --> F3
V1 -->|Yes| S4[Submit Short Closure Request]

S4 --> N1[Notify Head Audit by Email]
N1 --> H1[Head Audit Reviews Short Closure]

H1 --> D2{Approve or Reject}
D2 -->|Reject| R1[Rejection Remarks Mandatory]
R1 --> R2[Notify Audit Owner]
R2 --> S3

D2 -->|Approve| A1[Short Closure Approved]
A1 --> A2[PO Status Closed]
A2 --> A3[Pending Amount Set to Zero]
A3 --> A4[Block New Invoice Recording for PO]
A4 --> End

```

## 07_invoice_listing_and_recording.md

```mermaid
flowchart TD

%% ==========================================================
%% VENDOR MANAGEMENT - INVOICE LISTING AND INVOICE RECORDING
%% ==========================================================

S0([Start]) --> S1[Login to System]
S1 --> S2[Open Vendor Management Module]
S2 --> S3[Open Invoice Recording Module]
S3 --> S4[Invoice Listing Page]

S4 --> S5[Search Invoice Optional]
S4 --> S6[Sort Any Column by Clicking Header]
S4 --> S7[View Columns Including Payment Approval Reference]
S4 --> S8[Click Record New Invoice]
S8 --> F1[Invoice Recording Form]

F1 --> F2[Select PO Reference Mandatory]
F2 --> F3[System Auto Populates Vendor PAN PO Date Service Description]
F3 --> F4[Enter Invoice Number Mandatory]
F4 --> V1{Invoice Number Unique}
V1 -->|No| V2[Show Error Invoice Number Already Exists]
V1 -->|Yes| F5[Enter Basic Amount Mandatory Numeric]
F5 --> F6[Enter IGST CGST SGST Optional Based on Tax]
F6 --> F7[System Calculates Total Invoice Amount Basic Plus Taxes]

F7 --> F8[Attach Invoice Document Mandatory]

F8 --> C1{Deliverables Received}
C1 -->|Yes| C2[Proceed]
C1 -->|No| C3[Enter Remarks Mandatory]
C3 --> C2

C2 --> CHK1{Invoice Basic Amount Exceeds PO Amount}
CHK1 -->|Yes| ERR1[Show Error Invoice Amount Exceeds PO]
ERR1 --> End([End])
CHK1 -->|No| F9[Submit Invoice]

F9 --> S9[Invoice Created]
S9 --> End([End])

```

## 08_invoice_approval_and_payment_reference.md

```mermaid
flowchart TD

%% ==========================================================
%% VENDOR MANAGEMENT - INVOICE APPROVAL AND PAYMENT REFERENCE
%% ==========================================================

S0([Start]) --> S1[Invoice Submitted by Audit Owner]
S1 --> S2[Notify Head Audit by Email]
S2 --> S3[Head Audit Reviews Invoice]

S3 --> D1{Approve or Reject}
D1 -->|Reject| R1[Rejection Remarks Mandatory]
R1 --> R2[Reject Invoice]
R2 --> R3[Notify Audit Owner]
R3 --> U1[Audit Owner Updates Invoice]
U1 --> U2[Resubmit Invoice]
U2 --> S2

D1 -->|Approve| A1[Invoice Approved]
A1 --> A2[System Generates Unique Payment Approval Reference Number]
A2 --> A3[Show Reference Number in Invoice Listing]
A3 --> A4[Invoice Eligible for Payment Top Sheet]
A4 --> End([End])

```

## 09_payment_top_sheet_flow.md

```mermaid
flowchart TD

%% ==========================================================
%% VENDOR MANAGEMENT - PAYMENT TOP SHEET FLOW
%% ==========================================================

S0([Start]) --> S1[Invoice Approved]
S1 --> S2[Open Invoice Listing]
S2 --> S3[Select Invoice]
S3 --> S4[Generate Payment Top Sheet]
S4 --> S5[System Downloads Excel Template Automatically]

S5 --> S6[Upload Signed Payment Top Sheet Mandatory]
S6 --> S7[Upload Supporting Documents Optional]
S7 --> S8[Submit Payment Top Sheet]

S8 --> V1{Signed Payment Top Sheet Attached}
V1 -->|Yes| S9[Payment Top Sheet Completed]
S9 --> End([End])

V1 -->|No| REM1[Reminder Email to Audit Owner Every 15 Days]
REM1 --> S6

```

## 10_budget_vs_po_view.md

```mermaid
flowchart TD

%% ==========================================================
%% VENDOR MANAGEMENT - BUDGET VS PO VIEW
%% ==========================================================

S0([Start]) --> S1[Open Vendor Management Module]
S1 --> S2[Open Budget vs PO vs Invoice Module]
S2 --> S3[Default View Budget vs PO]

S3 --> S4[System Auto Populates Read Only Data]
S4 --> S5[Calculate Pending Budget]
S5 --> S6[Pending Budget Equals Budget Amount Minus Total PO Amount]
S6 --> S7[Pending Budget Can be Negative if PO Greater Than Budget]
S7 --> End([End])

```

## 11_po_vs_invoice_view_and_drilldown.md

```mermaid
flowchart TD

%% ==========================================================
%% VENDOR MANAGEMENT - PO VS INVOICE VIEW AND DRILLDOWN
%% ==========================================================

S0([Start]) --> S1[Open Vendor Management Module]
S1 --> S2[Open Budget vs PO vs Invoice Module]
S2 --> S3[Switch to PO vs Invoice View]

S3 --> S4[System Auto Populates Read Only Data]
S4 --> S5[Calculate Pending PO Amount]
S5 --> S6[Pending PO Equals PO Amount Minus Total Invoice Basic Amount]

S6 --> D1{User Clicks for Drilldown}
D1 -->|Click PO Reference| D2[Open PO Details Page]
D1 -->|Click Total Invoice Amount| D3[Open Invoice Details Page]

D2 --> End([End])
D3 --> End

```

## 99_vendor_management_full_end_to_end.md

```mermaid
flowchart TD

%% ==========================================================
%% VENDOR MANAGEMENT - FULL END TO END FLOW
%% GitHub Mermaid Compatible
%% ==========================================================

START([Start]) --> A1[Login to System]
A1 --> A2[Open Vendor Management Module]

A2 --> B1[Budget Creation Module]
B1 --> B2[Budget Listing and Create Budget]
B2 --> B3[Submit Budget for Approval]
B3 --> B4[Head Audit Approval]
B4 --> B5{Approved}
B5 -->|No| B6[Reject with Remarks and Resubmit]
B6 --> B4
B5 -->|Yes| B7[Budget Approved]

B4 --> BR1[Reminder Every 15 Days Until Approved]
BR1 --> B4

A2 --> V1[Vendor Creation Module]
V1 --> V2[Create Vendor with PAN Validation and KYC]
V2 --> V3[Vendor Created]

A2 --> P1[PO Creation Module]
P1 --> P2[Create PO with Budget Mapping]
P2 --> P3[Mandatory Attachments and Validations]
P3 --> P4[Submit PO]
P4 --> P5[Head Audit Approval]
P5 --> P6{Approved}
P6 -->|No| P7[Reject with Remarks and Resubmit]
P7 --> P5
P6 -->|Yes| P8[PO Approved Status Open]

P8 --> PS1[System Updates PO Status Based on Invoice Basic Totals]

PS1 --> SC1{Need Short Closure}
SC1 -->|No| NEXT1[Continue]
SC1 -->|Yes| SC2[Short Closure Request and Approval]
SC2 --> SC3[PO Closed and Block Invoices]

A2 --> I1[Invoice Recording Module]
I1 --> I2[Record Invoice Linked to PO]
I2 --> I3[Deliverables Confirmation]
I3 --> I4[Submit Invoice]
I4 --> I5[Head Audit Approval]
I5 --> I6{Approved}
I6 -->|No| I7[Reject with Remarks and Resubmit]
I7 --> I5
I6 -->|Yes| I8[Generate Payment Approval Reference Number]

I8 --> PT1[Generate and Upload Payment Top Sheet]
PT1 --> PT2{Signed Top Sheet Attached}
PT2 -->|No| PT3[Reminder Every 15 Days]
PT3 --> PT1
PT2 -->|Yes| PT4[Payment Top Sheet Completed]

A2 --> D1[Budget vs PO vs Invoice Module]
D1 --> D2[Budget vs PO View Pending Budget]
D1 --> D3[PO vs Invoice View Pending PO]
D3 --> D4[Drilldown to PO or Invoice Details]

END([End])

```

