---
name: wdl-workflow-authoring
description: Help author WDL workflows, ask for the target WDL standard version first, cache the relevant spec in the skill-local wdl_spec directory, and validate the workflow with Sprocket.
---

# WDL Workflow Authoring

Use this skill whenever the user wants to write, edit, or debug a workflow in the Workflow Description Language (WDL).

## Trigger

Trigger this skill when the user's request includes intent such as:
- "用 WDL 写一个 workflow"
- "用 WDL 写一个 pipeline"
- "create a WDL workflow"
- "help me write WDL"
- "write a workflow in WDL"

## Workflow

1. Pause and ask the user which WDL standard version they want to use.
   - If the user does not specify a version, default to WDL 1.0.
   - Keep the answer concise and explicit, for example: "我将按 WDL 1.0 来编写。"

2. Resolve the WDL specification for the selected version.
   - Use the official OpenWDL spec as the primary reference.
   - For WDL 1.0, the reference is:
     - https://github.com/openwdl/wdl/blob/legacy/versions/1.0/SPEC.md
   - For WDL 1.3, the reference is:
     - https://github.com/openwdl/wdl/blob/wdl-1.3/SPEC.md
   - For other versions, find the matching spec in the OpenWDL repository and use the corresponding branch or tag.
   - Cache the spec in the skill-local directory next to SKILL.md, under a wdl_spec folder using a versioned subdirectory, for example:
     - wdl_spec/1.0/SPEC.md
     - wdl_spec/1.3/SPEC.md
   - If the target version directory already exists under the skill's wdl_spec folder and contains a SPEC.md file, reuse it instead of downloading again.

3. Draft or revise the WDL workflow based on the chosen version and the cached spec.
   - Prefer syntax and features that match the selected standard.
   - Follow these style rules:
     - Write all comments in English.
     - Add parameter_meta to every task.
     - Ensure every task runtime includes cpu, memory, disks, and docker, and make these four values dynamic by reading them from task inputs.
   - If the user provides an existing workflow file, update it in place.

4. Validate the workflow with Sprocket after the script is written.
   - Check whether Sprocket is installed.
   - If it is not installed, install it before validation.
   - On macOS, prefer Homebrew:
     - brew install sprocket
   - If Homebrew is unavailable, install from Cargo:
     - cargo install sprocket --locked
   - Run validation with:
     - sprocket check <workflow_file>
   - If Sprocket reports syntax or semantic issues, fix them and rerun the check until the workflow validates cleanly.

## Output expectations

When you finish, report:
- the WDL standard version chosen
- the local spec path used from the skill's wdl_spec directory
- whether Sprocket validation passed or failed
- any syntax issues that were fixed
