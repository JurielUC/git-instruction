# Git and GitHub: A Beginner's Guide

This guide explains how to install Git, connect it to GitHub, save your first
project, and keep your local and online copies up to date.

## 1. What are Git and GitHub?

- **Git** tracks changes to files on your computer. It lets you save versions
  of a project and work safely with other people.
- **GitHub** is a website that stores Git repositories online. It is useful for
  backups, sharing projects, and teamwork.
- A **repository** (or **repo**) is a project folder that Git tracks.
- A **commit** is a saved checkpoint of your work.

## 2. What to install

Before starting, you need:

1. A free [GitHub account](https://github.com/signup).
2. [Git](https://git-scm.com/downloads) for your operating system.
3. A code editor, such as [Visual Studio Code](https://code.visualstudio.com/).

During Git installation, the default options are suitable for most beginners.
After installation, open **Git Bash**, **PowerShell**, **Terminal**, or the
terminal inside VS Code and check that Git works:

```bash
git --version
```

You should see a version number, such as `git version 2.x.x`.

## 3. Set up your Git identity

Tell Git which name and email to attach to your commits. Use the email address
connected to your GitHub account if you want GitHub to link commits to your
profile.

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Check the saved values:

```bash
git config --global user.name
git config --global user.email
```

> This identifies your commits, but it does not sign you in to GitHub.

## 4. Sign in to GitHub from Git

The simplest method for most beginners is HTTPS. The first time you push, Git
Credential Manager normally opens a browser and asks you to sign in to GitHub.
Complete the browser instructions and approve access. Your credentials can then
be stored securely for later commands.

GitHub does **not** accept your account password directly in the terminal. If
your setup asks for a password instead of opening a browser, use a GitHub
[personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)
as the password, or install and sign in with the optional
[GitHub CLI](https://cli.github.com/):

```bash
gh auth login
```

Follow the prompts and choose `GitHub.com`, `HTTPS`, and browser login.

## 5. Put your first project on GitHub

### A. Create an empty repository on GitHub

1. Sign in to GitHub and select **New repository**.
2. Enter a repository name, for example `my-first-project`.
3. Choose **Public** or **Private**.
4. To avoid conflicts with an existing local project, do **not** add a README,
   `.gitignore`, or license yet.
5. Select **Create repository**.
6. Copy the HTTPS URL. It will look like:
   `https://github.com/YOUR-USERNAME/my-first-project.git`.

### B. Initialize and commit your local project

Open a terminal and move into your project folder. Replace the example path
with the real path on your computer:

```bash
cd path/to/my-first-project
git init
git status
git add .
git commit -m "Initial commit"
```

What these commands do:

- `cd` moves the terminal into your project folder.
- `git init` starts a Git repository in that folder.
- `git status` shows changed, staged, and untracked files.
- `git add .` stages all current changes for the next commit.
- `git commit -m "Initial commit"` saves a checkpoint with a short message.

### C. Connect the project and push it

Replace the URL below with the HTTPS URL copied from your GitHub repository:

```bash
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/my-first-project.git
git push -u origin main
```

- `git branch -M main` names the current branch `main`.
- `git remote add origin ...` connects the local project to GitHub. `origin` is
  the usual nickname for that remote repository.
- `git push -u origin main` uploads the branch and remembers its destination.

Refresh the repository page on GitHub. Your files should now appear there.

## 6. Everyday add, commit, pull, and push workflow

Before beginning work, download and combine teammates' latest changes:

```bash
git pull origin main
```

After editing your files, review and upload your own work:

```bash
git status
git add .
git commit -m "Describe what you changed"
git push origin main
```

Write a clear commit message, such as `Add student registration form`, instead
of a vague message such as `changes`.

### Pull versus push

- `git pull` downloads changes from GitHub and merges them into your current
  local branch.
- `git push` uploads your local commits to GitHub.

If Git rejects a push because the remote repository contains newer work, first
run `git pull origin main`, resolve any conflicts if Git reports them, commit
the resolution when necessary, and then push again.

## 7. Fetch and merge separately

`git pull` is convenient because it performs two actions: **fetch** and
**merge**. You can run those actions separately when you want to inspect remote
changes before adding them to your branch.

```bash
git fetch origin
git log --oneline main..origin/main
git merge origin/main
```

- `git fetch origin` downloads information and commits from GitHub without
  changing your current files.
- `git log --oneline main..origin/main` previews commits that are on GitHub but
  not yet on your local `main` branch. No output means there are none.
- `git merge origin/main` combines the fetched GitHub version of `main` with
  your current branch.

Always check which branch you are using before merging:

```bash
git branch --show-current
```

If it is not `main`, switch to `main` first:

```bash
git switch main
```

## 8. Download an existing GitHub project

If a repository already exists on GitHub, clone it instead of running
`git init`:

```bash
git clone https://github.com/OWNER/REPOSITORY.git
cd REPOSITORY
```

Cloning downloads the project, its commit history, and its remote settings.

## 9. Useful commands and beginner tips

```bash
git status                 # Show the current repository state
git log --oneline          # Show a short commit history
git remote -v              # Show connected remote repositories
git diff                   # Show changes not staged yet
git diff --staged          # Show changes staged for the next commit
```

- Run Git commands from inside the correct project folder.
- Pull before starting shared work and before pushing.
- Check `git status` often; it usually explains what to do next.
- Commit small, related groups of changes with meaningful messages.
- Do not commit passwords, API keys, private tokens, or secret configuration.
- Use a `.gitignore` file for generated files and private local settings that
  Git should not track.
- Read an error message before trying another command; Git often includes the
  solution in its output.

## Quick workflow reminder

```bash
# Start the day
git pull origin main

# After making changes
git status
git add .
git commit -m "Describe the change"
git push origin main

# Inspect remote work before combining it manually
git fetch origin
git log --oneline main..origin/main
git merge origin/main
```
