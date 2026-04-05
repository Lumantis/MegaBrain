# Lumantis Skill Template

Use this skeleton when generating `/lumantis-*` skills in Phase 3 (COMPOSE).
Replace all `{{placeholders}}` with generated content.

---

```markdown
---
name: lumantis-{{kebab-name}}
description: Use when {{specific triggering conditions for this orchestration}}
generated_by: new-orchestration
generated_at: {{YYYY-MM-DD}}
complexity: {{trivial|small|medium|large|mega}}
pattern: {{sequential|parallel-fan-out|dag-pipeline|loop-iterate|hybrid}}
total_phases: {{N}}
total_agents: {{N}}
---

# /lumantis-{{kebab-name}} — {{Title}}

{{One-line description of what this orchestration achieves.}}

## Autonomy Contract

This orchestration runs FULLY AUTONOMOUSLY once launched.
- Zero questions to user during execution
- All decisions made by the Decision Engine (Section 6)
- All failures handled by Self-Healing Pipeline (Section 5)
- Progress notifications are non-blocking
- Terminal states only: SUCCESS | PARTIAL | BLOCKED

## Intent Map

```yaml
intent: {{intent}}
domains: [{{domains}}]
complexity: {{tier}}
tech_stack: [{{detected stack}}]
constraints: [{{constraints}}]
matched_skills: [{{existing skills that apply}}]
mcp_servers: [{{MCP servers to use}}]
```

## DAG Flowchart

```dot
digraph lumantis_{{name}} {
  rankdir=LR;
  {{Generated DAG nodes and edges}}
}
```

## Phases

{{For each phase, generate:}}

### Phase {{N}}/{{Total}}: {{Phase Name}} [{{tier}}]

| Attribute | Value |
|-----------|-------|
| **Agents** | {{subagent_type values}} |
| **Model** | {{haiku/sonnet/opus}} |
| **Autonomy** | {{FULL_AUTO/AUTO_WITH_FALLBACK}} |
| **Skills** | {{existing skills to invoke}} |
| **MCP** | {{MCP tools if applicable}} |
| **Gate** | {{pass condition}} |
| **On Fail** | {{retry strategy}} |

**Input:** {{What this phase receives from predecessor}}

**Action:**
{{Detailed instructions for the agent(s). Be specific.
Include exact commands to run, files to create/modify,
patterns to follow.}}

**Output:** {{Expected deliverable}}

---

{{Repeat for all phases}}

## Self-Healing Pipeline

Phase fails →
1. **Retry 1:** Same agent + error context enrichment
2. **Retry 2:** Same agent + alternative approach prompt
3. **Retry 3:** Different agent from same domain (fallback)
4. **Decompose:** Break phase into smaller sub-tasks, retry each
5. **Skip (non-critical):** Log in final report, continue
6. **Block (critical, all exhausted):** Save state → notify user

## Decision Engine (Autonomous)

| Decision Point | Auto-Resolution |
|---------------|-----------------|
| Architecture A vs B | Planner agent per best practices + instincts |
| Test failure | Auto-fix with error context (max 3) |
| Review rejection | Fix-agent with feedback, re-submit |
| Merge conflict | Agent with fewer files redoes phase |
| Missing dependency | Auto-install + log |
| Ambiguity | Choose conventional option + document |
| Style/design choice | Follow project conventions or modern defaults |

## Memory System

### Session Layer
- TodoWrite per atomic action: `[Phase N/{{Total}}] {{action}}`
- 1 in_progress at a time. Mark completed immediately.
- On failure: keep in_progress + add diagnostic todo.

### Project Layer
Persistent files in project memory:
- `lumantis-{{name}}-state.md` — Phase status, blockers
- `lumantis-{{name}}-decisions.md` — Autonomous decisions log
- `lumantis-{{name}}-context.md` — Cumulative handoff context

**On Launch:** Read state → detect resume point → continue or restart.
**After Each Phase:** Write updated state.

### Handoff Format
```
## HANDOFF: Phase N → Phase N+1
### State: Completed N/{{Total}}
### Cumulative Context: [All decisions since Phase 1]
### Deliverables: [Files from Phase N]
### Instructions: [What Phase N+1 must do]
```

## Loops

### Review-Fix Loop (per applicable phase)
```
implement → review → pass? → next phase
                  ↓ fail
              fix → re-review (max 3 passes)
```

### De-Sloppify Pass (post-implementation)
Separate cleanup agent removes: console.log, dead code, TODO comments,
over-defensive checks, test bloat, unused imports.

### Visual Validation Loop (UI phases only)
```
render → screenshot (Preview/Chrome MCP) → acceptable? → next
                                         ↓ no
                                    adjust → re-render (max 3)
```

## Auto-Dream (Post-Completion)

After orchestration completes, run 4-phase memory consolidation:

### ORIENT
Read project MEMORY.md + all topic files. Map existing knowledge.

### GATHER SIGNAL
Scan session for: decisions, techniques, agent performance,
retry patterns, skip reasons. Extract high-value patterns.

### CONSOLIDATE
Merge into project memory:
- `feedback_orchestration.md` — What worked/didn't
- `project_{{name}}_state.md` — Final state + deliverables
- `agent_performance.md` — Per-agent success/retry/fail rates
Convert relative dates to absolute. Delete contradictions. Merge duplicates.

### PRUNE & INDEX
Update MEMORY.md (max 200 lines). Remove stale entries.
Record timestamp in `.last-dream`.

## Learning Capture

1. **Retrospective:** Planner agent analyzes execution
2. **Instinct Capture:** `learn-eval` extracts patterns
   - Low (0.3) → 3x confirmed → Medium (0.6) → 5x → High (0.9)
3. **Agent Performance:** Update agent-performance.md
4. **User Rating Request:** "Rate 1-5 + optional comment"
   (Non-blocking. If no response in 30s, default to skip.)

## Progress Notifications

```
[lumantis-{{name}}] Phase 1/{{Total}} complete — {{summary}} ✓
[lumantis-{{name}}] Phase {{N}}/{{Total}} complete — {{summary}} ✓
[lumantis-{{name}}] COMPLETE — Final report below.
```

## Final Report

### Result: {{SUCCESS | PARTIAL | BLOCKED}}

### Metrics
- Phases: {{completed}}/{{total}}
- Agents dispatched: {{count}}
- Tests: {{pass}} passing, {{fail}} failing
- Retries: {{count}} ({{details}})

### Deliverables
{{List of files created/modified}}

### Autonomous Decisions
{{List of autonomous decisions with justification}}

### Skipped Phases
{{If any, with reason}}

### Visual Proofs
{{Screenshots from visual checkpoints}}

### Next Steps
{{Suggested follow-up actions}}
```
