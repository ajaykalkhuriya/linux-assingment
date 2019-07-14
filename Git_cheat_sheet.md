                                             
  Git installing -:

sudo apt-get install git-all

Your Identity
The first thing you should do when you install Git is to set your user name and email address. This is important because every Git commit uses this information, and it’s immutably baked into the commits you start creating:
$ git config  --global user.name “ajay kalkhuriya”   
$ git config  --global user.email “ajaykalkhuriya@gmail.com”   

Again, you need to do this only once if you pass the --global option, because then Git will always use that information for anything you do on that system.


Your Editor
Now that your identity is set up, you can configure the default text editor that will be used when Git needs you to type in a message.

$ git config --global core.editor vim


Checking Your Settings
If you want to check your configuration settings, you can use the git config --list command to list all the settings Git can find at that point:
$ git config --list

or
$ git config user.name
ajay kalkhuriya


$ git config user.email
ajaykalkhuriya@gmail.com



Getting Help
If you ever need help while using Git, there are three equivalent ways to get the comprehensive manual page (manpage) help for any of the Git commands
$ git help <verb>   
$ git <verb> --help  
$ man git-<verb>     



For example, you can get the manpage help for thegit config command by running

$ git help config


Getting a Git Repository

You typically obtain a Git repository in one of two ways:
    1. You can take a local directory that is currently not under version control, and turn it into a Git repository, or
    2. You can clone an existing Git repository from elsewhere.

Initializing a Repository in an Existing Directory
If you have a project directory that is currently not under version control and you want to start controlling it with Git, you first need to go to that project’s directory.

$ cd /home/user/my_project


$ git init

This creates a new subdirectory named.gitthat contains all of your necessary repository files — a Git repository skeleton.


Recording Changes to the Repository----
working directory can be in one of two states: tracked  ..or untracked. Tracked files are files that were in the last snapshot; they can be unmodified, modified, or staged. In short, tracked files are files that Git knows about.
Untracked files are everything else — any files in your working directory that were not in your last snapshot and are not in your staging area. When you first clone a repository, all of your files will be tracked and unmodified because Git just checked them out and you haven’t edited anything.

Checking the Status of Your Files

The main tool you use to determine which files are in which state is the git status command.
$ git status

If you run this command directly after a clone,

$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working directory clean

Tracking New Files

$ git add filename

If you run your status command again, you can see that your README file is now tracked and staged to be committed:

$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   filename


Short Status
While the git status output is pretty comprehensive, you run git status -s or git status –short you get a far more simplified output



Committing Your Changes
They will stay as modified files on your disk. In this case, let’s say that the last time you ran git status, you saw that everything was staged, so you’re ready to commit your changes. The simplest way to commit is to type git commit:

$ git commit
Viewing the Commit History
you’ll probably want to look back to see what has happened. The most basic and powerful tool to do this is the git log command.
$ git log
$ git log
commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    changed the version number

commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Sat Mar 15 16:40:33 2008 -0700

    removed unnecessary test

commit a11bef06a3f659402fe7563abf99ad00de2209e6
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Sat Mar 15 10:31:28 2008 -0700

    first commit
A huge number and variety of options to the git log command are available to show you exactly what you’re looking for. Here, we’ll show you some of the most popular.

the more helpful options is -p or --patch, which shows the difference (the patch output) introduced in each commit. You can also limit the number of log entries displayed, such as using -2 to show only the last two entries.

$ git log -p -2

if you want to see some abbreviated stats for each commit, you can use the –stat 
option:

$ git log --stat

Another really useful option is --pretty. This option changes the log output to formats other than the default. A few prebuilt options are available for you to use. The oneline option prints each commit on a single line, which is useful if you’re looking at a lot of commits. In addition, the short, full, and fuller options show the output in roughly the same format but with less or more information.


$ git log --pretty=oneline
ca82a6dff817ec66f44342007202690a93763949 changed the version number
085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7 removed unnecessary test
a11bef06a3f659402fe7563abf99ad00de2209e6 first commit


The most interesting option is format, which allows you to specify your own log output format. This is especially useful when you’re generating output for machine parsing — because you specify the format explicitly, you know it won’t change with updates to Git:

git log –pretty=format

$ git log --pretty=format:"%h - %an, %ar : %s"
ca82a6d - Scott Chacon, 6 years ago : changed the version number
085bb3b - Scott Chacon, 6 years ago : removed unnecessary test
a11bef0 - Scott Chacon, 6 years ago : first commit



  
Useful options for git log –pretty=format

Useful options for git log –pretty=formatlists some of the more useful options that formattakes.
                 
Option
Description of Output
 %H
Commit hash
 %h
Abbreviated commit hash
 %T
Tree hash
 %t
Abbreviated tree hash
 %P
Parent hashes
 %p
Abbreviated parent hashes
 %an
Author name
 %ae
Author email
 %ad
Author date (format respects the --date=option)
 %ar
Author date, relative
 %cn
Committer name
 %ce
Committer email
 %cd
Committer date
 %cr
Committer date, relative
 %s
Subject

Common options to git log


Option
Description
-p
Show the patch introduced with each commit.
--stat
Show statistics for files modified in each commit.
--shortstat
Display only the changed/insertions/deletions line from the --stat command.
--name-only
Show the list of files modified after the commit information.
--name-status
Show the list of files affected with added/modified/deleted information as well.
--abbrev-commit
Show only the first few characters of the SHA-1 checksum instead of all 40.
--relative-date
Display the date in a relative format (for example, “2 weeks ago”) instead of using the full date format.
--graph
Display an ASCII graph of the branch and merge history beside the log output.
--pretty
Show commits in an alternate format. Options include oneline, short, full, fuller, and format (where you specify your own format).
--oneline
Shorthand for --pretty=oneline --abbrev-commit used together.



Limiting Log Output--

the time-limiting options such as –since and –until are very useful. For example, this command gets the list of commits made in the last two weeks:
$ git log --since=2.weeks
This command works with lots of formats — you can specify a specific date like "2008-01-15", or a relative date such as"2 years 1 day 3 minutes ago".
You can also filter the list to commits that match some search criteria. The --author option allows you to filter on a specific author, and the --grep option lets you search for keywords in the commit messages.

In Options to limit the output of git log we’ll list these and a few other common options for your reference
Option
Description
-<n>
Show only the last n commits
--since, --after
Limit the commits to those made after the specified date.
--until, --before
Limit the commits to those made before the specified date.
--author
Only show commits in which the author entry matches the specified string.
--committer
Only show commits in which the committer entry matches the specified string.
--grep
Only show commits with a commit message containing the string
-S
Only show commits adding or removing code matching the string



Undoing Things

One of the common undos takes place when you commit too early and possibly forget to add some files, or you mess up your commit message. If you want to redo that commit, make the additional changes you forgot, stage them, and commit again using the --amend option:

$ git commit --amend

Unstaging a Staged File
The next two sections demonstrate how to work with your staging area and working directory changes. The nice part is that the command you use to determine the state of those two areas also reminds you how to undo changes to them. For example, let’s say you’ve changed two files and want to commit them as two separate changes, but you accidentally type git add * and stage them both. How can you unstage one of the two? The git status command reminds you:
$ git add *
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    renamed:    README.md -> README
    modified:   CONTRIBUTING.md
Right below the “Changes to be committed” text, it says use git reset HEAD <file>... to unstage. So, let’s use that advice to unstage the CONTRIBUTING.md file:
$ git reset HEAD CONTRIBUTING.md
Unstaged changes after reset:
M       CONTRIBUTING.md
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    renamed:    README.md -> README

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
The command is a bit strange, but it works. The CONTRIBUTING.md file is modified but once again unstaged.
Unmodifying a Modified File
What if you realize that you don’t want to keep your changes to the CONTRIBUTING.md file? How can you easily unmodify it — revert it back to what it looked like when you last committed (or initially cloned, or however you got it into your working directory)?
It tells you pretty explicitly how to discard the changes you’ve made. Let’s do what it says:
$ git checkout -- CONTRIBUTING.md
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    renamed:    README.md -> README
Important
It’s important to understand that git checkout -- <file> is a dangerous command. Any local changes you made to that file are gone — Git just replaced that file with the most recently-committed version. Don’t ever use this command unless you absolutely know that you don’t want those unsaved local changes.


Working with Remotes
Remote repositories can be on your local machine.
It is entirely possible that you can be working with a “remote” repository that is, in fact, on the same host you are. The word “remote” does not necessarily imply that the repository is somewhere else on the network or Internet, only that it is elsewhere. Working with such a remote repository would still involve all the standard pushing, pulling and fetching operations as with any other remote.

Showing Your Remotes
To see which remote servers you have configured, you can run the git remote command. It lists the shortnames of each remote handle you’ve specified
$ git remote
origin

You can also specify -v, which shows you the URLs that Git has stored for the shortname to be used when reading and writing to that remote
$ git remote -v
origin  https://github.com/schacon/ticgit (fetch)
origin  https://github.com/schacon/ticgit (push)

Adding Remote Repositories
We’ve mentioned and given some demonstrations of how the git clone command implicitly adds the origin remote for you. Here’s how to add a new remote explicitly. To add a new remote Git repository as a shortname you can reference easily, run               git remote add <shortname> <url>:
$ git remote
origin
$ git remote add pb https://github.com/paulboone/ticgit
$ git remote -v
origin  https://github.com/schacon/ticgit (fetch)
origin  https://github.com/schacon/ticgit (push)
pb      https://github.com/paulboone/ticgit (fetch)
pb      https://github.com/paulboone/ticgit (push)

if you want to fetch all the information that Paul has but that you don’t yet have in your repository, you can run git fetch pb:

$ git fetch pb
remote: Counting objects: 43, done.
remote: Compressing objects: 100% (36/36), done.
remote: Total 43 (delta 10), reused 31 (delta 5)
Unpacking objects: 100% (43/43), done.
From https://github.com/paulboone/ticgit
 * [new branch]      master     -> pb/master
 * [new branch]      ticgit     -> pb/ticgit
Fetching and Pulling from Your Remotes
As you just saw, to get data from your remote projects, you can run:
$ git fetch <remote>

Pushing to Your Remotes
When you have your project at a point that you want to share, you have to push it upstream. The command for this is simple: git push <remote> <branch>. If you want to push your master branch to your origin server (again, cloning generally sets up both of those names for you automatically), then you can run this to push any commits you’ve done back up to the server:
$ git push origin master

Inspecting a Remote

If you want to see more information about a particular remote, you can use the git remote show <remote> command. 
$ git remote show origin
* remote origin
  Fetch URL: https://github.com/schacon/ticgit
  Push  URL: https://github.com/schacon/ticgit
  HEAD branch: master
  Remote branches:
    master                               tracked
    dev-branch                           tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (up to date)

Renaming and Removing Remotes
You can run git remote rename to change a remote’s shortname. For instance, if you want to rename pb to paul, you can do so with git remote rename:
$ git remote rename pb paul
$ git remote
origin
paul

If you want to remove a remote for some reason — you’ve moved the server or are no longer using a particular mirror, or perhaps a contributor isn’t contributing anymore — you can either use git remote remove or git remote rm:
$ git remote remove paul
$ git remote
origin
Once you delete the reference to a remote this way, all remote-tracking branches and configuration settings associated with that remote are also deleted.
Tagging
Listing Your Tags
Listing the existing tags in Git is straightforward. Just type git tag (with optional -l or --list):
$ git tag
v1.0
v2.0

You can also search for tags that match a particular pattern. The Git source repo, for instance, contains more than 500 tags. If you’re interested only in looking at the 1.8.5 series, you can run this:
$ git tag -l "v1.8.5*"
v1.8.5
v1.8.5-rc0
v1.8.5-rc1
v1.8.5-rc2
v1.8.5-rc3
v1.8.5.1
v1.8.5.2
v1.8.5.3
v1.8.5.4
v1.8.5.5

Listing tag wildcards requires -l or –list option
If you want just the entire list of tags, running the command git tag implicitly assumes you want a listing and provides one; the use of -l or --list in this case is optional.
If, however, you’re supplying a wildcard pattern to match tag names, the use of-lor --list is mandatory.

Creating Tags
Git supports two types of tags: lightweight and annotated.
A lightweight tag is very much like a branch that doesn’t change — it’s just a pointer to a specific commit.
Annotated tags, however, are stored as full objects in the Git database. They’re checksummed; contain the tagger name, email, and date; have a tagging message; and can be signed and verified with GNU Privacy Guard (GPG). It’s generally recommended that you create annotated tags so you can have all this information;
$ git tag -a v1.4 -m "my version 1.4"
$ git tag
v0.1
v1.3
v1.4
The -m specifies a tagging message, which is stored with the tag.
$ git show v1.4
tag v1.4
Tagger: Ben Straub <ben@straub.cc>
Date:   Sat May 3 20:19:12 2014 -0700

my version 1.4

commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    changed the version number

Lightweight Tags
Another way to tag commits is with a lightweight tag. This is basically the commit checksum stored in a file — no other information is kept. To create a lightweight tag, don’t supply any of the -a, -s, or -moptions, just provide a tag name:
$ git tag v1.4-lw
$ git tag
v0.1
v1.3
v1.4
v1.4-lw
v1.5

if you run git show on the tag, you don’t see the extra tag information. The command just shows the commit:
$ git show v1.4-lw
commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    changed the version number
Tagging Later
$ git log --pretty=oneline
15027957951b64cf874c3557a0f3547bd83b3ff6 Merge branch 'experiment'
a6b4c97498bd301d84096da251c98a07c7723e65 beginning write support
0d52aaab4479697da7686c15f77a3d64d9165190 one more thing
6d52a271eda8725415634dd79daabbc4d9b6008e Merge branch 'experiment'
0b7434d86859cc7b8c3d5e1dddfed66ff742fcbc added a commit function
4682c3261057305bdd616e23b64b0857d832627b added a todo file
166ae0c4d3f420721acbb115cc33848dfcc2121a started write support
9fceb02d0ae598e95dc970b74767f19372d61af8 updated rakefile
964f16d36dfccde844893cac5b347e7b3d44abbc commit the todo
8a5cbc430f1a9c3d00faaeffd07798508422908a updated readme


 suppose you forgot to tag the project at v1.2, which was at the “updated rakefile” commit. You can add it after the fact. To tag that commit, you specify the commit checksum (or part of it) at the end of the command:
$ git tag -a v1.2 9fceb02
Sharing Tags
By default, the git push command doesn’t transfer tags to remote servers. You will have to explicitly push tags to a shared server after you have created them. This process is just like sharing remote branches — you can run git push origin <tagname>.
$ git push origin v1.5
Counting objects: 14, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (12/12), done.
Writing objects: 100% (14/14), 2.05 KiB | 0 bytes/s, done.
Total 14 (delta 3), reused 0 (delta 0)
To git@github.com:schacon/simplegit.git
 * [new tag]         v1.5 -> v1.5
If you have a lot of tags that you want to push up at once, you can also use the               --tags option to thegit pushcommand. This will transfer all of your tags to the remote server that are not already there.
$ git push origin --tags
Counting objects: 1, done.
Writing objects: 100% (1/1), 160 bytes | 0 bytes/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To git@github.com:schacon/simplegit.git
 * [new tag]         v1.4 -> v1.4
 * [new tag]         v1.4-lw -> v1.4-lw



git pushpushes both types of tags
Pushing tags usinggit push <remote> --tagsdoes not distinguish between lightweight and annotated tags; there is no simple option that allows you to select just one type for pushing.

Deleting Tags
To delete a tag on your local repository, you can use git tag -d <tagname>. For example, we could remove our lightweight tag above as follows:
$ git tag -d v1.4-lw
Deleted tag 'v1.4-lw' (was e7d5add)
Note that this does not remove the tag from any remote servers. There are two common variations for deleting a tag from a remote server.
The first variation isgit push <remote> :refs/tags/<tagname>:
$ git push origin :refs/tags/v1.4-lw
To /git@github.com:schacon/simplegit.git
 - [deleted]         v1.4-lw
The way to interpret the above is to read it as the null value before the colon is being pushed to the remote tag name, effectively deleting it.
The second (and more intuitive) way to delete a remote tag is with:
$ git push origin --delete <tagname>

Checking out Tags
If you want to view the versions of files a tag is pointing to, you can do a git checkout of that tag, although this puts your repository in “detached HEAD” state, which has some ill side effects:
$ git checkout 2.0.0
Note: checking out '2.0.0'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch>

HEAD is now at 99ada87... Merge pull request #89 from schacon/appendix-final

$ git checkout 2.0-beta-0.1
Previous HEAD position was 99ada87... Merge pull request #89 from schacon/appendix-final
HEAD is now at df3f601... add atlas.json and cover image

Git Aliases
Git doesn’t automatically infer your command if you type it in partially. If you don’t want to type the entire text of each of the Git commands, you can easily set up an alias for each command usinggit config. Here are a couple of examples you may want to set up:
$ git config --global alias.co checkout
$ git config --global alias.br branch
$ git config --global alias.ci commit
$ git config --global alias.st status

you can add your own unstage alias to Git:
$ git config --global alias.unstage 'reset HEAD --'
This makes the following two commands equivalent:
$ git unstage fileA
$ git reset HEAD -- fileA
This seems a bit clearer. It’s also common to add a last command, like this:
$ git config --global alias.last 'log -1 HEAD'
This way, you can see the last commit easily:
$ git last
commit 66938dae3329c7aebe598c2246a8e6af90d04646
Author: Josh Goebel <dreamer3@example.com>
Date:   Tue Aug 26 19:48:51 2008 +0800

    test for current head

    Signed-off-by: Scott Chacon <schacon@example.com>
As you can tell, Git simply replaces the new command with whatever you alias it for. However, maybe you want to run an external command, rather than a Git subcommand. In that case, you start the command with a ! character. This is useful if you write your own tools that work with a Git repository. We can demonstrate by aliasing git visual to run gitk:
$ git config --global alias.visual '!gitk'

                                                  Git Branching

Creating a New Branch

$ git branch brance_name

Switching Branches
$ git checkout testing


Switching branches changes files in your working directory
It’s important to note that when you switch branches in Git, files in your working directory will change. If you switch to an older branch, your working directory will be reverted to look like it did the last time you committed on that branch. If Git cannot do it cleanly, it will not let you switch at all.





Basic Branching and Merging


Branch Management
The git branch command does more than just create and delete branches. If you run it with no arguments, you get a simple listing of your current branches:

$ git branch
  iss53
* master
  testing

To see the last commit on each branch, you can run git branch -v:
$ git branch -v
  iss53   93b412c fix javascript issue
* master  7a98805 Merge branch 'iss53'
  testing 782fd34 add scott to the author list in the readmes
The useful --merged and --no-merged options can filter this list to branches that you have or have not yet merged into the branch you’re currently on. To see which branches are already merged into the branch you’re on, you can run git branch –merged:
$ git branch --merged
  iss53
* master
To see all the branches that contain work you haven’t yet merged in, you can run git branch --no-merged:
$ git branch --no-merged
  testing

This shows your other branch. Because it contains work that isn’t merged in yet, trying to delete it with git branch -d will fail:
$ git branch -d testing
error: The branch 'testing' is not fully merged.
If you are sure you want to delete it, run 'git branch -D testing'.

Branching Workflows

Remote Branches
You can get a full list of remote references explicitly with git ls-remote [remote], or git remote show [remote] for remote branches as well as more information. Nevertheless, a more common way is to take advantage of remote-tracking branches.
