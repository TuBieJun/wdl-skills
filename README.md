# WDL Workflow Authoring Skill

## Purpose

This skill helps users write, revise, and validate WDL workflows.

It pauses first to ask which WDL standard version the user wants to use, then looks up the corresponding specification and caches it in the skill's own directory for later reuse.

## Highlights

- Confirms the WDL version before writing to avoid using unsupported syntax
- Reuses locally cached specifications to reduce repeated downloads
- Runs Sprocket after authoring to check the workflow for syntax issues
- Offers installation guidance and installs Sprocket when it is not available

## Manual trigger example

Type: /wdl-workflow-authoring

## Install this skill
```
   git clone https://github.com/TuBieJun/wdl-skills.git ~/.agents/skills/wdl-skills
```

