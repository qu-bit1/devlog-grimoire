# Vercel Submodule Issue

## Problem Description

When deploying the [[Quartz]] site (`devlog-grimoire-digital-garden`) to [[Vercel]] for the first time after adding the `devlog-grimoire` notes repository as a [[Git_Submodules]] in the `content/` directory, the build failed.

The [[Vercel]] build logs showed the warning:
`Warning: Failed to fetch one or more git submodules`

This resulted in an empty `content/` directory during the build, causing [[Quartz]] to build a site with no notes.

## Root Cause

The `.gitmodules` file in the main repository specified the submodule URL using the [[SSH_vs_HTTPS_URLs]]:
`url = git@github.com:qu-bit1/devlog-grimoire.git`

[[Vercel]]'s build environment clones repositories using HTTPS by default and does not have access to the private SSH keys required to authenticate and clone via SSH. Therefore, it could not fetch the submodule content.

## Solution

The submodule URL in the `.gitmodules` file of the main repository (`devlog-grimoire-digital-garden`) was changed to the [[SSH_vs_HTTPS_URLs]]:
`url = https://github.com/qu-bit1/devlog-grimoire.git`

This change was then synchronized using `git submodule sync` and committed/pushed to the main repository. [[Vercel]] was then able to successfully clone the submodule during the next build.

## Side Effect

Applying this fix using `git submodule sync` inadvertently caused the [[Local_Push_Issue]].

