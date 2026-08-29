# Prototype API Reference

This reference describes the resource model used by the prototype. Exact routes and payloads should be checked against the implementation; no public or stable API contract is claimed.

## Authentication

The demonstration uses mock authentication. A production API would require authenticated identities, authorization checks, secret management, abuse controls, and an audit trail.

## Resources

### Generations

- Create a design-generation request.
- Retrieve a generation and its status.
- List generations associated with a user or project.

### Refinements

- Create a refinement request for an existing generation.
- Retrieve the request and resulting status.

### Files

- Associate an uploaded or generated file with a generation.
- Retrieve file metadata and content.
- List files for a generation.

### User State

- Retrieve the current workflow state.
- Save the current workflow state.

### Orders

- Create and retrieve demonstration order state.
- List order records associated with a user or project.

Order resources do not establish payment, supplier, manufacturing, or fulfillment integrations.

## Error Handling

A production contract should distinguish malformed input, unauthenticated access, denied access, missing resources, usage limits, generation failures, and internal failures. It should not expose provider secrets or sensitive implementation details.

## Output Validation

API success means that the workflow accepted or returned a resource. It does not certify generated hardware files. All outputs require engineering review, tool-specific checks, physical prototyping, and testing before procurement or manufacturing.

## Related Documentation

- [Architecture](architecture.md)
- [User guide](user-guide.md)
- [Getting started](getting-started.md)

[Back to project overview](../README.md)
