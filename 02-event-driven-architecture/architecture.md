# Architecture

## Overview
This project implements an event-driven architecture using fully managed AWS services.
The design decouples event producers from consumers while providing reliability,
scalability, and failure isolation.

## Architecture Flow
Event Producer → SNS Topic → SQS Queue → Lambda  
Failures → SQS Dead Letter Queue (DLQ)

## Components
- **Amazon SNS**: Acts as the event broker and enables fanout.
- **Amazon SQS**: Buffers messages and decouples producers from consumers.
- **AWS Lambda**: Processes messages asynchronously without managing servers.
- **Dead Letter Queue (DLQ)**: Captures messages that fail processing repeatedly.

## Why SNS + SQS instead of direct Lambda invocation
- SNS allows a single event to be delivered to multiple consumers.
- SQS protects consumers from traffic spikes.
- SQS enables retries and DLQ handling, which direct SNS → Lambda does not provide.
- This design improves resilience and operational control.

## Exam relevance (AWS SAA)
- SNS = pub/sub and fanout
- SQS = decoupling and buffering
- Lambda = event-driven compute
- DLQ = failure isolation
