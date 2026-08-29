# Postmortem: Cloud Pipeline Zero-Result Incident

## Summary

On December 27-28, 2025, pipeline testing returned no results despite source-data availability. The investigation identified three contributing conditions:

1. `MSCK REPAIR TABLE` could not discover partitions under the available storage-listing permissions.
2. The configured dataset partition identifier did not exist in the environment.
3. Application filtering rejected most of the retrieved records.

The incident notes record a switch to explicit partition registration, correction of the identifier, and broader domain filtering. They also record that queries subsequently returned results. This establishes recovery of the observed query path, not a general reliability or performance improvement.

## Timeline

| Time (UTC+8) | Observation or change |
| --- | --- |
| 2025-12-27 14:00 | Pipeline testing returned no results. |
| 2025-12-27 15:00 | Logs indicated that partition discovery had not added partitions. |
| 2025-12-27 17:00 | The query path was changed to explicit partition registration. |
| 2025-12-27 18:00 | The environment's available dataset identifier was identified. |
| 2025-12-27 19:00 | The configured identifier was updated. |
| 2025-12-27 20:00 | Queries returned results, but fewer than expected. |
| 2025-12-27 21:00 | Filtering was identified as the remaining constraint. |
| 2025-12-27 22:00 | Domain filtering was broadened. |
| 2025-12-28 00:31 | The tested query returned usable results. |

## Evidence

### Partition Discovery

Logs recorded warnings from `MSCK REPAIR TABLE` and showed no registered partition for the query. Explicit registration targeted the known partition path without relying on bucket-wide discovery.

### Dataset Configuration

Query-service errors indicated that the configured partition identifier was unavailable. Updating the environment-specific identifier allowed the query to address the available data.

### Filtering

One diagnostic run recorded 1,000 raw rows, of which 987 were rejected and 13 retained. This observation explained that run; it is not a general filtering rate or quality metric.

## Impact

The affected pipeline path did not ingest new content while it returned no results. The documentation does not establish data loss, a service-level availability percentage, business impact, or quantified query-cost impact.

## Changes Recorded During Investigation

- Replaced partition discovery with explicit registration for the tested dataset path.
- Updated the configured dataset identifier.
- Expanded domain matching used by the content filter.

Completion beyond the tested path, deployment scope, and regression coverage are not established by these notes.

## Recommended Follow-Up

These items are proposed and have no completion status in this repository:

- Add a preflight check for dataset and partition availability.
- Centralize environment-specific dataset configuration.
- Report counts after each filtering stage.
- Stop on partition-registration and query failures instead of continuing to filtering.
- Add an integration test with a known non-empty result.
- Record scanned bytes and query identifiers for cost investigation.

## Lessons

- Empty results can represent infrastructure or configuration failure rather than absence of data.
- Environment identifiers should be validated before query execution.
- Filtering stages need intermediate counts to make exclusion behavior observable.
- Explicit partition registration is appropriate when a known partition path is available and discovery permissions are restricted.

[Back to project overview](README.md)
