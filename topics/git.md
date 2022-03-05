Git it?

## How to Rename the master branch to main in Git

### Renaming the Local `master` Branch to `main`

The first step is to rename the "master" branch in your *local* Git repositories:

```bash
$ git branch -m master main
```

Let's quickly check if this has worked as expected:

```bash
$ git status
On branch main
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
```

So far, so good! The local branch has been renamed - but we now need to make some changes on the *remote* repository as well!

### Renaming the Remote `master` Branch as well

In the second step, we'll have to *create a new branch* on the remote named "main" - because Git does not allow to simply "rename" a  remote branch. Instead, we'll have to create a new "main" branch and  then delete the old "master" branch.

Make sure your current local HEAD branch is still "main" when executing the following command:

```bash
$ git push -u origin main
```

We now have a new branch on the remote named "main". Let's go on and remove the old "master" branch on the remote:

```bash
$ git push origin --delete master
```

Depending on your exact setup, this might have worked and the  renaming is successful. In many cases, however, you will see an error  message like the following one:

```bash
To https://github.com/gittower/git-crashcourse.git
! [remote rejected]   master (refusing to delete the current branch: refs/heads/master)
error: failed to push some refs to 'https://example@github.com/gittower/git-crashcourse.git'
```

GitHub, like other code-hosting platforms, too, expects you to define a "default" branch - and deleting this is not allowed. Additionally,  your old "master" might be set as "protected". You'll need to resolve this om GitHub before you can go on. It's located under the branches tab.

### What Your Teammates Have to Do

If other people on your team have local clones of the repository, they will also have to perform some steps on their end:

```bash
# Switch to the "master" branch:
$ git checkout master

# Rename it to "main":
$ git branch -m master main

# Get the latest commits (and branches!) from the remote:
$ git fetch

# Remove the existing tracking connection with "origin/master":
$ git branch --unset-upstream

# Create a new tracking connection with the new "origin/main" branch:
$ git branch -u origin/main
```

### Things to Keep in mind

As you've seen, the process of renaming "master" to "main" isn't terribly complicated. 

One thing to keep in mind, though, is your toolchain: if you're using a CI/CD tool, GitHub Actions, Azure DevOps / Atlassian Bamboo / GitLab  CI pipelines or anything like this, you should check these tools  thoroughly. If they depend on a specific "origin/master" branch, you  might have to change their settings, too.

## Using the Amend Command

```bash
git add changelog.md

git commit --amend --no-edit
# done. can push to origin like normal. Otherwise, run the following command below:

git push -f origin main
```





