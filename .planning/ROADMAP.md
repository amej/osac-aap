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

## Progress

| Phase | Milestone | Plans Complete | Status | Completed |
|-------|-----------|----------------|--------|-----------|
| 1. Windows VM Provisioning | v1.0 | 3/3 | Complete | 2026-04-28 |
