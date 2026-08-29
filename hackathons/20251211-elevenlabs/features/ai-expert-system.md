# AI Integration

SourceVoice combines model APIs to answer manufacturing questions, draft negotiation prompts, structure cost considerations, and request visual references.

## Prototype Flow

1. Collect the user's question, language, and part context.
2. Include recent conversation state in the model request.
3. Ask for a structured response containing assumptions and negotiation considerations.
4. Optionally request an image from the configured image model.
5. Present the result for user review.

## Implementation Notes

- Claude and Gemini are accessed through server-side integration code.
- Provider credentials are supplied through environment variables.
- Zustand maintains client-side conversation and feature state.
- Provider and validation errors should be surfaced to the interface.

## Limitations

The prototype does not establish a curated manufacturing knowledge base, model tuning, continuous learning, accuracy benchmarks, or validated cost prediction. Responses can be incomplete or wrong and require review against drawings, specifications, supplier data, and engineering judgment.

## Future Work

- Add source citations and assumption tracking.
- Define evaluation sets with manufacturing specialists.
- Add uncertainty and refusal behavior for insufficient inputs.
- Record model and prompt versions for reproducibility.

[Back to overview](../README.md)
