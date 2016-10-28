# Documentation: Help with Git and Github

## Contents

<table>
  <tr>
    <td>Table of Contents: The TOC is auto-created by using "Headings". To update, click below, then click the “Update table of contents” button.

* Glossary
General Overview: How to Contribute Code
Setup Instructions: Install “Github for Desktop (PC or Mac)” or “Git”
Initializing a Repository in an Existing Directory
Getting a Git Repository
Initializing a Repository in an Existing Directory
Cloning an Existing Repository
How to Work with a Git Repository
Git repositories need a README.md and .gitignore file
How to Add files to version-control
How to Commit files to version-control
How to Pull files from the Cloud repository
How to Push files from local repository to the Cloud repository
How to Remove files from version-control
How to Fork a Repository
How to Clone a Repository
How to Issue a Pull Request
More Great Help Documentation
</td>
  </tr>
</table>


## * [Glossary](https://git-scm.com/docs/gitglossary)

* **git **- Git was designed in order to interface with remote repository. Each repository is resolved to a URL, and given a name. By convention, GitHub uses the name "origin" for the repository on its server.

* **branches **- A branch in Git is simply a lightweight movable pointer to a commit. The default branch name in Git is master. As you start making commits, you’re given a master branch that points to the last commit you made. Every time you commit, it moves forward automatically. The "master" branch in Git is not a special branch. It is exactly like any other branch. The only reason nearly every repository has one is that the git init command creates it by default and most people don’t bother to change it

* **clone **- Download a copy of the repository; you can do this at the github website using the "clone or download" button. Download as a zip file to your laptop, or use the following notation in a shell to download programmatically:
$ git@github.com:Islandora-Collaboration-Group/icg_information.git

* **commit** - As a noun: A single point in the Git history; the entire history of a project is represented as a set of interrelated commits. The word "commit" is often used by Git in the same places other revision control systems use the words "revision" or "version". Also used as a short hand for [commit object](https://git-scm.com/docs/gitglossary#def_commit_object).
As a verb: The action of storing a new snapshot of the project’s state in the Git history, by creating a new commit representing the current state of the [index](https://git-scm.com/docs/gitglossary#def_index) and advancing [HEAD](https://git-scm.com/docs/gitglossary#def_HEAD) to point at the new commit.

* **create pull request **- 

* **fetch** - Fetching a [branch](https://git-scm.com/docs/gitglossary#def_branch) means to get the branch’s [head ref](https://git-scm.com/docs/gitglossary#def_head_ref) from a remote [repository](https://git-scm.com/docs/gitglossary#def_repository), to find out which objects are missing from the local [object database](https://git-scm.com/docs/gitglossary#def_object_database), and to get them, too. See also [git-fetch[1]](https://git-scm.com/docs/git-fetch).

* **fork **- Users who don’t have push permissions for a repository can "fork" it (create their own copy), push commits to that copy, and open a merge request from their fork back to the main project. This model allows the owner to be in CHAPTER 4: Git on the Server 148 full control of what goes into the repository and when, while allowing contributions from untrusted users. 

* **master** - The default development [branch](https://git-scm.com/docs/gitglossary#def_branch). Whenever you create a Git [repository](https://git-scm.com/docs/gitglossary#def_repository), a branch named "master" is created, and becomes the active branch. In most cases, this contains the local development, though that is purely by convention and is not required.

* **merge **- As a verb: To bring the contents of another [branch](https://git-scm.com/docs/gitglossary#def_branch) (possibly from an external [repository](https://git-scm.com/docs/gitglossary#def_repository)) into the current branch. In the case where the merged-in branch is from a different repository, this is done by first [fetching](https://git-scm.com/docs/gitglossary#def_fetch) the remote branch and then merging the result into the current branch. This combination of fetch and merge operations is called a [pull](https://git-scm.com/docs/gitglossary#def_pull). Merging is performed by an automatic process that identifies changes made since the branches diverged, and then applies all those changes together. In cases where changes conflict, manual intervention may be required to complete the merge.
As a noun: unless it is a [fast-forward](https://git-scm.com/docs/gitglossary#def_fast_forward), a successful merge results in the creation of a new [commit](https://git-scm.com/docs/gitglossary#def_commit) representing the result of the merge, and having as [parents](https://git-scm.com/docs/gitglossary#def_parent) the tips of the merged [branches](https://git-scm.com/docs/gitglossary#def_branch). This commit is referred to as a "merge commit", or sometimes just a "merge".

* **origin **- The default upstream [repository](https://git-scm.com/docs/gitglossary#def_repository). Most projects have at least one upstream project which they track. By default origin is used for that purpose. New upstream updates will be fetched into [remote-tracking branches](https://git-scm.com/docs/gitglossary#def_remote_tracking_branch) named origin/name-of-upstream-branch, which you can see using git branch -r.

* **pull **- Pulling a [branch](https://git-scm.com/docs/gitglossary#def_branch) means to [fetch](https://git-scm.com/docs/gitglossary#def_fetch) it and [merge](https://git-scm.com/docs/gitglossary#def_merge) it. See also [git-pull[1]](https://git-scm.com/docs/git-pull).

* **push **- Pushing a [branch](https://git-scm.com/docs/gitglossary#def_branch) means to get the branch’s [head ref](https://git-scm.com/docs/gitglossary#def_head_ref) from a remote [repository](https://git-scm.com/docs/gitglossary#def_repository), find out if it is a direct ancestor to the branch’s local head ref, and in that case, putting all objects, which are [reachable](https://git-scm.com/docs/gitglossary#def_reachable) from the local head ref, and which are missing from the remote repository, into the remote [object database](https://git-scm.com/docs/gitglossary#def_object_database), and updating the remote head ref. If the remote [head](https://git-scm.com/docs/gitglossary#def_head) is not an ancestor to the local head, the push fails.

* **rebase** - To reapply a series of changes from a [branch](https://git-scm.com/docs/gitglossary#def_branch) to a different base, and reset the [head](https://git-scm.com/docs/gitglossary#def_head) of that branch to the result.

* **repository ("repo") **- A collection of [refs](https://git-scm.com/docs/gitglossary#def_ref) together with an [object database](https://git-scm.com/docs/gitglossary#def_object_database) containing all objects which are [reachable](https://git-scm.com/docs/gitglossary#def_reachable) from the refs, possibly accompanied by meta data from one or more [porcelains](https://git-scm.com/docs/gitglossary#def_porcelain). A repository can share an object database with other repositories via [alternates mechanism](https://git-scm.com/docs/gitglossary#def_alternate_object_database).

* **remote repository **- A [repository](https://git-scm.com/docs/gitglossary#def_repository) which is used to track the same project but resides somewhere else. To communicate with remotes, see [fetch](https://git-scm.com/docs/gitglossary#def_fetch) or [push](https://git-scm.com/docs/gitglossary#def_push).

* **resolve **- The action of fixing up manually what a failed automatic [merge](https://git-scm.com/docs/gitglossary#def_merge) left behind.

* **revision **- Synonym for [commit](https://git-scm.com/docs/gitglossary#def_commit) (the noun).

* * *


## General Overview: How to Contribute Code

1. If you do not have your own github account, sign up for one.

2. Visit the home page for this repository and click "Fork" at the upper-right. This will create a repository within your github space that is a clone of this original.

3. Clone your fork down to your development environment. Or if you have already cloned Islandora-Collaboration-Group/icg_csv_import, you can change the remote [instructions](https://help.github.com/articles/changing-a-remote-s-url/).

4. Work on your local code, make changes, commit your changes, push back up to your github remote etc.

5. You can keep your fork updated from the ICG master [using this technique](http://stackoverflow.com/questions/7244321/how-do-i-update-a-github-forked-repository)

6. When you believe your work is ready for prime time, on your github repository, click the "Create Pull Request" button. Select Islandora-Collaboration-Group/icg_csv_import:master branch as the target. Describe the work you have done and what problem it solves.

7. Other "watchers" on this repository will be notified of your pull request. They can merge it into their own forks and test it.

8. Testers might have feedback for you and comment on the pull request. You might want to make changes and either withdraw your pull request or update it.

9. Once we are satisfied that your work should be committed to the master branch, the pull request will be merged and closed.

* * *


## Setup Instructions: Install "Github for Desktop (PC or Mac)" or “Git”

Choose either approach: 

1. [Install Git](https://git-scm.com/download/) - Git installs without the WYSIWYG client and assumes a greater knowledge of typing git commands into a shell based environment. See [Git Documentation](https://git-scm.com/doc).

2. [Install Github for Desktop](https://desktop.github.com/) - GitHub Desktop is a WYSIWYG client to contribute to projects on GitHub. See [GitHub Desktop Documentation](https://help.github.com/desktop/).

3. TODO - What happens if you install both versions? Do they conflict? 

* * *


## Initializing a Repository in an Existing Directory

### Getting a Git Repository

You can get a Git project using two main approaches. The first takes an existing project or directory and imports it into Git. The second clones an existing Git repository from another server.

#### Initializing a Repository in an Existing Directory

If you’re starting to track an existing project in Git, you need to go to the project’s directory and type:

*To initialize the new repository within a local working environment:*

* **$ git init**

This creates a new subdirectory named .git that contains all of your necessary repository files – a Git repository skeleton. At this point, nothing in your project is tracked yet. (See [Git Internals](https://git-scm.com/book/en/v2/ch00/_git_internals) for more information about exactly what files are contained in the .git directory you just created.)

At this point, you have a Git repository with tracked files and an initial commit.

### Cloning an Existing Repository

If you want to get a copy of an existing Git repository – for example, a project you’d like to contribute to – the command you need is git clone. If you’re familiar with other VCS systems such as Subversion, you’ll notice that the command is "clone" and not "checkout". This is an important distinction – instead of getting just a working copy, Git receives a full copy of nearly all data that the server has. Every version of every file for the history of the project is pulled down by default when you run git clone. In fact, if your server disk gets corrupted, you can often use nearly any of the clones on any client to set the server back to the state it was in when it was cloned (you may lose some server-side hooks and such, but all the versioned data would be there – see [Getting Git on a Server](https://git-scm.com/book/en/v2/ch00/_git_on_the_server) for more details).

You clone a repository with **git clone [url]**. For example, if you want to clone the Git linkable library called libgit2, you can do so like this:

* **$ git clone ****[https://github.com/libgit2/libgit**2](https://github.com/libgit2/libgit2)

That creates a directory named "libgit2", initializes a .git directory inside it, pulls down all the data for that repository, and checks out a working copy of the latest version. If you go into the new libgit2 directory, you’ll see the project files in there, ready to be worked on or used. If you want to clone the repository into a directory named something other than “libgit2”, you can specify that as the next command-line option:

* **$ git clone ****[https://github.com/libgit2/libgit**2](https://github.com/libgit2/libgit2)** mylibgit**

That command does the same thing as the previous one, but the target directory is called **mylibgit**.

Git has a number of different transfer protocols you can use. The previous example uses the https:// protocol, but you may also see git:// or user@server:path/to/repo.git, which uses the SSH transfer protocol. [Getting Git on a Server](https://git-scm.com/book/en/v2/ch00/_git_on_the_server) will introduce all of the available options the server can set up to access your Git repository and the pros and cons of each.

## How to Work with a Git Repository

### Git repositories need a README.md and .gitignore file

1. **README.md - **Each project should have at least one README file in markdown.  This is parsed by GitHub, and rendered as HTML documentation.

2. **.gitignore - **This file contain any number of globbing patterns or file/directory paths relative to the repository path itself. It ensures that certain files cannot be versioned by Git (i.e. .cfg files with passwords, or backup files)

### How to Add files to version-control

If you want to start version-controlling existing files (as opposed to an empty directory), you should probably begin tracking those files and do an initial commit. You can accomplish that with a few git add commands that specify the files you want to track, followed by a git commit:

To add all files:

* **$ git add *.***

Or to only add a certain type of files (i.e. .txt):

* **$ git add *.txt**

Or to add one specific file:

* **$ git add README.md**

Or to add multiple (in this case, two) specific files:

* **$ git add README.md .gitignore**

### How to Commit files to version-control

Git saves the state of a given branch for tracked files by "commits". Should one add a file for tracking or modify a file further after a commit, another commit must be issued. For the purposes of this outline, consider commits to only save the state of the local repository.

To commit all files with a descriptive message (the -m is the message flag):

* **$ git commit -m 'initial project version'**

### How to Pull files from the Cloud repository

Blah:

* **$ git pull**

### How to Push files from local repository to the Cloud repository

Git synchronizes commits on local branches to branches in remote repositories using a "push" operation. The “-u” argument ensures that the branch “master” in the remote repository “origin” is tracked by the local branch “master”. This, in turn, permits one to more easily synchronize modifications made to the branch “master” on origin, to the local branch “master”.

* **$ git push -u origin master**

### How to Remove files from version-control

One may remove files from tracking using the following invocation:

* **$ git rm README.md**

* * *


## How to Fork a Repository

Forking a repository means that you are downloading a copy of someone else’s repository and your fork is a distinct, entirely separate, repository that shows the original as the ancestor. You can issue a "pull request" as a means of offering commits you’ve made to your own repository back to the original (“parent”) repository; of course, the owner of the original repository must accept that pull request in order to accept your edits.

The github website offers a "fork" button

* * *


## How to Clone a Repository

Download a copy of the repository; you can do this at the github website using the "clone or download" button. Download as a zip file to your laptop, or use the following notation in a shell to download programmatically:

* **$ git@github.com:Islandora-Collaboration-Group/icg_information.git**

* * *


## How to Issue a Pull Request

The github website offers a "New pull request" button for initiating a pull request. A pull request sends your code edits to the original (“parent”) repository owner for review; they can either accept or reject your edits into their repository.

* * *


## More Great Help Documentation

1. [https://progit2.s3.amazonaws.com/en/2016-03-22-f3531/progit-en.1084.pdf](https://progit2.s3.amazonaws.com/en/2016-03-22-f3531/progit-en.1084.pdf)

2. [https://git-scm.com/](https://git-scm.com/)

3. [https://desktop.github.com/](https://desktop.github.com/) 

