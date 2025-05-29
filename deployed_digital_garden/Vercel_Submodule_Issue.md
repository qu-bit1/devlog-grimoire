# Vercel Submodule Issue

## Problem Description

When deploying the [[Concepts/Quartz|Quartz]] site (`devlog-grimoire-digital-garden`) to [[Concepts/Vercel|Vercel]] for the first time after adding the `devlog-grimoire` notes repository as a [[Concepts/Git Submodules|Git submodule]] in the `content/` directory, the build failed.

The [[Concepts/Vercel|Vercel]] build logs showed the warning:
`Warning: Failed to fetch one or more git submodules`

This resulted in an empty `content/` directory during the build, causing [[Concepts/Quartz|Quartz]] to build a site with no notes.

## Root Cause

The `.gitmodules` file in the main repository specified the submodule URL using the [[Concepts/SSH vs HTTPS URLs|SSH format]]:
`url = git@github.com:qu-bit1/devlog-grimoire.git`

[[Concepts/Vercel|Vercel]]'s build environment clones repositories using HTTPS by default and does not have access to the private SSH keys required to authenticate and clone via SSH. Therefore, it could not fetch the submodule content.

## Solution

The submodule URL in the `.gitmodules` file of the main repository (`devlog-grimoire-digital-garden`) was changed to the [[Concepts/SSH vs HTTPS URLs|HTTPS format]]:
`url = https://github.com/qu-bit1/devlog-grimoire.git`

This change was then synchronized using `git submodule sync` and committed/pushed to the main repository. [[Concepts/Vercel|Vercel]] was then able to successfully clone the submodule during the next build.

## Side Effect

Applying this fix using `git submodule sync` inadvertently caused the [[Local Push Issue]].

See also: [[Digital Garden Deployment Workflow]], [[Concepts/Git Submodules]], [[Concepts/SSH vs HTTPS URLs]]

