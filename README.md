flowchart TD
  A[User opens app] --> B[Select Module]
  B --> C[Create New Observation]
  C --> D[Assign to Process Owner]
  D --> E[Process Owner updates Action Plan]
  E --> F[Auditor reviews update]
  F --> G{Accepted?}
  G -- Yes --> H[Close Observation]
  G -- No --> I[Send back for Rework]
  I --> E
