# Backend Design

The backend design uses Convex to organize product briefs, design generation requests, refinements, files, and order state.

## Data Model

| Record | Responsibility |
| --- | --- |
| Document | Store an uploaded product brief |
| Generation | Track a design generation request |
| Design file | Associate outputs with a generation |
| Refinement | Record requested design changes |
| Order | Represent the manufacturing order workflow |
| User state | Track the current step in the experience |

## Functions

- Create and retrieve design generation requests
- Record refinement requests
- Associate files with a generation
- Save and retrieve workflow state

## Integration Points

The design separates file storage, AI generation, user state, and order processing so each service can be developed and evaluated independently.
