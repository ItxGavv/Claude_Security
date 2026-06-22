# Claude Security Skills

This repository serves as a centralized, open-source library of specialized system instructions, profile configurations, and context patterns designed to optimize Claude for advanced technical roles. Each plugin within this repository is engineered to enforce rigorous behavioral boundaries, domain-specific methodology, and strict quality controls.

## Repository Architecture

The repository is organized by engineering domain, each containing a dedicated configuration file ready to be integrated into Claude Projects, Custom Instructions, or API system prompts.

### 1. Security Analysis (`/security`)
* **Objective**: Eliminates optimistic assumptions regarding code execution environments and enforces an adversarial, zero-trust evaluation mindset.
* **Key Mechanisms**: Mandatory input sanitization checks, deep-dive documentation verification rules, and automated pre-output threat modeling requirements.

### 2. Systems Design (`/systems-design`)
* **Objective**: Shifts model output from surface-level architectural diagrams to comprehensive, production-grade distributed systems design.
* **Key Mechanisms**: Formal trade-off matrices (latency versus throughput, consistency versus availability), failure-mode analysis, and concrete scaling strategies.

### 3. Database Optimization (`/database`)
* **Objective**: Controls query generation and schema design to prevent performance regression in production environments.
* **Key Mechanisms**: Explicit indexing analysis, query execution plan considerations, and normalization trade-offs.

## Implementation Guide

To activate a specific skill within your workflow, choose one of the following methods:

### Method A: Claude Projects (Recommended)
1. Navigate to your Claude Project dashboard.
2. Open the Project Knowledge or Custom Instructions panel.
3. Copy the contents of the desired `.md` file from this repository and paste it directly into the instructions field.

### Method B: API Integration
When utilizing Claude via the Anthropic API, pass the markdown content of the selected skill file directly into the `system` parameter of your API payload.
