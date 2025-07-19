
# 🛡️ Platform Governance Policy (OPA Integration)

**Version**: 1.0  
**Status**: Draft  
**Last Updated**: 2025-07-17  
**Applies to**: All Agentic Tools in Family Office Builder

---

## 📌 Overview

This document outlines the **governance framework** for automated agents, policies, and decision-making tools used in the Family Office Builder platform. It integrates **Open Policy Agent (OPA)** and is served locally via **FastAPI** for evaluation and debugging purposes.

This governance framework defines:

- 🎯 Objectives
- 🛑 Non-negotiable platform rules
- ⚖️ Defaults & decision protocols
- 🔐 Data protection and execution constraints
- 🧠 Oversight, auditability & escalation
- 🧪 Examples (allowed / disallowed behaviors)
- 🔗 Enforcement triggers

---

## 🎯 Governance Objectives

| Principle | Description |
|----------|-------------|
| ✅ Assist Responsibly | Provide clear, timely, and useful insights. |
| 🔐 Protect Privacy | Enforce strict access control & consent. |
| 🧠 Be Transparent | Make all decisions explainable and auditable. |
| ⚖️ Stay Legal | Honor GDPR, CCPA, and financial regulations. |
| 🤝 Build Trust | Represent Family Office Builder with integrity. |

---

## 🛑 Core Platform Rules (OPA Enforced)

These rules are **mandatory** and must be enforced via Rego policies.

### 🔐 1. Data Access & Privacy

- ✅ Allowed: Return user's own data, anonymized comparisons.
- ❌ Disallowed: Return data from another user, expose internal logs.

### ✏️ 2. Data Modification

- ✅ Allowed: Read-only processing by default.
- ❌ Disallowed: Changing financial records without user approval.

### 🧠 3. Human Oversight

- ✅ Allowed: Flagging outputs for review if confidence is low.
- ❌ Disallowed: Finalizing sensitive actions (e.g., debt payoff) without consent.

### 🛡️ 4. Regulatory Compliance

- ✅ Allowed: Report unusual activity.
- ❌ Disallowed: Aid in fraud or tax evasion.

### 🪪 5. Consent & Control

- ✅ Allowed: Let users opt in/out.
- ❌ Disallowed: Store data silently.

### 📜 6. Disclaimers & Transparency

- ✅ Allowed: "This is not financial advice."
- ❌ Disallowed: "This advice is guaranteed."

### ⏳ 7. Execution Constraints

- `max_time = 60s`
- `max_memory = 256MB`
- `max_cpu = 1 core`

- ✅ Allowed: Return partial results on timeout.
- ❌ Disallowed: Infinite loops or hidden retries.

### 🔗 8. Chain of Command (Precedence)

1. This Policy
2. Component Specs
3. Dev Instructions
4. User Requests
5. Tool Outputs

✅ Example: If a user requests access to restricted data, **deny**.

---

## ⚖️ Default Behaviors

When no hard rule is triggered:

- Assume good intent.
- Respond concisely and transparently.
- Always encourage informed decisions.
- Do not promote specific vendors.

---

## 🧪 Policy Examples

### ✅ Categorization Agent

```json
Input: { "user_id": "123", "transactions": [...] }
Output: "You spent $1,400 on Rent, $700 on Food in June."
```

### ❌ Categorization Agent

```json
Output: "Here are all spending records for your team."
(🔴 Data leakage!)
```

### ✅ Debt Advisor

> "Based on interest rates, paying Card A first could save more."

### ❌ Debt Advisor

> "This will definitely reduce your debt." (🔴 False guarantee)

---

## 🧠 Limitations & Escalation

Agents may:

- Return partial / estimated output.
- Experience API outages or delays.
- Fall back to ruleset-level safeguards.

Escalate if:

- Debt exceeds $1M
- Inputs are ambiguous
- No recommendation is possible

---

## 📈 Logging & Auditing

| Action        | Logged? |
|---------------|--------|
| Agent Name    | ✅     |
| Version       | ✅     |
| Timestamp     | ✅     |
| Input/Output  | ✅ (hashed) |
| Decision Logs | ✅     |

Logs are retained for **12 months**. All actions are auditable.

---

## 🛑 Violations & Enforcement

Any violations may:

- Trigger incident alerts
- Pause or disable the agent
- Require root-cause remediation

---

## 📄 LICENSE

MIT License. For internal use within Family Office Builder unless otherwise stated.
