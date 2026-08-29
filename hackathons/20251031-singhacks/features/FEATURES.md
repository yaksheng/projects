# Prototype Feature Reference

This document separates the demonstrated interaction model from production features that would require insurer integrations, security review, and operational validation.

## Demonstrated Prototype Scope

### Conversational Discovery

- Collect destination, duration, planned activities, and coverage questions.
- Present plain-language coverage explanations.
- Preserve conversation context during the demonstration.

### Multimodal Intake

- Represent text, voice, image, and document input in the workflow.
- Convert supported input into structured fields for review.
- Identify missing claim information before handoff.

### Policy and Claim Flows

- Show example policy options and confirmation states.
- Walk through claim details and supporting-document collection.
- Simulate payment, policy issuance, claim review, and settlement states.

Prices, coverage terms, eligibility rules, and payout examples are illustrative and are not insurance products or validated business rules.

## Proposed Production Capabilities

The following would require future implementation and validation:

- Insurer product, pricing, underwriting, policy, and claim APIs
- Identity verification, authentication, authorization, and consent records
- Payment processing through an approved provider
- Secure document storage, malware scanning, retention, and deletion
- Human review and escalation for regulated or ambiguous decisions
- Monitoring, analytics, audit logging, accessibility testing, and incident response
- Mobile applications, offline behavior, notifications, subscriptions, and administration tools

No certification, regulatory conformity, security audit, deployment scale, processing time, model accuracy, or business outcome is claimed for the prototype.

## Evaluation

Candidate evaluation measures are task completion, coverage comprehension, claim-intake completeness, accessibility against a named standard, and the frequency and reason for human escalation. Results should only be reported after a documented evaluation.

## Related Documentation

- [Feature summary](README.md)
- [Architecture](../architecture/ARCHITECTURE.md)
- [User journeys](../user-journey/README.md)
- [Demo flow](../demo/README.md)
- [Evaluation framework](../impact/README.md)

[Back to project overview](../README.md)
