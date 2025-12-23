# System Architecture

## High-Level Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                       Client Layer                              │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────────┐ │
│  │  Web App    │  │  Mobile App │  │  Conversational Interface│ │
│  │  (Next.js)  │  │  (React     │  │  (Multi-modal)          │ │
│  │             │  │  Native)    │  │  - Text/Voice/Image     │ │
│  └──────┬──────┘  └──────┬──────┘  └──────────────┬────────────┘ │
│         │                │                        │             │
└─────────┼────────────────┼────────────────────────┼─────────────┘
          │                │                        │
┌─────────▼────────────────▼────────────────────────▼─────────────┐
│                       API Gateway                               │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────┐ │
│  │  Auth       │  │  Rate       │  │  API        │  │  Request│ │
│  │  Middleware │  │  Limiting   │  │  Routing    │  │  Logging│ │
│  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘  └────┬────┘ │
│         │                │                │               │     │
└─────────┼────────────────┼────────────────┼───────────────┼─────┘
          │                │                │               │
┌─────────▼────────────────▼────────────────▼───────────────▼─────┐
│                    Core Services Layer                          │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────┐ │
│  │  Auth       │  │  Policy     │  │  Claims     │  │  User   │ │
│  │  Service    │  │  Service    │  │  Service    │  │  Service│ │
│  │  (FastAPI)  │  │  (FastAPI)  │  │  (FastAPI)  │  │  (FastAPI)│ │
│  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘  └────┬────┘ │
│         │                │                │               │     │
└─────────┼────────────────┼────────────────┼───────────────┼─────┘
          │                │                │               │
┌─────────▼────────────────▼────────────────▼───────────────▼─────┐
│                  Multi-Agent Orchestration                     │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────┐ │
│  │  CrewAI     │  │  Sales      │  │  Claims     │  │  Support│ │
│  │  Orchestrator│  │  Agent      │  │  Agent      │  │  Agent  │ │
│  │  (Python)   │  │  (GPT-4)    │  │  (GPT-4)    │  │  (GPT-4)│ │
│  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘  └────┬────┘ │
│         │                │                │               │     │
└─────────┼────────────────┼────────────────┼───────────────┼─────┘
          │                │                │               │
┌─────────▼────────────────▼────────────────▼───────────────▼─────┐
│                    Data & Integration Layer                    │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────┐ │
│  │  PostgreSQL │  │  Redis      │  │  Stripe     │  │  External│ │
│  │  (Supabase) │  │  (Cache)    │  │  (Payment)  │  │  APIs    │ │
│  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘  └────┬────┘ │
│         │                │                │               │     │
└─────────┼────────────────┼────────────────┼───────────────┼─────┘
          │                │                │               │
┌─────────▼────────────────▼────────────────▼───────────────▼─────┐
│                    Monitoring & Analytics                      │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────┐ │
│  │  New Relic  │  │  CloudWatch │  │  Mixpanel   │  │  Sentry  │ │
│  │  (APM)      │  │  (Logging)  │  │  (Analytics)│  │  (Errors)│ │
│  └─────────────┘  └─────────────┘  └─────────────┘  └─────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

## Component Details

### Client Layer

#### Web Application
- **Framework**: Next.js with React
- **Deployment**: Vercel
- **Features**: Responsive design, PWA capabilities, real-time updates

#### Mobile Application
- **Framework**: React Native
- **Platforms**: iOS and Android
- **Features**: Offline support, push notifications, biometric authentication

#### Conversational Interface
- **Multi-modal Support**: Text, voice, image, document
- **Speech Processing**: Whisper API for speech-to-text, ElevenLabs for text-to-speech
- **OCR**: Tesseract and Google Vision API for document processing
- **Image Recognition**: OpenCV and CLIP for visual analysis

### API Gateway

- **Technology**: FastAPI with Kong API Gateway
- **Authentication**: JWT tokens with refresh tokens
- **Authorization**: Role-based access control (RBAC)
- **Rate Limiting**: Per-user and per-endpoint limits
- **Logging**: Structured logging with ELK stack

### Core Services Layer

#### Auth Service
- **JWT Authentication**: HS256 algorithm for token signing
- **User Management**: Registration, login, password reset
- **Social Login**: Google, Facebook, Apple integration
- **Two-Factor Authentication**: SMS and TOTP support

#### Policy Service
- **Policy Generation**: Dynamic policy creation based on user inputs
- **Pricing Engine**: Real-time price calculation
- **Policy Management**: CRUD operations for policies
- **Renewal System**: Automated policy renewals

#### Claims Service
- **Claim Filing**: Multi-modal claim submission
- **Validation Engine**: AI-powered claim validation
- **Payment Processing**: Claim settlement via Stripe
- **Status Tracking**: Real-time claim status updates

#### User Service
- **Profile Management**: User preferences and settings
- **Notification System**: Email, SMS, push notifications
- **Travel History**: Tracking of past trips and policies

### Multi-Agent Orchestration

#### CrewAI Orchestrator
- **Agent Management**: Registration, deployment, and scaling of agents
- **Task Assignment**: Intelligent routing of user queries to appropriate agents
- **Conversation Management**: Maintaining context across multi-agent interactions
- **Fallback Mechanism**: Human agent escalation when needed

#### Sales Agent
- **Intent Recognition**: Identify sales opportunities
- **Product Knowledge**: Comprehensive policy information
- **Cross-selling**: Recommend complementary products
- **Conversion Optimization**: Maximize policy sales

#### Claims Agent
- **Claim Classification**: Categorize claims by type
- **Document Processing**: Extract information from claims documents
- **Policy Verification**: Check claim eligibility against policy terms
- **Status Updates**: Keep users informed about claim progress

#### Support Agent
- **Issue Resolution**: Troubleshoot common problems
- **Knowledge Base**: Access to FAQs and troubleshooting guides
- **Escalation**: Route complex issues to human agents
- **Feedback Collection**: Gather user feedback

### Data & Integration Layer

#### Database
- **Primary DB**: PostgreSQL with Supabase for real-time capabilities
- **ORM**: SQLAlchemy for Python services
- **Schema Design**: Normalized relational schema with JSONB for flexible data
- **Backup**: Automated daily backups with point-in-time recovery

#### Cache
- **Technology**: Redis
- **Use Cases**: Session management, API response caching, rate limiting
- **Eviction Policy**: Least Recently Used (LRU)

#### Payment Gateway
- **Provider**: Stripe
- **Features**: One-click payments, subscription support, fraud detection
- **Integration**: Direct API integration with webhooks

#### External APIs
- **Flight Data**: Amadeus, Skyscanner for flight status and delays
- **Weather**: OpenWeatherMap for destination weather information
- **Geolocation**: Google Maps API for location services
- **Travel Advisories**: Government travel advisory APIs

### Monitoring & Analytics

#### Application Performance Monitoring
- **Tool**: New Relic
- **Metrics**: Response times, error rates, throughput
- **Alerts**: Configurable thresholds for critical metrics

#### Logging
- **Tool**: AWS CloudWatch with ELK stack
- **Log Types**: Application logs, API logs, error logs
- **Retention**: 90-day log retention with archiving

#### Analytics
- **Tool**: Mixpanel
- **Events**: User interactions, conversion funnels, retention rates
- **Reports**: Custom dashboards for business metrics

#### Error Tracking
- **Tool**: Sentry
- **Error Monitoring**: Real-time error tracking and alerting
- **Source Maps**: Detailed error information with source code context

## Security Architecture

### Authentication & Authorization
- **JWT Tokens**: Short-lived access tokens (15 minutes)
- **Refresh Tokens**: Long-lived tokens stored in HTTP-only cookies
- **Role-Based Access Control**: Fine-grained permissions for different user types
- **Password Security**: bcrypt hashing with 12 rounds of iteration

### Data Protection
- **Encryption**: AES-256 encryption for sensitive data at rest
- **Transport Security**: TLS 1.3 for all data in transit
- **Data Minimization**: Only collect necessary user information
- **Privacy Compliance**: GDPR, CCPA, and PDPA compliant

### Network Security
- **Firewalls**: WAF protection at API gateway level
- **DDoS Protection**: Cloudflare for DDoS mitigation
- **Access Control**: VPC with private subnets for backend services
- **Penetration Testing**: Regular security audits and testing

## Scalability Architecture

### Horizontal Scaling
- **Containerization**: Docker containers for all services
- **Orchestration**: Kubernetes for container management
- **Auto-scaling**: Based on CPU and memory utilization
- **Load Balancing**: Round-robin load balancing across instances

### Database Scaling
- **Read Replicas**: PostgreSQL read replicas for read-heavy operations
- **Sharding**: Horizontal sharding for large datasets
- **Caching**: Redis cache to reduce database load

### API Scaling
- **Rate Limiting**: Prevent abuse and ensure fair usage
- **Caching**: API response caching with Redis
- **Asynchronous Processing**: Celery for background tasks

## Deployment Architecture

### Development Environment
- **Local Setup**: Docker Compose for local development
- **CI/CD**: GitHub Actions for automated testing and deployment
- **Testing**: Unit tests, integration tests, end-to-end tests

### Production Environment
- **Cloud Provider**: AWS
- **Services**: ECS for container deployment, RDS for PostgreSQL, ElastiCache for Redis
- **Monitoring**: CloudWatch, New Relic, Sentry
- **Backups**: Automated backups with AWS Backup

### Disaster Recovery
- **Multi-AZ Deployment**: High availability across multiple availability zones
- **Cross-Region Replication**: Data replication to secondary region
- **Recovery Time Objective (RTO)**: 30 minutes
- **Recovery Point Objective (RPO)**: 1 hour

## Technology Stack

| Layer | Technology | Purpose |
|-------|------------|---------|
| Frontend | Next.js, React | Web application |
| Mobile | React Native | Mobile application |
| Backend | FastAPI, Python | API development |
| Database | PostgreSQL, Supabase | Data persistence |
| Cache | Redis | Performance optimization |
| AI Agents | CrewAI, GPT-4 | Conversational AI |
| Speech | Whisper, ElevenLabs | Voice processing |
| OCR | Tesseract, Google Vision | Document processing |
| Payment | Stripe | Payment processing |
| Deployment | Docker, Kubernetes, Vercel | Application deployment |
| Monitoring | New Relic, CloudWatch, Sentry | Performance and error monitoring |
| Analytics | Mixpanel | User analytics |

## Integration Points

### Internal Integration
- **API Contracts**: OpenAPI/Swagger documentation for all services
- **Event-Driven Architecture**: RabbitMQ for inter-service communication
- **Service Discovery**: Consul for dynamic service registration

### External Integration
- **Webhooks**: Real-time notifications from external services
- **API Keys**: Secure authentication with external APIs
- **OAuth 2.0**: Authorization for third-party API access

## Future Architecture Improvements

- **Serverless Architecture**: Migrate to AWS Lambda for cost optimization
- **GraphQL API**: Add GraphQL support for more flexible client queries
- **Edge Computing**: Deploy services closer to users with CDN edge locations
- **AI Model Optimization**: Fine-tune models for better performance and cost efficiency
- **Blockchain Integration**: Smart contracts for policy automation and claims processing

## Architecture Decision Records (ADRs)

For detailed architecture decisions, please refer to the [ADR directory](adr/).