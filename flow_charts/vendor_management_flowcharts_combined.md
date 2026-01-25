# Vendor Management Module Flowcharts (SVG-safe Mermaid for GitHub)

> This file contains **all Vendor Management flowcharts** combined into one Markdown file.
> Each flowchart is in an individual Mermaid block for GitHub preview + SVG export.

---

## 01_budget_listing_and_creation

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["BUDGET LISTING & CREATION"]:::heading --> S0([Start])

S0 --> S1[Open Vendor Management Module]
S1 --> S2[Go to Budget Creation]
S2 --> S3[Budget Listing Page]

S3 --> L1["Budget Listing Columns

- Budget Details
- Financial Year
- Budget Code
- Unique Budget Code
- Budget Amount
- Status"]:::info

S3 --> S4["Listing Actions

- Global Search (optional)
- Financial Year filter (optional)"]:::info

S3 --> S5[Click Add New Budget]
S5 --> F1[Budget Creation Form]

F1 --> FM1["Mandatory Fields

- Budget Details
- Financial Year
- Reference Number
- Budget Amount"]:::info

F1 --> FO1["Optional Fields

- Budget Details - Other Free Text
- Attachment
- Remarks"]:::info

FM1 --> C1{Budget Details selected as Other?}

C1 -->|Yes| C2[Show Other Free Text field as mandatory]
C1 -->|No| C3[Continue]

C2 --> V1{Validate Budget Amount}
C3 --> V1

V1 -->|Invalid| V2["Validation Error

- Only numeric allowed
- No negative values
- Amount excluding tax"]:::error

V1 -->|Valid| G1["System Action

- Generate Unique Budget Code using FY and Reference"]:::action

G1 --> SUB1[Submit Budget]
SUB1 --> OUT1["Budget Created

- Visible in listing"]:::action
OUT1 --> End([End])
```

---

## 02_budget_approval_workflow

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["BUDGET APPROVAL WORKFLOW"]:::heading --> S0([Start])

S0 --> S1[Audit Owner submits Budget]
S1 --> N1[Email to Head Audit]
N1 --> H1[Head Audit reviews Budget]

H1 --> D1{Approve or Reject?}

D1 -->|Approve| A1["Approved

- Status: Approved
- Budget usable for PO and invoice validations"]:::action
A1 --> End([End])

D1 -->|Reject| R1["Rejected

- Rejection remarks mandatory
- Attachment optional"]:::error

R1 --> R2[Status set to Rejected]
R2 --> R3[Notify Audit Owner]
R3 --> U1[Audit Owner edits and resubmits]
U1 --> N1

N1 --> REM1["Reminder Rule

- Reminder email every 15 days until approved"]:::info
REM1 --> H1
```

---

## 03_vendor_listing_and_creation

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["VENDOR LISTING & CREATION"]:::heading --> S0([Start])

S0 --> S1[Open Vendor Management Module]
S1 --> S2[Go to Vendor Creation]
S2 --> S3[Vendor Listing Page]

S3 --> L1["Listing Actions

- Search (optional)
- Sort by column header (optional)"]:::info

S3 --> S4[Click Add New Vendor]
S4 --> F1[Vendor Creation Form]

F1 --> FM1["Mandatory Fields

- Vendor Name
- PAN
- MSME (Yes/No)
- KYC Documents Attachment"]:::info

F1 --> FO1["Optional Fields

- Other Supporting Documents"]:::info

FM1 --> V1{PAN unique?}

V1 -->|No| V2["Validation Error

- PAN already exists"]:::error

V1 -->|Yes| SUB1[Submit Vendor]
SUB1 --> OUT1["Vendor Created

- Visible in listing
- KYC download link available"]:::action
OUT1 --> End([End])
```

---

## 04_po_listing_and_creation

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["PO LISTING & PO CREATION"]:::heading --> S0([Start])

S0 --> S1[Open Vendor Management Module]
S1 --> S2[Go to PO Creation]
S2 --> S3[PO Listing Page]

S3 --> L1["Listing Actions

- Search (optional)
- Sort by column header (optional)"]:::info

S3 --> S4[Click Add New PO]
S4 --> F1[Record New PO Form]

F1 --> FM1["Mandatory Fields

- Vendor Name
- PO Reference Number
- Unique Budget Code
- Service Description
- PO Amount
- Final PO Agreement / Rate Contract Attachment
- Approval Note Attachment"]:::info

F1 --> FO1["Optional Fields

- Remarks"]:::info

F1 --> AP1["System Action

- Auto populate PAN from Vendor Master"]:::action

AP1 --> V1{PO reference unique?}

V1 -->|No| V2["Validation Error

- PO reference already exists"]:::error

V1 -->|Yes| VAMT[Validate PO Amount: numeric and non-negative]
VAMT --> VATT{Mandatory attachments added?}

VATT -->|No| POP1["Popup

- Missing mandatory attachments
- Proceed Yes or No"]:::info

POP1 -->|No| F1
POP1 -->|Yes| VBUD[Check: PO Amount exceeds Budget?]

VATT -->|Yes| VBUD

VBUD -->|Yes| POP2["Popup

- PO amount exceeds budget
- Proceed Yes or No"]:::info

POP2 -->|No| F1
POP2 -->|Yes| SUB1[Submit PO]

VBUD -->|No| SUB1

SUB1 --> OUT1["PO Created

- Visible in listing"]:::action
OUT1 --> End([End])
```

---

## 05_po_approval_and_status_logic

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["PO APPROVAL & STATUS LOGIC"]:::heading --> S0([Start])

S0 --> S1[Audit Owner submits PO]
S1 --> N1[Email to Head Audit]
N1 --> H1[Head Audit reviews PO]

H1 --> D1{Approve or Reject?}

D1 -->|Approve| A1["PO Approved

- Notify Audit Owner and Head Audit
- PO status set to Open"]:::action

A1 --> ST1["Status Logic

- Compare PO amount with total invoice basic"]:::info

ST1 --> ST2{PO Amount >= Total Invoice Basic?}

ST2 -->|Yes| ST3[PO Status: Closed]
ST2 -->|No| ST4[PO Status: Open]

ST3 --> End([End])
ST4 --> End

D1 -->|Reject| R1["Rejected

- Rejection remarks mandatory
- Edit and resubmit required"]:::error

R1 --> U1[Audit Owner updates PO]
U1 --> N1
```

---

## 06_po_short_closure_workflow

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["PO SHORT CLOSURE WORKFLOW"]:::heading --> S0([Start])

S0 --> S1[Open PO Details]
S1 --> D1{PO Status is Open?}

D1 -->|No| E1["Not Allowed

- Short closure allowed only when PO status is Open"]:::error
E1 --> End([End])

D1 -->|Yes| S2[Click Short Closure]
S2 --> F1[Short Closure Form]

F1 --> FM1["Mandatory Fields

- Short Closure Amount
- Reason"]:::info

F1 --> FS1["System Fields

- Pending PO amount displayed"]:::info

F1 --> V1{Short Closure Amount <= Pending?}

V1 -->|No| V2["Validation Error

- Short closure amount exceeds pending amount"]:::error

V1 -->|Yes| SUB1[Submit Short Closure Request]
SUB1 --> N1[Email to Head Audit]
N1 --> H1[Head Audit reviews request]

H1 --> D2{Approve or Reject?}

D2 -->|Reject| R1["Rejected

- Rejection remarks mandatory"]:::error
R1 --> S2

D2 -->|Approve| A1["Approved

- PO closed
- Pending becomes zero
- New invoices blocked"]:::action
A1 --> End([End])
```

---

## 07_invoice_listing_and_recording

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["INVOICE LISTING & RECORDING"]:::heading --> S0([Start])

S0 --> S1[Open Vendor Management Module]
S1 --> S2[Go to Invoice Recording]
S2 --> S3[Invoice Listing Page]

S3 --> L1["Listing Actions

- Search (optional)
- Sort by column header (optional)
- Payment approval reference visible"]:::info

S3 --> S4[Click Record New Invoice]
S4 --> F1[Invoice Recording Form]

F1 --> FM1["Mandatory Fields

- PO Reference
- Invoice Number
- Basic Amount
- Invoice Attachment"]:::info

F1 --> FO1["Optional Fields

- IGST
- CGST
- SGST
- Remarks (if deliverables not received)"]:::info

F1 --> AP1["System Action

- Auto populate PAN, PO date, service description
- Total amount = basic + taxes"]:::action

AP1 --> V1{Invoice number unique?}

V1 -->|No| V2["Validation Error

- Invoice number already exists"]:::error

V1 -->|Yes| C1{Deliverables received?}

C1 -->|Yes| P1[Proceed]
C1 -->|No| R1[Enter Remarks (mandatory)]
R1 --> P1

P1 --> CHK1{Invoice basic amount exceeds PO amount?}

CHK1 -->|Yes| ERR1["Error

- Invoice amount exceeds PO amount"]:::error

CHK1 -->|No| SUB1[Submit Invoice]
SUB1 --> OUT1["Invoice Created

- Visible in listing"]:::action
OUT1 --> End([End])
```

---

## 08_invoice_approval_and_payment_reference

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["INVOICE APPROVAL & PAYMENT REFERENCE"]:::heading --> S0([Start])

S0 --> S1[Audit Owner submits Invoice]
S1 --> N1[Email to Head Audit]
N1 --> H1[Head Audit reviews Invoice]

H1 --> D1{Approve or Reject?}

D1 -->|Reject| R1["Rejected

- Rejection remarks mandatory
- Edit and resubmit required"]:::error
R1 --> U1[Audit Owner updates Invoice]
U1 --> N1

D1 -->|Approve| A1["Approved

- Generate Unique Payment Approval Reference Number
- Reference visible in listing"]:::action
A1 --> End([End])
```

---

## 09_payment_top_sheet_flow

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;

T["PAYMENT TOP SHEET FLOW"]:::heading --> S0([Start])

S0 --> S1[Invoice Approved]
S1 --> S2[Generate Payment Top Sheet]
S2 --> S3["System Action

- Excel template auto downloaded"]:::action

S3 --> FM1["Mandatory Upload

- Signed Payment Top Sheet"]:::info

S3 --> FO1["Optional Upload

- Supporting Documents"]:::info

FM1 --> SUB1[Submit Payment Top Sheet]
SUB1 --> V1{Signed top sheet attached?}

V1 -->|Yes| DONE1["Completed

- Payment top sheet successfully attached"]:::action
DONE1 --> End([End])

V1 -->|No| REM1["Reminder Rule

- Reminder email every 15 days to Audit Owner"]:::info
REM1 --> FM1
```

---

## 10_budget_vs_po_view

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;

T["BUDGET VS PO VIEW"]:::heading --> S0([Start])

S0 --> S1[Open Budget vs PO vs Invoice Module]
S1 --> S2[Default View: Budget vs PO]

S2 --> BOX1["Read Only Columns

- Budget Amount
- Total PO Amount
- Pending Budget Amount"]:::info

BOX1 --> CALC1["Pending Budget Formula

- Pending = Budget Amount - Total PO Amount
- Can be negative if PO exceeds budget"]:::info

CALC1 --> End([End])
```

---

## 11_po_vs_invoice_view_and_drilldown

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;

T["PO VS INVOICE VIEW & DRILLDOWN"]:::heading --> S0([Start])

S0 --> S1[Open Budget vs PO vs Invoice Module]
S1 --> S2[Switch to PO vs Invoice View]

S2 --> BOX1["Read Only Columns

- PO Amount
- Total Invoice Basic Amount
- Pending PO Amount"]:::info

BOX1 --> CALC1["Pending PO Formula

- Pending = PO Amount - Total Invoice Basic Amount"]:::info

CALC1 --> D1{Drilldown Action}

D1 -->|Click PO Reference| D2[Open PO Details Page]
D1 -->|Click Total Amount| D3[Open Invoice Details Page]

D2 --> End([End])
D3 --> End
```

---

## 99_vendor_management_full_end_to_end

```mermaid
flowchart TD

classDef heading fill:#111827,stroke:#111827,color:#ffffff,stroke-width:3px,font-weight:bold;
classDef info fill:#F3F4F6,stroke:#D1D5DB,color:#111827;
classDef action fill:#DBEAFE,stroke:#2563EB,color:#111827,stroke-width:2px;
classDef error fill:#FEE2E2,stroke:#EF4444,color:#111827,stroke-width:2px;

T["VENDOR MANAGEMENT - FULL END TO END"]:::heading --> START([Start])

START --> A1[Login to System]
A1 --> A2[Open Vendor Management Module]

A2 --> B1[Budget Creation]
B1 --> B2["Listing Actions

- Search (optional)
- Financial Year filter (optional)
- View columns"]:::info

B2 --> B3[Create Budget Form]
B3 --> B4["Mandatory Fields

- Budget Details
- Financial Year
- Reference Number
- Budget Amount"]:::info

B3 --> B5["Optional Fields

- Budget Details other free text
- Attachment
- Remarks"]:::info

B3 --> B6[Submit Budget]
B6 --> B7[Head Audit Review]
B7 --> B8{Approved?}

B8 -->|No| B9["Rejected

- Remarks mandatory
- Resubmit loop"]:::error
B9 --> B7

B8 -->|Yes| B10["Budget Approved

- Budget usable in PO validation"]:::action

B7 --> BR1["Reminder Rule

- Reminder email every 15 days until approved"]:::info
BR1 --> B7

A2 --> V1[Vendor Creation]
V1 --> V2["Mandatory Fields

- Vendor Name
- PAN unique
- MSME yes or no
- KYC documents"]:::info
V1 --> V3[Submit Vendor]
V3 --> V4[Vendor Created]

A2 --> P1[PO Creation]
P1 --> P2["Mandatory Fields

- Vendor
- PO reference unique
- Budget code
- PO amount
- Mandatory attachments"]:::info

P1 --> P3["Validation Popups

- Missing attachments: proceed yes/no
- PO exceeds budget: proceed yes/no"]:::info

P1 --> P4[Submit PO]
P4 --> P5[Head Audit Review]
P5 --> P6{Approved?}

P6 -->|No| P7["Rejected

- Reject with remarks and resubmit"]:::error
P7 --> P5

P6 -->|Yes| P8["PO Approved

- Status: Open"]:::action

P8 --> PS1["Auto Status

- Closed if PO amount >= total invoice basic
- Open otherwise"]:::info

PS1 --> SC1{Short Closure Needed?}

SC1 -->|No| NEXT1[Continue]

SC1 -->|Yes| SC2["Short Closure

- Allowed only if PO open
- Head audit approval"]:::info

SC2 --> SC3["On Approval

- PO closed
- Pending zero
- Block invoices"]:::action

A2 --> I1[Invoice Recording]
I1 --> I2["Mandatory Fields

- PO reference
- Invoice number unique
- Basic amount
- Invoice attachment"]:::info

I1 --> I3["System Actions

- Auto populate PAN, PO date, service
- Total = basic + taxes"]:::action

I1 --> I4["Deliverables Confirmation

- If No then remarks mandatory"]:::info

I1 --> I5[Submit Invoice]
I5 --> I6[Head Audit Review]
I6 --> I7{Approved?}

I7 -->|No| I8["Rejected

- Reject with remarks and resubmit"]:::error
I8 --> I6

I7 -->|Yes| I9["Invoice Approved

- Generate payment approval reference"]:::action

I9 --> PT1["Payment Top Sheet

- Auto download excel
- Upload signed top sheet mandatory"]:::info

PT1 --> PT2{Signed attached?}

PT2 -->|No| PT3["Reminder

- Every 15 days"]:::info
PT3 --> PT1

PT2 -->|Yes| PT4[Completed]

A2 --> D1[Budget vs PO vs Invoice Views]
D1 --> D2[Budget vs PO View: Pending Budget]
D1 --> D3[PO vs Invoice View: Pending PO Drilldowns]

D3 --> END([End])
```

---
