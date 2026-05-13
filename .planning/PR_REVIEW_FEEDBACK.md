author:	openshift-ci
association:	none
edited:	false
status:	none
--
[APPROVALNOTIFIER] This PR is **NOT APPROVED**

This pull-request has been approved by: *<a href="https://github.com/osac-project/osac-aap/pull/294#" title="Author self-approved">amej</a>*
**Once this PR has been reviewed and has the lgtm label**, please assign [larsks](https://github.com/larsks) for approval. For more information see [the Code Review Process](https://git.k8s.io/community/contributors/guide/owners.md#the-code-review-process).

The full list of commands accepted by this bot can be found [here](https://go.k8s.io/bot-commands?repo=osac-project%2Fosac-aap).

<details open>
Needs approval from an approver in each of these files:

- **[OWNERS](https://github.com/osac-project/osac-aap/blob/main/OWNERS)**

Approvers can indicate their approval by writing `/approve` in a comment
Approvers can cancel approval by writing `/approve cancel` in a comment
</details>
<!-- META={"approvers":["larsks"]} -->
--
author:	coderabbitai
association:	none
edited:	true
status:	none
--
<!-- This is an auto-generated comment: summarize by coderabbit.ai -->
<!-- This is an auto-generated comment: rate limited by coderabbit.ai -->

> [!WARNING]
> ## Rate limit exceeded
> 
> `@amej` has exceeded the limit for the number of commits that can be reviewed per hour. Please wait **45 minutes and 58 seconds** before requesting another review.
> 
> You’ve run out of usage credits. Purchase more in the [billing tab](https://app.coderabbit.ai/settings/subscription?tab=usage&tenantId=0b528585-12d0-4626-abb1-1624e9f669ad).
> 
> <details>
> <summary>⌛ How to resolve this issue?</summary>
> 
> After the wait time has elapsed, a review can be triggered using the `@coderabbitai review` command as a PR comment. Alternatively, push new commits to this PR.
> 
> We recommend that you space out your commits to avoid hitting the rate limit.
> 
> </details>
> 
> 
> <details>
> <summary>🚦 How do rate limits work?</summary>
> 
> CodeRabbit enforces hourly rate limits for each developer per organization.
> 
> Our paid plans have higher rate limits than the trial, open-source and free plans. In all cases, we re-allow further reviews after a brief timeout.
> 
> Please see our [FAQ](https://docs.coderabbit.ai/faq) for further information.
> 
> </details>
> 
> <details>
> <summary>ℹ️ Review info</summary>
> 
> <details>
> <summary>⚙️ Run configuration</summary>
> 
> **Configuration used**: Organization UI
> 
> **Review profile**: CHILL
> 
> **Plan**: Pro
> 
> **Run ID**: `f7cb0cf6-1e46-49e2-8d1a-75f091db454b`
> 
> </details>
> 
> <details>
> <summary>📥 Commits</summary>
> 
> Reviewing files that changed from the base of the PR and between b638f1aa726344eaf958ece83bbd22f892a042a2 and b2f9798f66b9f358cb8640286c9ee14c25ef723a.
> 
> </details>
> 
> <details>
> <summary>📒 Files selected for processing (1)</summary>
> 
> * `tests/integration/fixtures/computeinstance-windows-test.yaml`
> 
> </details>
> 
> </details>

<!-- end of auto-generated comment: rate limited by coderabbit.ai -->

<!-- walkthrough_start -->

## Walkthrough

This PR extends the ocp_virt_vm Ansible template role with Windows VM support: it adds guest OS family inference (annotation or image-ref heuristic), Windows-specific defaults and validations (including required image.sourceRef and sysprep password rules), OS-conditional spec building (EFI/Hyper-V tweaks), sysprep/Unattend.xml handling, adjusted wait/delete flows, and tests/fixtures plus README updates.

## Estimated code review effort

🎯 3 (Moderate) | ⏱️ ~25 minutes

## Possibly related PRs

- [osac-project/osac-aap#232](https://github.com/osac-project/osac-aap/pull/232): Both modify the ocp_virt_vm template's build-spec logic and argument specs to conditionally append GPU passthrough patches into vm_template_spec.
- [osac-project/osac-aap#246](https://github.com/osac-project/osac-aap/pull/246): Both touch ocp_virt_vm defaults, metadata, and argument_specs changes for template parameter handling.
- [osac-project/osac-aap#220](https://github.com/osac-project/osac-aap/pull/220): Both refactor ocp_virt_vm template steps and introduce platform-specific handling and workflow hooks.

## Suggested labels

`lgtm`, `jira/valid-reference`, `approved`

## Suggested reviewers

- adriengentil
- tzumainn
- akshaynadkarni

<!-- walkthrough_end -->

<!-- pre_merge_checks_walkthrough_start -->

<details>
<summary>🚥 Pre-merge checks | ✅ 5</summary>

<details>
<summary>✅ Passed checks (5 passed)</summary>

|         Check name         | Status   | Explanation                                                                                                                                                                                              |
| :------------------------: | :------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|      Description Check     | ✅ Passed | Check skipped - CodeRabbit’s high-level summary is enabled.                                                                                                                                              |
|         Title check        | ✅ Passed | The title accurately summarizes the primary feature: adding Windows VM support to the ocp_virt_vm template role. It is specific, concise, and directly reflects the main objective documented in the PR. |
|     Docstring Coverage     | ✅ Passed | No functions found in the changed files to evaluate docstring coverage. Skipping docstring coverage check.                                                                                               |
|     Linked Issues check    | ✅ Passed | Check skipped because no linked issues were found for this pull request.                                                                                                                                 |
| Out of Scope Changes check | ✅ Passed | Check skipped because no linked issues were found for this pull request.                                                                                                                                 |

</details>

<sub>✏️ Tip: You can configure your own custom pre-merge checks in the settings.</sub>

</details>

<!-- pre_merge_checks_walkthrough_end -->

<!-- finishing_touch_checkbox_start -->

<details>
<summary>✨ Finishing Touches</summary>

<details>
<summary>🧪 Generate unit tests (beta)</summary>

- [ ] <!-- {"checkboxId": "f47ac10b-58cc-4372-a567-0e02b2c3d479", "radioGroupId": "utg-output-choice-group-unknown_comment_id"} -->   Create PR with unit tests

</details>

</details>

<!-- finishing_touch_checkbox_end -->
<!-- announcements_start -->

> [!TIP]
> <details>
> <summary>💬 Introducing Slack Agent: The best way for teams to turn conversations into code.</summary>
> 
> [Slack Agent](https://www.coderabbit.ai/agent) is built on CodeRabbit's deep understanding of your code, so your team can collaborate across the entire SDLC without losing context.
> 
> - Generate code and open pull requests
> - Plan features and break down work
> - Investigate incidents and troubleshoot customer tickets together
> - Automate recurring tasks and respond to alerts with triggers
> - Summarize progress and report instantly
> 
> Built for teams:
> 
> - **Shared memory** across your entire org—no repeating context
> - **Per-thread sandboxes** to safely plan and execute work
> - **Governance built-in**—scoped access, auditability, and budget controls
> 
> One agent for your entire SDLC. Right inside Slack.
> 
> 👉 [Get started](https://agent.coderabbit.ai/)
> 
> </details>

<!-- announcements_end -->

<!-- tips_start -->

---

Thanks for using [CodeRabbit](https://coderabbit.ai?utm_source=oss&utm_medium=github&utm_campaign=osac-project/osac-aap&utm_content=294)! It's free for OSS, and your support helps us grow. If you like it, consider giving us a shout-out.

<details>
<summary>❤️ Share</summary>

- [X](https://twitter.com/intent/tweet?text=I%20just%20used%20%40coderabbitai%20for%20my%20code%20review%2C%20and%20it%27s%20fantastic%21%20It%27s%20free%20for%20OSS%20and%20offers%20a%20free%20trial%20for%20the%20proprietary%20code.%20Check%20it%20out%3A&url=https%3A//coderabbit.ai)
- [Mastodon](https://mastodon.social/share?text=I%20just%20used%20%40coderabbitai%20for%20my%20code%20review%2C%20and%20it%27s%20fantastic%21%20It%27s%20free%20for%20OSS%20and%20offers%20a%20free%20trial%20for%20the%20proprietary%20code.%20Check%20it%20out%3A%20https%3A%2F%2Fcoderabbit.ai)
- [Reddit](https://www.reddit.com/submit?title=Great%20tool%20for%20code%20review%20-%20CodeRabbit&text=I%20just%20used%20CodeRabbit%20for%20my%20code%20review%2C%20and%20it%27s%20fantastic%21%20It%27s%20free%20for%20OSS%20and%20offers%20a%20free%20trial%20for%20proprietary%20code.%20Check%20it%20out%3A%20https%3A//coderabbit.ai)
- [LinkedIn](https://www.linkedin.com/sharing/share-offsite/?url=https%3A%2F%2Fcoderabbit.ai&mini=true&title=Great%20tool%20for%20code%20review%20-%20CodeRabbit&summary=I%20just%20used%20CodeRabbit%20for%20my%20code%20review%2C%20and%20it%27s%20fantastic%21%20It%27s%20free%20for%20OSS%20and%20offers%20a%20free%20trial%20for%20proprietary%20code)

</details>


<sub>Comment `@coderabbitai help` to get the list of available commands and usage tips.</sub>

<!-- tips_end -->

<!-- internal state start -->


<!-- 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 -->

<!-- internal state end -->
--
author:	coderabbitai
association:	none
edited:	false
status:	commented
--
**Actionable comments posted: 5**

> [!CAUTION]
> Some comments are outside the diff and can’t be posted inline due to platform limitations.
> 
> 
> 
> <details>
> <summary>⚠️ Outside diff range comments (2)</summary><blockquote>
> 
> <details>
> <summary>collections/ansible_collections/osac/templates/roles/ocp_virt_vm/meta/osac.yaml (1)</summary><blockquote>
> 
> `10-12`: _⚠️ Potential issue_ | _🟠 Major_ | _⚡ Quick win_
> 
> **Add required `meta/osac.yaml` keys for template roles.**
> 
> Line 11 defines `template_type`, but `implementation_strategy` and `capabilities` are missing. Please add them to satisfy template metadata requirements.
> 
>  
> 
> As per coding guidelines "`collections/ansible_collections/osac/templates/roles/*/meta/osac.yaml`: Add `meta/osac.yaml` with `implementation_strategy`, `template_type`, and `capabilities` in template roles".
> 
> <details>
> <summary>🤖 Prompt for AI Agents</summary>
> 
> ```
> Verify each finding against current code. Fix only still-valid issues, skip the
> rest with a brief reason, keep changes minimal, and validate.
> 
> In
> `@collections/ansible_collections/osac/templates/roles/ocp_virt_vm/meta/osac.yaml`
> around lines 10 - 12, The template meta file is missing required keys; update
> meta/osac.yaml for the ocp_virt_vm role to include implementation_strategy and
> capabilities alongside the existing template_type: add an
> implementation_strategy field (e.g., a strategy name or reference used by your
> framework) and a capabilities list/array describing what this compute_instance
> template supports (e.g., ["create","delete","update"] or the project-specific
> capability keys) so the file contains implementation_strategy, template_type,
> and capabilities entries to satisfy the template metadata contract.
> ```
> 
> </details>
> 
> </blockquote></details>
> <details>
> <summary>collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tasks/create_secrets.yaml (1)</summary><blockquote>
> 
> `104-110`: _⚠️ Potential issue_ | _🔴 Critical_ | _⚡ Quick win_
> 
> **Critical: Missing kubeconfig for cross-cluster Secret read**
> 
> The task reads a Secret from the `ComputeInstance` namespace (typically on the hub/orchestrator cluster) but doesn't specify a `kubeconfig` parameter. Meanwhile, line 122 uses `remote_cluster_kubeconfig` to write to the spoke cluster. This will fail when the ComputeInstance and VM target are on different clusters.
> 
> The PR summary mentions "kubeconfig handling for hub vs spoke secret reads" was fixed, but this read operation appears to lack the necessary kubeconfig specification.
> 
> 
> 
> 
> <details>
> <summary>🔧 Proposed fix to specify source cluster kubeconfig</summary>
> 
> If the ComputeInstance is always on the same cluster where the playbook runs (in-cluster), add explicit documentation:
> 
> ```diff
>     - name: Read user-data secret from ComputeInstance namespace
>       kubernetes.core.k8s_info:
> +       # Note: Reads from the hub/controller cluster (in-cluster auth) where ComputeInstance exists
> +       # Do NOT use remote_cluster_kubeconfig here - that targets the spoke cluster
>         api_version: v1
>         kind: Secret
> ```
> 
> Otherwise, if a hub kubeconfig variable exists, use it:
> 
> ```diff
>     - name: Read user-data secret from ComputeInstance namespace
>       kubernetes.core.k8s_info:
> +       kubeconfig: "{{ hub_cluster_kubeconfig | default(omit) }}"
>         api_version: v1
>         kind: Secret
> ```
> </details>
> 
> <details>
> <summary>🤖 Prompt for AI Agents</summary>
> 
> ```
> Verify each finding against current code. Fix only still-valid issues, skip the
> rest with a brief reason, keep changes minimal, and validate.
> 
> In
> `@collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tasks/create_secrets.yaml`
> around lines 104 - 110, The task "Read user-data secret from ComputeInstance
> namespace" is missing a kubeconfig so it will fail when the ComputeInstance
> secret lives on a different cluster than the VM target; update that
> kubernetes.core.k8s_info task to include the kubeconfig parameter pointing to
> the source/hub cluster kubeconfig (e.g., a variable like hub_kubeconfig or
> compute_instance_kubeconfig) rather than relying on the
> remote_cluster_kubeconfig used later for writes, and ensure the play passes that
> hub kubeconfig variable when the ComputeInstance is remote.
> ```
> 
> </details>
> 
> </blockquote></details>
> 
> </blockquote></details>

<details>
<summary>🧹 Nitpick comments (1)</summary><blockquote>

<details>
<summary>collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tests/test.yml (1)</summary><blockquote>

`175-183`: _⚡ Quick win_

**Strengthen test assertion by validating error message**

The rescue block sets `windows_missing_image_failed: true` for any failure, which could mask unexpected errors unrelated to the missing Windows image validation.




<details>
<summary>🧪 Proposed enhancement to validate the specific error message</summary>

```diff
         rescue:
-          - name: Record expected failure
+          - name: Record expected failure and verify error message
             ansible.builtin.set_fact:
               windows_missing_image_failed: true
+              validation_error: "{{ ansible_failed_result.msg | default('') }}"
+
+          - name: Verify failure was due to missing Windows image
+            ansible.builtin.assert:
+              that:
+                - "'spec.image.sourceRef' in validation_error or 'Windows' in validation_error"
+              fail_msg: "Validation failed for unexpected reason: {{ validation_error }}"
```
</details>

<details>
<summary>🤖 Prompt for AI Agents</summary>

```
Verify each finding against current code. Fix only still-valid issues, skip the
rest with a brief reason, keep changes minimal, and validate.

In
`@collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tests/test.yml`
around lines 175 - 183, The rescue currently sets windows_missing_image_failed:
true for any failure; change it to only set that fact when the failure message
matches the specific validation error from the create_validate task (use the
rescue-supplied ansible_failed_result.msg or ansible_failed_result.stderr) —
e.g., inside the rescue block check the error text (substring or regex) for the
known "missing Windows image" validation message before setting
windows_missing_image_failed so unrelated errors are not masked; reference the
include_role/tasks_from: create_validate.yaml and the variable
windows_missing_image_failed and use ansible_failed_result.msg in the
conditional.
```

</details>

</blockquote></details>

</blockquote></details>

<details>
<summary>🤖 Prompt for all review comments with AI agents</summary>

```
Verify each finding against current code. Fix only still-valid issues, skip the
rest with a brief reason, keep changes minimal, and validate.

Inline comments:
In
`@collections/ansible_collections/osac/templates/roles/ocp_virt_vm/defaults/main.yaml`:
- Line 15: The default plaintext weak password vm_sysprep_admin_password:
"123456" must be removed and replaced with validation: delete the insecure
default from defaults/main.yaml, make vm_sysprep_admin_password a required
variable, and add a validation rule in create_validate.yaml that enforces
presence (and optionally complexity) when guest_os_family == 'windows' and
vm_enable_sysprep == true; alternatively implement runtime random generation and
secure output if you prefer automatic passwords, but do not ship a fixed weak
default.

In
`@collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tasks/create_build_spec.yaml`:
- Around line 43-81: The Windows VM template (when guest_os_family == 'windows')
currently sets domain.resources.requests.memory but lacks domain.memory.guest,
while the Linux template uses domain.memory.guest but lacks
domain.resources.requests.memory; update both vm_template_spec blocks so they
include both domain.memory.guest and domain.resources.requests.memory set to "{{
vm_memory }}" (i.e., add domain.memory.guest: "{{ vm_memory }}" to the Windows
branch and add domain.resources.requests.memory: "{{ vm_memory }}" under
domain.resources.requests in the Linux branch) so that vm_template_spec
consistently specifies guest-visible memory and Kubernetes scheduling requests.

In
`@collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tests/fixtures/computeinstance-windows-with-image-test.yaml`:
- Around line 4-11: The fixture for templateID osac.templates.ocp_virt_vm
(metadata.name test-win-with-image) will not be inferred as Windows because
spec.image.sourceRef "registry.example.com/osac/windows-golden:ltsc2022" doesn't
match the containerdisks/windows heuristic and there's no explicit
osac.openshift.io/guest-os-family annotation; fix by adding the annotation
osac.openshift.io/guest-os-family: windows to metadata.annotations (or
alternatively adjust spec.image.sourceRef to match the containerdisks/windows
pattern) so the guest OS inference picks the Windows code path.

In `@TESTING-GOLDEN-IMAGES.md`:
- Around line 80-101: Update the ComputeInstance annotation extraction to read
osac.openshift.io/vm-enable-sysprep and propagate it to the ocp_virt_vm role by
adding logic analogous to infer_guest_os_family.yaml: parse the annotation value
(treating "false"/"true" strings as booleans), set/override the role variable
vm_enable_sysprep accordingly, and ensure the playbook/operator passes
vm_enable_sysprep into the ocp_virt_vm role invocation so the role no longer
always defaults to true.

In `@tests/integration/fixtures/computeinstance-windows-test.yaml`:
- Around line 4-16: The integration fixture can be mis-detected as Linux because
the image path (spec.image.sourceRef) doesn't match the containerdisks/windows
heuristic; update the manifest for the resource named by metadata.name
(test-windows-vm) to explicitly force Windows family by adding a
metadata.annotations entry (e.g. add metadata.annotations: {
"osac.cloud/family": "windows" } or the equivalent annotation your codebase
reads for family inference) so the family inference logic uses the provided
value instead of heuristics.

---

Outside diff comments:
In
`@collections/ansible_collections/osac/templates/roles/ocp_virt_vm/meta/osac.yaml`:
- Around line 10-12: The template meta file is missing required keys; update
meta/osac.yaml for the ocp_virt_vm role to include implementation_strategy and
capabilities alongside the existing template_type: add an
implementation_strategy field (e.g., a strategy name or reference used by your
framework) and a capabilities list/array describing what this compute_instance
template supports (e.g., ["create","delete","update"] or the project-specific
capability keys) so the file contains implementation_strategy, template_type,
and capabilities entries to satisfy the template metadata contract.

In
`@collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tasks/create_secrets.yaml`:
- Around line 104-110: The task "Read user-data secret from ComputeInstance
namespace" is missing a kubeconfig so it will fail when the ComputeInstance
secret lives on a different cluster than the VM target; update that
kubernetes.core.k8s_info task to include the kubeconfig parameter pointing to
the source/hub cluster kubeconfig (e.g., a variable like hub_kubeconfig or
compute_instance_kubeconfig) rather than relying on the
remote_cluster_kubeconfig used later for writes, and ensure the play passes that
hub kubeconfig variable when the ComputeInstance is remote.

---

Nitpick comments:
In
`@collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tests/test.yml`:
- Around line 175-183: The rescue currently sets windows_missing_image_failed:
true for any failure; change it to only set that fact when the failure message
matches the specific validation error from the create_validate task (use the
rescue-supplied ansible_failed_result.msg or ansible_failed_result.stderr) —
e.g., inside the rescue block check the error text (substring or regex) for the
known "missing Windows image" validation message before setting
windows_missing_image_failed so unrelated errors are not masked; reference the
include_role/tasks_from: create_validate.yaml and the variable
windows_missing_image_failed and use ansible_failed_result.msg in the
conditional.
```

</details>

<details>
<summary>🪄 Autofix (Beta)</summary>

Fix all unresolved CodeRabbit comments on this PR:

- [ ] <!-- {"checkboxId": "4b0d0e0a-96d7-4f10-b296-3a18ea78f0b9"} --> Push a commit to this branch (recommended)
- [ ] <!-- {"checkboxId": "ff5b1114-7d8c-49e6-8ac1-43f82af23a33"} --> Create a new PR with the fixes

</details>

---

<details>
<summary>ℹ️ Review info</summary>

<details>
<summary>⚙️ Run configuration</summary>

**Configuration used**: Organization UI

**Review profile**: CHILL

**Plan**: Pro

**Run ID**: `5c5985eb-2ff4-4bb6-b5d8-a66dd487b884`

</details>

<details>
<summary>📥 Commits</summary>

Reviewing files that changed from the base of the PR and between 744bc2ca0f8e393f8c4be1116956d2c4b1329060 and bc4cd806dfca4c8b7cfa8884bfe7a1319fb95408.

</details>

<details>
<summary>📒 Files selected for processing (17)</summary>

* `TESTING-GOLDEN-IMAGES.md`
* `collections/ansible_collections/osac/templates/README.md`
* `collections/ansible_collections/osac/templates/roles/ocp_virt_vm/defaults/main.yaml`
* `collections/ansible_collections/osac/templates/roles/ocp_virt_vm/meta/argument_specs.yaml`
* `collections/ansible_collections/osac/templates/roles/ocp_virt_vm/meta/osac.yaml`
* `collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tasks/create.yaml`
* `collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tasks/create_build_spec.yaml`
* `collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tasks/create_secrets.yaml`
* `collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tasks/create_validate.yaml`
* `collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tasks/create_wait_annotate.yaml`
* `collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tasks/delete.yaml`
* `collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tasks/delete_resources.yaml`
* `collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tasks/infer_guest_os_family.yaml`
* `collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tests/fixtures/computeinstance-windows-with-image-test.yaml`
* `collections/ansible_collections/osac/templates/roles/ocp_virt_vm/tests/test.yml`
* `samples/windows_golden_image_payload.json`
* `tests/integration/fixtures/computeinstance-windows-test.yaml`

</details>

</details>

<!-- This is an auto-generated comment by CodeRabbit for review status -->
--
author:	amej
association:	member
edited:	false
status:	none
--
@coderabbit review
--
author:	coderabbitai
association:	none
edited:	false
status:	none
--
<!-- This is an auto-generated reply by CodeRabbit -->
<details>
<summary>✅ Actions performed</summary>

Review triggered.

> Note: CodeRabbit is an incremental review system and does not re-review already reviewed commits. This command is applicable only when automatic reviews are paused.

</details>
--
author:	eranco74
association:	member
edited:	false
status:	commented
--
## Code Review

**+549 / -93** | **16 files** | **36 commits**

### Overall

Good design decision to unify `windows_oci_vm` into `ocp_virt_vm` with OS-family dispatch rather than maintaining two parallel roles. The inference chain (explicit var → annotation → image heuristic → default), validation logic (required image, password strength, port ranges), and VMI disappearance wait for delete sequencing are all well done.

### Issues to address

#### 1. Sysprep admin password stored in ConfigMap, not Secret (Security)
The sysprep unattend.xml (containing `vm_sysprep_admin_password` in plaintext) is stored in a **ConfigMap**. ConfigMaps are readable by anyone with namespace-level read access and are not treated as sensitive by Kubernetes (no encryption at rest by default, visible in `kubectl get cm -o yaml`). Consider using a **Secret** instead, or at minimum document that this ConfigMap contains sensitive data so operators know to restrict access.

#### 2. Sysprep unattend.xml inline in task file (Maintainability)
The entire unattend.xml (~50 lines of XML) is embedded inline in `create_secrets.yaml`. Moving it to a Jinja2 template file under `templates/` would make the XML easier to read, modify, and diff without touching task logic.

#### 3. Test rescue block doesn't validate error message
In `test.yml` Test 4, the rescue block sets `windows_missing_image_failed: true` for **any** failure. If `create_validate` fails for an unrelated reason (missing variable, syntax error), the test still passes. Capture the error message and assert it contains the expected validation text (e.g., `spec.image.sourceRef` or `Windows`).

#### 4. Commit history
36 commits including multiple rounds of fix-the-fix (WR-01/02/03 twice), a reverted feature (containerDisk added then removed), and incremental test fixes. Consider squashing into a smaller set of logical commits before merge.

### Minor notes

- `exposed_ports` no longer has a `default:` in argument_specs (removed in commit 5b16344). Runtime default comes from `defaults/main.yaml` which works, but `ansible-doc` won't show a default — users may be confused. A note in the description would help.
- The `failed_when` guard on LB Service delete is fine but the pattern (`failed is defined AND failed AND 'not found' not in msg`) is an AND chain — if `.failed` is undefined the task silently passes. `kubernetes.core.k8s` with `state: absent` already handles missing resources gracefully, so these guards may be redundant.
- Verify both Linux and Windows spec blocks in `create_build_spec.yaml` have both `domain.memory.guest` **and** `domain.resources.requests.memory` in the final state (commit 148c064 may have added this after the main diff).

### What's good

- Unified template with OS-family dispatch is cleaner than two roles
- Strong validation: no placeholder Windows image, password >= 8 chars, port range checks
- VMI disappearance wait with upstream KubeVirt references is the correct delete pattern
- `vm_enable_sysprep` flag for golden image support is practical
- Inference priority chain is well-designed and documented
--
