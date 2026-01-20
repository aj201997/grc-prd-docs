```mermaid
flowchart TD

%% ======================================
%% ENGAGEMENT CREATION + LIST VIEW FILTERS
%% ======================================

A0([Start]) --> A1[Login to GRC Tool]
A1 --> A2[Open Internal Audit Module]
A2 --> A3[Engagement Listing Page]

A3 --> A4["Use Filters: Audit Plan, Date Range, Audit Type, Audit Sub-type, Created By"]
A4 --> A5[Click Add New]
A5 --> A6[Engagement Creation Form Opens]

A6 --> A7[Enter Engagement Name (Mandatory)]
A7 --> A8{Engagement Name Unique}
A8 -->|No| A9[Error: Name already exists, change name]
A8 -->|Yes| A10[Select Audit Plan (Mandatory)]
A10 --> A11[Select Audit Start Date and Audit End Date (Mandatory)]
A11 --> A12[Select Coverage Period (Mandatory)]

A12 --> A13{Auditor Type Selected}
A13 -->|Internal| A14[Audit Firm Field Hidden]
A13 -->|External| A15[Select Audit Firm from Master (Mandatory)]

A14 --> A16
A15 --> A16

A16{Requested By Selected}
A16 -->|No| A17[Skip Request Details]
A16 -->|Yes| A18[Select Requested By User(s)]
A18 --> A19[Select Department(s) (Mandatory)]
A19 --> A20[Select Request Date (Mandatory)]
A20 --> A21[Attach File Optional]

A17 --> A22
A21 --> A22

A22[Click Add New to Add Team Members]
A22 --> A23[Select Team Members + Assign Roles]
A23 --> A24[Submit Team Modal]
A24 --> A25[Submit Engagement Form]

A25 --> A26{Mandatory Fields Filled}
A26 -->|No| A27[Show Validation Errors + Highlight Fields]
A26 -->|Yes| A28[Engagement Created Successfully]
A28 --> A29[Redirect to Engagement List]
A29 --> A30[New Engagement Visible on Top]
A30 --> A31[Open Engagement]

A31 --> Z([End])

```
