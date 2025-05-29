# Local Push Issue

## Problem Description

After fixing the [[Vercel_Submodule_Issue]] by changing the submodule URL in `.gitmodules` to [[SSH_vs_HTTPS_URLs]] and running `git submodule sync`, the [[Automation_Script]] (`update_garden.sh`) started failing.

Specifically, when the script attempted to push changes from within the local `content/` submodule directory, it prompted for GitHub username and password:
`Username for 'https://github.com':`

This indicated it was trying to authenticate via HTTPS instead of using the user's configured SSH keys.

## Root Cause

The `git submodule sync` command, while necessary to update the parent repository's configuration for [[Vercel]], also updated the `remote.origin.url` setting within the *local submodule's* Git configuration (`content/.git/config`). It changed this URL from the original [[SSH_vs_HTTPS_URLs]] (`git@github.com:...`) to the HTTPS URL (`https://github.com/...`) specified in the updated `.gitmodules` file.

Therefore, subsequent `git push` commands executed *inside* the `content/` directory (like the one in the [[Automation_Script]]) defaulted to using HTTPS authentication, which requires credentials or a token, rather than the preferred SSH key authentication.

## Solution

The remote URL *specifically for the local submodule clone* needed to be set back to the SSH address, without altering the `.gitmodules` file (which Vercel relies on).

This was achieved by running the following commands from the root of the main repository (`devlog-grimoire-digital-garden`):

```bash
cd content
git remote set-url origin git@github.com:qu-bit1/devlog-grimoire.git
cd ..
```

This command modifies *only* the `content/.git/config` file, telling the local Git client to use the SSH URL when pushing or fetching from the `origin` remote *while inside the `content` directory*. The `.gitmodules` file in the parent repository remains unchanged, preserving the HTTPS URL needed for [[Vercel]].

**Result:** The [[Automation_Script]] could once again push submodule changes using SSH key authentication, while [[Vercel]] continued to clone the submodule using HTTPS.

See also: [[Digital_Garden_Deployment_Workflow]], [[Automation_Script]], [[Git_Submodules]], [[SSH_vs_HTTPS_URLs]]

