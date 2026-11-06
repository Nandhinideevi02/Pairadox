# System Architecture of our workflow

## Overview

Our workflow is a collaborative AI-powered investigation that connects a team communication platform with an AI coding agent through Switch.

The system allows team members to submit technical investigation requests through Telegram. Switch acts as the orchestration layer and connects these requests to Codex, which investigates the accessible project repository and returns findings.

The workflow was demonstrated using EdgeRetina, an existing federated learning project.

## System Components

### 1. Telegram – Communication Interface

Telegram provides the interface through which team members communicate with the AI agent.

Team members can:
- Submit technical investigation questions.
- Request code and experiment analysis.
- Receive investigation reports.
- Discuss findings collaboratively.

### Switch – Orchestration Layer

Switch is an opensource infrastructure that connects the communication platform with the AI agent.

Its role in the workflow is to route incoming requests and coordinate communication between Telegram and the connected agent.

### Codex – AI Coding Agent

Codex performs the technical investigation.

Depending on repository access and the request, it can:
- Inspect source code.
- Understand project architecture.
- Examine configuration files.
- Analyze saved experimental results.
- Identify potential implementation issues.
- Generate structured investigation reports.

### EdgeRetina – Investigation Target

EdgeRetina is the existing machine learning project used to demonstrate our workflow.

It focuses on privacy-preserving diabetic retinopathy classification using federated learning and differential privacy.

### Human Review

Team members review the agent's findings, verify supporting evidence, and decide whether further investigation or implementation changes are necessary.

## Architecture Diagram

<img width="3792" height="248" alt="image" src="https://github.com/user-attachments/assets/d5b25c51-a4d6-4d6c-a6d4-1dd35396e67b" />

## Request Processing Flow

1. A team member submits a natural-language investigation request through Telegram.
2. Switch receives and routes the request to the connected Codex agent.
3. Codex accesses the configured project repository.
4. The agent inspects relevant source files, configurations, and saved reports.
5. The agent prepares findings with supporting evidence where available.
6. The response is returned to the Telegram group.
7. Team members review the findings and determine the next action.

## Design Considerations

- Natural-language interaction for easier collaboration.
- Evidence-based technical investigation.
- Separation of confirmed observations and hypotheses.
- Human oversight before implementation changes.
- No assumption that an AI-generated finding is automatically correct.

## Scope

The demonstrated workflow focuses on AI-assisted technical investigation and analysis. 
Automated implementation, experimentation, and validation of proposed improvements are not claimed as completed capabilities of the current demonstration.
