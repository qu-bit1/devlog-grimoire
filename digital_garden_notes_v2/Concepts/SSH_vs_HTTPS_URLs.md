When interacting with remote Git repositories (like those on GitHub), you primarily use either SSH or HTTPS URLs.

## HTTPS URLs

*   **Format:** `https://github.com/user/repo.git`
*   **Authentication:** Typically uses username/password (deprecated for command-line Git operations on GitHub) or, more commonly now, Personal Access Tokens (PATs) or OAuth.
*   **Pros:** Generally easier to set up initially, often works without firewall issues.
*   **Cons:** Can require entering credentials or managing tokens.
*   **Use Case in This Project:** Required in the `.gitmodules` file of the parent repository (`devlog-grimoire-digital-garden`) so that [[Vercel]]'s build system can clone the public `devlog-grimoire` submodule without needing SSH keys.

## SSH URLs

*   **Format:** `git@github.com:user/repo.git`
*   **Authentication:** Uses SSH key pairs. You add your public key to your GitHub account, and your private key (stored locally) is used for authentication.
*   **Pros:** More secure and convenient for frequent use once set up (no need to enter credentials).
*   **Cons:** Requires initial setup of SSH keys, might be blocked by some firewalls.
*   **Use Case in This Project:** Used for personal push/pull operations within the local clone of the `devlog-grimoire` submodule (`content/`). The `origin` remote URL inside `content/.git/config` is set to the SSH URL to allow pushing changes using the user's SSH key via the [[Automation_Script]].

## The Conflict

The core issue in the [[Digital_Garden_Deployment_Workflow]] arose because [[Vercel]] needed an HTTPS URL to clone the submodule, while the user's personal workflow preferred an SSH URL for pushing changes to the same submodule. The `git submodule sync` command, used to apply the HTTPS URL for Vercel, unfortunately also changed the local push URL, leading to the [[Local_Push_Issue]]. The solution involved setting different URLs for different contexts: HTTPS in `.gitmodules` (for Vercel) and SSH in the local submodule's remote configuration (for personal pushes).

See also: [[Git_Submodules]], [[Vercel_Submodule_Issue]], [[Local_Push_Issue]]

