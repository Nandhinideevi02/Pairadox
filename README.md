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

## Setup and Reproduction Guide

This section describes how to reproduce the PAIRADOX workflow using Switch Console, Telegram, Codex, and the EdgeRetina research agent.

### Prerequisites

Ensure the following are available:

- Windows laptop or compatible environment.
- Docker Desktop.
- Switch Console (version 0.31.0 used in our implementation).
- Telegram account.
- Telegram bot created through BotFather.
- Codex agent configured and accessible through the Switch environment.
- EdgeRetina GitHub repository: https://github.com/lingeshwar18/EdgeRetina

### Set Up Switch Console

1. Install and launch Switch Console locally.
2. Run Switch Core using the default workspace.
3. Verify that the Switch environment is running.
4. Ensure the required workspace agents are available.

###  Configure Telegram Integration

1. Open Telegram and create a dedicated bot using BotFather.
2. Use the `/setprivacy` command in BotFather and disable privacy mode so the bot can process group messages.
3. Open the Messaging Apps section in Switch Console.
4. Connect the Telegram bot using its credentials.
5. Have each team member message the bot directly to register their Telegram account.
6. Add the bot to the PAIRADOX Telegram group and grant the required administrator permissions.
7. Link the Telegram group to the Switch workspace.

**Security:** Keep bot tokens and API credentials private. Never include them in the public repository.

### Configure the AI Agents

Our workflow uses the following agents:

- **Codex:** Used for AI-assisted project investigation and technical analysis.
- **EdgeRetina Research Agent (`@edgeretina-researcher`):** Used to investigate the EdgeRetina project and its implementation.
- **Switch Buddy Admin (`@switch-buddy-admin`):** Used for Switch-related assistance and workspace administration.

Ensure the required agents are available in the Switch workspace and can participate in the Telegram workflow.

### Provide Access to the EdgeRetina Repository

1. Clone the EdgeRetina repository onto the machine running the research workflow.
2. Ensure the research agent has access to the local repository files.
3. Invite the research agent to the Telegram group using:

   `!invite-agent @edgeretina-researcher`

   Alternatively, use:

   `/invite_agent @edgeretina-researcher`

4. Verify that the agent can inspect the relevant project files.

The repository is maintained separately from the public PAIRADOX documentation repository.

### Send and Test an Investigation Request

1. Open the PAIRADOX Telegram group.
2. Submit an investigation request by mentioning the research agent.
3. Allow the connected agent workflow to process the request.
4. Review the response and its supporting evidence in the group.

**Example investigation request:**

`@edgeretina-researcher Investigate why the Severe DR class has zero recall in the saved federated evaluation. Identify the relevant evaluation metrics, confusion matrix, and possible contributing factors. Do not modify any project files.`

A successful investigation should produce:

- Relevant project files or evaluation artifacts inspected.
- Confirmed observations supported by evidence.
- Possible explanations clearly distinguished from confirmed findings.
- A response available for human review in Telegram.

### Human Review and Safety

- Treat agent-generated findings as investigative assistance, not automatically verified conclusions.
- Check the cited files and metrics before accepting conclusions.
- Keep investigation operations read-only unless changes are explicitly authorized.
- Never expose private credentials, tokens, or sensitive configuration files.

### Reproduction Notes

The EdgeRetina project is maintained separately from PAIRADOX. Reproducing the investigation requires access to the EdgeRetina repository and the appropriate local agent configuration.

Exact agent authentication and workspace settings may depend on the local Switch environment.

## Demo 

Watch the demo video through this link - https://drive.google.com/file/d/1_31fGvzdJ_K9P2NRS02N8dbLmxpue8K_/view?usp=sharing

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
