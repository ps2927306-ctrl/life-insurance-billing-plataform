# Business Rules

## Data integrity rules

### Identifier normalization

National identifiers are treated as strings. Imported values are stripped to digits and, when the source length is plausibly shortened by spreadsheet number formatting, left-padded to the expected length. The final export explicitly writes the identifier as text to preserve leading zeros.

Values outside the expected length range are not guessed; they remain visible for user review.

### Safe automatic correction

The automatic correction action is intentionally limited to non-financial formatting changes: identifier normalization, name whitespace cleanup, and consistent presentation. It does not automatically change salary, insured capital, premium, dates, or other financial data.

## Record validation

Each record is checked as data is imported or edited. A critical issue prevents layout export; an informational or optional-field warning remains visible without blocking the workflow.

Typical checks include:

- identifier format and duplicate identifier detection;
- required name and whitespace quality;
- valid birth date and configured age range;
- duplicate enrollment number, with configurable company-level exceptions;
- required admission date when applicable;
- capital minimum and maximum thresholds;
- required policyholder or plan fields for applicable configurations.

## Capital and premium calculation

| Model | Rule |
| --- | --- |
| Uniform | A fixed insured-capital amount per eligible record. |
| Salary multiple | Capital calculated from salary multiplied by a configured factor. |
| Role-based tier | Capital and premium selected from a configured tier for the employee role. |

Company-level floors, ceilings, and rate parameters are applied where configured. Values remain subject to validation before export.

## Layout generation

The platform maps normalized internal data to insurer-specific column structures. The export is blocked if any record has a critical validation error. Exports preserve text identifiers and may produce separate files for configured sub-invoice groups.

## Reconciliation

Reconciliation compares up to three sources: an imported working base, a client base, and an insurer base. Matching primarily uses normalized identifier plus enrollment number. A controlled name-based fallback may surface likely matches for review when identifiers conflict.

The output categorizes matched records, new records, exits or exclusions, missing records by source, and field-level divergences. Exclusion interpretation is configurable because source layouts may communicate status through different fields and labels.

## Invoice check

The reconciliation step compares total covered lives, insured capital, and premium against invoice values entered by the analyst. A small monetary tolerance can be configured to avoid false positives caused by rounding.

## Historical cycle comparison

The comparison baseline is the latest archived competency earlier than the competency currently being processed; it is not necessarily the immediately preceding calendar month. This preserves a meaningful comparison even when a month is skipped or a cycle is reprocessed out of sequence.

Records are matched primarily by normalized identifier, with a controlled name-based fallback for review. The output classifies differences into:

- **Registration:** name, date of birth, or enrollment number changed;
- **Salary:** salary changed between archived and current data;
- **Insured capital:** insured-capital amount changed;
- **Premium:** premium amount changed.

Salary, capital, and premium are compared only when both records contain a value. Registration fields remain relevant even when one source is empty, because those gaps represent a data-quality issue rather than a financial comparison.

## Monthly checklist

Checklist completion is recorded by company and billing month. The status captures the completion date and can be exported for operational follow-up.
