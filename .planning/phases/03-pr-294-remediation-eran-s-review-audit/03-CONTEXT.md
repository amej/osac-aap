# Phase 03: PR #294 Remediation (Eran's Review Audit) - Context

**Gathered:** 2026-05-13
**Status:** Ready for planning

<domain>
## Phase Boundary

Remediate 7 specific security, maintainability, logic, and hygiene issues identified by @eranco74 in PR #294 code review before merge. This phase addresses review feedback for Windows VM support in the `ocp_virt_vm` role, ensuring production-ready quality standards are met.

</domain>

<decisions>
## Implementation Decisions

### SEC-01: Sysprep Secret Storage
- **D-01:** Create unattend.xml Secret in the same namespace where the VirtualMachine will be created (matches current ConfigMap pattern, minimal code change)
- **D-02:** Delete the old sysprep ConfigMap resource entirely (Secrets are not backward compatible with ConfigMaps, clean deletion is clearer)
- **D-03:** Rename Secret to clarify it's secret data — append `-secret` suffix to the name
- **D-04:** Store unattend.xml using `stringData` field (Kubernetes auto-encodes to base64, easier to template and debug)

### MAINT-01: Jinja2 Template Extraction
- **D-05:** Place unattend.xml template at `templates/unattend.xml.j2` (standard Ansible role convention)
- **D-06:** Minimal parameterization — only current variables: `vm_sysprep_admin_password`, `vm_hostname`, `vm_timezone` (keeps template focused on current usage)
- **D-07:** Include brief XML section header comments for major sections (Administrator setup, Hostname, Timezone) — makes template maintainable without bloat
- **D-08:** Use `ansible.builtin.template` module with `src: unattend.xml.j2` to render and inject into Secret (standard template rendering, clear and direct)

### TEST-01: Test Error Message Validation
- **D-09:** Validate error contains key substring: `'spec.image.sourceRef' OR 'Windows'` (catches validation failure without being brittle to exact wording)
- **D-10:** Capture error message from `ansible_failed_result.msg` (standard rescue-supplied variable for task failure messages)
- **D-11:** Include actual error message in assertion `fail_msg` (makes test failures easy to diagnose)
- **D-12:** Only set `windows_missing_image_failed: true` if error matches expected pattern — unrelated errors should fail the test, not pass with the wrong flag

### HYG-01: Commit History Squashing
- **D-13:** Group 36 commits logically into 3 commits: 1) core Windows VM feature, 2) bug fixes and refinements, 3) integration tests (mirrors development phases)
- **D-14:** Use conventional commit format: `feat:`, `fix:`, `test:` (matches osac-aap git log patterns)
- **D-15:** Write fresh concise commit messages based on grouped work — do not preserve original commit messages (avoids WIP/fix-the-fix noise)

### Remaining Items (Not Discussed)
- **DOC-01:** Restore `default:` description for `exposed_ports` in `meta/argument_specs.yaml` — straightforward restoration
- **LOGIC-01:** Remove redundant `failed_when` guards on LB Service delete — `kubernetes.core.k8s` with `state: absent` handles missing resources gracefully
- **CONS-01:** Verify both Linux and Windows VM spec blocks include both `domain.memory.guest` AND `domain.resources.requests.memory` — standard verification task

</decisions>

<canonical_refs>
## Canonical References

**Downstream agents MUST read these before planning or implementing.**

### Code Review Feedback
- `.planning/PR_REVIEW_FEEDBACK.md` — Eran's detailed review with 7 specific issues and recommendations

### Role Implementation
- `collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tasks/create_secrets.yaml` — Current sysprep ConfigMap creation logic (to be refactored)
- `collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tasks/create_build_spec.yaml` — VM spec building with Linux/Windows branches (memory consistency check)
- `collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tests/test.yml` — Integration test with rescue block (Test 4)
- `collections/ansible_collections/osac/templates/roles/ocp_virt_vm/meta/argument_specs.yaml` — Role parameter specifications (exposed_ports default)
- `collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tasks/delete_resources.yaml` — LB Service deletion with failed_when guards

### Codebase Conventions
- `.planning/codebase/CONVENTIONS.md` — Ansible naming conventions, YAML style, module FQCN patterns
- `.planning/codebase/TESTING.md` — Integration test structure, assertion patterns, rescue block conventions
- `.planning/codebase/STRUCTURE.md` — Role directory layout, template file locations

</canonical_refs>

<code_context>
## Existing Code Insights

### Reusable Assets
- **Jinja2 templates in `templates/` directories:** Standard Ansible role convention for extracting inline content to template files
- **ansible.builtin.template module:** Standard pattern for rendering Jinja2 templates into Kubernetes resources
- **kubernetes.core.k8s with stringData:** Used throughout codebase for creating Secrets from template-rendered content
- **Integration test rescue blocks:** Existing patterns in `tests/test.yml` for validating expected failures

### Established Patterns
- **Secret vs ConfigMap:** Sensitive data (passwords, keys) should use Kubernetes Secrets, not ConfigMaps
- **Template parameterization:** Keep templates minimal — only parameterize what's actually used
- **Test assertions:** Use `ansible.builtin.assert` with specific substring checks, not exact string matches (resilient to wording changes)
- **Commit squashing:** osac-aap uses conventional commits (`feat:`, `fix:`, `test:`) with descriptive messages

### Integration Points
- **Secret references in VirtualMachine spec:** Current code creates a ConfigMap and references it; the Secret must be referenced the same way with `secretRef` instead of `configMapRef`
- **Test fixture validation:** Test 4 validates missing Windows image requirement — rescue block must verify the specific validation error
- **Git history for PR:** Branch `run-windows-vm` has 36 commits to be squashed before merge

</code_context>

<specifics>
## Specific Ideas

No specific requirements — decisions follow established Ansible and Kubernetes best practices from the codebase conventions.

</specifics>

<deferred>
## Deferred Ideas

None — discussion stayed within phase scope (remediating 7 specific PR review findings)

</deferred>

---

*Phase: 03-pr-294-remediation-eran-s-review-audit*
*Context gathered: 2026-05-13*
