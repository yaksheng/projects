# Cloud Query Pipeline: Documentation and Postmortem

This directory documents a deployed cloud query pipeline and a postmortem for a zero results incident encountered during operation.

## Incident Summary

The investigation identified three causes:

1. Partition discovery failed under storage listing restrictions.
2. A dataset partition identifier was incorrect.
3. Result filtering was too restrictive.

The correction used explicit partition registration, corrected configuration, and broader filtering.

## Documentation

- [Pipeline documentation](cloud-data-pipeline-documentation.md)
- [Incident postmortem](postmortem-0-results-issue.md)
- [Technical takeaways](takeaways.md)

The documentation covers the deployed pipeline, the incident investigation, and the resulting engineering changes.

## License

This project documentation is covered by the repository [MIT License](../../LICENSE).
