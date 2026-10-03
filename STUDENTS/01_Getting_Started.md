# ANTICODE_AGENT — Student Getting Started

## What You'll Build
A local AI coding agent that reads your codebase, plans changes, writes code, and verifies with tests — all running on your machine with no cloud API keys.

## Prerequisites
- Python 3.10+
- Basic Python programming experience
- [Ollama](https://ollama.ai) installed locally
- 8 GB RAM minimum (16 GB recommended for 13B models)

## Install
```bash
ollama pull codellama:13b
pip install anticode-agent
```

## First Working Example
```python
from anticode_agent import Agent

agent = Agent(
    model_backend="ollama",
    model_name="codellama:13b",
    workspace="./my_project"
)

# Ask the agent to write a function
result = agent.run("Write a Python function that reads a JSON file and validates required fields")
print(result.code)
# The agent creates the file and runs tests automatically
print(f"Tests passed: {result.tests_passed}")
print(f"Files modified: {result.files_changed}")
```

## Try a Real Task
```python
# Point it at an existing project
agent = Agent(model_backend="ollama", model_name="codellama:13b",
              workspace="./your_project")

plan = agent.plan("Add input validation to all API endpoints")
print("Planned steps:")
for step in plan.steps:
    print(f"  - {step.description}")

# Execute step by step
for step in plan.steps:
    result = agent.execute(step)
    print(f"Step done: {result.status}")
```

## On Kaggle (loiskleinner account, T4 GPU)
1. Create a new notebook on Kaggle
2. Enable GPU accelerator (T4 x2 recommended)
3. In the first cell:
```python
!pip install anticode-agent
!curl -fsSL https://ollama.ai/install.sh | sh
!ollama serve &
import time; time.sleep(3)
!ollama pull codellama:13b
```
4. Then run the examples above — the T4 GPU will accelerate generation significantly

## What's Next
- Explore `agent.plan()` for multi-step refactoring
- Read the EDUCATORS Teaching Guide for deeper internals
- Connect to AIOSS_FORMAT to log agent sessions for audit
