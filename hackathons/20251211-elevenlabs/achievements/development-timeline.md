# Four-Hour Development Timeline

SourceVoice was built during a four-hour hackathon on December 11, 2025 at Lorong AI. The timeline records the prototype scope rather than a longer product-development process.

| Time | Focus | Prototype work |
| --- | --- | --- |
| 0:00-0:30 | Setup | Initialized the Next.js and TypeScript project, UI components, routes, and client state. |
| 0:30-1:30 | Voice | Connected browser speech recognition, ElevenLabs text to speech, and recording/playback controls. |
| 1:30-2:30 | AI integration | Connected model APIs and established the core conversation flow for manufacturing questions. |
| 2:30-3:30 | Negotiation interface | Built the chat, voice, cost-breakdown, bilingual, and visual-reference interactions. |
| 3:30-4:00 | Demonstration | Fixed blocking issues and prepared the deployed demonstration. |

## Technical Scope

- Next.js route handlers for model and speech-service calls
- Zustand state for conversation, voice, negotiation, and visualization views
- English and Mandarin interaction paths
- Prompt-based manufacturing guidance and cost-breakdown output
- Generated visual references

## Constraints

- The project was not developed through week-long iterations or a multi-person delivery process.
- No test-coverage, load-test, security-audit, usability-study, or code-size claim is made.
- Manufacturing guidance, translations, cost estimates, and generated images were not independently benchmarked during the hackathon.
- The deployment supported demonstration, not an operational service-level commitment.

## Future Work

- Evaluate translation quality with bilingual manufacturing specialists.
- Validate cost models against documented supplier quotations.
- Add explicit uncertainty, source provenance, and human-review controls.
- Test accessibility, failure handling, privacy, and model-provider limits.
- Evaluate additional manufacturing processes only after the core workflow is validated.

[Back to overview](../README.md)
