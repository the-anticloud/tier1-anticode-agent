# Deploy Guide — ANTICODE_AGENT
## Prerequisites
- Python 3.11+, tree-sitter 0.21+, PAX 27B weights (pax-27b-q4.gguf, ~15GB)
- ANTICLOUD_CORE on PYTHONPATH

## Environment
- GPU: 24GB VRAM recommended (PAX 27B Q4). CPU inference: ~8 tok/s vs ~97 tok/s GPU.
- 32GB RAM minimum for full context window.

## Install
```bash
pip install anticloud-anticode-agent
```

## Air-Gap
Download all pip wheels on networked machine, transfer to air-gap host:
```bash
pip download -r requirements.txt -d ./wheels/
pip install --no-index --find-links ./wheels/ -r requirements.txt
```

## AIOSS Integration
```bash
aioss init --module ANTICODE_AGENT --output ./codegen.aioss
# Each generated file is appended automatically when using agent.generate()
```

## PAX Harness Wiring
```python
from anticloud_pax import PAXHarness
harness = PAXHarness(model_path="./pax-27b-q4.gguf", module="ANTICODE_AGENT",
                     aioss_chain="./codegen.aioss", classification="L5_NARROW_L2_GENERAL")
```

## Verification
```bash
python -m anticode_agent.tests.smoke
aioss verify --chain ./codegen.aioss --verbose
```
