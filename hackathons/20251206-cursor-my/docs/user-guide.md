# AI Hardware Design Platform User Guide

## Prototype Workflow

The application uses mock authentication for demonstration purposes.

1. Enter a product brief and constraints.
2. Review the generated concept and assumptions.
3. Submit a refinement request.
4. Inspect available previews and files.
5. Continue to the demonstration order-planning screen.

## Design Review

The interface supports requests concerning dimensions, component placement, materials, and features. A generated revision should be treated as a new concept artifact, not as an approved engineering change.

## Three-Dimensional Preview

The viewer supports model rotation, zoom, pan, and view reset. It is a visualization aid and does not perform tolerance, interference, structural, thermal, electrical, safety, or manufacturing analysis.

## Files

The workflow can present files labeled as STL, STEP, PCB, Gerber, bill of materials, assembly instructions, firmware, and manufacturing information. Availability and content depend on the configured generator.

Before any downstream use:

1. Confirm the requirements and assumptions.
2. Open each file in an appropriate engineering tool.
3. Run mechanical, electrical, firmware, safety, and manufacturing checks.
4. Verify components, materials, tolerances, interfaces, and regulatory requirements.
5. Obtain review from qualified engineers and the intended manufacturer.
6. Build and test physical prototypes.

Do not send unvalidated generated files directly to procurement or manufacturing.

## Order Planning

Order states in the prototype illustrate a possible workflow. They do not establish payment processing, supplier acceptance, manufacturing, shipping, or delivery integrations.

## Limitations

- Authentication is mocked.
- Generation quality and timing are not guaranteed.
- Engineering correctness, manufacturability, and safety are not automatically verified.
- Supplier, payment, fulfillment, and support services are not established.

## Related Documentation

- [Getting started](getting-started.md)
- [Architecture](architecture.md)
- [Prototype API reference](api-reference.md)

[Back to project overview](../README.md)
