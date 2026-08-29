# Technical Challenges and Solutions

This document outlines the key technical challenges encountered during the AI assistant project development and the solutions implemented to address them.

## 1. OpenAI 429 "Too Many Requests" Error

### Problem

The system encountered frequent OpenAI API rate limit errors with the message: "Limit 30000, Used 15488, Requested 26147". This resulted in failed API calls and poor user experience, especially during periods of high traffic.

### Root Cause

The AI assistant was making requests too frequently, exceeding OpenAI's Token Per Minute (TPM) limits. The system had no mechanism to handle these rate limits gracefully.

### Solution

Implemented exponential backoff with random jitter:

```typescript
function getExponentialBackoffDelay(retries: number, baseDelay: number = 1000, maxDelay: number = 30000): number {
  const exponentialDelay = baseDelay * Math.pow(2, retries);
  const jitter = exponentialDelay * 0.2 * (Math.random() * 2 - 1);
  return Math.max(baseDelay, Math.min(exponentialDelay + jitter, maxDelay));
}
```

**Key Features:**
- **Exponential Growth**: Delay increases exponentially with each retry (`Math.pow(2, retries)`)
- **Random Jitter**: Adds ±20% randomness to avoid synchronized retries
- **Base Delay**: 1 second initial delay
- **Max Delay**: 30 seconds upper limit to prevent excessive waiting
- **Retry Count**: 3 retry attempts before failure

### Lessons Learned

- Provider rate-limit errors need an explicit terminal failure path.
- Exponential backoff with jitter spaces retry attempts; its effect was not benchmarked here.
- Token-usage monitoring would help diagnose provider limits but is not established as implemented.
- Timeout values should be measured against actual request behavior.

## 2. "Who am I?" Response Timeout

### Problem

The AI assistant showed a typing animation when responding to "Who am I?" prompts but never delivered a response. The issue was isolated to this specific prompt, which triggered more complex processing.

### Root Cause

The GPT-4.1 model required more than 25 seconds to generate a response for this complex prompt, exceeding both:
- The AI API call timeout
- The Telegram webhook update timeout

### Solution

Increased timeouts to 60 seconds in both components:

1. **API Layer**: Increased webhook update timeout
2. **AI Gateway**: Increased API call timeout

### Lessons Learned

- Complex AI models may require longer processing times
- Setting appropriate timeouts is critical for user experience
- Different prompts may require different processing times
- Recording response times would make slow paths easier to identify.

## 3. Contaminated AI Response Search Failure

### Problem

A script to find specific contaminated AI responses returned 0 rows despite known occurrences of the target content: "Products: Gemini AppsWhy is this here..."

### Root Cause

The target response contained non-standard whitespace characters (non-breaking spaces, extra tabs) and encoding discrepancies that prevented exact string matching.

### Solution

Implemented partial pattern matching using SQL's `LIKE` operator with key phrases:

```sql
SELECT record_id, user_input, ai_output, created_at
FROM interaction_records
WHERE LOWER(ai_output) LIKE '%gemini appswhy is this here%'
   OR LOWER(ai_output) LIKE '%saved to your google account%'
ORDER BY created_at DESC;
```

**Key Features:**
- Used `LOWER()` for case-insensitive matching
- Identified unique key phrases within the contaminated response
- Avoided exact matching of problematic whitespace
- Generalized table and column names for open source publication

### Lessons Learned

- AI responses can contain unexpected whitespace or encoding issues
- Partial pattern matching is more robust for finding specific content
- Test search patterns against known samples before updating records.
- Character encoding should be considered when working with AI-generated content

## 4. OpenRouter Integration Removal

### Problem

The OpenRouter integration was no longer needed, but its removal required careful consideration of data retention and metrics continuity.

### Analysis

- Only one column was directly related to the legacy integration
- Over 99% of rows had NULL values for this column, indicating minimal usage
- Critical metrics (token counts, response lengths) were already captured through direct AI provider logging

### Solution

- Confirmed only one integration-specific column existed
- Decided to retain the column for historical data integrity
- Retained existing fields used by direct-provider records

### Lessons Learned

- Minimal usage of a feature may justify its removal
- Historical data should be preserved when possible
- Metric fields should have documented source and completeness.
- Regular review of integrations helps maintain a clean codebase

## 5. Context Management for Large Conversations

### Problem

Long conversations resulted in excessively large prompts that exceeded AI model token limits, causing API errors.

### Root Cause

The system was including full conversation history in every prompt without considering token limits.

### Solution

Implemented intelligent context truncation:

- Maintains most recent messages while removing older, less relevant content
- Preserves user facts and important context
- Adapts to different model token limits
- Keeps prompts within the configured context budget

### Lessons Learned

- Context management is critical for AI model performance
- Different models have different token limit requirements
- Balancing context retention with prompt size is essential
- User experience benefits from maintaining conversation continuity

## 6. Database Performance Optimization

### Problem

As the number of interaction records grew, database queries became slower, affecting system responsiveness.

### Root Cause

Lack of proper indexing and inefficient query patterns.

### Solution

Added indexes for the documented query paths:

- BTREE indexes on frequently queried fields (context identifiers, timestamps)
- GIN index on JSONB column for efficient JSON querying
- Composite index for targeted user context queries

### Lessons Learned

- Database performance requires ongoing monitoring
- Index impact should be confirmed with query plans and measurements.
- Query patterns should be analyzed to determine optimal indexes
- Database maintenance should be scheduled according to observed database behavior.

## 7. Environment Configuration Management

### Problem

Managing different configuration settings for development, staging, and production environments was error-prone.

### Root Cause

Configuration was scattered across multiple files with inconsistent naming conventions.

### Solution

Implemented a centralized environment loader:

- Loads environment variables from appropriate files
- Validates required configuration
- Provides consistent access to environment settings
- Handles defaults and fallbacks

### Lessons Learned

- Centralized configuration management reduces errors
- Environment-specific settings should be clearly separated
- Validation of required configurations prevents runtime errors
- Documentation of configuration options aids maintainability

## Summary

The documented changes address specific provider-limit, timeout, contaminated-data, context-size, query, and configuration problems. Broader reliability, performance, and monitoring outcomes require separate measurement.
