# Developer Cookbook — ANTICODE_AGENT
**Stack:** Python 3.11, tree-sitter, PAX 27B, AIOSS_FORMAT

## Generate a new module
```python
from anticode_agent import AnticodeAgent
agent = AnticodeAgent(pax_model="./pax-27b-q4.gguf")
code = agent.generate(
    task="Implement AIOSS chain reader with streaming support",
    context_files=["aioss_format.py"],
    output_path="./aioss_reader.py"
)
print(code.ast_valid, code.chain_hash)
```

## Review and patch existing code
```python
patch = agent.review_and_patch(
    file_path="./pax_harness.py",
    issue="Add retry logic for chain append failures"
)
patch.apply()
```

## Scaffold a new tier project
```python
agent.scaffold_project(
    tier="TIER_4_INFERENCE_AGENTS", name="K_NEWPROJECT",
    components=["aioss_integration", "pax_harness", "deploy_guide", "tests"]
)
```

## Self-improving loop
```python
agent.self_improve(target_metric="code_coverage", max_iterations=5,
                   aioss_chain="./self_improve.aioss")
```

## AIOSS append for code artifacts
```python
import hashlib
code_bytes = open("./generated_module.py", "rb").read()
chain_hash = aioss_append("./codegen.aioss", code_bytes, "ANTICODE_AGENT")
```

## Performance
Cache PAX model: `agent.keep_model_loaded()`. Batch scaffolding: `agent.batch_mode()`.
Context window: 8192 for most tasks, 32768 for large refactors.

## Integration
Reads KAMELOT_SEARCH for code context. Feeds KANTOR_K5 with API signature facts.
Used by KAZCADE_RUNTIME to generate runtime adapters.
