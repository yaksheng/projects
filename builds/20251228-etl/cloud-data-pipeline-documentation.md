# Cloud Data Pipeline

## Overview

The pipeline queries a partitioned cloud dataset, retrieves selected fields, and applies content filters. The documented incident established that partition registration, the dataset identifier, and filtering criteria directly affect whether the pipeline returns results.

## Documented Components

### Pipeline Entry Point

The pipeline coordinates cloud clients, partition registration, query execution, result retrieval, and content filtering.

### Partition Registration

The incident correction replaced automatic discovery through `MSCK REPAIR TABLE` with explicit `ALTER TABLE ADD PARTITION` statements. This avoids dependence on storage listing for the known partition path. It does not by itself establish broader reliability or performance improvements.

### Query and Filtering

Queries use a selected partition, retrieve required columns, and limit returned rows. Application filtering then evaluates the retrieved content. A `LIMIT` controls result count but does not necessarily reduce scanned data; partition and column selection are the relevant query controls.

## Required Access

The executing identity needs permissions for query execution, query-result storage, and the specific dataset operations used by partition registration. Exact policies depend on the cloud account and should be tested with least privilege.

## Observed Failure Modes

### Empty Results

Check that the expected partition is registered, the configured dataset identifier exists, and each filtering stage retains the expected records.

### Partition Registration Failure

Check query-service errors, storage location, dataset identifier, and the permissions required by the chosen registration statement.

### Permission Errors

Test dataset access and query-result storage separately. Avoid treating an empty result as proof that the source contains no matching data.

## Recommended Controls

The following are recommendations; this documentation does not establish that they are implemented:

- Validate the dataset and partition before the main query.
- Fail with a specific error when registration or query execution fails.
- Record the query identifier, selected partition, applied filter stages, and result counts.
- Track scanned bytes and execution time if exposed by the query service.
- Add integration tests for missing partitions, incorrect identifiers, empty datasets, and over-restrictive filters.
- Review query plans and cost controls before increasing result volume.

Retries, query caching, batch processing, dashboards, and application metrics are not documented as implemented pipeline behavior.

## Future Work

- Evaluate additional datasets after the existing path is measured.
- Consider incremental processing with an explicit checkpoint design.
- Add monitoring only after defining the signals, retention, and alert response.

## Related Documentation

- [Incident postmortem](postmortem-0-results-issue.md)
- [Technical takeaways](takeaways.md)
- [Project overview](README.md)
