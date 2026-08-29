# API Design

SourceVoice uses Next.js route handlers to keep model-provider credentials out of the browser and provide a small application-facing interface.

## Routes

### Chat

`POST /api/chat` accepts user text, language, recent conversation context, and available manufacturing inputs. It returns model-generated guidance and structured data for the interface.

### Text to Speech

`POST /api/tts` accepts text and voice settings, calls ElevenLabs, and returns audio or an error response.

### Image Generation

The image route accepts a prompt derived from reviewed part context and returns a generated visual reference.

Speech recognition uses the browser Web Speech API and does not require a server route in the documented prototype.

## Error Handling

Route handlers should distinguish invalid input, missing configuration, provider rejection, provider timeout, and unexpected failures. The client should preserve editable user input and offer text fallback when speech or model services fail.

## Security Boundaries

- Keep provider credentials in server-side environment configuration.
- Validate request shape, size, language, and supported values.
- Avoid logging sensitive negotiation content by default.
- Treat provider usage controls and request throttling as configuration that must be verified, not assumed.

The prototype did not establish user authentication, authorization, durable audit records, formal threat modeling, or security testing.

[Back to overview](../README.md)
