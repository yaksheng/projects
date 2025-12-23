# API Design

SourceVoice's API layer provides a comprehensive set of endpoints for voice processing, AI interaction, and negotiation tools, following RESTful principles and modern API design best practices.

## API Overview

### Base URL
All API endpoints are prefixed with `/api/` when running the application locally or deployed.

### Authentication
- API keys for external services are stored as environment variables
- No authentication required for client-side API calls within the application
- Rate limiting implemented for external API integrations

### Response Format
All API responses follow a consistent JSON format with success status, data field, and error field.

Error responses include error code and message fields.

## API Endpoints

### 1. Chat API

**Endpoint**: `POST /api/chat`

**Description**: Processes user input and generates AI responses using Claude and Gemini APIs.

**Request Body**: Contains messages array, user input, language, and context information.

**Response**: Includes conversational response, cost breakdown, visualization URL, and negotiation tips.

### 2. Text-to-Speech API

**Endpoint**: `POST /api/tts`

**Description**: Converts text to speech using ElevenLabs API.

**Request Body**: Contains text, language, voice ID, and voice settings.

**Response**:

- **Success**: Audio blob (binary data) in MP3 format
- **Error**: JSON error object

### 3. Speech-to-Text API

**Endpoint**: `POST /api/stt`

**Description**: Converts speech to text using Web Speech API.

**Request Body**: Multipart form data containing audio file and language.

**Response**: Includes transcript, confidence score, and language.

### 4. Image Generation API

**Endpoint**: `POST /api/generate-image`

**Description**: Generates mold visualizations using Gemini Image API.

**Request Body**: Contains prompt, specifications, and style.

**Response**: Includes image URL, prompt, and generation time.

## API Implementation

### Route Handlers

All API endpoints are implemented using Next.js Route Handlers with request validation, error handling, and integration with AI services.

### Integration Layer

API endpoints integrate with external services through a dedicated integration layer that handles API client creation and request processing.

### Error Handling

Comprehensive error handling across all API endpoints with error codes for validation errors, AI API errors, audio processing errors, image generation errors, and internal server errors.

## Performance Optimization

- **Caching**: Frequently used responses cached for faster access
- **Batching**: AI API calls batched when possible
- **Compression**: Audio and image data compressed for efficient transfer
- **Edge Deployment**: Next.js edge functions for low-latency processing

## Rate Limiting

- **Claude API**: 5 requests per second
- **Gemini API**: 10 requests per second
- **ElevenLabs API**: 10 requests per minute
- **Web Speech API**: No explicit limits

## Security Measures

- **Input Validation**: All requests validated with Zod schemas
- **API Key Protection**: External API keys stored as environment variables
- **CORS Configuration**: Restricted to application domains
- **Data Sanitization**: All user inputs sanitized to prevent injection attacks
- **Audio Processing**: Local processing where possible to protect sensitive data

---

[Back to Overview](../README.md)