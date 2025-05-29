# Getting Started: Clone, Pull & Fork
This page explains three essential Git operations:

* **Clone:** Copy a remote repository to your local machine.
* **Pull:** Update your local repository with latest changes from remote.
* **Fork:** Create a personal copy of someone else’s repository on GitHub.

Follow the sections below to learn when and how to use each command.

<br/>
<br/>

# Table of Contents

1. [Clone](#clone)
2. [Pull](#pull)
3. [Fork](#fork)
4. [Summary Comparison](#summary-comparison)

<br/>
<br/>

# Clone
Cloning a repository in Git means Creates a copy of the remote repository on your local machine that's fully synchronized with the remote repository.

```bash
git clone <repository-url>
```

This enables you to explore the history, make changes, and later push those changes back to the remote repository if needed.

![alt text](Images/git-clone.png)

By cloning you're downloading everything from that remote repository, including:

* **The Entire Commit History:** All commits, branches, and tags are copied, so you have full access to the repository's past developments.

* **All Files and Folders:** The working directory is recreated on your local machine with the project's files, allowing you to work offline.

* **The .git Directory:** This hidden folder contains all the metadata, configurations, and version history that Git uses to manage the repository.


<br/>
<br/>
<br/>

# Pull
In Git, the pull command is used to update your local repository with changes from a remote repository. It’s essentially a shortcut that does two things:

* Fetches changes from the remote.

* Merges those changes into your current branch.

![alt text](Images/git-pull.png)

```bash
git pull origin <branch>
```
Git retrieves any new commits from the remote repository's main branch and attempts to merge them with your local branch.

### Purpose
Pulling ensures that your local copy stays up to date with work done by others, reducing the likelihood of conflicts when you later push your commits.

<br/>
<br/>
<br/>

# Fork
A fork is a personal copy of another user's repository that lives on GitHub (or another distributed hosting service). This process creates an independent copy of the repository under your GitHub account.

![alt text](Images/git-fork.png)

### How to Fork a Repository

1. Go to the GitHub repository you want to fork.

2. Click the Fork button (top-right corner).

3. GitHub creates a copy of the repo under your account.

4. Clone your fork locally:

```bash
git clone https://github.com/<your-username>/<repo-name>.git
```

### Usage Scenario:

* **Open Source Contributions:** If you want to contribute to a project but don’t have write access to the original repository, you can fork it. This lets you experiment freely—modify code, commit changes, and push them to your own fork.

* **Personal Experimentation:** You might also fork a repository to try out new ideas without risking the integrity of the original project.

### Workflow with Forks: 
After forking a repository, you typically:

* Clone your fork locally using git clone.

* Make changes, commit them, and push back to your fork.

* Finally, submit a pull request to propose merging your updates back into the original repository if you want your changes to be incorporated.

<br/>
<br/>
<br/>

# Summary Comparison
| Feature  | Clone                                    | Pull                                      | Fork                                      |
|----------|------------------------------------------|-------------------------------------------|-------------------------------------------|
| **Purpose** | Create a local copy of a repository      | Update your local repository with remote changes  | Make a personal, online copy of a repository in your account |
| **Usage**   | `git clone <repository-url>`             | `git pull` (fetch + merge)                | Use GitHub's "Fork" button; then work with your forked copy |
| **Scope**   | Local environment                        | Synchronizing local and remote repositories | Remote repository copy under your own account |
