# Agent-to-Terminal Execution Protocol (ATXP)

Author: Richard Gann

---

## Overview

The Agent-to-Terminal Execution Protocol (ATXP) defines a lightweight interface for connecting AI agent systems with terminal-based execution environments.

It introduces a structured way for AI systems to plan, execute, and iteratively refine real-world software tasks through command-line interfaces.

---

## Problem

Modern AI agents can generate plans for complex software tasks, but lack:

- A standardized execution interface
- Safe command execution in real environments
- Reliable feedback loops from system output
- Structured task decomposition across steps

Meanwhile, terminal environments are powerful but not designed for agent orchestration.

---

## Proposal

ATXP defines a minimal protocol enabling:

- Structured JSON task graphs from AI agents
- Sequential or dependency-based execution of terminal commands
- Standardized execution outputs (stdout, stderr, status)
- Iterative feedback loops between execution and planning systems

---

## System Architecture

### 1. Planning Layer (AI Agent)

The agent generates structured task graphs consisting of:

- Tasks
- Steps
- Dependencies
- Commands

---

### 2. Execution Layer (Terminal Runtime)

The execution system processes each step and returns structured results.

Each step executes one command and returns:

- stdout
- stderr
- exit code
- success/failure status

---

### 3. Feedback Loop

Execution results are returned to the agent for:

- correction
- retry logic
- task refinement
- continuation of workflow

This creates an iterative execution cycle until completion.

---

## Execution Rules (Core Contract)

The execution layer MUST follow these deterministic rules:

---

### 1. Atomic Step Execution

Each step MUST:

- execute exactly one command
- produce one structured output
- remain independent unless dependencies are explicitly defined

---

### 2. Deterministic Ordering

Execution order is defined as:

- Steps without dependencies execute in sequence order
- Steps with dependencies wait for successful completion of required steps

---

### 3. Execution Output Contract

Each step MUST return:

```json
{
  "id": 1,
  "command": "string",
  "stdout": "string",
  "stderr": "string",
  "status": "success | failure",
  "exit_code": 0
}
