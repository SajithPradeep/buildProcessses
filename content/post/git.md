+++
Categories = []
Tags = []
title = "Git"
draft = false
+++
<p class="custom-heading"> What is version control, and why should you care? </p>
<p>Version control is a system that records changes to a file or a set of files over time so that you can recall specific versions later. If you’re a developer and want to keep every version of your code, it is very wise to use a Version Control System (VCS). 
A VCS allows you to: revert files back to a previous state, revert the entire project back to a previous state, review changes made over time, see who last modified something that might be causing a problem, who introduces an issue and when, and more. Using a VCS also means that if you mess things up or lose files, you can generally recover easily.</p>

<p class="custom-heading"> What is a commit? </p>
<p> A commit should be a wrapper for related changes. For example, fixing two different bugs should produce two separate commits. Small commits make it easier for other team members to understand the changes and roll them back if something went wrong. With tools like the staging area and the ability to stage only parts of a file, Git makes it easy to create very granular commits. </p>

<p class="custom-heading"> What are the good practices while committing the code? </p>

<p class="custom-sub-heading"> How often should you commit?</p>
<p> Committing often keeps your commits small and, again, helps you commit only related changes. Moreover, it allows you to share your code more frequently with others. That way it’s easier for everyone to integrate changes regularly and avoid having merge conflicts. Having few large commits and sharing them rarely, in contrast, makes it hard both to solve conflicts and to comprehend what happened. </p>

<p class="custom-sub-heading"> Don’t Commit Half-Done Work </p>
<p> You should only commit code when it’s completed. This doesn’t mean you have to complete a whole, large feature before committing. Quite the contrary: split the feature’s implementation into logical chunks and remember to commit early and often. But don’t commit just to have something in the repository before leaving the office at the end of the day. If you’re tempted to commit just because you need a clean working copy (to check out a branch, pull in changes, etc.) consider using Git’s “Stash” feature instead. </p>

<p class="custom-sub-heading"> Test Before You Commit </p>
<p> Resist the temptation to commit something that you “think” is completed. Test it thoroughly to make sure it really is completed and has no side effects (as far as one can tell). While committing half-baked things in your local repository only requires you to forgive yourself, having your code tested is even more important when it comes to pushing / sharing your code with others.</p>

<p class="custom-sub-heading"> Write Good Commit Messages</p>
<p> Begin your message with a short summary of your changes (up to 50 characters as a guideline). Separate it from the following body by including a blank line. The body of your message should provide detailed answers to the following questions: What was the motivation for the change? How does it differ from the previous implementation? Use the imperative, present tense („change“, not „changed“ or „changes“) to be consistent with generated messages from commands like git merge.</p>

<p class="custom-sub-heading"> Version Control is not a Backup System</p>
<p> Having your files backed up on a remote server is a nice side effect of having a version control system. But you should not use your VCS like it was a backup system. When doing version control, you should pay attention to committing semantically (see “related changes”) – you shouldn’t just cram in files.</p>

<p class="custom-sub-heading"> Use Branches</p>
<p> Branching is one of Git’s most powerful features – and this is not by accident: quick and easy branching was a central requirement from day one. Branches are the perfect tool to help you avoid mixing up different lines of development. You should use branches extensively in your development workflows: for new features, bug fixes, experiments, ideas… etc.</p>

<p class="custom-sub-heading"> Agree on a Workflow</p>
<p> Git lets you pick from a lot of different workflows: long-running branches, topic branches, merge or rebase, git-flow… Which one you choose depends on a couple of factors: your project, your overall development and deployment workflows and (maybe most importantly) on your and your teammates’ personal preferences. However you choose to work, just make sure to agree on a common workflow that everyone follows.</p>
<p>The general idea of git-flow is to use the following branch structure in your repository:</p>
<p><b>•	Development branch (usually called ‘develop’)</b>
This is your main development branch where all the changes destined for the next release are placed, either by directly committing small changes or by merging other branches (e.g. feature branches) into this branch.</p>
<p><b>•	Production branch (usually called ‘master’)</b>
This branch represents the latest released / deployed codebase. Only updated by merging other branches into it.</p>
<p><b>•	Feature branches (usually prefixed with ‘feature/’)</b>
When you start work on anything non-trivial, you create a feature branch. When finished, you’ll merge this branch back into the development branch to queue it for the next release.</p>
<p><b>•	Release branches (usually prefixed with ‘release/’)</b>
When you’re about to package a new release, you create a release branch from the development branch. You can commit to it during your preparation for a release, and when it’s ready to be deployed, you merge it into both the development branch and the master branch (to indicate that the release has been deployed).</p>
<p><b>•	Hotfix branches (usually prefixed with ‘hotfix/’)</b>
If you need to patch the latest release without picking up new features from the development branch, you can create a hotfix branch from the latest deployed code in master. Once you’ve made your changes, the hotfix branch is then merged back into both the master branch (to update the released version) and the development branch (to make sure the fixes go into the next release too)</p>

<p class="custom-heading"> Git in sourceTree </p>

<p class="custom-sub-heading"> Getting started with git-flow</p>
<p>There’s a handy new addition to the toolbar in SourceTree 1.5 (keyboard shortcut Cmd-Alt-F):

Based on the current state of the repository, the Git-flow button will bring up a dialog with the most likely action you’d want to perform next. So if you haven’t set up git-flow on this repo yet, it’ll help you do that by default. If you’re on the development branch, it will default to starting a new feature. If you’re already on a feature branch, it will offer to finish your current feature and merge it back into the development branch, and so on. You can always get to all the other git-flow actions via this button as well, but most of the time the default option will be the action you’ll want SourceTree to perform.
If you haven’t used git-flow already on this repository, the first thing SourceTree will do is initialise your repository to use it. You’ll probably just want to use the defaults in the initialisation window so that’s not covered here. For more details please see the Help section included in SourceTree.
</p>

<p class="custom-sub-heading">Starting a feature</p>
<p>You can commit trivial changes directly to the development branch (‘develop’) if you like, but any time you start on something non-trivial you should explicitly start a new feature. This ‘Start Feature’ action will be the default action when you click the Git-flow button if you are currently on the dev branch.
</p>
<img src="/img/git1.jpg"/>

<p>The first thing to note is the ‘Preview’ window, which is present on all of the action dialogs and shows you what will actually happen when you confirm the dialog. In this case, a new feature branch called ‘feature/my-new-feature’ will be created (I used the default prefix when I initialised this repository). You commit your feature implementations to this branch. If you want, you can push the feature branch to your remote while you work on it (your team can decide on whether that’s normal practice or not).
If at any time you want to switch branches, either to another feature branch or to somewhere else, just use the normal mechanisms in SourceTree to do that, such as double-clicking a log entry or a branch in the sidebar. Git-flow determines your context simply from the branch you currently have checked out, so it’s fine to jump around if you like.
</p>

<p class="custom-sub-heading">Finishing a feature </p>
<p>Eventually when you’re done implementing a feature, use the ‘Finish Feature’ action (again, this will be the default action from the toolbar button if you’re on a feature branch):
</p>
<img src="/img/git2.jpg"/>

<p>Again, the Preview shows you what will happen — the feature branch will merge into the main development branch, essentially queueing it for inclusion in the next release. Feature branches are deleted by default but you can opt to retain them if you like.
</p>

<p class="custom-sub-heading">Starting a release </p>
<p>You start a release branch when you want to start preparing a new release, which probably coincides with a feature freeze. Accessing the Start Release option –either from the menu or from the toolbar action selection window — brings up the following dialog:
</p>
<img src="/img/git3.jpg"/>

<p>The preview shows that a new release branch will be created. Most of the time, you want to start the release from the latest commit in the development branch, but you can choose to base it on another commit if you wish. This essentially freezes the release, so it’s not affected by subsequent development. You can also perform preparatory tasks for the release process on this branch, such as updating the version number in source files, updating changelogs, or committing other tweaks. Once these tweaks are done, you can finish the release as described below.
</p>

<p class="custom-sub-heading">Finishing a release </p>
<p>Once all the adjustments required for the release are done and committed, you can conclude the release process. If you’re on the release branch already, the git-flow button will show you the following dialog:
</p>
<img src="/img/git4.jpg"/>

<p>The preview illustrates that the release branch will be merged into the production branch (‘master’ or ‘default’ normally) to indicate an update to the deployed version. Sourcetree will also create a tag here for the release. The release branch changes will also merge back into the development branch to make sure the develop branch is kept up to date.
</p>

<p class="custom-sub-heading">Starting a hotfix </p>
<p>What if you need to just fix a bug on the latest release? You don’t want to create a new release, because that will pick up the recent changes from the development branch. So instead, you can start a hot fix:
</p>
<img src="/img/git5.jpg"/>

<p>Hot fixes always start from the latest production code from the ‘master’ or ‘default’ branch. Other than that, they’re basically the same as release branches. Moreover, when you’re finished with the hot-fix, they behave the same way as finishing a release branch. The changes are merged back into both the production branch and the development branch, and a tag is created on the production branch for the hot fix release.
</p>

<p class="custom-heading"> What are some basic git commands? </p>
<table class="table-style">
    <thead class="table-head-style">
        <tr>
            <td class="table-column-style" width="20%"><strong><u>Git tasks </u></strong></td>
            <td class="table-column-style" width="30%"><strong><u>Notes</u> </strong></td>
            <td class="table-column-style" width="50%"><strong><u>Git Commands </u></strong> </td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td class="table-column-style">Tell Git who you are</td>
            <td class="table-column-style">Configure the author name and email address to be used with your commits. Note that Git strips some characters (for example trailing periods) from user.name.</td>
            <td class="table-column-style">
                git config --global user.name "Sam Smith" <br>
                git config --global user.email sam@example.com
            </td>
        </tr>
         <tr>
            <td class="table-column-style">Create a new local repository</td>
            <td class="table-column-style"></td>
            <td class="table-column-style">
                git init
            </td>
        </tr>
         <tr>
            <td class="table-column-style" rowspan=2>Check out a repository</td>
            <td class="table-column-style">Create a working copy of a local repository</td>
            <td class="table-column-style">
                git clone /path/to/repository
            </td>
        </tr>
         <tr>
            <td class="table-column-style">For a remote server, use:</td>
            <td class="table-column-style">
                git clone username@host:/path/to/repository
            </td>
        </tr>
         <tr>
            <td class="table-column-style">Add files</td>
            <td class="table-column-style">Add one or more files to staging (index)</td>
            <td class="table-column-style">
                git add < filename > <br>git add *
            </td>
        </tr>
        <tr>
            <td class="table-column-style" rowspan=2>Commit</td>
            <td class="table-column-style">Commit any files you've added with git add, and also commit any files you've changed since then</td>
            <td class="table-column-style">
                git commit -a
            </td>
        </tr>
        <tr>
            <td class="table-column-style">Commit changes to head (but not yet to the remote repository)</td>
            <td class="table-column-style">
                git commit -m "Commit message"
            </td>
        </tr>
        <tr>
            <td class="table-column-style">Push</td>
            <td class="table-column-style">Send changes to the master branch of your remote repository</td>
            <td class="table-column-style">
                git push origin master
            </td>
        </tr>
        <tr>
            <td class="table-column-style">Status</td>
            <td class="table-column-style">List the files you've changed and those you still need to add or commit</td>
            <td class="table-column-style">
                git status
            </td>
        </tr>
        <tr>
            <td class="table-column-style" rowspan=2>Connect to a remote repository</td>
            <td class="table-column-style">If you haven't connected your local repository to a remote server, add the server to be able to push to it</td>
            <td class="table-column-style">
                git remote add origin < server >
            </td>
        </tr>
         <tr>
            <td class="table-column-style">List all currently configured remote repositories</td>
            <td class="table-column-style">
                git remote -v
            </td>
        </tr>
        <tr>
            <td class="table-column-style" rowspan=7>Branches</td>
            <td class="table-column-style">Create a new branch and switch to it</td>
            <td class="table-column-style">
               git checkout -b < branchname >
            </td>
        </tr>
         <tr>
            <td class="table-column-style">Switch from one branch to another</td>
            <td class="table-column-style">
                git checkout < branchname >
            </td>
        </tr>
        <tr>
            <td class="table-column-style">List all the branches in your repo, and also tell you what branch you're currently in</td>
            <td class="table-column-style">
                git branch
            </td>
        </tr>
        <tr>
            <td class="table-column-style">Delete the feature branch</td>
            <td class="table-column-style">
                git branch -d < branchname >
            </td>
        </tr>
         <tr>
            <td class="table-column-style">Push the branch to your remote repository, so others can use it</td>
            <td class="table-column-style">
                git push origin < branchname >
            </td>
        </tr>
        <tr>
            <td class="table-column-style">Push all branches to your remote repository</td>
            <td class="table-column-style">
                git push --all origin
            </td>
        </tr>
        <tr>
            <td class="table-column-style">Delete a branch on your remote repository</td>
            <td class="table-column-style">
                git push origin :< branchname >
            </td>
        </tr>
        <tr>
            <td class="table-column-style" rowspan=4>Update from the remote repository</td>
            <td class="table-column-style">Fetch and merge changes on the remote server to your working directory</td>
            <td class="table-column-style">
                git pull
            </td>
        </tr>
         <tr>
            <td class="table-column-style">To merge a different branch into your active branch</td>
            <td class="table-column-style">
                git merge < branchname >
            </td>
        </tr>
        <tr>
            <td class="table-column-style">View all the merge conflicts:
                <br>View the conflicts against the base file:
                <br>Preview changes, before merging</td>
            <td class="table-column-style">
                git diff
                <br> git diff --base < filename >
                <br> git diff < sourcebranch > < targetbranch >
            </td>
        </tr>
        <tr>
            <td class="table-column-style">After you have manually resolved any conflicts, you mark the changed file</td>
            <td class="table-column-style">
                git add < filename >
            </td>
        </tr>
        <tr>
            <td class="table-column-style" rowspan=3>Tags</td>
            <td class="table-column-style">You can use tagging to mark a significant changeset, such as a release</td>
            <td class="table-column-style">
                git tag 1.0.0 < commitID >
            </td>
        </tr>
         <tr>
            <td class="table-column-style">CommitId is the leading characters of the changeset ID, up to 10, but must be unique. Get the ID using</td>
            <td class="table-column-style">
                git log
            </td>
        </tr>
        <tr>
            <td class="table-column-style">Push all tags to remote repository</td>
            <td class="table-column-style">
               git push --tags origin
            </td>
        </tr>
        <tr>
            <td class="table-column-style" rowspan=2>Undo local changes</td>
            <td class="table-column-style">If you mess up, you can replace the changes in your working tree with the last content in head:
            Changes already added to the index, as well as new files, will be kept</td>
            <td class="table-column-style">
                git checkout -- < filename >
            </td>
        </tr>
         <tr>
            <td class="table-column-style">Instead, to drop all your local changes and commits, fetch the latest history from the server and point your local master branch at it, do this:</td>
            <td class="table-column-style">
                git fetch origin
                <br>git reset --hard origin/master
            </td>
        </tr>
         <tr>
            <td class="table-column-style">Search</td>
            <td class="table-column-style">Search the working directory for foo():</td>
            <td class="table-column-style">
                git grep "foo()"
            </td>
        </tr>
    </tbody>
</table>


<p class="custom-heading">Wrapping up</p>
<p>Git-flow is a great way to automate your handling of branch-based development in Git, and SourceTree now provides a simple and clear way to use it with an easy-to-use and intuitive GUI. Big thanks to Vincent Driessen for coming up with git-flow in the first place!
</p>
