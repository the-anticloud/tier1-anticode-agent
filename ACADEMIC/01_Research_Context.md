# ANTICODE AGENT — Academic Research Context

## Research Contribution

Antikode demonstrates that a production-grade AI coding agent can be built terminal-native with zero cloud dependency. Key design contributions:

1. **Bun single-binary compilation** — a complete TypeScript agent compiles to a 60MB executable with no runtime dependency
2. **Provider abstraction with fallback** — LlamafileProvider → OllamaProvider → OpenAI-compat, all sharing a single interface
3. **ANT-XXXX error taxonomy** — structured error codes for agents enable programmatic retry and recovery
4. **AIOSS audit integration** — first coding agent with cryptographic audit trails per generation event

## Related Work

| System | Language | Local-first | Audit trail |
|--------|----------|-------------|------------|
| Antikode | TypeScript/Bun | ✅ llamafile | ✅ AIOSS |
| Aider | Python | Partial (API default) | No |
| Continue.dev | TypeScript | Partial | No |
| Cursor | Electron | No | No |
| GitHub Copilot | Cloud-only | No | No |

## Citations

```bibtex
@software{alpasan2026anticode,
  author    = {Alpasan, Lois-Kleinner},
  title     = {Antikode: Terminal-Native Local-First AI Coding Agent},
  year      = {2026},
  publisher = {The Anticloud},
  note      = {MIT License},
}
```
