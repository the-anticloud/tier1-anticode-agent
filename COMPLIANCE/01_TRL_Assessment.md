# ANTICODE AGENT — Compliance & TRL Assessment

## TRL 8.0 — System Complete and Qualified

| TRL | Criterion | Evidence |
|-----|-----------|---------|
| TRL 1–4 | Research to lab validation | TypeScript agent framework proven; llamafile integration tested |
| TRL 5–6 | Relevant environment | Pre-built binaries for Windows/Linux/macOS; Bun compile pipeline |
| TRL 7 | Prototype demonstrated | `antikode.exe` runs locally, MCP support, RAG integrated |
| TRL 8 | **Complete and qualified** | **Production binaries ship; AIOSS audit logging in place** |

## OWASP LLM Top 10 Coverage

| OWASP ID | Threat | Anticode Mitigation |
|----------|--------|-------------------|
| LLM01 | Prompt Injection | ANT-2001 config validation; no system-level shell injection |
| LLM04 | Model DoS | Local model only — no quota exhaustion |
| LLM06 | PII Disclosure | AIOSS ledger stores prompt hashes, not raw prompts |
| LLM08 | Excessive Agency | Tool execution requires explicit user confirmation |

## No Frontier API Keys

```bash
# Verify no cloud API keys in source
grep -r "OPENAI_API_KEY\|ANTHROPIC_API_KEY\|GEMINI_API_KEY" packages/ --include="*.ts"
# → 0 matches (optional via config only, never hardcoded)
```

Default provider is llamafile (local). Cloud providers are opt-in via config, not required.

## OSINT Surface

| Surface | Exposure |
|---------|---------|
| Network | Local only (calls localhost:8080 or :11434) |
| Binary | Compiled single-file exe — no source exposed |
| Config | `~/.config/anticode/config.toml` — local only |
| AIOSS Ledger | Local file — no network sync |

## License

MIT. Commercial use permitted.
