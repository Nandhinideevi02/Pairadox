# Workflow and Execution

## Workflow Execution

### Step 1: Submit an Investigation Request

Team members send technical questions or investigation requests in the Telegram group where the configured agent is available.

Example:

"Investigate why the Severe Diabetic Retinopathy class has zero recall in the federated evaluation results."

### Step 2: Request Routing Through Switch

Switch acts as the orchestration layer between Telegram and the configured Codex AI agent. It receives the request and routes it to the appropriate agent.

### Step 3: Repository Investigation

The Codex AI agent accesses the configured EdgeRetina project workspace and examines relevant source code, configuration files, saved metrics, and experiment reports.

Depending on the request, the investigation may involve:
- Understanding the project architecture.
- Examining model training and evaluation logic.
- Comparing centralized and federated learning results.
- Investigating classification performance.
- Reviewing Federated Averaging (FedAvg) implementation.
- Examining differential privacy configuration.

### Step 4: Generate Evidence-Based Findings

The agent returns its findings through Telegram, referencing relevant project files, implementation details, and experimental results where available.

The response may include:
- Identified observations.
- Relevant file references.
- Possible explanations for observed behaviour.
- Limitations of the available evidence.
- Suggested follow-up investigations.

### Step 5: Human Review

Team members examine the agent's findings, assess the supporting evidence, and decide whether further investigation is required.

No code changes or experimental modifications are considered approved merely because the agent suggests them.

## Demonstrated Investigation Scenarios

The PAIRADOX workflow was demonstrated using the following EdgeRetina investigation scenarios:

1. **Model Performance Analysis:** Comparing centralized and federated learning evaluation metrics.
2. **Classification Failure Investigation:** Examining the zero recall observed for the Severe Diabetic Retinopathy class.
3. **FedAvg Implementation Review:** Investigating the sample-weighted aggregation logic.
4. **Differential Privacy Review:** Examining the implementation and configuration of privacy-related mechanisms.
5. **Dataset Analysis:** Reviewing class distributions and client-level data distribution.

## Safety and Human Oversight

- Investigation requests are reviewed by team members.
- Findings are interpreted in the context of the available source code and saved experiment artifacts.
- Agent-generated explanations are treated as investigation results, not independently validated scientific conclusions.
- Code modifications and additional experiments require human review and approval.
- Sensitive credentials, bot tokens, and private configuration details must not be shared in public documentation.

NOTE: The accuracy and completeness of investigation results depend on the agent's repository access, available project artifacts, and the quality of the submitted requests.
