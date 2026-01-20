flowchart TD
  A[Start] --> B[Login]
  B --> C{Valid User?}
  C -- Yes --> D[Dashboard]
  C -- No --> E[Error Message
