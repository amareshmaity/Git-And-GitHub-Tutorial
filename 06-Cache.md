# Understanding Caches in Git & GitHub

Git and GitHub use several forms of “caching” to speed up workflows, manage intermediate states, and avoid re-entering credentials. This guide covers:

* [Staging Area (Index) Cache](#staging-area-index-cache)
* [Removing from Cache](#removing-from-cache)
* [Credential Caching](#credential-caching)
* [GitHub Actions Cache](#github-actions-cache)
* [Clearing Caches](#clearing-caches)

<br/>
<br/>

## Staging Area (Index) Cache

The **staging area**, also called the **index**, acts as a cache between your working directory and the repository. When you run `git add`, Git stores a snapshot of file contents in the index before committing.

* **Purpose:** Build up a set of changes (the “cache”) you plan to commit in one logical batch.
* **Commands:**

  ```bash
  git status         # See staged vs. unstaged changes
  git add <file>     # Cache file contents to index
  git diff --cached  # Compare index vs. last commit
  ```

<br/>
<br/>

## Removing files from Cache

You can remove files from the index cache without deleting them from your working directory:

* **Unstage a File:**

  ```bash
  git reset HEAD <file>
  ```

  This removes the file from the index (cache) but leaves the working copy untouched.

* **Remove Tracking, Keep File Locally:**

  ```bash
  git rm --cached <file>
  ```

  Stops tracking the file entirely while keeping it in your folder. Remember to add it to `.gitignore` if you don’t want Git to re-add it.

<br/>
<br/>

## Credential Caching

To avoid retyping your GitHub username and password (or token), Git can cache credentials locally.

* **Enable the Credential Helper (Memory Cache):**

  ```bash
  git config --global credential.helper cache
  ```

  By default, credentials are cached for 15 minutes.

* **Set Custom Timeout (e.g., 1 hour):**

  ```bash
  git config --global credential.helper 'cache --timeout=3600'
  ```

* **OS-Specific Helpers:**

  * **macOS Keychain:** `git config --global credential.helper osxkeychain`
  * **Windows Credential Manager:** `git config --global credential.helper manager`

<br/>
<br/>

## GitHub Actions Cache

In **GitHub Actions**, caching dependencies and build outputs speeds up CI workflows.

* **Cache Key:** A unique string (often based on OS, language version, and lockfile checksum).
* **Actions Cache Steps:**

  ```yaml
  - name: Cache dependencies
    uses: actions/cache@v3
    with:
      path: ~/.npm
      key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
      restore-keys: |
        ${{ runner.os }}-node-
  ```
* **What it does:** Stores and restores specified paths between workflow runs to avoid re-downloading packages.

<br/>
<br/>

## Clearing Caches

* **Clear Credential Cache:**

  ```bash
  git credential-cache exit
  ```
* **Remove GitHub Actions Cache (via UI):**

  1. Go to your repository on GitHub.
  2. Click **Actions** > **Caches** on the left sidebar.
  3. Select and **Delete** caches you no longer need.


