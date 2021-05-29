This is a guide to a typical Git workflow with yuzu. It covers forking from the main repository, creating a branch, keeping your branch up to date with the main repository, resolving conflicts, and merging back into the main repository. It's not meant to be a hard-and-fast set of rules. However, if you follow something along these lines, you'll be less likely to piss people off.

It's appreciated if every single commit in a branch on its own compiles on all supported platforms (Windows, Linux, and OS X) and doesn't cause any regressions if the commits after it were left unmerged. We understand that with early development, sometimes it's easier to commit early-and-often, and sometimes you may unintentionally break things (and then later fix them in your branch). If this is part of your workflow, we expect appropriate use of Git rebase to squash broken commits and resolve merge conflicts. If you don't know how Git rebase works, please read [this article](http://git-scm.com/book/en/Git-Branching-Rebasing) before developing for yuzu.

## Terminology

* `upstream`: Main project repository (https://github.com/yuzu-emu/yuzu)
* `origin`: Your GitHub forked project repository (e.g. https://github.com/bunnei/yuzu)

## Before you begin

1. GitHub fork the project
2. Clone your GitHub fork locally
    * `git clone https://github.com/your-username/yuzu.git`
3. Grab the submodules
    * `git submodule update --init --recursive`
4. Set your `upstream` to the main project repository
    * `git remote add upstream https://github.com/yuzu-emu/yuzu.git`
5. Set your Git identity configuration
    * `git config --global user.name "your-username"`
    * `git config --global user.email your-email@example.com`

## Create a new branch

1. Create your branch from the latest `upstream/master` (Note: please format-branch-names-like-this)
    * `git fetch upstream && git checkout -b new-branch-name upstream/master`
2. Push your new branch to `origin` (required later for a pull request)
    * `git push origin new-branch-name`

## Scenario A: You did some work in your branch... Then, someone committed something to `upstream/master` that you want!

1. Make sure you're on your branch
    * `git checkout new-branch-name`
2. Rebase `upstream/master` onto it. With the rebase, move all of your changes to the top, and put all of the new master changes immediately after where you branched from. The goal should be that the branch now appears as though you just created it from `upstream/master`, and then committed all of your new stuff.
    * `git rebase upstream/master`

## Scenario B: You did some more work in your branch... Then, someone committed something to `upstream/master` that will cause conflicts when trying to get the branch merged back to upstream/master!

1. From your branch, rebase `upstream/master`
    * `git checkout new-branch-name`
    * `git rebase -i upstream/master`

## Scenario C: I made a commit and want to add other changes to it

To append changes to the most recently made commit, simply perform the following:

1. Stage the changed files to append to the commit with either:
    * `git add <list of files separated by spaces>`
    * or `git add -u` to stage all modified files.

2. Enter:
    * `git commit --amend` — if you want to also change your commit message
    * `git commit --amend --no-edit` — if you want to append your changes to the commit and make no changes to the commit message

3. Done

## Your branch is getting near completion, now you're ready for a pull request!

1. From your branch, rebase `upstream/master`
    * `git checkout new-branch-name`
    * `git rebase -i upstream/master`
2. Update `origin/new-branch-name`
    * `git push origin new-branch-name --force`
3. Create the pull request on GitHub to merge `origin/new-branch-name` into `upstream/master`

## Gracefully receive feedback from the team

* Address each comment with a commit as needed

## Once your pull request is ready to be merged...

1. From your branch, interactive rebase to squash all of the new commits (as a result of the pull request feedback) into the commits that they were addressing
    * `git checkout new-branch-name`
    * `git rebase -i upstream/master`
        * Now, you should see a file containing all the commits on this branch.
        * For all commits that address feedback, replace `pick` with `fixup`. Re order if required (beware, you might get conflicts at this stage! Resolve them carefully, then use `git rebase --continue`)
        * You can also change commit messages by replacing `pick` with `reword`.
        * Then follow the steps as directed by Git (These are not specific to yuzu, so you shouldn't have a problem if you use Git regularly.)
        * Rebase complete!
2. Update `origin/new-branch-name`
    * `git push origin new-branch-name --force`
3. Merge your branch in
    * Always merge using the >merge< button in the GitHub pull request
    * If GitHub says the branch cannot be merged automatically, you've likely done something incorrectly (e.g. you did not fully rebase changes from `upstream/master` into your branch). If things don't work for you, don't hesitate to ask us for help @ #yuzu-emu on [libera](https://web.libera.chat) or @ #yuzu-general on [Discord](https://discordapp.com/invite/u77vRWY). Mastering Git is not as easy as it might sound, but we'll happily help you get started.