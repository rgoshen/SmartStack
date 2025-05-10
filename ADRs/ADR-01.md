# ADR-001: Task Processing Architecture

## Status:

Proposed

## Context:

Tasks come from multiple sources but need unified processing
AI processing may fail and need retry logic
System needs to track processing status

## Decision:

Use message queue pattern with AWS SQS for async processing
Implement adapter pattern for queue abstraction (allows future replacement)
Track AI processing status with defined states: PENDING → PROCESSING → COMPLETED/FAILED/NEEDS_REVIEW
Allow maximum 3 retry attempts before manual intervention

## Consequences:

(+) Resilient to processing failures
(+) Can scale processing independently
(+) Queue implementation can be swapped
(-) Additional AWS service dependency
