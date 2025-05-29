# Vercel

[[Vercel]] is a cloud platform for static sites and Serverless Functions that fits perfectly with frontend frameworks and static site generators.

## Key Features

*   **Git Integration:** Automatically deploys projects upon commits to connected Git repositories (GitHub, GitLab, Bitbucket).
*   **CDN:** Provides a global edge network for fast content delivery.
*   **Build System:** Handles the build process for various frameworks and static site generators, including [[Concepts/Quartz|Quartz]].
*   **Preview Deployments:** Creates unique URLs for each Git branch or pull request for easy testing and collaboration.

## Usage in This Project

*   The `devlog-grimoire-digital-garden` [[Concepts/Quartz|Quartz]] site is hosted on Vercel.
*   Deployment is triggered automatically when changes are pushed to the `v4` branch of the main repository on GitHub.
*   Vercel's build process needed specific configuration to handle the [[Concepts/Git Submodules|Git submodule]] used for content, specifically requiring an [[Concepts/SSH vs HTTPS URLs|HTTPS URL]] in `.gitmodules`.

## Related Issues

*   [[Vercel Submodule Issue]]: Initial problem where Vercel couldn't clone the submodule via SSH.

See also: [[Digital Garden Deployment Workflow]]

