We are continuing the laptop-ai project.

CURRENT CHECKPOINT:
- Phase 7.4A Task Dependency Model: COMPLETE
- Phase 7.4B Dependency Resolution: COMPLETE
- Phase 7.4C Workflow Scheduler: COMPLETE
- Phase 7.4D Sequential Workflow Execution: COMPLETE
- Phase 7.4E Parallel-Ready Task Detection: COMPLETE
- Latest commit: 000d0f0 feat: add parallel-ready task detection
- Working tree is clean.

NEXT SCOPE:
Implement ONLY Phase 7.4F — Actual Parallel Execution.

FIRST:
1. Inspect the existing implementation of:
   - app/models.py
   - app/dependency_resolution.py
   - app/scheduler.py
   - app/workflow.py
   - app/parallel_detection.py
   - relevant tests
2. Understand and preserve the existing APIs and semantics.
3. Do not redesign previous phases.

GOAL:
Add provider-agnostic parallel workflow execution that consumes the parallel batches produced by Phase 7.4E.

REQUIREMENTS:
1. Reuse the existing:
   - TaskGraph
   - ExecutionState
   - transition()
   - resolve_dependency_state()
   - schedule_workflow()
   - detect_parallel_batches()
   - ParallelBatches
   - SpecialistTask
   - existing sequential workflow semantics where appropriate.

2. Implement actual concurrent execution of tasks belonging to the same parallel batch.

3. Tasks in different batches MUST NOT execute concurrently.
   Batch N must complete before Batch N+1 begins.

4. Preserve dependency ordering.
   A task may execute only after all of its dependencies have successfully completed.

5. Keep execution provider-agnostic.
   The executor must remain an injected callable.
   Do NOT directly invoke:
   - OpenCode
   - Gemini
   - OpenAI
   - subprocess
   - CLI commands
   - filesystem operations
   - network APIs

6. Use a standard Python concurrency primitive appropriate for I/O-bound executor calls.
   Keep the implementation minimal; do not introduce a new dependency.

7. Executor exceptions must be converted into task failure rather than crashing the entire scheduler unexpectedly.

8. State transitions must remain valid and must use the existing transition mechanism.
   Preserve:
   PENDING → READY → RUNNING → SUCCESS/FAILED

9. Determinism:
   - Batch ordering must remain deterministic.
   - Task ordering in returned results must remain deterministic according to the graph/batch ordering.
   - Do not let thread completion order determine public result ordering.

10. Do NOT implement Phase 7.4G failure propagation.
    Do not add new semantics for recursively marking descendants BLOCKED.
    Keep failure handling limited to the parallel execution scope.

11. Do NOT implement Phase 7.4H workflow finalization beyond what is strictly necessary for returning the execution result.

12. Do not modify unrelated modules.

TESTS:
Add focused tests for Phase 7.4F covering at minimum:

- two independent ready tasks execute concurrently
- three independent ready tasks execute concurrently
- dependent tasks do not execute until their dependencies' batch completes
- tasks from different batches never overlap
- a single-task batch still executes correctly
- empty workflow
- all tasks already successful
- executor returns success
- executor returns failure
- executor raises an exception
- task state transitions remain valid
- deterministic result ordering despite nondeterministic completion order
- no dependency violation can occur
- parallel execution still respects the existing TaskGraph topological structure
- existing sequential workflow behavior remains unchanged

Concurrency tests must verify REAL overlap, not merely that multiple executor calls were made.
Use synchronization primitives/events/barriers where appropriate, but keep tests deterministic and non-flaky.

IMPORTANT:
- Do not weaken existing tests.
- Do not rewrite previous phases.
- Do not introduce unnecessary abstractions.
- Do not add external dependencies.
- Do not commit changes.
- Do not touch git history.

VALIDATION:
After implementation run:

1. Focused Phase 7.4F tests.
2. Full test suite.
3. git diff --check
4. git status --short

Report:
- files changed
- implementation summary
- exact focused test count/result
- exact full-suite count/result
- diff-check result
- git status
- any design decisions or limitations

STOP after Phase 7.4F is complete.
Do NOT proceed to Phase 7.4G.
