# Automation Script (update_garden.sh)

This script automates the two-step process required to update the [[Quartz]] digital garden when using [[Git_Submodules]] for content.

## Purpose

When notes are updated in the `content/` submodule (`devlog-grimoire`), two separate Git operations are needed:

1.  Commit and push the changes within the submodule repository.
2.  Commit and push the updated submodule reference (the new commit hash) in the parent repository (`devlog-grimoire-digital-garden`).

This script performs both steps sequentially.

## Script Code

```bash
#!/bin/bash

# Script to commit and push changes in the submodule (content) and then the parent repository.

# Check if a commit message was provided
if [ -z "$1" ]; then
  echo "Error: Please provide a commit message."
  echo "Usage: ./update_garden.sh \"Your commit message\""
  exit 1
fi

COMMIT_MESSAGE="$1"
SUBMODULE_DIR="content"
PARENT_DIR=$(pwd)

# --- Submodule Operations --- 
echo "--- Processing submodule ($SUBMODULE_DIR) --- "

# Navigate into the submodule directory
cd "$SUBMODULE_DIR" || exit 1

# Add all changes
echo "Staging changes in submodule..."
git add .

# Commit changes
echo "Committing changes in submodule with message: $COMMIT_MESSAGE"
git commit -m "$COMMIT_MESSAGE"

# Push changes
echo "Pushing submodule changes..."
# This push uses the 'origin' remote defined in content/.git/config
# which should be set to the SSH URL for key-based auth
git push origin

# Check if submodule push was successful
if [ $? -ne 0 ]; then
  echo "Error: Failed to push submodule changes. Aborting."
  cd "$PARENT_DIR"
  exit 1
fi

echo "Submodule push successful."

# --- Parent Repository Operations --- 
echo "--- Processing parent repository --- "

# Navigate back to the parent directory
cd "$PARENT_DIR" || exit 1

# Add the updated submodule and any other changes in the parent repo
echo "Staging changes in parent repository (including submodule update)..."
git add "$SUBMODULE_DIR"
# Optional: Add all other changes in the parent repo too. Uncomment if needed.
# git add .

# Commit changes in the parent repository
# Using a standard message, but you can customize this
PARENT_COMMIT_MESSAGE="Update content submodule to latest commit"
echo "Committing changes in parent repository with message: $PARENT_COMMIT_MESSAGE"
git commit -m "$PARENT_COMMIT_MESSAGE"

# Push changes
echo "Pushing parent repository changes..."
# Assuming your branch is 'v4', change if necessary
BRANCH_NAME="v4" 
git push origin "$BRANCH_NAME"

# Check if parent push was successful
if [ $? -ne 0 ]; then
  echo "Error: Failed to push parent repository changes."
  exit 1
fi

echo "Parent repository push successful."
echo "--- All done! --- "

exit 0
```

## Usage

1.  Save the script as `update_garden.sh` in the root of the `devlog-grimoire-digital-garden` repository.
2.  Make it executable: `chmod +x update_garden.sh`.
3.  Run from the root directory: `./update_garden.sh "Your commit message"`.

## Important Note

This script relies on the `origin` remote within the `content/` submodule being configured to use the [[SSH_vs_HTTPS_URLs]] (`git@github.com:...`) to allow pushing via SSH keys. If it prompts for HTTPS credentials, it indicates the [[Local_Push_Issue]] needs to be addressed by setting the submodule's remote URL back to SSH.

See also: [[Digital_Garden_Deployment_Workflow]], [[Local_Push_Issue]]

