# PAIRADOX
### AI-Powered Collaborative Experiment Investigation Using Switch and Codex

We developed an AI-powered collaborative investigation workflow that connects a team communication platform with an AI coding agent through **Switch**. 

It enables teams to investigate existing software and machine learning projects through natural-language requests, allowing an AI agent to inspect project files, analyze implementation details, examine experimental results, and report findings with supporting evidence.

Unlike a simple conversational interface, PAIRADOX enables an AI agent to investigate actual project files and experimental artifacts, helping teams move from questions to evidence-backed technical findings.

Built for the **Flip the Switch Hackathon** by WeMakeDevs × DevTools Academy.

---

## Problem Statement

Machine learning projects often involve multiple components, including model architectures, training pipelines, evaluation scripts, datasets, and experimental reports.

Understanding why a model performs poorly or identifying issues in an existing implementation can require significant manual investigation. Teams may spend considerable time navigating project files, comparing experimental results, and tracing implementation logic. We explored how AI agents can make this investigation process more collaborative, structured, and efficient.

## Our Solution

Our workflow connects team communication with an AI-powered investigation.

Instead of manually inspecting every file, team members can submit investigation requests through a connected chat platform.

Through Switch, requests are routed to an AI coding agent powered by Codex, which can inspect the accessible project repository and return structured findings.

The workflow emphasizes:
1. Natural-language investigation requests.
2. AI-assisted code and experiment analysis.
3. Evidence-backed findings with relevant file references.
4. Clear separation between confirmed observations and hypotheses.
5. Human review before implementation changes.

## Architecture

Our architecture consists of the following components:

1. **Telegram** – Team communication interface for submitting investigation requests and receiving responses.
2. **Switch** – Orchestration layer connecting the communication platform with the AI agent.
3. **Codex** – AI coding agent responsible for inspecting project files and investigating technical questions.
4. **EdgeRetina** – Existing machine learning project used as the investigation target.
5. **Human Review** – Team members evaluate findings and decide whether further investigation or code changes are required.

### Workflow

<img width="3966" height="164" alt="mermaid-diagram" src="https://github.com/user-attachments/assets/84461aa6-ed7b-4b74-8402-2aea929d4fcf" />

## Investigation Use Cases

We used a Telegram group chat and investigated an existing federated learning project, EdgeRetina.

The following are examples of investigations conducted through the AI agent.

### 1. Severe Diabetic Retinopathy Recall Investigation

**Question:** Why does the federated learning model fail to correctly identify Severe Diabetic Retinopathy cases?

The agent inspected saved evaluation reports, class distributions, training configuration, and model-related implementation details.

Key reported findings:
- Severe DR had zero recall in the saved federated evaluation.
- The test set contained only 29 Severe DR samples.
- The starting global checkpoint also showed zero Severe DR recall.
- The federated training configuration used categorical cross-entropy without class weighting.

The investigation identified potential contributing factors, including class imbalance, inherited model limitations, and training configuration. These remain hypotheses requiring controlled experiments for confirmation.

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

The federated model was fine-tuned from an existing global checkpoint, and the two training procedures were not identical. Therefore, the observed improvements cannot be attributed to federated learning alone.

### 3. Federated Averaging Implementation Analysis

**Question:** How is Federated Averaging implemented, and are there potential issues in the training workflow?

The agent inspected the server-side training process and FedAvg implementation.

Key reported findings:
- The project uses four simulated clients.
- Local model updates are aggregated using sample-count-based weights.
- The recorded training configuration used five federated rounds.
- The inspected implementation used sample-count-based weighting, consistent with the standard FedAvg aggregation formula on its normal execution path.
- The investigation identified areas for further validation, including update diagnostics, input validation, and per-round evaluation monitoring.

These investigations demonstrate how an AI agent can help developers understand existing implementations and identify areas requiring further experimentation.

*Note: The investigation findings are based on the saved project artifacts and agent inspection. They are not claims of independent clinical validation or proof of causation.*

## Technology Stack

| Component | Technology |
|---|---|
| Communication | Telegram |
| Orchestration | Switch |
| AI Coding Agent | Codex |
| Containerization | Docker |
| Investigation Target | EdgeRetina |
| Version Control | Git and GitHub |

## Safety and Human Oversight

This workflow follows a human-reviewed investigation approach.

- Investigation requests focus on inspecting existing project files and reports.
- Findings should include supporting file references wherever available.
- Confirmed observations are distinguished from possible explanations.
- Code modifications and experimental changes require human review.
- Credentials, private datasets, and sensitive project artifacts should not be exposed in public documentation.

The workflow is intended to assist developers, not replace their technical judgment.

## Setup and Execution

### Prerequisites

- Docker Desktop
- Switch Console
- Telegram account and bot
- Codex agent configuration
- Access to the project repository

### Configuration Steps

1. Install and launch Docker Desktop.
2. Download and launch Switch Console.
3. Configure the Telegram bot and connect it to the Switch workspace.
4. Connect and configure the Codex agent.
5. Provide the agent with access to the intended project repository.
6. Invite the agent to the Telegram group.
7. Send an investigation request through Telegram and review the agent's response.

## Demo 

Watch the demo video through this link - https://drive.google.com/file/d/1_31fGvzdJ_K9P2NRS02N8dbLmxpue8K_/view?usp=sharing

**Project Demonstration:** 

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

## Documentation

Explore the detailed project documentation:

- [System Architecture](docs/architecture.md)
- [Workflow and Execution](docs/workflow.md)
- [Technical Investigation Reports](docs/investigations.md)

## Demo and Project Evidence

All project demonstration videos and supporting screenshots are available here:

[PAIRADOX – Demo Videos and Screenshots](https://drive.google.com/drive/folders/19fdqkvn2J2sjI3KxXver09os-Vp59W85?usp=sharing)


## About the Team

**Team Name:** PAIRADOX
## Team Contributions

**Nandhini Deevi R**
- Project documentation and repository organization.
- Technical investigation and evaluation of agent-generated findings.
- README and demonstration preparation.

**Lingeshwar G**
- Switch and Telegram integration.
- Codex agent configuration.
- Project workflow demonstration.


**Hackathon:** Flip the Switch Hackathon  
**Organized by:** WeMakeDevs × DevTools Academy

---

*Turning team conversations into structured technical investigations.*
