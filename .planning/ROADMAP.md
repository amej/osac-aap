# Roadmap: Windows VM Provisioning for OpenShift Virtualization

## Milestones

- ✅ **v1.0 Windows VM Provisioning** — Phase 1 (shipped 2026-04-29) — [archive](milestones/v1.0-ROADMAP.md)

## Phases

<details>
<summary>✅ v1.0 Windows VM Provisioning (Phase 1) — SHIPPED 2026-04-29</summary>

- [x] Phase 1: Windows VM Provisioning (3/3 plans) — completed 2026-04-28

### Phase 1: Windows VM Provisioning
**Goal**: Ansible template role can create Windows VMs with proper configuration and networking
**Depends on**: Nothing (first phase)
**Requirements**: PROV-01, PROV-02, PROV-03, PROV-04, PROV-05
**Success Criteria** (what must be TRUE):
  1. Template creates VirtualMachine CR with Windows-optimized configuration (virtio-win, Hyper-V enlightenments)
  2. VM boots from OCI container image using DataVolume registry source
  3. VM receives specified CPU, memory, and disk sizing from ComputeInstance spec
  4. VM connects to specified VirtualNetwork and Subnet
  5. Windows hostname is set from ComputeInstance metadata
**Plans**: 3 (complete)

### ~~Phase 2: VM Verification~~ (REMOVED)
**Reason**: Basic VM verification (Ready state wait, ComputeInstance annotation) is already implemented in Phase 1's `create_wait_annotate.yaml`, matching the Linux `ocp_virt_vm` pattern. Deeper checks (ping, RDP port, guest agent, VNC console) deferred to v2 milestone.
</details>
### Phase 3: PR #294 Remediation (Eran's Review Audit)
**Goal**: Address 7 specific security, maintainability, and logic issues identified by @eranco74.
**Depends on**: Phase 1
**Requirements**:
  - [ ] **SEC-01**: Refactor sysprep `unattend.xml` storage from a Kubernetes ConfigMap to a **Secret** to protect the plaintext `vm_sysprep_admin_password`.
  - [ ] **MAINT-01**: Extract the ~50 lines of inline XML from `tasks/create_secrets.yaml` and move it to a dedicated Jinja2 template in `templates/unattend.xml.j2`.
  - [ ] **TEST-01**: Update the `tests/test.yml` (Test 4) rescue block to capture `ansible_failed_result.msg` and assert it specifically contains "spec.image.sourceRef" or "Windows".
  - [ ] **HYG-01**: Squash the 36-commit history into a logical, clean set of commits before the final merge. **[DEFERRED: Awaiting @eranco74 acceptance of current changes]**
  - [ ] **DOC-01**: Restore the missing `default:` description for `exposed_ports` in `meta/argument_specs.yaml` so the runtime default is visible in `ansible-doc`.
  - [ ] **LOGIC-01**: Remove redundant/brittle `failed_when` guards in the LB Service deletion task; rely on `kubernetes.core.k8s` with `state: absent` to handle missing resources natively.
  - [ ] **CONS-01**: Verify that both Windows and Linux spec blocks in `tasks/create_build_spec.yaml` include both `domain.memory.guest` AND `domain.resources.requests.memory`.

**Success Criteria** (Definition of Done):
  1. **Security**: No `ConfigMap` resources created by the role contain sensitive `unattend.xml` data or plaintext passwords.
  2. **Security**: The `unattend.xml` is successfully stored as a Kubernetes **Secret**.
  3. **Refactor**: `tasks/create_secrets.yaml` contains no inline XML and correctly uses the Jinja2 template hook.
  4. **Validation**: Integration tests fail if an unrelated error occurs during Windows validation instead of masking it with a "false pass".
  5. **Logic**: Service deletion logic is idempotent and utilizes native module behavior without complex conditional guards.
  6. **Standardization**: `vm_template_spec` consistently specifies both guest-visible memory and scheduling requests across all OS families.
  7. **Documentation**: `ansible-doc` accurately reflects the default values for `exposed_ports`.
  8. **Hygiene**: The PR git history is clean and free of "fix-the-fix" or incremental "WIP" commits.

**Plans**: 4 plans in 2 waves (3 complete, 1 deferred)

Plans:
- [x] 03-01-PLAN.md — Security & maintainability (SEC-01, MAINT-01): ConfigMap→Secret + XML extraction
- [x] 03-02-PLAN.md — Testing & documentation (TEST-01, DOC-01, LOGIC-01): Test validation + docs + idempotent delete
- [x] 03-03-PLAN.md — Consistency verification (CONS-01): Memory field audit
- [ ] 03-04-PLAN.md — Git hygiene (HYG-01): Squash commit history **[DEFERRED: Awaiting @eranco74 acceptance]**

## Progress

| Phase | Milestone | Plans Complete | Status | Completed |
|-------|-----------|----------------|--------|-----------|
| 1. Windows VM Provisioning | v1.0 | 3/3 | Complete | 2026-04-28 |
| 3. PR #294 Remediation | v1.0 | 3/3 (1 deferred) | Awaiting Feedback | 2026-05-13 |
