# Undoing Changes in Git

This guide explains how to reverse different types of changes in Git, from uncommitted edits to published commits.

<br/>

## Table of Contents

1. [Working Directory Changes](#working-directory-changes)
2. [Staging Area Changes](#staging-area-changes)
3. [Undoing Commits](#undoing-commits)
4. [Removing Untracked Files](#removing-untracked-files)
5. [Resolving Merge Conflicts](#resolving-merge-conflicts)

---

<br/>

## Working Directory Changes

When you’ve edited files but haven’t staged or committed them yet.

* **Discard Unstaged Changes (Old Git):**

  ```bash
  git checkout -- <file-name>
  ```
* **Discard Unstaged Changes (New Git):**

  ```bash
  git restore <file-name>
  ```
* **Discard All Unstaged Changes:**

  ```bash
  git restore .
  ```

<br/>

## Staging Area Changes

When you’ve used `git add` but haven’t committed yet.

* **Unstage a File:**

  ```bash
  git reset HEAD <file-name>
  ```
This command resets the file from the staging area while leaving your working directory unchanged.

<br/>

## Undoing Commits

Techniques vary based on whether commits are local or already pushed.

### Amend the Last Commit
* **When to Use:** If you just committed and realized you forgot to add a file or need to update the commit message.
    ```bash
    git commit --amend
    ```

* This opens your editor with the previous commit message, allowing you to modify it and include any additional staged changes.

* This rewrites history, so it should only be used on commits that haven’t been pushed yet.

### Reset the Branch Pointer
Reset lets you move the branch pointer to an earlier commit. There are several options:

* **Soft Reset:** Keep changes staged:

  ```bash
  git reset --soft HEAD~1
  ```
  Moves the HEAD pointer back by one commit without touching the working directory or staging area. This is useful if you want to “uncommit” changes but keep them staged for editing.

* **Mixed Reset (default):** Keep changes unstaged:

  ```bash
  git reset HEAD~1
  ```
  Moves HEAD back by one commit and unstages the changes (they remain in the working directory). This is the default if no flag is provided.

* **Hard Reset:** Discard changes completely:

  ```bash
  git reset --hard HEAD~1
  ```
  Moves HEAD back by one commit and discards changes in both the staging area and your working directory.

> **Caution:** Hard reset is irreversible.

<br/>

### Revert a Commit
When changes have been pushed and you don’t want to rewrite history (or you are working collaboratively), you can “undo” a commit without changing the commit history.

```bash
git revert <commit-id>
```

* Creates a new commit that undoes the specified commit without rewriting history. 
* It’s the safest way to undo changes in a shared repository.

<br/>

## Removing Untracked Files

Clear out files Git isn’t tracking.

* **Dry Run:** See what will be removed:

  ```bash
  git clean -n
  ```
* **Remove Untracked Files:**

  ```bash
  git clean -f
  ```
* **Include Directories:**

  ```bash
  git clean -fd
  ```

<br/>

## Resolving Merge Conflicts
When merging branches, conflicts may arise if the same lines were modified differently. Resolving these conflicts is another type of “undo” where you must manually choose what the final content should be:


1. After a Merge Fails, **Identify Conflicts:**

   ```bash
   git status
   ```
2. **Edit Marked Files:**
   Open the files and look for conflict markers that resemble:

   ```text
   <<<<<<< HEAD
   Your changes...
   =======
   Incoming changes...
   >>>>>>> branch-name
   ```
3. **Remove Markers & Save.**
4. **Stage Resolved Files:**

   ```bash
   git add <file-name>
   ```
5. **Complete the Merge:**

   ```bash
   git commit
   ```

<br/>

---

*For more details, consult the [Pro Git Book](https://git-scm.com/book/en/v2).*