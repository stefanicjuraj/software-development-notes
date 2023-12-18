# Version Control - Git

Git is a free and open source distributed version control system invented by Linus Torvalds. Linus originally developed Git in order to help him manage the work of maintaining the Linux Kernel.

## Git Internals

The change is being recorded as a tree of objects. Every object is identified by its SHA-1 hash. There are 4 types of objects.

### Blob

Blob is a binary large object that represents any file checked in the git. It stores the file data but does not contain any metadata about the file, such as its name or its directory structure.

When files are committed to a Git repository, they are stored as blobs.

The blob object is immutable, meaning once it is created, it cannot be changed. This ensures that every version of every file in the repository's history is permanently recorded and recoverable.

### Tree

Tree represents a directory listing of blobs and other trees. Each item in the tree is associated with a SHA-1 hash that uniquely identifies it, as well as permissions, type (blob or tree), and the name of the file or directory. Trees play a crucial role in organizing the structure of the repository.

### Commit

Commit is an object with two pointers: one that points to the root tree, and one that points to the older commit. Additionally, a commit object has one or more parent commits (pointers to older commits), allowing Git to track the history of changes. Commits also contain metadata such as the author, committer, commit message, and timestamps, providing context and history to the changes made.

### Tag

Tag holds information about the commit name. It points to the commit. Unlike a branch, which is a pointer to the latest commit in a line of development, a tag points to a specific commit and does not change. Tags can be lightweight or annotated. Lightweight tags are simple pointers to commits, whereas annotated tags are stored as full objects in the Git database. They can contain metadata such as the tagger's name, email, tagging date, and an optional tagging message, similar to a commit message.

![[git-internals.png]]

Branches are pointers to commits. When you create a branch, Git creates a new pointer, and it doesn’t change the repository in any other way.

**HEAD** is a special pointer that points to the branch you’re currently on.

## Creating & Initializing a Repository

### `git init`

The `.git` folder contains all the information Git stores to track your project. If you do not want Git to track your project, just delete the `.git` folder.

## Customizing the Git Environment

### `git config`

As soon as you initialize a Git repository, configure git with your user name and email. This step is crucial and useful when working in a group to identify the user who introduced the changes into the repo.

The config variables can be stored in three different places depending on how you initiate the `git config` command.

```bash
git config user.name "username"
```

- Config data is stored in `.git/config` and applied to the current user and the current working directory. This command needs to be initiated inside your working/project directory.

```bash
git config --global user.name "username"
```

- Config data is stored in `~/.gitconfig` or `~/.config/git/config` file and applied to the current user on the system and all his/her repos.

```bash
git config --system user.name "username"
```

- Config data is stored in `/etc/gitconfig` and applied to all users on the system and all their repositories.

## Checking the Status of Your Changes

Each file in your working directory can be in either **untracked** OR **tracked** (unmodified, modified, or staged).

To determine which files are in which state use the `git status` command.

## Excluding Files from Git

Git provides a mechanism to list files and file patterns that Git should ignore when tracking the repo.

To set up Git to ignore certain files and file patterns, create a `git ignore` containing the list of files to be ignored.

![[gitignore-examples.png]]

### Local `.gitignore`

This file is created and stored in your repository. In order to share the ignore rules with any other users that clone the repository, the `.gitignore` file should also be committed into your repository.

### Global `.gitignore`

You can also create a global `.gitignore` file in your home dir to list rules for ignoring files in every Git repositories on your computer. Once created, you will have to tell Git where the file resides:

```bash
$ git config --global core.excludesfile ~/.gitignore
```

### Explicit repository excludes

If you don't want the `.gitignore` file to be shared with others, you can edit the `.git/info/exclude` file. Any rule you add here will not be checked in, and will only ignore files for your local repository.

## Version-Controlling Existing Files

Developing a project revolves around the edit/stage/commit activities. First, you edit your files in the working directory. When you are ready to save a copy of the current state of the project, you first **stage** changes with `git add`. After you are happy with the staged snapshot, you **commit** it to the project history with `git commit`. The `git reset` command is used to undo a commit or staged snapshot.

Git’s version control model is based on snapshots. The `git commit` command captures a snapshot of the project's currently staged changes. Git records the entire content of each staged file in every commit as opposed to SVN that commits diffs compared to the original file added to the repository.

While committing, write the message in the **imperative** mode. For example, start the line with "Fix", "Add", "Change" instead of "Fixed", "Added", "Changed".

Use `git reset` to undo your local private commits. This will discard commits in a private branch or throw away uncommitted changes.

### Showing Commit Logs - `git log`

After you have created several commits, you can look back to see what is being done so far. Each commit has a unique SHA-1 identifying hash.

### `git tag`

Git has the ability to tag specific points in history as being important. Typically people use this functionality to mark release points (v1.0, and so on).

Git's tagging functionality is particularly useful for marking significant points in the development history, like release points, as it allows developers and teams to identify specific versions easily.

This practice is crucial in version control as it helps in tracking the evolution of the software, managing releases, and coordinating with team members and stakeholders.

![[git-tag.png]]

### Working with branches

A branch represents an independent line of development. The diagram visualizes a repository with two isolated lines of development, one for testing a feature, and one for the main master branch. By developing in branches, it’s not only possible to work on both of them in parallel, but it also keeps the main master branch free from questionable code.

![[working-with-branches.png]]

A branch in Git is simply a movable pointer to one of the commits. The default branch name in Git is **master**. The master branch points to the last commit you made. Every time you commit, it moves forward automatically.

### `git branch`

The `git branch` command lets you create, list, rename, and delete branches. It doesn’t let you switch between branches. For this, you use the `git checkout` and `git merge` commands.

When you create a branch, Git creates a new pointer, it doesn’t change the repository in any other way. So, how does Git know what branch you’re currently on? - It keeps a special pointer called **HEAD**.

### `git checkout`

The `git checkout` command lets you to switch to an existing branch. Checking out a branch updates the files in the working directory to match the version stored in that branch, and it tells Git to record all new commits on that branch. Think of it as a way to select which line of development you’re working on. This also moves the **HEAD** to point to the branch you switched to.

### `git merge`

The `git merge` command lets you take the independent line of development created by `git branch` and integrate it into a single branch.

## Merging Conflicts

If you changed the same part of the same file differently in the two branches you are merging together, Git won’t be able to automatically resolve the conflict – your help will be needed.

![[merging-conflicts.png]]

## A Simple Feature Branch Workflow

1. Whenever you need to develop and test a new feature, create and checkout a new working branch for it.
2. Work in that branch - make changes.
3. Once you have test your feature and got everything working, merge your changes back into the master branch.
4. You may delete the feature branch.
5. Deploy the master.
