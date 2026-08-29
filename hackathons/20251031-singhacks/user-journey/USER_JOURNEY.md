# Prototype User Journeys

## Policy Discovery

```mermaid
graph TD
    Start[Start conversation] --> Input{Input type}
    Input -->|Text or voice| Needs[Describe travel needs]
    Input -->|Image or document| Extract[Extract information for review]
    Extract --> Needs
    Needs --> Options[Review illustrative coverage options]
    Options --> Questions[Ask follow-up questions]
    Questions --> Handoff[Continue with an authorized insurer]
```

## Claim Intake

```mermaid
graph TD
    Start[Start claim intake] --> Details[Provide incident details]
    Details --> Documents[Attach supporting documents]
    Documents --> Review[Review and correct extracted information]
    Review --> Missing{Information complete?}
    Missing -->|No| Details
    Missing -->|Yes| Handoff[Submit to an authorized insurer]
```

## Voice Interaction

```mermaid
graph TD
    Speak[User speaks] --> STT[Speech to text]
    STT --> Review[User reviews transcript]
    Review --> Conversation[Conversation workflow]
    Conversation --> TTS[Optional text to speech]
```

## Boundaries

- The prototype demonstrates interaction and intake flows.
- Payment, policy issuance, claim decisions, settlement, account management, and analytics are not established as live integrations.
- A production journey would require authorization, consent, accessibility testing, data-protection controls, insurer review, and failure handling.

[Back to user-journey summary](README.md)
