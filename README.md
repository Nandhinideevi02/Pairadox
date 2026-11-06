# PAIRADOX
### AI-Powered Collaborative Experiment Investigation Using Switch and Codex

We developed an AI-powered collaborative investigation workflow that connects a team communication platform with an AI coding agent through **Switch**. It enables teams to investigate existing software and machine learning projects through natural-language requests, allowing an AI agent to inspect project files, analyze implementation details, examine experimental results, and report findings with supporting evidence.

Built for the **Flip the Switch Hackathon** by WeMakeDevs × DevTools Academy.

---

## Problem Statement

Machine learning projects often involve multiple components, including model architectures, training pipelines, evaluation scripts, datasets, and experimental reports.
Understanding why a model performs poorly or identifying issues in an existing implementation can require significant manual investigation.
Teams may spend considerable time navigating project files, comparing experimental results, and tracing implementation logic.
We explored how AI agents can make this investigation process more collaborative, structured, and efficient.

## Our Solution

In this workflow we connect team communication with an AI-powered investigation.

Instead of manually inspecting every file, team members can submit investigation requests through a connected chat platform.

Through Switch, requests are routed to an AI coding agent powered by Codex, which can inspect the accessible project repository and return structured findings.

The workflow emphasizes:
1. Natural-language investigation requests.
2. AI-assisted code and experiment analysis.
3. Evidence-backed findings with relevant file references.
4. Clear separation between confirmed observations and hypotheses.
5. Human review before implementation changes.

## Architecture

The workflow consists of the following components:

1. **Telegram** – Team communication interface for submitting investigation requests and receiving responses.
2. **Switch** – Orchestration layer connecting the communication platform with the AI agent.
3. **Codex** – AI coding agent responsible for inspecting project files and investigating technical questions.
4. **EdgeRetina** – Existing machine learning project used as the investigation target.
5. **Human Review** – Team members evaluate findings and decide whether further investigation or code changes are required.

### Workflow

```text
       Team Members
             |
             v
         Telegram
             |
             v
           Switch
        (Orchestration)
             |
             v
        Codex Agent
             |
             v
     EdgeRetina Project
             |
             v
   Investigation & Analysis
             |
             v
    Evidence-Based Report
             |
             v
       Human Review
```

## Investigation Use Cases

We used the telegram group chat and investigated an existing federated learning project, EdgeRetina.

The following are examples of investigations conducted through the AI agent.

### 1. Severe Diabetic Retinopathy Recall Investigation

**Question:** Why does the federated learning model fail to correctly identify Severe Diabetic Retinopathy cases?

The agent inspected saved evaluation reports, class distributions, training configuration, and model-related implementation details.

Key reported findings:
- Severe DR had zero recall in the saved federated evaluation.
- The test set contained only 29 Severe DR samples.
- The starting global checkpoint also showed zero Severe DR recall.
- The federated training configuration used categorical cross-entropy without class weighting.

The investigation identified possible contributing factors, including class imbalance and the existing model's decision boundaries.

### 2. Centralized vs Federated Learning Comparison

**Question:** How does the federated model compare with the centralized model?

The agent inspected saved evaluation reports and compared their metrics.

| Metric | Centralized | Federated |
|---|---:|---:|
| Accuracy | 0.5109 | 0.6709 |
| Macro F1-score | 0.3380 | 0.4008 |
| Weighted F1-score | 0.5347 | 0.6348 |
| Macro Recall | 0.3598 | 0.4032 |
| QWK | 0.4889 | 0.6867 |

**Important observation:** Although the saved federated evaluation showed improvements in aggregate metrics, Severe DR recall remained zero. The comparison also had experimental limitations because the training procedures were not identical.

### 3. Federated Averaging Implementation Analysis

**Question:** How is Federated Averaging implemented, and are there potential issues in the training workflow?

The agent inspected the server-side training process and FedAvg implementation.

Key reported findings:
- The project uses four simulated clients.
- Local model updates are aggregated using sample-count-based weights.
- The recorded training configuration used five federated rounds.
- The implementation's FedAvg arithmetic was structurally consistent with weighted averaging.
- The investigation identified areas for further validation, including update diagnostics, input validation, and per-round evaluation monitoring.

These investigations demonstrate how an AI agent can help developers understand existing implementations and identify areas requiring further experimentation.

*Note: The investigation findings are based on the saved project artifacts and agent inspection. They are not claims of independent clinical validation or proof of causation.*

## Technology Stack

| Component | Technology |
|---|---|
| Communication | Telegram |
| Orchestration | Switch |
| AI Coding Agent | OpenAI Codex |
| Containerization | Docker |
| Investigation Target | EdgeRetina |
| Version Control | Git and GitHub |

## Safety and Human Oversight

This Workflow follows a human-reviewed investigation approach.

- Investigation requests focus on inspecting existing project files and reports.
- Findings should include supporting file references wherever available.
- Confirmed observations are distinguished from possible explanations.
- Code modifications and experimental changes require human review.
- Credentials, private datasets, and sensitive project artifacts should not be exposed in public documentation.

The workflow is intended to assist developers, not replace their technical judgment.

## Setup and Execution

The following components are required:

- Docker Desktop
- Switch
- Telegram
- Codex agent configuration
- Access to the project repository being investigated

### General Workflow

1. Install and configure Docker Desktop.
2. Set up and launch Switch.
3. Configure the Telegram integration.
4. Connect the Codex agent through Switch.
5. Provide the agent with access to the intended project repository.
6. Submit an investigation request through Telegram.
7. Review the agent's response and supporting evidence.

**TODO:** Add the exact installation instructions, configuration steps, and verified commands used by the team.

## 🎥 Demo

**Project Demonstration:** TODO – (Add demo video link.)

The demonstration will showcase:
- Docker and Switch setup.
- Telegram integration.
- Codex agent connection.
- Investigation request submitted through Telegram.
- Switch orchestration and agent execution.
- Evidence-based investigation response.

## Limitations and Future Improvements
- The quality of AI-generated findings depends on the accessibility and quality of the underlying project files.
- AI-generated analysis may contain inaccuracies and requires human verification.
- Experimental observations should be validated through controlled experiments before drawing conclusions.
- The current workflow focuses on investigation and analysis; automated implementation and validation of suggested improvements are areas for future development.

## About the Team

**Team Name:** PAIRADOX

- **Nandhini Deevi R** 
- **Lingeshwar G** 

**Hackathon:** Flip the Switch Hackathon  
**Organized by:** WeMakeDevs × DevTools Academy

---

*PAIRADOX — Turning team conversations into structured technical investigations.*
