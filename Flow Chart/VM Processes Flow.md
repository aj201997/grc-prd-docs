# Vendor Management Individual Flowcharts (Formatted GitHub Mermaid)

## 01_budget_listing_and_creation.md

```mermaid
flowchart TD

%% ======================================
%% BUDGET LISTING + CREATION (FORMATTED)
%% ======================================

S0([Start]) --> S1[Open Vendor Management Module]
S1 --> S2[Go to Budget Creation]
S2 --> S3[Budget Listing Page]

S3 --> L1["<b>Budget Listing Columns</b><br/><br/>- Budget Details<br/>- Financial Year<br/>- Budget Code<br/>- Unique Budget Code<br/>- Budget Amount<br/>- Status"]

S3 --> S4["<b>Listing Actions</b><br/><br/>- Global Search optional<br/>- Financial Year filter optional"]
S3 --> S5[Click Add New Budget]
S5 --> F1[Budget Creation Form]

F1 --> FM1["<b>Mandatory Fields:-</b><br/><br/>- Budget Details<br/>- Financial Year<br/>- Reference Number<br/>- Budget Amount"]
F1 --> FO1["<b>Optional Fields:-</b><br/><br/>- Budget Details - Other Free Text<br/>- Attachment<br/>- Remarks"]

FM1 --> C1{Budget Details Selected as Other}
C1 -->|Yes| C2[Show Other Free Text Field Mandatory]
C1 -->|No| C3[Continue]

C2 --> V1{Validate Budget Amount}
C3 --> V1

V1 -->|Invalid| V2["<b>Validation Error</b><br/><br/>- Only numeric allowed<br/>- No negative values<br/>- Amount excluding tax"]
V1 -->|Valid| G1["<b>System Action</b><br/><br/>- Generate Unique Budget Code using FY and Reference"]

G1 --> SUB1[Submit Budget]
SUB1 --> OUT1[Budget Created and Visible in Listing]
OUT1 --> End([End])

```

## 02_budget_approval_workflow.md

```mermaid
flowchart TD

%% ======================================
%% BUDGET APPROVAL WORKFLOW (FORMATTED)
%% ======================================

S0([Start]) --> S1[Audit Owner Submits Budget]
S1 --> N1[Email to Head Audit]
N1 --> H1[Head Audit Reviews Budget]

H1 --> D1{Approve or Reject}
D1 -->|Approve| A1["<b>Approved</b><br/><br/>- Status Approved<br/>- Budget usable for PO and invoice validations"]
A1 --> End([End])

D1 -->|Reject| R1["<b>Rejected</b><br/><br/>- Rejection remarks mandatory<br/>- Attachment optional"]
R1 --> R2[Status Rejected]
R2 --> R3[Notify Audit Owner]
R3 --> U1[Audit Owner Edits and Resubmits]
U1 --> N1

N1 --> REM1["<b>Reminder Rule</b><br/><br/>- Reminder email every 15 days until approved"]
REM1 --> H1

```

## 03_vendor_listing_and_creation.md

```mermaid
flowchart TD

%% ======================================
%% VENDOR LISTING + CREATION (FORMATTED)
%% ======================================

S0([Start]) --> S1[Open Vendor Management Module]
S1 --> S2[Go to Vendor Creation]
S2 --> S3[Vendor Listing Page]

S3 --> L1["<b>Listing Actions</b><br/><br/>- Search optional<br/>- Sort by column header optional"]
S3 --> S4[Click Add New Vendor]
S4 --> F1[Vendor Creation Form]

F1 --> FM1["<b>Mandatory Fields:-</b><br/><br/>- Vendor Name<br/>- PAN<br/>- MSME Yes or No<br/>- KYC Documents Attachment"]
F1 --> FO1["<b>Optional Fields:-</b><br/><br/>- Other Supporting Documents"]

FM1 --> V1{PAN Unique}
V1 -->|No| V2["<b>Validation Error</b><br/><br/>- PAN already exists"]
V1 -->|Yes| SUB1[Submit Vendor]

SUB1 --> OUT1["<b>Vendor Created</b><br/><br/>- Visible in listing<br/>- KYC download link available"]
OUT1 --> End([End])

```

## 04_po_listing_and_creation.md

```mermaid
flowchart TD

%% ======================================
%% PO LISTING + PO CREATION (FORMATTED)
%% ======================================

S0([Start]) --> S1[Open Vendor Management Module]
S1 --> S2[Go to PO Creation]
S2 --> S3[PO Listing Page]

S3 --> L1["<b>Listing Actions</b><br/><br/>- Search optional<br/>- Sort by column header optional"]
S3 --> S4[Click Add New PO]
S4 --> F1[Record New PO Form]

F1 --> FM1["<b>Mandatory Fields:-</b><br/><br/>- Vendor Name<br/>- PO Reference Number<br/>- Unique Budget Code<br/>- Service Description<br/>- PO Amount<br/>- Final PO Agreement Rate Contract Attachment<br/>- Approval Note Attachment"]
F1 --> FO1["<b>Optional Fields:-</b><br/><br/>- Remarks"]

F1 --> AP1["<b>System Action</b><br/><br/>- Auto populate PAN from vendor master"]
AP1 --> V1{PO Reference Unique}

V1 -->|No| V2["<b>Validation Error</b><br/><br/>- PO reference already exists"]
V1 -->|Yes| VAMT[Validate PO Amount Numeric and Non Negative]

VAMT --> VATT{Mandatory Attachments Added}
VATT -->|No| POP1["<b>Popup</b><br/><br/>- Missing mandatory attachments<br/>- Proceed Yes or No"]
POP1 -->|No| F1
POP1 -->|Yes| VBUD[Check PO Amount Exceeds Budget]

VATT -->|Yes| VBUD

VBUD -->|Yes| POP2["<b>Popup</b><br/><br/>- PO amount exceeds budget<br/>- Proceed Yes or No"]
POP2 -->|No| F1
POP2 -->|Yes| SUB1[Submit PO]

VBUD -->|No| SUB1

SUB1 --> OUT1[PO Created and Visible in Listing]
OUT1 --> End([End])

```

## 05_po_approval_and_status_logic.md

```mermaid
flowchart TD

%% ======================================
%% PO APPROVAL + STATUS LOGIC (FORMATTED)
%% ======================================

S0([Start]) --> S1[Audit Owner Submits PO]
S1 --> N1[Email to Head Audit]
N1 --> H1[Head Audit Reviews PO]

H1 --> D1{Approve or Reject}
D1 -->|Approve| A1["<b>PO Approved</b><br/><br/>- Notify Audit Owner and Head Audit<br/>- PO status set to Open"]
A1 --> ST1["<b>Status Logic</b><br/><br/>- Compare PO amount with total invoice basic"]
ST1 --> ST2{PO Amount Greater Than or Equal Total Invoice Basic}
ST2 -->|Yes| ST3[PO Status Closed]
ST2 -->|No| ST4[PO Status Open]
ST3 --> End([End])
ST4 --> End

D1 -->|Reject| R1["<b>Rejected</b><br/><br/>- Rejection remarks mandatory<br/>- Edit and resubmit required"]
R1 --> U1[Audit Owner Updates PO]
U1 --> N1

```

## 06_po_short_closure_workflow.md

```mermaid
flowchart TD

%% ======================================
%% PO SHORT CLOSURE WORKFLOW (FORMATTED)
%% ======================================

S0([Start]) --> S1[Open PO Details]
S1 --> D1{PO Status Open}

D1 -->|No| E1["<b>Not Allowed</b><br/><br/>- Short closure allowed only when PO status is Open"]
E1 --> End([End])

D1 -->|Yes| S2[Click Short Closure]
S2 --> F1[Short Closure Form]

F1 --> FM1["<b>Mandatory Fields:-</b><br/><br/>- Short Closure Amount<br/>- Reason"]
F1 --> FS1["<b>System Fields</b><br/><br/>- Pending PO amount displayed"]

F1 --> V1{Short Closure Amount Less Than or Equal Pending}
V1 -->|No| V2["<b>Validation Error</b><br/><br/>- Short closure amount exceeds pending amount"]
V1 -->|Yes| SUB1[Submit Short Closure Request]

SUB1 --> N1[Email to Head Audit]
N1 --> H1[Head Audit Reviews Request]

H1 --> D2{Approve or Reject}
D2 -->|Reject| R1["<b>Rejected</b><br/><br/>- Rejection remarks mandatory"]
R1 --> S2

D2 -->|Approve| A1["<b>Approved</b><br/><br/>- PO closed<br/>- Pending becomes zero<br/>- New invoices blocked"]
A1 --> End([End])

```

## 07_invoice_listing_and_recording.md

```mermaid
flowchart TD

%% ======================================
%% INVOICE LISTING + RECORDING (FORMATTED)
%% ======================================

S0([Start]) --> S1[Open Vendor Management Module]
S1 --> S2[Go to Invoice Recording]
S2 --> S3[Invoice Listing Page]

S3 --> L1["<b>Listing Actions</b><br/><br/>- Search optional<br/>- Sort by column header optional<br/>- Payment approval reference visible"]
S3 --> S4[Click Record New Invoice]
S4 --> F1[Invoice Recording Form]

F1 --> FM1["<b>Mandatory Fields:-</b><br/><br/>- PO Reference<br/>- Invoice Number<br/>- Basic Amount<br/>- Invoice Attachment"]
F1 --> FO1["<b>Optional Fields:-</b><br/><br/>- IGST<br/>- CGST<br/>- SGST<br/>- Remarks if deliverables not received"]

F1 --> AP1["<b>System Action</b><br/><br/>- Auto populate PAN PO date service description<br/>- Total amount = basic + taxes"]
AP1 --> V1{Invoice Number Unique}

V1 -->|No| V2["<b>Validation Error</b><br/><br/>- Invoice number already exists"]
V1 -->|Yes| C1{Deliverables Received}

C1 -->|Yes| P1[Proceed]
C1 -->|No| R1[Enter Remarks Mandatory]
R1 --> P1

P1 --> CHK1{Invoice Basic Amount Exceeds PO Amount}
CHK1 -->|Yes| ERR1["<b>Error</b><br/><br/>- Invoice amount exceeds PO amount"]
CHK1 -->|No| SUB1[Submit Invoice]

SUB1 --> OUT1[Invoice Created and Visible in Listing]
OUT1 --> End([End])

```

## 08_invoice_approval_and_payment_reference.md

```mermaid
flowchart TD

%% ======================================
%% INVOICE APPROVAL + PAYMENT REFERENCE (FORMATTED)
%% ======================================

S0([Start]) --> S1[Audit Owner Submits Invoice]
S1 --> N1[Email to Head Audit]
N1 --> H1[Head Audit Reviews Invoice]

H1 --> D1{Approve or Reject}
D1 -->|Reject| R1["<b>Rejected</b><br/><br/>- Rejection remarks mandatory<br/>- Edit and resubmit required"]
R1 --> U1[Audit Owner Updates Invoice]
U1 --> N1

D1 -->|Approve| A1["<b>Approved</b><br/><br/>- Generate Unique Payment Approval Reference Number<br/>- Reference visible in listing"]
A1 --> End([End])

```

## 09_payment_top_sheet_flow.md

```mermaid
flowchart TD

%% ======================================
%% PAYMENT TOP SHEET FLOW (FORMATTED)
%% ======================================

S0([Start]) --> S1[Invoice Approved]
S1 --> S2[Generate Payment Top Sheet]
S2 --> S3["<b>System Action</b><br/><br/>- Excel template auto downloaded"]

S3 --> FM1["<b>Mandatory Upload:-</b><br/><br/>- Signed Payment Top Sheet"]
S3 --> FO1["<b>Optional Upload:-</b><br/><br/>- Supporting Documents"]

FM1 --> SUB1[Submit Payment Top Sheet]
SUB1 --> V1{Signed Top Sheet Attached}

V1 -->|Yes| DONE1["<b>Completed</b><br/><br/>- Payment top sheet successfully attached"]
DONE1 --> End([End])

V1 -->|No| REM1["<b>Reminder Rule</b><br/><br/>- Reminder email every 15 days to Audit Owner"]
REM1 --> FM1

```

## 10_budget_vs_po_view.md

```mermaid
flowchart TD

%% ======================================
%% BUDGET VS PO VIEW (FORMATTED)
%% ======================================

S0([Start]) --> S1[Open Budget vs PO vs Invoice Module]
S1 --> S2[Default View Budget vs PO]

S2 --> BOX1["<b>Read Only Columns</b><br/><br/>- Budget Amount<br/>- Total PO Amount<br/>- Pending Budget Amount"]
BOX1 --> CALC1["<b>Pending Budget Formula</b><br/><br/>- Pending = Budget Amount - Total PO Amount<br/>- Can be negative if PO exceeds budget"]
CALC1 --> End([End])

```

## 11_po_vs_invoice_view_and_drilldown.md

```mermaid
flowchart TD

%% ======================================
%% PO VS INVOICE VIEW + DRILLDOWN (FORMATTED)
%% ======================================

S0([Start]) --> S1[Open Budget vs PO vs Invoice Module]
S1 --> S2[Switch to PO vs Invoice View]

S2 --> BOX1["<b>Read Only Columns</b><br/><br/>- PO Amount<br/>- Total Invoice Basic Amount<br/>- Pending PO Amount"]
BOX1 --> CALC1["<b>Pending PO Formula</b><br/><br/>- Pending = PO Amount - Total Invoice Basic Amount"]
CALC1 --> D1{Drilldown Action}

D1 -->|Click PO Reference| D2[Open PO Details Page]
D1 -->|Click Total Amount| D3[Open Invoice Details Page]

D2 --> End([End])
D3 --> End

```

## 99_vendor_management_full_end_to_end.md

```mermaid
flowchart TD

%% ==========================================================
%% VENDOR MANAGEMENT - FULL END TO END FLOW (FORMATTED)
%% ==========================================================

START([Start]) --> A1[Login to System]
A1 --> A2[Open Vendor Management Module]

A2 --> B1[Budget Creation]
B1 --> B2["<b>Listing Actions</b><br/><br/>- Search optional<br/>- Financial Year filter optional<br/>- View columns"]
B2 --> B3[Create Budget Form]
B3 --> B4["<b>Mandatory Fields</b><br/><br/>- Budget Details<br/>- Financial Year<br/>- Reference Number<br/>- Budget Amount"]
B3 --> B5["<b>Optional Fields</b><br/><br/>- Budget Details other free text<br/>- Attachment<br/>- Remarks"]
B3 --> B6[Submit Budget]
B6 --> B7[Head Audit Review]
B7 --> B8{Approved}
B8 -->|No| B9["<b>Rejected</b><br/><br/>- Remarks mandatory<br/>- Resubmit loop"]
B9 --> B7
B8 -->|Yes| B10["<b>Budget Approved</b><br/><br/>- Budget usable in PO validation"]

B7 --> BR1["<b>Reminder Rule</b><br/><br/>- Reminder email every 15 days until approved"]
BR1 --> B7

A2 --> V1[Vendor Creation]
V1 --> V2["<b>Mandatory Fields</b><br/><br/>- Vendor Name<br/>- PAN unique<br/>- MSME yes or no<br/>- KYC documents"]
V1 --> V3[Submit Vendor]
V3 --> V4[Vendor Created]

A2 --> P1[PO Creation]
P1 --> P2["<b>Mandatory Fields</b><br/><br/>- Vendor<br/>- PO reference unique<br/>- Budget code<br/>- PO amount<br/>- Mandatory attachments"]
P1 --> P3["<b>Validation Popups</b><br/><br/>- Missing attachments proceed yes or no<br/>- PO exceeds budget proceed yes or no"]
P1 --> P4[Submit PO]
P4 --> P5[Head Audit Review]
P5 --> P6{Approved}
P6 -->|No| P7[Reject with remarks and resubmit]
P7 --> P5
P6 -->|Yes| P8["<b>PO Approved</b><br/><br/>- Status Open"]

P8 --> PS1["<b>Auto Status</b><br/><br/>- Closed if PO amount >= total invoice basic<br/>- Open otherwise"]

PS1 --> SC1{Short Closure Needed}
SC1 -->|No| NEXT1[Continue]
SC1 -->|Yes| SC2["<b>Short Closure</b><br/><br/>- Allowed only if PO open<br/>- Head audit approval"]
SC2 --> SC3["<b>On Approval</b><br/><br/>- PO closed<br/>- Pending zero<br/>- Block invoices"]

A2 --> I1[Invoice Recording]
I1 --> I2["<b>Mandatory Fields</b><br/><br/>- PO reference<br/>- Invoice number unique<br/>- Basic amount<br/>- Invoice attachment"]
I1 --> I3["<b>System Actions</b><br/><br/>- Auto populate PAN PO date service<br/>- Total = basic + taxes"]
I1 --> I4["<b>Deliverables Confirmation</b><br/><br/>- If no then remarks mandatory"]
I1 --> I5[Submit Invoice]
I5 --> I6[Head Audit Review]
I6 --> I7{Approved}
I7 -->|No| I8[Reject with remarks and resubmit]
I8 --> I6
I7 -->|Yes| I9["<b>Invoice Approved</b><br/><br/>- Generate payment approval reference"]

I9 --> PT1["<b>Payment Top Sheet</b><br/><br/>- Auto download excel<br/>- Upload signed top sheet mandatory"]
PT1 --> PT2{Signed attached}
PT2 -->|No| PT3[Reminder every 15 days]
PT3 --> PT1
PT2 -->|Yes| PT4[Completed]

A2 --> D1[Budget vs PO vs Invoice Views]
D1 --> D2[Budget vs PO View Pending Budget]
D1 --> D3[PO vs Invoice View Pending PO Drilldowns]

END([End])

```

