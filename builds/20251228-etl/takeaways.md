# ETL Pipeline Takeaways

For an overview, see the project [README](README.md). The [incident postmortem](postmortem-0-results-issue.md) contains the supporting failure analysis.

## Partition Management

Storage listing restrictions prevented automatic partition discovery from finding the dataset. Explicit `ALTER TABLE ADD PARTITION` statements made partition registration independent of that listing behavior.

Operational checks should verify that:

- The configured dataset identifier exists in the target environment.
- Expected partitions are registered before queries run.
- Storage and query permissions are tested separately.

## Query Design

Partition pruning and selective projection reduce scanned data. A result limit controls returned rows but does not replace partition and column filtering for cost control.

Filtering should be introduced in observable stages. The incident showed that combining several restrictive conditions can produce an empty result without identifying which condition excluded the data. Record counts after each stage make that failure easier to diagnose.

## Failure Handling

The pipeline should stop with a specific error when prerequisites such as partition registration, dataset selection, or result storage fail. Logs should include the query identifier, selected partition, applied filters, output location, and service error without exposing credentials.

## Configuration

Dataset identifiers and available partitions vary by environment. Keep those values in environment-specific configuration and validate them before query execution rather than embedding assumptions in query logic.

## Future Work

- Add preflight checks for dataset and partition availability.
- Add tests for empty, malformed, and unexpectedly filtered result sets.
- Track scanned bytes and query failures for cost and reliability review.
- Evaluate incremental processing and additional datasets after the existing path is measured.
