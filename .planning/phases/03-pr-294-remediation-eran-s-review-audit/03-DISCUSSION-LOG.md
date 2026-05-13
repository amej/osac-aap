# Phase 03: PR #294 Remediation (Eran's Review Audit) - Discussion Log

> **Audit trail only.** Do not use as input to planning, research, or execution agents.
> Decisions are captured in CONTEXT.md — this log preserves the alternatives considered.

**Date:** 2026-05-13
**Phase:** 03-pr-294-remediation-eran-s-review-audit
**Areas discussed:** Secret storage strategy, Jinja2 template design, Test error validation, Commit history squashing

---

## Secret Storage Strategy (SEC-01)

### Where should the unattend.xml Secret be created?

| Option | Description | Selected |
|--------|-------------|----------|
| Same namespace as VM | Create Secret in the same namespace where the VirtualMachine will be created — matches the current ConfigMap pattern, minimal code change. | ✓ |
| ComputeInstance namespace | Create Secret in the namespace where the ComputeInstance CR exists — requires cross-namespace Secret reference. | |

**User's choice:** Same namespace as VM (Recommended)

### What should happen to the old sysprep ConfigMap?

| Option | Description | Selected |
|--------|-------------|----------|
| Delete it | Remove the ConfigMap resource entirely — Secrets are not backward compatible with ConfigMaps, so clean deletion is clearer. | ✓ |
| Leave it but stop using it | Keep the ConfigMap creation code but only create/use the Secret — adds complexity without benefit. | |

**User's choice:** Delete it (Recommended)

### How should the Secret be named?

| Option | Description | Selected |
|--------|-------------|----------|
| Keep same name as ConfigMap | Use the existing name pattern — simplest migration, but resource type change from ConfigMap to Secret. | |
| Rename to clarify it's a Secret | Use a name that makes it clear it's secret data (e.g., append -secret suffix) — clearer intent. | ✓ |

**User's choice:** Rename to clarify it's a Secret (Recommended)

### How should the unattend.xml be stored in the Secret?

| Option | Description | Selected |
|--------|-------------|----------|
| stringData | Use stringData field — Kubernetes auto-encodes to base64, easier to template and debug. | ✓ |
| data with explicit base64 | Manually base64 encode the XML before storing — more verbose, harder to maintain. | |

**User's choice:** stringData (Recommended)

---

## Jinja2 Template Design (MAINT-01)

### Where should the unattend.xml template file be placed?

| Option | Description | Selected |
|--------|-------------|----------|
| templates/unattend.xml.j2 | Standard Ansible role convention — templates/ directory at role root, matches existing patterns. | ✓ |
| templates/sysprep/unattend.xml.j2 | Nested under sysprep subdirectory — clearer organization if we add more sysprep templates later. | |

**User's choice:** templates/unattend.xml.j2 (Recommended)

### How much should the unattend.xml template be parameterized?

| Option | Description | Selected |
|--------|-------------|----------|
| Minimal - only variables used today | Only parameterize vm_sysprep_admin_password, vm_hostname, vm_timezone — matches current usage, keeps template focused. | ✓ |
| Extensible - add common customization points | Add parameters for common Windows setup options (keyboard layout, locale, domain join) even if not used yet — more flexible but adds complexity. | |

**User's choice:** Minimal - only variables used today (Recommended)

### Should the template include XML comments explaining sections?

| Option | Description | Selected |
|--------|-------------|----------|
| Yes - brief section headers | Add short XML comments marking major sections (Administrator setup, Hostname, Timezone) — makes template more maintainable without bloat. | ✓ |
| No - keep it minimal | No comments — the XML element names are self-explanatory. | |

**User's choice:** Yes - brief section headers (Recommended)

### How should the task file reference the template?

| Option | Description | Selected |
|--------|-------------|----------|
| template module with src | Use ansible.builtin.template module with src: unattend.xml.j2 — standard template rendering, clear and direct. | ✓ |
| lookup('template') in stringData | Use lookup plugin inline in the Secret definition — more compact but harder to debug. | |

**User's choice:** template module with src (Recommended)

---

## Test Error Validation (TEST-01)

### What error message pattern should the test validate?

| Option | Description | Selected |
|--------|-------------|----------|
| Key substring | Check for 'spec.image.sourceRef' OR 'Windows' in the error message — catches the validation failure without being brittle to exact wording. | ✓ |
| Exact message match | Validate the full error message text — more precise but breaks if error wording changes. | |

**User's choice:** Key substring (Recommended)

### Which Ansible variable should capture the error message?

| Option | Description | Selected |
|--------|-------------|----------|
| ansible_failed_result.msg | Standard rescue-supplied variable for task failure messages — most reliable source. | ✓ |
| ansible_failed_result.stderr | Standard error output — might be empty if error is in msg. | |
| Both msg and stderr | Check both fields — more robust but adds complexity. | |

**User's choice:** ansible_failed_result.msg (Recommended)

### What should the test assertion failure message say?

| Option | Description | Selected |
|--------|-------------|----------|
| Show actual error | Include the actual error message in fail_msg — makes test failures easy to diagnose. | ✓ |
| Generic message | Just say 'Validation failed for unexpected reason' — shorter but less helpful. | |

**User's choice:** Show actual error (Recommended)

### How should the test handle unrelated errors?

| Option | Description | Selected |
|--------|-------------|----------|
| Fail test if error doesn't match | Only set windows_missing_image_failed: true if error contains expected substring — unrelated errors fail the test, not the rescue block. | ✓ |
| Set flag for any error | Keep current behavior — any error sets windows_missing_image_failed: true, simpler but masks problems. | |

**User's choice:** Fail test if error doesn't match (Recommended)

---

## Commit History Squashing (HYG-01)

### How should the 36 commits be squashed?

| Option | Description | Selected |
|--------|-------------|----------|
| Single atomic commit | Squash all 36 commits into one: 'feat: add Windows VM support to ocp_virt_vm' — clean history, matches project convention for feature PRs. | |
| Logical grouping (3-4 commits) | Preserve logical phases: 1) core feature, 2) fixes, 3) tests — more context but adds complexity. | ✓ |

**User's choice:** Logical grouping (3-4 commits)

### How should commits be grouped logically?

| Option | Description | Selected |
|--------|-------------|----------|
| Feature/Fixes/Tests | 3 commits: 1) core Windows VM feature, 2) bug fixes and refinements, 3) integration tests — mirrors development phases. | ✓ |
| By component | Group by what they touch: 1) role tasks, 2) fixtures/tests, 3) docs — clearer file-level organization. | |
| Chronological phases | Group by when they were added: 1) initial implementation, 2) review feedback, 3) final polish — tells the story. | |

**User's choice:** Feature/Fixes/Tests (Recommended)

### What commit message format should be used?

| Option | Description | Selected |
|--------|-------------|----------|
| Conventional Commits | Use conventional format: 'feat: description', 'fix: description', 'test: description' — matches osac-aap patterns. | ✓ |
| Descriptive without prefix | Just descriptive messages: 'Add Windows VM support', 'Fix sysprep issues' — simpler, less formal. | |

**User's choice:** Conventional Commits (Recommended)

### Should any original commit messages be preserved in the new commits?

| Option | Description | Selected |
|--------|-------------|----------|
| No - write fresh messages | Write new concise commit messages based on the grouped work — cleaner, avoids WIP/fix-the-fix noise. | ✓ |
| List key commits in body | Reference important original commits in the commit body — preserves context but adds length. | |

**User's choice:** No - write fresh messages (Recommended)

---

## Claude's Discretion

None — all areas had explicit user decisions.

## Deferred Ideas

None — discussion stayed within phase scope.
