# [Case Study Summary] Bluesight: Multi-Agent Orchestration Architecture for GPO Prohibition Compliance on AWS

## 📌 Document Metadata
* **Domain:** Healthcare FinTech, Pharmaceutical Compliance, Generative AI Systems, AWS Architecture.
* **Target System:** Bluesight (Medication Intelligence Platform).
* **Key Architecture Pattern:** Multi-Agent Orchestration + Deterministic Scoring Pipeline + Model Context Protocol (MCP).
* **AWS Core Stack:** Amazon Bedrock (Claude 3.5 Sonnet / Haiku), Amazon Cognito, AWS Lambda, AgentCore Gateway, Amazon CloudWatch, AWS VPC Private Subnets.

---

## 1. Business Context & Problem Statement

### 1.1 Business Domain Concepts
* **340B Drug Pricing Program:** A US federal program allowing safety-net healthcare providers to purchase outpatient drugs at significant discounts (20%–50%).
* **GPO Prohibition:** Participating 340B hospitals are strictly prohibited from purchasing outpatient drugs through Group Purchasing Organization (GPO) contracts. 
* **Compliance Impact:** Violating GPO Prohibition results in severe financial penalties (millions of USD), retroactive repayments to drug manufacturers, or disqualification from the 340B program.

### 1.2 Audit Complexity & Technical Bottleneck
To evaluate GPO Prohibition compliance, compliance officers must cross-reference data across three isolated products/siloed data sources:
1. **340BCheck:** Patient eligibility and 340B prescription allocation status.
2. **ShortageCheck:** FDA and internal drug supply shortage data (shortages can grant legal exceptions).
3. **CostCheck:** Price differentials across purchasing channels (WAC vs. GPO vs. 340B).

### 1.3 Why Traditional / Single-Agent AI Failed
* **Context Window Overload:** Feeding 340B federal guidelines, real-time pricing databases, and transaction logs into a single prompt degraded reasoning quality.
* **Hallucination Risks in Legal Audit:** Deterministic accuracy is mandatory; an LLM making subjective guesses regarding legal compliance creates massive liability risks.

---

## 2. Technical Architecture Breakdown

### Component Deep-Dive

#### A. Ingress & Security Layer
* **Amazon Cognito:** Handles OAuth2 + JWT authentication for `Hospital Compliance Users`.
* **VPC Private Subnets:** Enforces network isolation for the `AgentCore Runtime` to comply with healthcare data privacy standards.

#### B. Orchestration Layer (Brain)
* **GPO Orchestrator Agent:** Powered by **Amazon Bedrock (Claude 3.5 Sonnet / Haiku)**. Acts as the central reasoning engine that parses user intents, decomposes tasks, delegates sub-tasks to specialized worker agents, and tracks reasoning traces via **Amazon CloudWatch**.

#### C. Data-Worker Layer (Specialized Agents)
Rather than executing queries directly, the Orchestrator delegates tasks to 3 domain-specific worker agents:
* **`340BCheck Worker`:** Queries 340B prescription allocations and patient eligibility rules.
* **`ShortageCheck Worker`:** Queries FDA and market drug shortage statuses.
* **`CostCheck Worker`:** Queries historical pricing, WAC vs. GPO vs. 340B cost differentials.

#### D. Integration & Tooling Layer
* **AgentCore Gateway:** Orchestrates API communications between Worker Agents and underlying data sources.
* **Lambda-backed MCP Tools:** Standardizes tool execution using the **Model Context Protocol (MCP)** implemented as AWS Lambda functions to query product databases (`CostCheck`, `ShortageCheck`, `340BCheck`).

#### E. Deterministic Scoring Pipeline (Zero-Hallucination Guardrail)
* **Function:** A non-LLM, purely mathematical/logical pipeline running **13 deterministic signals (rules)**.
* **Execution:** Worker Agents fetch raw data and package them into structured **Evidence**. The Evidence is processed by the Scoring Pipeline to compute a mathematically verified compliance risk score ($100\%$ deterministic accuracy).

---

## 3. End-to-End Execution Sequence

1. **Request Ingestion:** The user authenticates via Cognito and submits a compliance query regarding a list of purchased outpatient drugs.
2. **Intent Parsing & Delegation:** `GPO Orchestrator` receives the request, plans the execution flow via Bedrock, and delegates tasks asynchronously to `340BCheck Worker`, `ShortageCheck Worker`, and `CostCheck Worker`.
3. **Data Retrieval via MCP:** Each Worker Agent executes `Lambda-backed MCP Tools` via `AgentCore Gateway` to fetch relevant records from product databases.
4. **Deterministic Validation:** Raw evidence from all workers is passed into the `Deterministic Scoring Pipeline (13 Signals)` for mathematical compliance calculation.
5. **Report Generation:** `GPO Orchestrator` receives the validated compliance score, formats the findings into a natural language audit report with citations, and returns it to the user.

---

## 4. Key Engineering Takeaways

1. **Decoupled Multi-Agent Pattern:** Splitting domain knowledge across dedicated Worker Agents prevents context window bloat, reduces latency through parallel execution, and improves tool selection precision.
2. **Hybrid Intelligence (LLM + Deterministic Engine):** LLMs are optimal for reasoning, task planning, and language generation; deterministic algorithms are mandatory for legal/financial calculations. Merging both eliminates AI hallucinations in high-stakes domains.
3. **Standardized Tooling with MCP:** Adopting Model Context Protocol (MCP) decouples the agent orchestration logic from data-source integrations, enabling seamless onboarding of new products or databases.