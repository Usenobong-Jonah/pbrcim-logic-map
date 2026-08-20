# PBRCIM Logic-Map

## Structured Root Cause Analysis for Complex System Failures

PBRCIM Logic-Map is a browser-based diagnostic workspace built for investigating software failures that are difficult to explain through logs alone.

It helps engineers compare what a system was expected to do with what it actually did.

The investigation then moves stage by stage until the first meaningful divergence is isolated.

The tool is built around the **Pattern-Based Root Cause Isolation Model (PBRCIM)**.

> **Core question:** What pattern was supposed to happen, and where did that intent diverge?

---
## Interface Preview

<img width="1366" height="768" alt="pbrcim-logic-map-interface" src="https://github.com/user-attachments/assets/4de4315b-a6b8-4628-bb69-55d4bba9ed9a" />

PBRCIM Logic-Map provides a structured side-by-side workspace for tracing expected and observed system behavior, isolating divergence points, and documenting the full investigation.

## What It Does

PBRCIM Logic-Map provides a structured workspace for investigating failures across:

- Frontend applications
- APIs
- Backend services
- CI/CD pipelines
- Container builds
- Distributed systems
- Deployment workflows
- Database migrations
- Automation pipelines
- Runtime failures
- Developer tooling

The tool guides an investigation through the following process:

1. Record the observed behavior.
2. Define the expected behavior flow.
3. Map the stages of actual execution.
4. Identify the mismatch.
5. Compare working and broken paths.
6. Isolate the divergence point.
7. Record the root cause, corrective action, prevention strategy, and verification result.

The final investigation can be generated as a structured Markdown report.

---

## The Problem PBRCIM Logic-Map Is Built For

Some failures are obvious.

A process crashes.  
An exception is thrown.  
A test fails.  
A service returns an error.

Other failures are less cooperative.

The logs may look normal.

The build may complete successfully.

The application may appear healthy.

Yet the system still produces the wrong result.

PBRCIM Logic-Map is designed for that kind of investigation.

Instead of starting with:

> "What error did the system throw?"

PBRCIM starts with:

> "What was expected to happen, what actually happened, and where did those paths stop matching?"

That comparison often exposes failures hidden inside execution order, conditions, state changes, inputs, outputs, dependencies, runtime environments, configuration, timing, or control flow.

---

# The PBRCIM Investigation Flow

## 1. Observe the Failure

Start with the visible problem.

Record what is broken or behaving unexpectedly.

The observation should describe the actual symptom without jumping to a conclusion about the cause.

Example:

```text
Deployment completed successfully, but the new application version was not running in production.

At this stage, the goal is simple:

Describe what happened.

2. Define Expected Behavior

Document what the system was supposed to do.

For example:

Commit
  ↓
Build
  ↓
Test
  ↓
Deploy
  ↓
Verify

This creates the reference path.

Without a clear expected path, there is nothing reliable to compare against actual behavior.

3. Map the Observed Execution

Record what actually happened at each stage.

PBRCIM Logic-Map allows the investigation to be broken into individual stages.

Example:

Stage	Observed Behavior
Commit	Trigger received
Build	Completed successfully
Test	Passed
Deploy	Step skipped
Verify	Previous version still running

This is where the expected path and the observed path begin to become comparable.

4. Identify the Divergence

Compare both paths stage by stage.

Expected:


Stage 1 → Stage 2 → Stage 3 → Stage 4 → Expected Result




Actual:


Stage 1 → Stage 2 → Divergence → Unexpected Result

The objective is not to inspect every part of the system forever.

The objective is to locate the first meaningful point where expected behavior and observed behavior stopped matching.

That point becomes the primary area for root cause analysis.

5. Compare Working and Broken Paths

A working execution path can reveal information that a broken path cannot.

PBRCIM Logic-Map provides separate fields for comparing both.

Example:

WORKING


Auth
  ↓
Fetch
  ↓
Process
  ↓
Respond
BROKEN


Auth
  ↓
Fetch
  ↓
Timeout

The divergence becomes visible:

Expected:
Auth → Fetch → Process → Respond


Observed:
Auth → Fetch → Timeout

The investigation can now focus on the conditions surrounding the break.

6. Isolate the Root Cause

Once the divergence point is known, trace the conditions that produced it.

Possible areas include:
- Upstream inputs
- Downstream effects
- Environment differences
- Configuration values
- Dependency behavior
- Conditional logic
- State transitions

The root cause should explain why the execution path diverged.

Not merely what the visible failure looked like.

7. Record the Corrective Action

Document the change required to restore expected behavior.

A useful corrective action should answer:
- What was changed?
- Why was it changed?
- What behavior should the change restore?

The goal is to fix the actual divergence.
Not apply unrelated changes until the failure disappears.

8. Add Prevention and Verification

The investigation does not end when the immediate issue is fixed.

PBRCIM Logic-Map also records:
- Prevention strategy
- Audit guidance
- Verification results

This turns the investigation into a reusable diagnostic record.
The generated report can then document the complete chain from observed behavior to root cause and verification.

Representative Investigation Areas
CI/CD Failure

A deployment step may be skipped even though earlier stages pass.
Possible investigation areas:
- Branch conditions
- Workflow triggers
- Environment rules
- Deployment permissions
- Conditional execution logic
The expected path can be compared directly against the observed workflow.

API Timeout

An API chain may fail intermittently under load.
Possible investigation areas:
- Retry behavior
- Connection limits
- Upstream latency
- Timeouts
- Concurrency
- Queue pressure
The failure may not exist during ordinary testing.
PBRCIM helps compare the successful execution path with the path observed during the failure.

Database Migration Failure

A migration may complete without an obvious error while records are missing or inconsistent.
Possible investigation areas:
- Timestamp handling
- Schema differences
- Mapping logic
- Delta queries
- Transaction boundaries
The investigation focuses on where the expected data flow diverged from the actual result.

Frontend Interaction Failure

A button may appear functional but produce no response.
Possible investigation areas:
- Event binding
- DOM selectors
- Dynamic rendering
- State conditions
- Handler registration
The visual state may look correct while the execution path behind the interface is broken.

Generated Root Cause Report

PBRCIM Logic-Map generates a structured Markdown report from the investigation.

The report records:

System
Analyst
Date


1. Observed Behavior
2. Expected Behavior Flow
3. Divergence Analysis
4. Path Comparison
5. Root Cause
6. Corrective Action
7. Prevention Strategy
8. Audit Guidance
9. Verification

Stage-by-stage observations are also generated as a Markdown table.

This makes it possible to preserve an investigation as a portable audit record.

The report can be copied to the clipboard or downloaded as a .md file.

Browser-Based and Self-Contained

PBRCIM Logic-Map runs in the browser.

The investigation state is saved locally during use so work can be retained between interactions.
Core capabilities include:
- Structured multi-step investigation
- Expandable investigation sections
- Dynamic stage rows
- Stage-by-stage observation mapping
- Expected versus observed comparison
- Working versus broken path analysis
- Root cause documentation
- Corrective action tracking
- Prevention and audit guidance
- Verification recording
- Automatic local state saving
- Markdown report generation
- Clipboard report export
- .md report download
- Clear and reset controls
- Responsive browser interface
No server-side diagnostic pipeline is required for the core workflow.

Relationship to PBRCIM

PBRCIM Logic-Map is a practical implementation of the Pattern-Based Root Cause Isolation Model.

The framework provides the diagnostic approach.

Logic-Map provides the workspace for applying it manually.

The basic reasoning model is:

Expected Behavior
        │
        ▼
Execution Path
        │
        ▼
Observed Behavior
        │
        ▼
Compare
        │
        ▼
Identify Divergence
        │
        ▼
Trace Conditions
        │
        ▼
Root Cause
        │
        ▼
Corrective Action
        │
        ▼
Verification

The process is language-agnostic and tool-independent.

PBRCIM does not replace logs, debuggers, traces, tests, or monitoring tools.

It provides another layer of investigation when those tools show activity but do not clearly explain why the system behaved differently from what was intended.

PBRCIM Ecosystem
- PBRCIM Framework
  https://cursorlordsystems.com/pbrcim
- PBRCIM Diagnosis Engine
  https://cursorlordsystems.com/diagnosis-engine
- PBRCIM Logic-Map
  https://cursorlordsystems.com/pbrcim-logicmap
- PBRCIM Evaluation Dataset for LLM Code Reasoners
  Available from CursorLord Systems.
The Diagnosis Engine is designed to analyze system logs and failure patterns.

PBRCIM Logic-Map supports structured manual investigation.

Both are built around the same central principle:

Define what should happen. Trace what actually happens. Find where the two diverge.

Project Status
PBRCIM Logic-Map is an active project within the PBRCIM diagnostic ecosystem.
The tool is part of the broader work around deterministic software diagnostics, execution-path analysis, and structured root cause isolation.

Authorship and Attribution
PBRCIM stands for Pattern-Based Root Cause Isolation Model.
The model was developed and refined by Usenobong Jonah during applied diagnostic work on complex software and execution failures.
PBRCIM Logic-Map was built as a practical workspace for applying the model to real investigations.
The framework and related tools are developed under CursorLord Systems.
If referencing PBRCIM, please provide appropriate attribution.

Contact
For collaboration or technical enquiries:

CursorLord Systems

https://cursorlordsystems.com

contact@cursorlordsystems.com

© 2023–Present CursorLord Systems
