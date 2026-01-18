# Agent Operational Protocols & Context

This file serves as a reference for the AI Agent regarding system constraints, preferred workflows, and lessons learned.

## System Environment
- **Operating System**: Windows
- **Shell**: PowerShell

## Operational Protocols

### 1. Tool Availability Checks (Pre-flight)
- **Rule**: Before using external tools (git, node, python, etc.), ALWAYS verify they are installed and available in the current PATH.
- **Method**: Use `Get-Command <tool_name> -ErrorAction SilentlyContinue` in PowerShell.
- **Action**:
  - **If Found**: Proceed with the command.
  - **If Missing**: 
    1. **Attempt Installation**: If applicable (e.g., using `winget`, `npm`, or `pip`), propose or perform installation.
    2. **Fallback**: If installation is not possible or desired, use a native alternative (e.g., `Invoke-WebRequest` instead of `git clone`).

### 2. Execution Safety & Stall Detection
- **Observation**: Background commands may fail silently or hang if dependencies are missing or prompts are waiting.
- **Rule**: 
  - If a command takes longer than expected, **check its status and output** immediately using `command_status`.
  - If a command is stuck in an error loop or waiting for input that can't be provided, **TERMINATE** the process.
  - Do not assume "silence" means "working"; it often means "waiting" or "failed".

### 3. Specific Tool Context
#### Git
- **Current State**: Likely not installed or not in PATH.
- **Strategy**: Check first. If missing, prefer `Invoke-WebRequest` (Zip download) for simple retrieval tasks to avoid installation overhead, unless full version control features are required.
