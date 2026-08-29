# AI Assistant: Architecture and Operations Notes

This directory documents a deployed Telegram based AI assistant. The system handled messaging requests, routed work across AI providers, maintained conversation context, and recorded operational data in PostgreSQL.

## Topics

- Telegram webhook request handling
- Routing between AI providers
- Conversation context management
- PostgreSQL interaction logging
- Exponential backoff for provider rate limits
- Timeout, indexing, and data cleaning work

## Documentation

- [System architecture](architecture/system-architecture.md)
- [Data flow](architecture/data-flow.md)
- [Database analysis](data/database-analysis.md)
- [Project learnings](learnings/project-learnings.md)
- [Technical challenges](learnings/technical-challenges.md)

The documentation focuses on the architecture, operational incidents, and engineering decisions behind the deployed system.

## License

See [LICENSE](LICENSE).
