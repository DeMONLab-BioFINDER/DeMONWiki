# Git wiki

---

This page provides basic intro/setup/usage of Git and GitHub. If you want to learn more about git and github, always recommended to check [Git doc](https://git-scm.com/doc) and [GitHub docs](https://docs.github.com/en). Majority of this page is from [Git doc](https://git-scm.com/doc).

## Introduction & Setup

---

### Why version control

Version control is a system that records changes to a file or set of files over time so that you can recall specific versions later. For example, you will use software source code as the files being version controlled,
though in reality you can do this with nearly any type of file on a computer.

If you are a graphic or web designer and want to keep every version of an image or layout (which
you would most certainly want to), a Version Control System (VCS) is a very wise thing to use. It
allows you to revert selected files back to a previous state, revert the entire project back to a
previous state, compare changes over time, see who last modified something that might be causing
a problem, who introduced an issue and when, and more. Using a VCS also generally means that if
you screw things up or lose files, you can easily recover. In addition, you get all this for very little
overhead.

### Why Git

Git is a free distributed VCS with fast speed and strong support for non-linear development (many branches), which was invented by
Linus Torvalds for Linux project in 2005.

### GitHub

GitHub is the single largest host for Git repositories, and is the central point of collaboration for
millions of developers and projects. A large percentage of all Git repositories are hosted on GitHub,
and many open-source projects use it for Git hosting, issue tracking, code review, and other things.
So while it’s not a direct part of the Git open source project, there’s a good chance that you’ll want
or need to interact with GitHub at some point while using Git professionally.

### Setup

#### Remote setup

In DeMONLab, we used Github as remote repo, you could visit [Github](github.com/) to create a account. Once you have your account, you could ask labmates to invite you to join our [DeMONLab-BioFINDER](https://github.com/DeMONLab-BioFINDER) organization.

#### Local setup

Most Linux and Macos machines are installed with git. If you are using Windows (unfortunately), you could download and install git from [here](https://gitforwindows.org/).

> [!NOTE]
> Always recommended to use latest stable version of softwares, for new features and safety reasons.

##### Configuration

Once you have installed/updated git, you need to setup with your Github `<username>` and `<email>`.

```sh
# If <username> is AlzheimerDisease and <email> is ad1901@brain.com
$ git config --global user.name "AlzheimerDisease"
$ git config --global user.email ad1901@brain.com
```

## DeMONLab Git Workflow

---

> [!TODO]
> Please stay tuned.

## Git Commands

---

You could always check the usage of `git` commands using `git help <verb>`. For example, you could get the manpage help for the `git config` command by running this:

```sh
$ git help config
```

You could also find in-person help on [stack overflow](https://stackoverflow.com/questions/tagged/git).

#### Initializing a repository

You could initialize a repo for a existing directory using:

```sh
$ git init <ProjDir>
```

If you want to start version-controlling existing files (as opposed to an empty directory), you should probably begin tracking those files and do an initial commit. You can accomplish that with a few `git add` commands that specify the files you want to track, followed by a `git commit`:

```
$ git add .
$ git add LICENSE
$ git commit -m 'Initial project version'
```

Alternatively, you could clone an existing repo using:

```
$ git clone <url>
```

#### Ignoring files

You will have a class of files (e.g., `.DS_Store` from macos) you don't want Git to automatically add/track. In such case, you can create a file listing patterns to match them named `.gitignore`. Here is an example `.gitignore` file:

```sh
# An .gitignore example

# ignore all .DS_Store files
*.DS_Store

# ignore all .a files
*.a
# but do track lib.a, even though you're ignoring .a files above
!lib.a

# only ignore the TODO file in the current directory, not subdir/TODO
/TODO

# ignore all files in any directory named build
build/

# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt

# ignore all .pdf files in the doc/ directory and any of its subdirectories
doc/**/*.pdf
```

Note that `.gitignore` works by commands `git add .gitignore` and `git commit -m "gitignore"`. Then git will ignore/untrack these files in future commits.

If you want to ignore a file that is already checked in, you must untrack the file before you add a rule to ignore it. From your terminal, untrack the file.

```sh
$ git rm --cached <filename>
```

#### Checking the status of your files

The main tool you use to determine which files are in which state is the `$ git status` command. If you run this command directly after a clone, you should see something like this:

```sh
$ git status
# On branch main
nothing to commit (working directory clean)
```

If you add a new file (e.g., `README` file) to your project, and the file didn't exist before, when you run a `$ git status` you should see your untracked file like this:

```sh
$ git status
# On branch main
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#   README
nothing added to commit but untracked files present (use "git add" to track)
```

#### Staging files

After initializing a git repository in the chosen directory, all files will now be tracked. Any changes made to any file will be shown after a `$ git status` as changes not staged for commit.

To stage changes for commit you need to add the file(s) - or in other words, stage file(s).
In order to begin tracking a new file, you use the command `git add`. To begin tracking the README file, you can run this:

```sh
$ git add README
```

If you run your status command again, you can see that your `README` file is now tracked and staged to be committed:

```sh
$ git status
# On branch main
# Your branch is up-to-date with 'origin/main'.
# Changes to be committed:
#   (use "git restore --staged <file>..." to unstage)
#       new file: README
```

Here are some options of `git add` command:

```sh
# Adding a file
$ git add filename

# Adding all files
$ git add -A

# Adding all files changes in a directory
$ git add .

# Choosing what changes to add (this will got through all your changes and you can 'Y' or 'N' the changes)
$ git add -p
```

#### Viewing your staged/unstaged changes

If the `git status` command is too vague for you — you want to know exactly what you changed, not just which files were changed — you can use the `git diff` command.

Basically, `git diff` answers two questions:

- What have you changed but not yet staged?
- what have you staged that you are about to commit?

Let’s say you edit and stage the `README` file again and then edit the `CONTRIBUTING.md` file without staging it. If you run your git status command, you once again see something like this:

```sh
$ git status
# On branch main
# Your branch is up-to-date with 'origin/main'.
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#       modified: README
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#       modified: CONTRIBUTING.md
```

To see what you’ve changed but not yet staged, type git diff with no other arguments:

```sh
$ git diff
# diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
# index 8ebb991..643e24f 100644
# --- a/CONTRIBUTING.md
# +++ b/CONTRIBUTING.md
# @@ -65,7 +65,8 @@ branch directly, things can get messy.
# Please include a nice description of your changes when you submit your PR;
# if we have to read the whole diff to figure out why you're contributing
# in the first place, you're less likely to get feedback and have your change
# -merged in.
# +merged in. Also, split your changes into comprehensive chunks if your patch is
# +longer than a dozen lines.
# If you are starting to work on a particular area, feel free to submit a PR
# that highlights your work in progress (and note in the PR title that it's
```

That command compares what is in your working directory with what is in your staging area. The result tells you the changes you’ve made that you haven’t yet staged.

If you want to see what you’ve staged that will go into your next commit, you can use `git diff --staged`. This command compares your staged changes to your last commit:

```sh
$ git diff --staged
# diff --git a/README b/README
# new file mode 100644
# index 0000000..03902a1
# --- /dev/null
# +++ b/README
# @@ -0,0 +1 @@
# +My Project
```

Some options for `git diff`:

```sh
# See all (non-staged) changes done to a local repo
$ git diff

# See all (staged) changes done to a local repo
$ git diff --cached

# Check what the changes between the files you've committed and your Github repo
$ git diff --stat origin/main

# Check what the changes between the files you've committed and DeMONLab's repo
$ git diff --stat upstream/main
```

#### Committing files

After adding/staging a file, the next step is to commit staged file(s) using:

```
git commit
```

Some options for `git commit`:

```sh
# Commit staged file(s)
$ git commit -m 'commit message'

# Add file and commit
$ git commit filename -m 'commit message'

# Add file and commit staged file
$ git commit -am 'insert commit message'

# Amending the last commit
$ git commit --amend 'new commit message' or no message to maintain previous message

# Squashing commits together
$ git rebase -i
This will give you an interface on your core editor:
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
```

#### Removing files

To remove a file from Git, you have to remove it from your tracked files (more accurately, remove it
from your staging area) and then commit. The `git rm` command does that, and also removes the file
from your working directory so you don’t see it as an untracked file the next time around.

If you simply remove the file from your working directory, it shows up under the “Changes not
staged for commit” (that is, unstaged) area of your git status output:

```sh
$ rm PROJECTS.md
$ git status
# On branch main
# Your branch is up-to-date with 'origin/main'.
# Changes not staged for commit:
#   (use "git add/rm <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#       deleted: PROJECTS.md
# no changes added to commit (use "git add" and/or "git commit -a")
```

Then, if you run git rm, it stages the file’s removal:

```sh
$ git rm PROJECTS.md
rm 'PROJECTS.md'
$ git status
# On branch main
# Your branch is up-to-date with 'origin/main'.
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#       deleted: PROJECTS.md
```

The next time you commit, the file will be gone and no longer tracked. If you modified the file or
had already added it to the staging area, you must force the removal with the `-f` option. This is a
safety feature to prevent accidental removal of data that hasn’t yet been recorded in a snapshot and
that can’t be recovered from Git.

Another useful thing you may want to do is to keep the file in your working tree but remove it from
your staging area. In other words, you may want to keep the file on your hard drive but not have
Git track it anymore. This is particularly useful if you forgot to add something to your `.gitignore`
file and accidentally staged it, like a large log file or a bunch of .a compiled files. To do this, use the
`--cached` option:

```sh
$ git rm --cached README
```

#### Viewing the Commit History

After you have created several commits, or if you have cloned a repository with an existing commit
history, you’ll probably want to look back to see what has happened. The most basic and powerful
tool to do this is the `git log` command.

```sh
# Show a list of all commits in a repository. This command shows everything about a commit, such as commit ID, author, date and commit message.
$ git log

# List of commits showing commit messages and changes
$ git log -p

# List of commits with the particular expression you are looking for
$ git log -S 'something'

# List of commits by author
$ git log --author 'Author Name'

# Show a list of commits in a repository in a more summarised way. This shows a shorter version of the commit ID and the commit message.
$ git log --oneline

# Show a list of commits in a repository since yesterday
$ git log --since=yesterday

# Shows log by author and searching for specific term inside the commit message
$ git log --grep "term" --author "name"
```

#### Undoing Things

> [! WARNING]
> At any stage, you may want to undo something. Here, we’ll review a few basic tools for undoing
> changes that you’ve made. Be careful, because you can’t always undo some of these undos. This is
> one of the few areas in Git where you may lose some work if you do it wrong.

#### Amending commit

One of the common undos takes place when you commit too early and possibly forget to add some
files, or you mess up your commit message. If you want to redo that commit, make the additional
changes you forgot, stage them, and commit again using the `--amend` option:

```sh
$ git commit --amend
```

As an example, if you commit and then realize you forgot to stage the changes in a file you wanted
to add to this commit, you can do something like this:

```sh
$ git commit -m 'Initial commit'
$ git add forgotten_file
$ git commit --amend
```

> [! CAUTION]
> Only amend commits that are still local and have not been pushed somewhere.
> Amending previously pushed commits and force pushing the branch will cause
> problems for your collaborators. For more on what happens when you do this and
> how to recover if you’re on the receiving end read [The Perils of Rebasing]().

##### Unstaging a staged file

For example, let’s say you’ve changed two files and
want to commit them as two separate changes, but you accidentally type git add \* and stage them
both. How can you unstage one of the two? The git status command reminds you:

```sh
$ git add *
$ git status
# On branch main
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#       renamed: README.md -> README
#       modified: CONTRIBUTING.md
```

Right below the “Changes to be committed” text, it says `use git reset HEAD <file>… to unstage`. So,
let’s use that advice to unstage the CONTRIBUTING.md file:

```sh
$ git reset HEAD CONTRIBUTING.md
# Unstaged changes after reset:
# M CONTRIBUTING.md
$ git status
# On branch main
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#       renamed: README.md -> README
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#       modified: CONTRIBUTING.md
```

The command is a bit strange, but it works. The CONTRIBUTING.md file is modified but once again
unstaged.

> [!CAUTION]
> It’s true that git reset can be a dangerous command, especially if you provide the
> --hard flag. However, in the scenario described above, the file in your working
> directory is not touched, so it’s relatively safe.

Some options for `git reset` commands:

```sh
# Mixes your head with a give sha
# This lets you do things like split a commit
$ git reset --mixed [sha]

# Upstream main
$ git reset HEAD upstream/main -- filename

# The version from the most recent commit
$ git reset HEAD -- filename

# The version before the most recent commit
$ git reset HEAD^ -- filename

# Move head to specific commit
$ git reset --hard sha

# Reset the staging area and the working directory to match the most recent commit. In addition to unstaging changes, the --hard flag tells Git to overwrite all changes in the working directory, too.
$ git reset --hard
```

##### Unmodifying a Modified File

What if you realize that you don’t want to keep your changes to the CONTRIBUTING.md file? How can
you easily unmodify it — revert it back to what it looked like when you last committed (or initially
cloned, or however you got it into your working directory)? Luckily, git status tells you how to do
that, too. In the last example output, the unstaged area looks like this:

```sh
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#       modified: CONTRIBUTING.md
```

It tells you pretty explicitly how to discard the changes you’ve made. Let’s do what it says:

```sh
$ git checkout -- CONTRIBUTING.md
$ git status
# On branch main
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#       renamed: README.md -> README
```

You can see that the changes have been reverted.

> [!CAUTION]
> It’s important to understand that git checkout -- <file> is a dangerous command.
> Any local changes you made to that file are gone — Git just replaced that file with
> the last staged or committed version. Don’t ever use this command unless you
> absolutely know that you don’t want those unsaved local changes.

> [!NOTE]
> Remember, anything that is committed in Git can almost always be recovered. Even commits that
> were on branches that were deleted or commits that were overwritten with an --amend commit can
> be recovered. However, anything you lose that was never
> committed is likely never to be seen again.

If you would like to keep the changes you’ve made to that file but still need to get it out of the way
for now, there is a better command `git stash`:

Git stash is a very useful command, where git will 'hide' the changes on a dirty directory - but no worries you can re-apply them later. The command will save your local changes away and revert the working directory to match the HEAD commit.

```sh
# Stash local changes
$ git stash

# Stash local changes with a custom message
$ git stash save "this is your custom message"

# Re-apply the changes you saved in your latest stash
$ git stash apply

# Re-apply the changes you saved in a given stash number
$ git stash apply stash@{stash_number}

# Drops any stash by its number
$ git stash drop stash@{0}

# Apply the stash and then immediately drop it from your stack
$ git stash pop

# 'Release' a particular stash from your list of stashes
$ git stash pop stash@{stash_number}

# List all stashes
$ git stash list

# Show the latest stash changes
$ git stash show

# See diff details of a given stash number
$ git diff stash@{0}
```

Git version 2.23.0 introduced a new command: `git restore`. It’s basically an alternative to git reset
which we just covered. From Git version 2.23.0 onwards, Git will use `git restore` instead of `git
reset` for many undo operations.

#### Branching and Merging

```sh
# Creating a local branch
$ git checkout -b branchname

# Switching between 2 branches (in fact, this would work on terminal as well to switch between 2 directories - $ cd -)
$ git checkout -

# Pushing local branch to remote
$ git push -u origin branchname

# Deleting a local branch - this won't let you delete a branch that hasn't been merged yet
$ git branch -d branchname

# Deleting a local branch - this WILL delete a branch even if it hasn't been merged yet!
$ git branch -D branchname

# Remove any remote refs you have locally that have been removed from your remote (you can substitute <origin> to any remote branch)
$ git remote prune origin

# Viewing all branches, including local and remote branches
$ git branch -a

# Viewing all branches that have been merged into your current branch, including local and remote
$ git branch -a --merged

# Viewing all branches that haven't been merged into your current branch, including local and remote
$ git branch -a --no-merged

# Viewing local branches
$ git branch

# Viewing remote branches
$ git branch -r
```

#### Fetching and Checking Out Remote Branches

```sh
# This will fetch all the remote branches for you.
$ git fetch origin

# With the remote branches in hand, you now need to check out the branch you are interested in, giving you a local working copy:
$ git checkout -b test origin/test

# Deleting a remote branch
$ git branch -rd origin/branchname
$ git push origin --delete branchname  or  $ git push origin:branchname
```

#### Merging branch to main

```sh
# First checkout main
$ git checkout main

# Now merge branch to main
$ git merge main

# To cancel a merge
$ git merge --abort
```

#### Updating a local repository with changes from a Github repository

```sh
$ git pull origin main
```

#### Tracking existing branch

```sh
$ git branch --set-upstream-to=origin/foo foo
```

#### Git remote

```sh
# Show where 'origin' is pointing to and also tracked branches
$ git remote show origin

# Show where 'upstream' is pointing to and also tracked branches
$ git remote show upstream

# Show where 'origin' or 'upstream' is pointing to
$ git remote -v

# Change the 'origin' remote's URL
$ git remote set-url origin https://github.com/user/repo.git

# Add a new remote
# Usually use to 'rebase' from forks
$ git remote add [NAME] https://github.com/user/fork-repo.git
```

#### Git grep

```sh
# 'Searches' for parts of strings in a directory
$ git grep 'something'

# 'Searches' for parts of strings in a directory and the -n prints out the line numbers where git has found matches
$ git grep -n 'something'

# 'Searches' for parts of string in a context (some lines before and some after the grepped term)
$ git grep -C<number of lines> 'something'

# 'Searches' for parts of string and also shows lines BEFORE the grepped term
$ git grep -B<number of lines> 'something'

# 'Searches' for parts of string and also shows lines AFTER the grepped term
$ git grep -A<number of lines> 'something'
```

#### Git blame

```sh
# Show alteration history of a file with the name of the author
$ git blame [filename]

# Show alteration history of a file with the name of the author && SHA
$ git blame [filename] -l
```

#### Useful commands

```sh
# Check if a sha is in production
$ git tag --contains [sha]

# Number of commits by author
$ git shortlog -s --author 'Author Name'

# List of authors and commits to a repository sorted alphabetically
$ git shortlog -s -n

# List of commit comments by author
$ git shortlog -n --author 'Author Name'
# This also shows the total number of commits by the author

# Number of commits by contributors
$ git shortlog -s -n

# Undo local changes to a File
$ git checkout -- filename

# Shows more detailed info about a commit
$ git cat-file sha -p

# Show number of lines added and removed from a repository by an author since some time in the past.
$ git log --author="Author name" --pretty=tformat: --numstat --since=month | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "added lines: %s, removed lines: %s, total lines: %s\n", add, subs, loc }'
```

#### Useful alias

To add an alias simply open your .gitconfig file on your home directory and include the alias code

```sh
# Shows the log in a more consisted way with the graph for branching and merging
lg = log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit
```

## Bugs and questions

---

If you have any questions or find any bugs for this page, you could check with Lijun (anlijuncn@gmail.com)
