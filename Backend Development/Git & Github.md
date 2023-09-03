Git is an open source distributed version control system. It tracks changes in any set of computer files. 

**Difference between Git & Github** 
 - Git is an version control system.
 - GitHub is a online tool which uses the power to GitHub or similar version control systems to create a collaborative workspace for open and closed source applications.

## Git Commands 

1. `git init` -> Power your folder to use git and initialize and empty git repository.It also creates a .git file which contains all the logic for managing the versions of your project.

2. `git add < filename >` -> Use this command to add a file to the staging area from the working. Note - To add all the files to the staging area use `git add .` .

3. `git rm --cached < filename >` -> Use this command to remove a file from staging area back to working area.

4. `commit` -> Commit is a particular version of the project. It captures a snapshot of the projects staged changes and creates a version out of it.

5. `git commit -m "Message"` -> Use this command to register staging changes to the commit.

6. `git log` -> Lists down all the commits in the repository.

7. `git restore < filename >` ->  It removes all the file changes from the working area which are to be staged. This can help in removing dirty piece of code.

8. `git restore --staged < filename >` -> It removes all the file changes from the staging area to the working area.

9. `git diff <commit id-1> <commit id-2>` -> Used to see the new changes added between two commits. You can get the commit id's using the `git log` command.

10. `git remote` -> Lists down all the remote connection names.

11. Remote connection -> It links two git repositories for uploading and downloading changes from each other.

12. `git remote add <name of remote> <link of remote>` -> This commands helps us to add a new link to the remote repo and gives a name to it. Ex- origin

13. `git remote rm <name of remote>` -> Deletes the remote connection.

14. `git remote rename <old-name> <new-name>` -> This renames the remote connection.
Note - The name of the remote connection is always used to establish a connection between the two repos.

15. `git pull <remote name> <branch name>` -> Download latest changes from the branch of the mentioned remote
16. `git commit --amend` -> This is used to append the changes to the last commit instead of creating a new commit.
17. `git reflog` -> It stores the previous commit id as well as the amended id after a commit has been amended.
18. `git ls-files` -> Lists downs all the files in the staging area.

### Recommended Practice to do - 
   
      - make changes
      - git add <file>
      - git commit
      - git pull
      - git push


## Different Areas in Git

1. `Working area` -> Files which are not being currently handled by git are in the working area.It means changes done to these files are not managed by git. When on using the `git status` command if there are `untracked files` then these are the files currently in the working area.

2. `Staging area` -> Files in the staging area represent what all files are going to be the part of the next version. The staging area is the place were git knows what all changes are going to be done in the previous version to the next version.

3. `Repository area` -> This area contains all the details of the previously registered versions. Git knows and manages the version history of all the files in this area.

Difference between rm and restore
 - Ans - git rm is used to move back the entire file to an untracked state whereas git restore is used to move the files from working and staging area.

- Merge conflicts are very common scenario.
  Merge conflicts can occur if multiple people try to make changes to the same file and try to collaborate.

# How Git is Internally Works

Git is heavily dependent on Hashing and Tree/Graph data structures for its working.

1. Git is like key value store 
 - Key - Hash of the data
 - Value - Data
Git used a cryptographic  hashing function SHA-1 (Secure Hashing Algorithm ) which for a given data outputs a 40 digit Hexadecimal number which remains same for given set of data.
2. After this Git compresses the data in form of blob and stores some meta data about it.
    Note - BLOB - It stand for Big Large Binary Object. Inside the block it stores the characters size, delimiters and the actual data.
3. Inside the .git folder all the files added to the git are stored inside the objects folder in form of key value pairs wherein the first 2 digits of the hash are the folder name whereas the last 38 digits are value of key value pair (filename). 
     Note - The data in these files in stored in form of BLOB hence cannot be accessed with cat function.

4.  `tree .git` -> Used this command to visualise the entire .git folder structure.
5. `git cat-file -p < entire hash value >` -> Use this command to print the contents of the files added to git with the respective hash value.
6. The **directed tree** structure of Git stores the data in the following manner - 
     - It uses the hash as pointers to store
         1. To store BLOBs
         2.  Also internal trees in maintained.
     - Also stores the meta-data
         1. Type of meta-data
         2. Directory name or filename
         3. Mode of file(.exe, .txt etc.)
     Note - It also manages the directory structures as these points can point to different trees and blobs as well.

### .git Tree
```js
.git
├── COMMIT_EDITMSG
├── HEAD
├── config
├── description
├── hooks
│   ├── applypatch-msg.sample
│   ├── commit-msg.sample
│   ├── fsmonitor-watchman.sample
│   ├── post-update.sample
│   ├── pre-applypatch.sample
│   ├── pre-commit.sample
│   ├── pre-merge-commit.sample
│   ├── pre-push.sample
│   ├── pre-rebase.sample
│   ├── pre-receive.sample
│   ├── prepare-commit-msg.sample
│   ├── push-to-checkout.sample
│   ├── sendemail-validate.sample
│   └── update.sample
├── index
├── info
│   └── exclude
├── logs
│   ├── HEAD
│   └── refs
│       └── heads
│           └── master
├── objects
│   ├── 24
│   │   └── fc88acf07c0e198e8fba4a001a260a9697baf8
│   ├── 33
│   │   └── 2547e1f712d3634f0fef55cb56a5e753916766
│   ├── 6b
│   │   └── 2b3db0f6520c7b9ef75fa769bed07353446437
│   ├── 8b
│   │   └── d34b7011eac4aa6a72f5434b8d0ab7ba2411b3
│   ├── 98
│   │   └── f6cc37e7a31358b1f9ddcc47987a5676064713
│   ├── e7
│   │   └── 0ec4d2e0fe47650c1a2689291630053ae191c8
│   ├── info
│   └── pack
└── refs
    ├── heads
    │   └── master
    └── tags
```

Terminal Outputs
```js
- git cat-file -p e70ec4d2e0fe47650c1a2689291630053ae191c8 
100644 blob 24fc88acf07c0e198e8fba4a001a260a9697baf8	Readme.md
- 100644 blob 6b2b3db0f6520c7b9ef75fa769bed07353446437	index.js
- 040000 tree 332547e1f712d3634f0fef55cb56a5e75391676 src


- git cat-file -t 98f6cc37e7a31358b1f9ddcc47987a5676064713
commit


-git cat-file -p 98f6cc37e7a31358b1f9ddcc47987a5676064713  
tree e70ec4d2e0fe47650c1a2689291630053ae191c8
author Priyanshu0512 <priyanshuk0595@gmail.com> 1693655251 +0530
committer Priyanshu0512 <priyanshuk0595@gmail.com> 1693655251 +0530

Added index.js files

- git cat-file -p 98500e6663b8774d9cdab671a0e14e7ce4aa7283 
tree c304a0693d80fec904d6058611d538a929ddbafa
parent 98f6cc37e7a31358b1f9ddcc47987a5676064713
author Priyanshu0512 <priyanshuk0595@gmail.com> 1693656741 +0530
committer Priyanshu0512 <priyanshuk0595@gmail.com> 1693656741 +0530

Added test.js
// Other files can also be checked.
```

After the initial commit the commit object in the tree will also be pointing to the parent element.The root commit will not have a parent element in it.

- `git gc` -> This command does the garbage collection manually. It packs the hashed data into pack files.This is also done automatically when commits are done.
```js
git verify-pack -v .git/objects/pack/pack-e773582e7873476b0d10b94dd1b48933d9a8249a.pack

98500e6663b8774d9cdab671a0e14e7ce4aa7283 commit 242 161 12
98f6cc37e7a31358b1f9ddcc47987a5676064713 commit 201 135 173
24fc88acf07c0e198e8fba4a001a260a9697baf8 blob   88 85 308
6b2b3db0f6520c7b9ef75fa769bed07353446437 blob   28 38 393
8bd34b7011eac4aa6a72f5434b8d0ab7ba2411b3 blob   31 41 431
e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 blob   0 9 472
c304a0693d80fec904d6058611d538a929ddbafa tree   138 140 481
332547e1f712d3634f0fef55cb56a5e753916766 tree   36 47 621
e70ec4d2e0fe47650c1a2689291630053ae191c8 tree   5 16 668 1 c304a0693d80fec904d6058611d538a929ddbafa
non delta: 8 objects
chain length = 1: 1 object
.git/objects/pack/pack-e773582e7873476b0d10b94dd1b48933d9a8249a.pack: ok
```

**Stashes** - Stashes are used to store the changes which you want to be present in the staging area but does want to commit them to the repo.
**Internally a stack structure is maintained for storing stacks.** 

**Basic commands relating to stashes** - 
- `git stash` -> This command stashes all the files present in the staging area.
     Note - An initial commit is required before you can start stashing the files.

- `git stash list` -> Use this command to get the list of all the stashes made.
- `git stash apply` -> This commands brings backs the  last stashed files to the staging area while maintaining the stash as well.
- `git stash apply stash@{<stash number>}` -> This is used in case of multiple stashes being done. Using this we can apply a particular stash as per the need using the stash number from the `git stash list`.
    Note - Git does not allow multiple stashes to be applied to the same file.As after applying one stash and committing the changes and then when you apply the apply any other stash then merge conflict occurs if changes are done to same line which needs to resolved manually in the file or by using the VS code merge conflict resolver.

- `git stash --include-untracked` -> This commands allows you to even track the changes of the untracked files.
- `git stash --all` -> Used to stash all the files both tracked and untracked.
- `git stash --included-untracked --<filename>` -> To stash a particular file from the untracked files.
- `git stash --<filename>` -> To stash a particular file being tracked.
- `git stash clear` -> Removes all the stashes 
- `git stash pop`- > Applies the last stash and drops(removes) it.
- `git stash drop` -> Drops the last stash without applying it.
- `git stash drop @stash{<stash-number>}` -> Removes the mentioned stash.
- `git stash save"message" --include-untracked` -> Used to stash files with a meaningful message. (Add --include-untracked after the message to stash untracked files with a message.)

# Branches
Branch is just a pointer to a particular commit.

- `git checkout -b "name of the new branch"` -> Creates a new branch with the given name
- `git checkout "name of the branch"` - > Used to switch to the entered branch.
- `git log --all --decorate --oneline --graph` -> To get a visual representation of all the branches.
- `git log --graph` -> To get the logs in form of a graph view.
- `git branch` -> Shows a list of the branches present where * symbol represents the current branch.

**Head** - It tell about the current working branch and the current commit.

What happens it branch switching is that the branches point to particular commit. When we switch the branch it is the head pointer which starts to point at the specified branch to show the  workflow of that branch.

### Tags  

- `git tag -a <tag-name> -m "message"` -> This command creates a tag.
- `git show <tag-name>`-> Displays info about the mentioned tag.
- `git show-ref --tags` -> Displays all the tags.
- `git push --tags origin master` -> To push the tags to Github.
**Difference between tags and branch pointer** 
 - The tags pointer to a particular commit and does not moves with future commits whereas the branch pointer moves ahead with the new commit.

### Cloning a Repo 

- `git clone <link to the repo>` -> This clones the repository from your Github to your local machine.
    Note - Before cloning you first need to fork the repo to your own Github first.

**Forking** - It is just creating a copy a project from some repo on Github to your own Github.


### Upstreams 
When you fork a repo from Github the start to contribute to the repository on an issue in your fork repo meanwhile other changes are been pushed to the main repository(Project). In order to keep up to date which the changes being made a upstream can be set-upped to include the changes being made to the main directory. 
 - Upstream - The repository being Forked.
 - Forked Repo - It is origin master.

- `git remote add upstream <link to the upstream>` -> This creates a upstream to the forked repo which further can be pulled to the local repository of the system.
- `git pull upstream` -> Pulls all the changes from all the branches
- `git pull upstream <name-of-the-branch` -> Pulls changes changes from the specified branch only.


### Git mistakes fixes 

- `git checkout --<file-name>` -> If there are a file in staging area to be committed and some changes to the same file are in the working area then the above commands overwrites the changes of the working area with the staging area.
- `git checkout <commit-id> --<filename>` -> This command is used to revert the changes to state of the file during the mentioned commit-id.This works for the files in the staging area.
- `git clean -f` - Cleans the working area by removing the untracked files.
     `git clean -f -d` -> Removes all the directories in the working area.
- `git clean --dry-run` -> This is displays the files which it is going to remove if the `git clean -f` command is executed. Sort of a dry run.
    `git clean -d --dry-run` -> If shows what directories its is going to remove along with the files.

- `git checkout <commit-id>` -> This command makes the head pointer point at the mentioned commit-id. In this case you will be in a detached HEAD state where the head pointer will be pointing to the mentioned commit whereas the branch pointer will point the current commit. (checkout command makes your head pointer move.)
- `git switch -` -> Use this command to revert the changes made by the above command.
- `git branch -f <branch-name> <commit-id-of head>`- >This is used to move you branch pointer to the head pointer in case of a detached HEAD state.
    Note - Now the commits in the branch which are not pointed by some pointer become dangling commits and will be removed by the Git garbage collector when it runs.

**Filter for Git log**
- `git log --since="yesterday"` ->Shows all the commits made since yesterday. 
    Some other values are 
    - "1 minute ago"
    - "5\ minute age"
    Alternate Form - `git log --since=1.minute`

- `git log --grep=second`-> Fetches the commits which have "second" substring in there data.

**Parents & Ancestors** 
- `git log <commit-id>^n` -> This command gives you the nth node (immediate parent) of the the commit.
- `git log <commit-id>~n` -> This command gives you the nth node(ancestor) of the commit.

### Merging Branches

- `git merge <branch name>` -> This merges the current branch with the mentioned branch in the command.
    Note - Now in a merged branches `~` moves you to  ancestors of the same branch while `^` moves to  parents in different branch.
- Fast - forward -> If a new branch is created but the master or the branch from which this new branch was originally created does not move forward and you try to merge the two branches that **fast-forward** occurs wherein the master branch pointer or the branch pointer moves the current(created branch Head pointer).
- `git switch <branch-name>` -> This command is also used to change the branch apart from the `git checkout` command.

This merging of multiple branches can make the commit log a bit untidy there a better way to merge features etc. is by using the rebase method.
 - `git rebase <branch-name to be merged>` -> Rebase command makes a copy of the branch to be merged and then attached it to the head of the master branch and moves the branch pointer to it.

Now on rebasing the commits to master branch all the commits gets added to the master branch but by using the squash method we get squash or combine all the commits to be rebased into a single commit and then rebase that commit.
- **For squashing and rebasing you first need to switch to the branch to be squashed.**
- `git rebase --interactive <name of the branch to which this branch has to be added>` - > On using this command an interactive mode in vim opens up where all the commits of the branch to be squashed are listed. Now you call squash all the commits by writing the squash keyword before then where they are listed. 
    Note - > You need to pick one commit which will get attached to the master branch by writing pick before it. 

### Git Reset

Git reset have three modes namely 
 - Soft -> It just move the head and branch pointer and does not do any changes to staging and working area.
 - Mixed(default) ->  It not only moves the head  but also rests the staging area to the staging area of that particular commit and brings backs any files in the staging index to working directory(not the working area).
 - Hard -> It moves the Head pointer to the specified commit-id and resets the staging and working area to match the state to the commit restated to.(By default if commit-id is mentioned the HEAD is the default entry.)

Git reset not only moves your head pointer but also the branch pointer.

- `git reset --soft <commit-id>` -> Moves the branch and head pointer to the mentioned commit-id.
- `git ORIG_HEAD` -> This command brings the head to the position of the head before the last reset.
    Note - If two resets arre done then you cannot go back to the second commit unless you have some tag or some other branch pointer pointing at it.

**Note- Now previously in Git mistakes section we encounter the problem of dangling commits. Now this dangling commits can be restored only and only if no further commits have been made to its parents after it has gone to a dangling state then by using the command `git reset ORIG_HEAD` the branch and head pointer moves to the dangling commit.**

**Git Revert** -
Git revert instead of changing the position of the head pointer creates a new inverse commit and then reverts the changes to that commit. It is a more safer way to revert the changes. 
- `git revert <commit-id>` 
**Note** - If changes are made to multiple files then on reverting the changes merge conflicts might occur which needs to resolved manually in the resolve editor in VS code.

**Git Fetch** - Git fetch download all the changes of the branches you are currently having from the Github.
- To download the changes of a particular branch use `git fetch origin <name of branch>` after switching to that branch first.
- `git fetch/pull --all ` -> To fetch all the branches from Github.
- `git branch -r` -> To check all the remote branches download from Github.

