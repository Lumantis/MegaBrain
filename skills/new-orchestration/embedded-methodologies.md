# Embedded Methodologies — Standalone Reference

These methodologies are embedded so the plugin works WITHOUT any external plugins installed.
When generating `/lumantis-*` skills, embed the relevant methodology INLINE in the generated skill
rather than referencing external skill names. If external skills ARE available, prefer them.

## Brainstorming Methodology (from superpowers:brainstorming)

Before any creative or design work:
1. Explore project context (files, docs, git history)
2. Ask clarifying questions one at a time (prefer multiple choice)
3. Propose 2-3 approaches with trade-offs and recommendation
4. Present design in sections, get approval for each
5. Write design doc to `docs/specs/YYYY-MM-DD-<topic>-design.md`
6. Self-review: scan for placeholders, contradictions, ambiguity
7. Get user approval before implementation

Key principles: YAGNI ruthlessly, explore alternatives, incremental validation, one question at a time.

## Test-Driven Development (from superpowers:tdd)

For EVERY implementation phase:
1. **RED**: Write failing test first — define what "done" looks like
2. **GREEN**: Write minimal code to make the test pass — nothing more
3. **REFACTOR**: Clean up while tests stay green

Rules:
- Never write code before the test. Delete and start over if you do.
- Tests first = "what should this do?" not "what does this do?"
- Target 80%+ coverage for new code
- Run tests after EVERY change

## Verification Before Completion (from superpowers:verification)

Before declaring ANY phase complete:
1. Run the build — must pass with zero errors
2. Run all tests — must be green
3. Run linter/formatter — must be clean
4. Check for regressions — no existing tests broken
5. Review diff — does it match the intent?

Never claim "done" without running verification commands. "It should work" is not verification.

## Security Review Checklist (from security-review)

For phases touching auth, user input, APIs, or sensitive data:
- Input validation on ALL user-facing endpoints
- Parameterized queries (never string concat SQL)
- Auth/authz checks on every protected route
- Secrets in env vars, never in code
- CORS configured correctly
- Rate limiting on auth endpoints
- Dependencies scanned for known vulnerabilities
- No sensitive data in logs or error messages

## Code Review Standards (from code-reviewer)

Every review checks:
1. **Correctness**: Does it do what it's supposed to?
2. **Security**: Any injection, XSS, auth bypass risks?
3. **Performance**: N+1 queries? Unnecessary re-renders? Memory leaks?
4. **Maintainability**: Can someone else understand this in 6 months?
5. **Tests**: Are edge cases covered? Are tests meaningful?

Review output format: PASS / NEEDS_WORK / BLOCK with specific issues.

## Blueprint Planning (from blueprint)

For complex multi-phase projects:
1. Break objective into 1-PR-sized steps (3-12 typical)
2. Detect dependencies between steps
3. Identify which steps can run in parallel
4. Assign model tier per step (haiku/sonnet/opus)
5. Define rollback strategy for each step
6. Write self-contained plan with exit criteria per step

## De-Sloppify Pattern (from autonomous-loops)

After all implementation phases are done, run a SEPARATE cleanup pass:
- Fresh agent context (no author bias)
- Remove: console.log, dead code, TODO comments, unused imports
- Remove: over-defensive error handling, excessive comments
- Remove: test bloat (duplicate assertions, over-mocking)
- Verify: all tests still pass after cleanup

## Adversarial Review (from santa-method)

For critical quality gates, use TWO independent reviewers:
1. Reviewer A checks against spec/requirements
2. Reviewer B checks code quality and security
3. BOTH must PASS before the phase is complete
4. If either rejects: fix, then BOTH re-review
5. Convergence loop: max 3 rounds

## Context Bridging (from autonomous-loops)

For multi-phase orchestrations, bridge context between phases:
- Each phase produces a HANDOFF document (Markdown)
- Handoff is CUMULATIVE: includes summary of ALL previous phases
- An agent in Phase 5 can understand everything since Phase 1
- State file tracks: completed phases, current phase, blockers
- On session resume: read state file, load last handoff, continue

## Auto-Dream Memory Consolidation

After orchestration completes:
1. **ORIENT**: Read project MEMORY.md + all topic files
2. **GATHER SIGNAL**: Scan session for decisions, techniques, agent perf, retries
3. **CONSOLIDATE**: Merge into topic files, convert relative dates, delete contradictions
4. **PRUNE & INDEX**: Update MEMORY.md (max 200 lines), remove stale entries

Topic file categories:
- `feedback_*.md` — What worked, what didn't
- `project_*.md` — Project state and deliverables
- `agent_performance.md` — Per-agent success/retry/fail rates

## Continuous Learning / Instincts

After each orchestration:
1. Extract reusable patterns from the session
2. Save as instincts with confidence scoring:
   - New instinct: confidence 0.3 (low)
   - Confirmed 3x: confidence 0.6 (medium)
   - Confirmed 5x: confidence 0.9 (high)
3. High-confidence instincts become implicit rules
4. Instincts that are contradicted get demoted or deleted
5. Instincts not confirmed after 30 days get pruned

## Deployment Patterns

For phases involving deployment:
- Docker containerization when applicable
- Health checks on all services
- Environment variables for configuration (never hardcode)
- CI/CD pipeline setup (GitHub Actions preferred)
- Rollback strategy defined before deploy
- Zero-downtime deployment when possible
- Post-deploy smoke tests

## Content Engine Patterns

For marketing/content phases:
- Platform-native content (don't cross-post identical content)
- X/Twitter: threads, engagement hooks, hashtag strategy
- LinkedIn: thought leadership, professional tone, carousel posts
- TikTok/Instagram: visual-first, trending audio, hooks in first 3 seconds
- Blog/SEO: keyword research first, H1/H2 structure, internal linking
- Email: subject line testing, segmentation, clear CTA

## API Design Patterns

For backend/API phases:
- RESTful resource naming (plural nouns)
- Consistent error response format
- Pagination on list endpoints
- Rate limiting headers
- API versioning strategy
- OpenAPI/Swagger documentation
- Input validation middleware
