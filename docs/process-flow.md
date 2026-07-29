# Process Flow

## Monthly operational flow

```mermaid
flowchart TD
  A[Select company and billing month] --> B[Import one or more source workbooks]
  B --> C[Map fields and normalize identifiers]
  C --> D[Complete common fields in bulk when needed]
  D --> E[Review inline data and validation dashboard]
  E --> F{Critical issues remain?}
  F -- Yes --> G[Correct source data or allowed formatting issues]
  G --> E
  F -- No --> H[Preview insurer-specific layout]
  H --> I[Export layout workbook]
  I --> J[Load reconciliation sources]
  J --> K[Compare records and invoice totals]
  K --> L[Review divergences and exceptions]
  L --> M[Mark monthly checklist complete]
```

## Workflow modules

| Module | User objective | Main output |
| --- | --- | --- |
| Data | Import and maintain the monthly insured-member list. | Normalized, editable working data. |
| Validation | Identify issues before delivery. | Record- and field-level issue list. |
| Layout | Create the required workbook. | Validated spreadsheet export. |
| Reconciliation | Verify source consistency and invoice totals. | Summary and discrepancy reports. |
| Companies | Maintain reusable operational parameters. | Calculation and exception settings. |
| Checklist | Track closure by billing month. | Completion log for the cycle. |

## Control principles

1. Normalize identifiers at every entry and comparison point.
2. Keep automatic corrections limited to safe formatting fixes.
3. Preserve evidence: flag data instead of silently deleting records.
4. Validate before export, not only after a file has been sent.
5. Keep defaults recoverable and company exceptions explicit.
