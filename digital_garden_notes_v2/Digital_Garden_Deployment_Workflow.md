# Digital Garden Deployment Workflow

This note outlines the workflow for deploying and maintaining a [[Quartz]] digital garden hosted on [[Vercel]], where the content is managed in a separate Git repository using [[Git_Submodules]].

## Overview

1.  **Content Creation:** Notes are written in Obsidian within a local clone of the `devlog-grimoire` repository.
2.  **Content Sync:** Changes are committed and pushed to the `devlog-grimoire` GitHub repository (using [[SSH_vs_HTTPS_URLs]]).
3.  **Deployment Update:** The main `devlog-grimoire-digital-garden` repository (which includes `devlog-grimoire` as a submodule in `content/`) needs to be updated to point to the latest commit of the submodule.
4.  **Vercel Build:** Pushing the update to the main repository triggers a [[Vercel]] build. Vercel clones the main repository and then clones the submodule using the [[SSH_vs_HTTPS_URLs]]] specified in `.gitmodules`.
5.  **Site Live:** Vercel builds the [[Quartz]] site and deploys it.

## Challenges Encountered

*   [[Vercel_Submodule_Issue]]: Initial deployment failed because Vercel couldn't clone the submodule via SSH.
*   [[Local_Push_Issue]]: The automation script initially failed because the local submodule remote was incorrectly set to HTTPS.

## Automation

To simplify the update process (steps 2 and 3), an [[Automation_Script]] was created to handle committing and pushing changes to both the submodule and the parent repository sequentially.

## Key Files & Configuration

*   `.gitmodules` (in parent repo): Defines the submodule path and the **HTTPS URL** for Vercel cloning.
*   `content/.git/config` (in local submodule clone): Defines the **SSH URL** for personal push/pull operations.
*   `update_garden.sh`: The [[Automation_Script]].

