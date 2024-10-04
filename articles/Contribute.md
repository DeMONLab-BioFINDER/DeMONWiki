# How to contribute to DeMON Lab wiki

---

This documentation shows how to contribute to DeMON Lab wiki.

## 1. Get access to DeMONLabWiki repo

---

DeMonWiki is a public repo, you should visit it by clicking its [link](https://github.com/DeMONLab-BioFINDER/DeMONWiki).

## 2. Contribute contents

---

The way contributing to DeMONWiki follows general git workflow. If you are not familiar with git workflow, you are highly recommended to check [Chapter 1.1](https://demonlab-biofinder.github.io/DeMONWiki/articles/chapter_1/Ch1.1_GitWiki.html) for more details. You should edit contents on a new branch, add your changes and commit your changes.

### Clone repo locally

---

You could clone DeMONWiki repo to your local machine using `git clone git@github.com:DeMONLab-BioFINDER/DeMONWiki.git` showing as follows. If you are working on a Windows machine, you might need to install git bash following [Chapter 1.1](https://demonlab-biofinder.github.io/DeMONWiki/articles/chapter_1/Ch1.1_GitWiki.html).

Once you have cloned DeMONWiki on your local machine, you could run `cd DeMONWiki` to enter DeMONWiki directory.

### Create a new branch

---

For easy tracking, you are required to edit on other branches instead of on `main` branch. You could run `git branch` to check how many branches are available.

If you want to create a new branch, you could run `git checkout -b <NewBranchName>`.

### Edit

---

The DeMONWiki is powered by the Gitbook service, which means all documents are in form of MarkDown format. If you are not familiar with MarkDown format, you could refer [here](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax) for MarkDown usage.

A Preview mode will be very helpful for editing MarkDown files, there are many tools, for example, VS Code.

### Add & commit

---

Once you have edited the contents locally, you are ready to submit all your changes.

You could check the status of current branch by `git status` command.

If you are satisfied with all your changes, you will need to run `git add .` command to add these changes, then run `git commit -m <Your Short Commit Summary>` to commit changes.

## 3. Submit Pull Request (PR)

---

If you have added and committed all your changes, you are ready to push your commits to the remote repo by running `git push origin <NewBranchName>`.

If succeed, you will see the updated `<NewBranchName>` branch on GitHub page (remote repo).

To make the changed you made merge into `main` branch, a PR is expected. You could got to `Pull Request` tab and click submit a new PR. You will need to ask DeMON labmates to review your PR.

## 4. Review & merge your PR

---

The purpose of PR is multi-fold. The main reason is that to protect changes from untrusted parties given DeMONWiki is a public repo. Only authorized DeMON labmates could merge a PR. Another reason is to improve the quality of DeMONWiki.

### PR review

---

As a reviewer, you should keep in mind that the DeMONWiki should be detailed for new DeMON members as much as possible. For example, are the instructions intuitive for new DeMON members with diverse backgrounds? If text is not informative, should figures be provided? Are there any

When you review the PR, you could help improve the quality by finding typos, bugs, grammar mistakes etc.

Once all comments from reviewers have been solved, the PR could be merged into `main` branch.

# Bugs and questions

---

If you have any questions or find any bugs for this page, you could check with Lijun (anlijuncn@gmail.com)
