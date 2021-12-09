## [_GUIDES_][guides] > **Git Commands** *(Cheat-sheet)*

### <p align=center>[Git & GitHub][git] | [Windows][win] | [Linux][linux] | [Networks][nets] <br/> [Programming][progLang] | [Databases][db] | [Docker & Kubernetes][docker] | [Embedded systems][embSys] | [CMake][CMake] </p>

<!--
* [_GUIDES_][guides]
* [Git & GitHub][git]
* [Windows][win]
* [Linux][linux] (Unix)
* [Networks][nets]
* [Programming Languages][progLang]
* [Databases][db]
* [Docker & Kubernetes][docker]
* [Embedded systems][embSys]
* [CMake][CMake]
-->

[guides]:   ../../../../../README.md
[git]:      ../../../Git_And_GitHub.md
[win]:      ../../../../002_Windows_/Windows.md
[linux]:    ../../../../003_Linux_(Unix)_/Linux_(Unix).md
[nets]:     ../../../../004_Networks_/Networks.md
[progLang]: ../../../../005_Programming_languages_/Programming.md
[db]:       ../../../../006_Databases_/Databases.md
[docker]:   ../../../../007_Docker_and_Kubernetes_/Docker_and_Kubernates.md
[embSys]:   ../../../../008_Embedded_systems_/Embedded_systems.md
[CMake]:    ../../../../009_CMake_/CMake_Tutorial.md

---
<!-- ---------------------------------- * Navigation * ---------------------------------- -->

# <p align=center><b>The most Commonly used commands</b> <i>(Cheat Sheet)</i></p>

### CONTENTS:

* Git Setup
* Git Configuration
* Ignoring patterns
* Managing Files
* Tracking path changes
* Git Branches
* Making Changes
* Undoing Changes
* Rewriting History
* Temporary commits
* Remote Repositories
* Git Cheat Sheet PDF

---

### In case you **don't quite know** something, use the help:

```git
git command --help
```

![Git stage scheme][imgStages]

---

## Git Setup

### Create a **new Git repository** from an existing directory:

```git
git init [directory]
```

### **Clone a repository** *(local or remote via HTTP/SSH)*:

```git
git clone [repo / URL]
```

### Clone a repository **into a specified folder** on your local machine:

```git
git clone [repo / URL] [folder]
```

---

## Git Configuration

### **Display** an information about **configuration** including user name and email:

```git
git config -l
```

### Attach an **author name** to all commits that will appear in the version history:

```git
git config --global user.name "[your_name]"
```

### Attach an **email address** to all commits by the current user:

```git
git config --global user.email "[email_address]"
```

### Apply Git’s automatic **command line coloring** which helps you keep track and revise repository changes:

```git
git config --global color.ui auto
```

### Create a **shortcut** (**alias**) for a Git command:

```git
git config --global alias.[alias_name] [git_command]
```

> ***NOTE:*** Git requires you to type out the entire command to perform actions. Setting shortcuts for commonly used commands can speed up and simplify development. For example, you can use the alias `st` for the status command by typing the command: **`git config --global alias.st status`**

### Set a **default text editor**:

```git
git config --system core.editor [text_editor]
```

### Open Git’s **global configuration file**:

```git
git config --global --edit
```

---

## Ignoring patterns

*Preventing unintentional staging or commiting of files*

### **Save a file** with desired patterns as .gitignore with either direct string matches or wildcard globs:

```git
logs/
*.notes
pattern*/
```

### System **wide ignore pattern** for all local repositories:

```git
git config --global core.excludesfile [file]
```

---

## Managing Files

### Show the **state of the current directory** *(list staged, unstaged, and untracked files)*:

```git
git status
```

### List of the **commit history** of the current branch:

```git
git log
```

### List of the **file / folder history** including of the changes (diffs):

```git
git log -p [file / directory]
```

### List of **all commits from all branches**:

```git
git log --all
```

### **Compare two branches** by showing which commits from the first branch are missing from the second branch:

```git
git log [branch1]..[branch2]
```

### Examine the difference between the **working directory and the index**:

```git
git diff
```

### Explore the difference between the **last commit and the index**:

```git
get diff --cached
```

### Explore the difference **what is staged but not yet** committed**:

```git
get diff --staged
```

### See the difference between the **last commit and the working directory**:

```git
get diff HEAD
```

### See the difference between the **two commits**:

```git
get diff commit1 commit2
```

### See the difference between the **two branches**:

```git
get diff branch1 branch2
```

### See the **date of last changes** and the **author** of the file:

```git
get blame [file]
```

### Display the **content and metadata** of an object *(blob, tree, tag or commit, SHA)*:

```git
git show [object]
```

### Display the **commit** and/or **file changes**:

```git
git show [commit] : [file]
```

---

## Tracking path changes

*Versioning file remove and path changes*

### **Delete the file** from project and stage the removal for commit:

```git
git rm [file]
```

### **Change an existing file path** and stage the move:

```git
git mv [existing_path][new_path]
```

### **Show** all commit logs with **indication of any paths that moved**:

```git
git log --stat -M
```

---

## Git Branches

### List of **all branches** in the repository:

```git
git branch
```

### List of **all remote branches**:

```git
git branch -aa
```

### List of **all local and remote branches**:

```git
git branch -av
```

### **Create a new branch** under a specified name:

```git
git branch [new_branch]
```

### **Switch to a branch** under a specified name *(if it doesn’t exist, a new one will be created)*:

```git
git checkout [branch]
```

> ***NOTE:*** For a more detailed tutorial on working with Git branches, you can refer to our article on [How to Create a New Branch][newBranch] or [How to Switch Branches in Git][gitBranch].

### [**Delete**][gitDelete] a local branch:

```git
git branch -d [branch]
```

### [**Rename**][gitRename] a branch you are **currently working in**:

```git
git branch -m [new_branch_name]
```

### **Merge** the specified branch with the current branch:

```git
git merge [branch]
```

### **Merge** the specified branch_a to the current branch_b:

```git
git checkout [branch_b]
git merge [branch_a]
```

---

## Making Changes

### **Stage changes** for the next commit:

```git
git add [file / directory]
```

### **Stage everything** in the directory for an initial commit:

```git
git add .
```

### **Commit staged snapshots** in the version history with a descriptive message included in the command:

```git
git commit -m "[descriptive_message]"
```

### **Commit all tracked** files with a descriptive message:

```git
git commit -am "[descriptive_message]"
```

### **Add the Tag** to the current commit:

```git
git tag [tag]"
```

---

## Undoing Changes

### **Undo changes** in a file or directory and create a new commit with the [git revert][gitRevert] command:

```git
git revert [file/directory]
```

### [Unstage a file][gitUnstage] without overwriting changes:

```git
git reset [file]
```

### **Clear staging area** up to the last commit:

```git
git reset --hard
```

### **Clear staging area**, rewrite working tree from specified commit:

```git
git reset --hard [commit]
```

### Undo any changes introduced **after the specified commit**:

```git
git reset [commit]
```

### **Show untracked files** which will be removed when you run `git clean` *(do a dry run)*:

```git
git clean -n
```

### **Remove** untracked files:

```git
git clean -f
```

---

## Rewriting History

### **Replace the last commit** with a combination of the staged changes and the last commit combined:

```git
git commit --amend
```

### **Rebase the current branch** with the specified base *(it can be a branch name, tag, reference to a HEAD, or a commit ID)*:

```git
git rebase [branch]
```

### List **changes made to the HEAD** of the local repository:

```git
git reflog
```

---

## Temporary commits

*Temporarily store modified and tracked files in order to change branches.*

### **Save modified and staged changes**:

```git
git stash
```

### **List stack-order** of stashed files canges:

```git
git stash list
```

### **Write working from top** of the stash stack:

```git
git stash pop
```

### **Discard the changes** from top of the stash stack:

```git
git stash drop
```

---

## Remote Repositories

### Create a new **connection to a remote repository** *(give it a name to serve as a shortcut to the URL)*:

```git
git remote add [name] [URL]
```

### **Fetch a branch** from a remote repository *(without merging)*:

```git
git fetch [remote_repo] [branch]
```

### **Fetch a repository** and merge it with the local copy:

```git
git pull [remote_repo]
```

### **Fetch a repository** and rebase it with the local copy:

```git
git pull --rebase
```

### **Push a branch** to a remote repository with all its commits and objects:

```git
git push [remote_repo] [branch]
```

> ***NOTE:*** When a particular remote is no longer needed, you can [remove a git remote from a repository][gitRemove].

---

## [Git Cheat Sheet PDF][pdfCommands]

For future use, you can refer to the one-page Git Commands Reference. Click the [Download][pdfCommands] Cheat Sheet button to save the Git Commands PDF.
<!--
* [Create New Branch][newBranch]
* [Switch Branches][gitBranch]
* [Delete][gitDelete]
* [Rename][gitRename]
* [Revert][gitRevert]
* [Unstaged][gitUnstage]
* [Remove][gitRemove]
* [Download][pdfCommands]
* ![Git stage scheme][imgStages]
-->

[newBranch]:   https://phoenixnap.com/kb/git-create-new-branch
[gitBranch]:   https://phoenixnap.com/kb/git-switch-branch
[gitDelete]:   https://phoenixnap.com/kb/delete-remote-and-local-git-branch
[gitRename]:   https://phoenixnap.com/kb/how-to-rename-git-branch-local-remote
[gitRevert]:   https://phoenixnap.com/kb/git-revert-last-commit
[gitUnstage]:  https://phoenixnap.com/kb/git-unstage-files
[gitRemove]:   https://phoenixnap.com/kb/git-remove-remote
[pdfCommands]: ../files/git-command.pdf
[imgStages]:   ../img/CZ62a.png

---