---
phase: 03
plan: 03-01
subsystem: ocp_virt_vm
tags: [security, maintainability, templates]
dependencies: []
tech_stack: [ansible, jinja2, kubernetes]
key-files:
  created:
    - collections/ansible_collections/osac/templates/roles/ocp_virt_vm/templates/unattend.xml.j2
  modified:
    - collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tasks/create_secrets.yaml
  deleted: []
decisions:
  - "Use Secret instead of ConfigMap for sysprep data to properly handle sensitive credentials"
  - "Extract inline XML to Jinja2 template for maintainability and reusability"
metrics:
  lines_added: 85
  lines_removed: 32
  files_changed: 2
  commits: 3
---

# 03-01: Migrate Sysprep Storage

## Summary

Migrated Windows sysprep unattend.xml storage from ConfigMap to Secret and extracted inline XML to a Jinja2 template. This change improves security by using the appropriate Kubernetes resource type for sensitive data and enhances maintainability by separating configuration logic from task definitions.

## Tasks Completed

| Task | Description | Status | Commit |
|------|-------------|--------|--------|
| STOR-01 | Extract inline unattend.xml to Jinja2 template | ✓ | 41bc6006 |
| STOR-02 | Update create_secrets.yaml to use Secret | ✓ | a9bbbdf3 |
| STOR-03 | Update VirtualMachine volume mount to reference Secret | ✓ | 6f3d4210 |
| STOR-04 | Verify template rendering and Secret creation | ✓ | 6f3d4210 |

## Deviations

None.

## Technical Implementation

### Created Jinja2 Template
- File: `templates/unattend.xml.j2`
- Renders Windows sysprep unattend.xml with variables for:
  - Computer name (`{{ windows_computer_name }}`)
  - Administrator password (`{{ windows_admin_password }}`)
- Follows Windows Answer File schema for unattended setup

### Refactored Secret Creation
- Updated `tasks/create_secrets.yaml` to create Secret instead of ConfigMap
- Secret name: `{{ vm_name }}-sysprep`
- Data key: `unattend.xml` (base64-encoded by Kubernetes)
- Template rendered inline using `template` lookup

### Updated Volume Mount
- Changed VirtualMachine spec to use `cloudInitNoCloud.secretRef` instead of `cloudInitConfigDrive.userData`
- Properly references the Secret created in earlier task
- Maintains same functionality with improved security posture

## Verification

- ✓ Template file created and syntactically valid
- ✓ Secret creation task uses correct Jinja2 template lookup
- ✓ VirtualMachine spec correctly references Secret
- ✓ No hardcoded credentials remain in task files

## Requirements Resolved

N/A (remediation work, no explicit requirements)

## Success Criteria

- [x] Inline XML extracted to separate Jinja2 template
- [x] create_secrets.yaml uses Secret instead of ConfigMap
- [x] VirtualMachine spec updated to mount Secret
- [x] Template variables properly parameterized
- [x] All commits atomic and signed

## Self-Check: PASSED

All tasks completed successfully. Changes improve security (Secret vs ConfigMap), maintainability (template separation), and align with Kubernetes best practices for sensitive data handling.
