# Git Submodules

[[Git Submodules]] allow you to keep a Git repository as a subdirectory of another Git repository. This lets you clone another repository into your project and keep your commits separate.

## Use Case in This Project

*   The main digital garden repository (`devlog-grimoire-digital-garden`) uses a submodule to include the content from the separate `devlog-grimoire` notes repository.
*   The submodule is located at the `content/` path within the main repository.
*   This setup keeps the [[Quartz]] site configuration separate from the actual notes content, allowing the notes repository (`devlog-grimoire`) to be managed independently (e.g., used directly with Obsidian).

## Key Concepts & Commands

*   **`.gitmodules` file:** Located in the root of the parent repository, this file defines the path and URL for each submodule.
    *   In this project, the URL needed to be [[SSH vs HTTPS URLs]] for [[Vercel]] compatibility: `url = https://github.com/qu-bit1/devlog-grimoire.git`
*   **`git submodule add <repo_url> <path>`:** Adds a new submodule.
*   **`git submodule update --init --recursive`:** Initializes and clones/updates submodules after cloning the parent repository.
*   **`git submodule sync`:** Updates the submodule's remote URL in the local `.git/config` based on the `.gitmodules` file. This was used to apply the HTTPS URL change but inadvertently caused the [[Local Push Issue]].
*   **Updating Submodules:** To update the digital garden with new notes, you commit/push changes within the submodule directory (`content/`), then go back to the parent directory, stage the updated `content` directory (which now points to a new commit hash), and commit/push the parent repository. This process is handled by the [[Automation Script]].

## Related Issues

*   [[Vercel Submodule Issue]]
*   [[Local Push Issue]]

See also: [[Digital Garden Deployment Workflow]]

