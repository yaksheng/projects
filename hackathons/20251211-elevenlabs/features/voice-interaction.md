# Voice Interaction

SourceVoice's voice-first interface enables natural, conversational interaction with the AI assistant, making it accessible and efficient for users to communicate their needs.

## Core Capabilities

### Speech-to-Text (STT)
- **Real-time transcription** of user speech using Web Speech API
- **Language support** for both English and Mandarin
- **Audio processing** with MediaRecorder API for optimal quality
- **Background noise filtering** to improve transcription accuracy

### Text-to-Speech (TTS)
- **Natural-sounding voices** powered by ElevenLabs' advanced TTS technology
- **Bilingual support** with appropriate accents for English and Mandarin
- **Seamless integration** with conversation flow
- **Volume and speed control** for user preference

### Voice Command Recognition
- **Context-aware responses** based on conversation history
- **Intelligent fallback** to text input if voice recognition fails
- **Processing indicators** to keep users informed of system status

## Technical Implementation

### STT Workflow

### TTS Integration

### State Management

The voice interaction system uses a finite state machine pattern:
- **IDLE**: Ready for user input
- **LISTENING**: Actively recording speech
- **PROCESSING**: Converting speech to text and generating response
- **SPEAKING**: Playing back TTS response

## User Benefits

- **Hands-free operation**: Users can focus on their work while communicating
- **Faster input**: Natural speech is quicker than typing for complex requests
- **Accessibility**: Enables use by those with typing difficulties
- **Intuitive interface**: Familiar conversation patterns reduce learning curve
- **Multitasking support**: Allows users to reference other materials while interacting

## Performance Metrics

- **STT Accuracy**: ~95% for clear speech in optimal conditions
- **Response Time**: <2 seconds for simple queries, <5 seconds for complex analyses
- **TTS Quality**: Human-like naturalness with ElevenLabs voices
- **Error Rate**: <3% for voice command recognition

## User Experience

The voice interface is designed to be:
- **Responsive**: Visual feedback for all voice states
- **Forgiving**: Clear error messages and retry options
- **Contextual**: Maintains conversation flow across voice/text inputs
- **Accessible**: Follows WCAG guidelines for inclusive design

---

[Back to Overview](../README.md)