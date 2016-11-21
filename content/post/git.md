+++
Categories = []
Tags = []
title = "Git"
draft = false
+++

Commit Related Changes
A commit should be a wrapper for related changes. For example, fixing two different bugs should produce two separate commits. Small commits make it easier for other team members to understand the changes and roll them back if something went wrong. With tools like the staging area and the ability to stage only parts of a file, Git makes it easy to create very granular commits.
Commit Often
Committing often keeps your commits small and, again, helps you commit only related changes. Moreover, it allows you to share your code more frequently with others. That way it’s easier for everyone to integrate changes regularly and avoid having merge conflicts. Having few large commits and sharing them rarely, in contrast, makes it hard both to solve conflicts and to comprehend what happened.
Don’t Commit Half-Done Work
You should only commit code when it’s completed. This doesn’t mean you have to complete a whole, large feature before committing. Quite the contrary: split the feature’s implementation into logical chunks and remember to commit early and often. But don’t commit just to have something in the repository before leaving the office at the end of the day. If you’re tempted to commit just because you need a clean working copy (to check out a branch, pull in changes, etc.) consider using Git’s “Stash” feature instead.
Test Before You Commit
Resist the temptation to commit something that you “think” is completed. Test it thoroughly to make sure it really is completed and has no side effects (as far as one can tell). While committing half-baked things in your local repository only requires you to forgive yourself, having your code tested is even more important when it comes to pushing / sharing your code with others.
Write Good Commit Messages
Begin your message with a short summary of your changes (up to 50 characters as a guideline). Separate it from the following body by including a blank line. The body of your message should provide detailed answers to the following questions: What was the motivation for the change? How does it differ from the previous implementation? Use the imperative, present tense („change“, not „changed“ or „changes“) to be consistent with generated messages from commands like git merge.
Version Control is not a Backup System
Having your files backed up on a remote server is a nice side effect of having a version control system. But you should not use your VCS like it was a backup system. When doing version control, you should pay attention to committing semantically (see “related changes”) – you shouldn’t just cram in files.
Use Branches
Branching is one of Git’s most powerful features – and this is not by accident: quick and easy branching was a central requirement from day one. Branches are the perfect tool to help you avoid mixing up different lines of development. You should use branches extensively in your development workflows: for new features, bug fixes, experiments, ideas…
Agree on a Workflow
Git lets you pick from a lot of different workflows: long-running branches, topic branches, merge or rebase, git-flow… Which one you choose depends on a couple of factors: your project, your overall development and deployment workflows and (maybe most importantly) on your and your teammates’ personal preferences. However you choose to work, just make sure to agree on a common workflow that everyone follows.
The general idea of git-flow is to use the following branch structure in your repository:
•	Development branch (usually called ‘develop’)
This is your main development branch where all the changes destined for the next release are placed, either by directly committing small changes or by merging other branches (e.g. feature branches) into this branch.
•	Production branch (usually called ‘master’)
This branch represents the latest released / deployed codebase. Only updated by merging other branches into it.
•	Feature branches (usually prefixed with ‘feature/’)
When you start work on anything non-trivial, you create a feature branch. When finished, you’ll merge this branch back into the development branch to queue it for the next release.
•	Release branches (usually prefixed with ‘release/’)
When you’re about to package a new release, you create a release branch from the development branch. You can commit to it during your preparation for a release, and when it’s ready to be deployed, you merge it into both the development branch and the master branch (to indicate that the release has been deployed).
•	Hotfix branches (usually prefixed with ‘hotfix/’)
If you need to patch the latest release without picking up new features from the development branch, you can create a hotfix branch from the latest deployed code in master. Once you’ve made your changes, the hotfix branch is then merged back into both the master branch (to update the released version) and the development branch (to make sure the fixes go into the next release too)
Git in sourceTree
Getting started with git-flow
There’s a handy new addition to the toolbar in SourceTree 1.5 (keyboard shortcut Cmd-Alt-F):

Based on the current state of the repository, the Git-flow button will bring up a dialog with the most likely action you’d want to perform next. So if you haven’t set up git-flow on this repo yet, it’ll help you do that by default. If you’re on the development branch, it will default to starting a new feature. If you’re already on a feature branch, it will offer to finish your current feature and merge it back into the development branch, and so on. You can always get to all the other git-flow actions via this button as well, but most of the time the default option will be the action you’ll want SourceTree to perform.
If you haven’t used git-flow already on this repository, the first thing SourceTree will do is initialise your repository to use it. You’ll probably just want to use the defaults in the initialisation window so that’s not covered here. For more details please see the Help section included in SourceTree. Next up, we’ll concentrate on the actions we can perform with Git-flow and SourceTree.
Starting a feature
You can commit trivial changes directly to the development branch (‘develop’) if you like, but any time you start on something non-trivial you should explicitly start a new feature. This ‘Start Feature’ action will be the default action when you click the Git-flow button if you are currently on the dev branch.

The first thing to note is the ‘Preview’ window, which is present on all of the action dialogs and shows you what will actually happen when you confirm the dialog. In this case, a new feature branch called ‘feature/my-new-feature’ will be created (I used the default prefix when I initialised this repository). You commit your feature implementations to this branch. If you want, you can push the feature branch to your remote while you work on it (your team can decide on whether that’s normal practice or not).
If at any time you want to switch branches, either to another feature branch or to somewhere else, just use the normal mechanisms in SourceTree to do that, such as double-clicking a log entry or a branch in the sidebar. Git-flow determines your context simply from the branch you currently have checked out, so it’s fine to jump around if you like.
Finishing a feature
Eventually when you’re done implementing a feature, use the ‘Finish Feature’ action (again, this will be the default action from the toolbar button if you’re on a feature branch):

Again, the Preview shows you what will happen — the feature branch will merge into the main development branch, essentially queueing it for inclusion in the next release. Feature branches are deleted by default but you can opt to retain them if you like.
Starting a release
You start a release branch when you want to start preparing a new release, which probably coincides with a feature freeze. Accessing the Start Release option –either from the menu or from the toolbar action selection window — brings up the following dialog:

The preview shows that a new release branch will be created. Most of the time, you want to start the release from the latest commit in the development branch, but you can choose to base it on another commit if you wish. This essentially freezes the release, so it’s not affected by subsequent development. You can also perform preparatory tasks for the release process on this branch, such as updating the version number in source files, updating changelogs, or committing other tweaks. Once these tweaks are done, you can finish the release as described below.
Finishing a release
Once all the adjustments required for the release are done and committed, you can conclude the release process.If you’re on the release branch already, the git-flow button will show you the following dialog:

The preview illustrates that the release branch will be merged into the production branch (‘master’ or ‘default’ normally) to indicate an update to the deployed version. Sourcetree will also create a tag here for the release. The release branch changes will also merge back into the development branch to make sure the develop branch is kept up to date.
Starting a hotfix
What if you need to just fix a bug on the latest release? You don’t want to create a new release, because that will pick up the recent changes from the development branch. So instead, you can start a hot fix:

Hot fixes always start from the latest production code from the ‘master’ or ‘default’ branch. Other than that, they’re basically the same as release branches. Moreover, when you’re finished with the hot-fix, they behave the same way as finishing a release branch. The changes are merged back into both the production branch and the development branch, and a tag is created on the production branch for the hot fix release.
Wrapping up
Git-flow is a great way to automate your handling of branch-based development in Git, and SourceTree now provides a simple and clear way to use it with an easy-to-use and intuitive GUI. Big thanks to Vincent Driessen for coming up with git-flow in the first place!
