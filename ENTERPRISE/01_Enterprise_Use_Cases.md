# ANTICODE AGENT — Enterprise Use Cases

## Use Case 1: Air-Gap Developer Environment

**Problem**: Defense/finance organizations cannot use cloud coding assistants (GitHub Copilot, Cursor, Claude) due to data sovereignty requirements.

**Solution**: Antikode + llamafile runs completely offline. No network required after initial binary download.

```bash
# Air-gap setup
cp antikode.exe /secure-workstation/
cp Qwen2.5-Coder-7B.llamafile /secure-workstation/

# Run locally
./Qwen2.5-Coder-7B.llamafile --server --port 8080 &
./antikode.exe --model http://localhost:8080
```

**Outcome**: Full AI coding assistance with zero data exfiltration risk.

## Use Case 2: Regulated Code Generation Audit

**Problem**: Healthcare/finance code must be auditable — prove what AI generated what code and when.

**Solution**: AIOSS integration logs every generation event with prompt hash, output hash, timestamp.

```typescript
// Every generation creates an immutable AIOSS ledger entry
await ledger.append({
  entry_type: "code_generation",
  actor: "anticode-agent",
  content: {
    session_id: session.id,
    prompt_hash: sha3_256(prompt),  // HIPAA: no raw prompt stored
    output_hash: sha3_256(code),
    tokens_in: countTokens(prompt),
    cost_if_cloud_microcents: 0,
  }
});
```

**Outcome**: SOC2 + HIPAA compliant AI coding audit trail.

## Use Case 3: Team Coding Agent Deployment

```bash
# Deploy shared model server
docker run -p 8080:8080 vllm/vllm-openai \
  --model kleinnner/pax-one-27b-fp8

# Each developer runs antikode pointing to shared server
anticode --endpoint http://model-server:8080 --model pax-27b
```

Each developer's sessions are independently logged to their own AIOSS ledgers.

## Use Case 4: Plugin-Extended Capabilities

```typescript
// Custom plugin: database query tool
const dbPlugin: Plugin = {
  name: "database",
  tools: [{
    name: "query_db",
    description: "Execute read-only SQL on the project database",
    execute: async ({ sql }) => {
      // Validate: SELECT only, no DDL/DML
      if (!sql.trim().toUpperCase().startsWith("SELECT")) {
        throw new AntiError("ANT-3002", "Only SELECT queries allowed");
      }
      return db.query(sql);
    }
  }]
};

anticode.use(dbPlugin);
```
