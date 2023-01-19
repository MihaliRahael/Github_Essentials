# Github and Github Actions Essentials

## Contents

-   Need for GitHub
-   Git basic operations
-   Git basic commands
-   How to participate in open-source community?
-   Resolving conflict scenarios
-   **Github operations in Linux**
-   Creating repository in Git
-   Check repository history
-   Doing Commits
-   Git restore
-   Git ignore
-   Tagging
-   Branching
-   Merging
-   Remote Repository cloning
-   Working with remote directory
-   Pull requests
-   Cherry picking
-   **Github Actions**
-   Introduction
-   Why Git hub actions, why not Jenkins?
-   Workflow file syntax
-   Jobs
-   Build docker image and push to private repo

## Need for GitHub

Github is a platform for open-source projects. Lot of developers who have developed their own libraries for python or other languages, can host their projects on github and make them publicly available so that the community can use the projects also they can contribute to the project. So team or individual developers manage those project can new contributors or things happening inside their repository like creating pull requests, new people joining in as contributors and so on, they have a lot of organizational tasks to manage.

Example for a task

Say I have created a Python library which have few contributors and users of that library. Whenever a use of library sees that a new release of library has a bug or somethings isn’t working, they can create an issue. I have to check the issue and sort it under minor or major or is it reproduceable etc. They I can assign this issue to a contributor or I can take it myself. Lets say one of the contributor has fixed the issue and raised a pull request, so that I can merge it with the next release of the library. So I will check the pull request, review the code, bug fixing etc and then will merge it to the master branch. So, I will be releasing it in the next version, so the users can upgrade the version.

![image](https://user-images.githubusercontent.com/106816732/213403448-4eef940f-9333-4ede-b841-b2fc850185a9.png)

So after the pull request is merged with the master branch, I need to build a pipeline which will test my code, build my artifact and deployment. Moreover I need to prepare some release notes where I can document about what got added in the new version, and need to update the version number.

![image](https://user-images.githubusercontent.com/106816732/213403737-67aee21f-8b4c-4919-b62c-41af8b67746c.png)

So the following screenshots shows some of the workflows I need to do as a maintainer of this repository.

![image](https://user-images.githubusercontent.com/106816732/213403784-1a286370-f536-4ada-a19d-8384bd3bbe77.png)

Suppose project is getting bigger, more contributors are joining, more issues and pull requests are getting created, the more organizational effort its going to be. So I want to automate these managerial tasks as much as possible. For that purpose Github actions is created (Tutorial follows below)

## Practical Thought on GitHub

Suppose 10 members are working in a project. New changes will be happening very usual (CR – Change request). There will be a ‘main’ branch where all the stable codes and files associated with the project will be merged. This main branch will be deployed in the production. If any member needs to make any changes in the code, will they directly do into this main branch? If they do, it will create conflicts, bugs and chaos. Suppose sprint 1 is going on where 10 stories are there which will be divided among the developers. In order to avoid the above-mentioned issue, developers will create a branch which will be the copy of main branch and each developer can work independently on their stories. This process is called cloning the branch.

Suppose dev 1 has finished his story and updated his branch. After then the code shall be merged with the main branch. This request is called push request. Suppose dev 2 has finished the story and updated own branch. Now he needs to merge this with main. But in order to do that, he need to initiate a pull request from main branch for getting the updated version of code as dev 1 has already pushed his code. This will resolves the conflicts.

The above explained is one strategy. In practical, there will be a single source of truth ie main branch. Then there will be developer branch (dev), which is the exact replica of main. SO the developers will clone from dev branch.

Create an efficient and easy README file using readme.so/ <https://www.youtube.com/watch?v=QcZKsbgsLa4>

## Github basic operations

1.  Create Github profile
2.  Create a new repository in public mode
3.  Give repository name
4.  Check “Add a README file”
5.  Select gitignore template as Python. (gitignore contains the files and data which needn’t to get committed or push to github.
6.  Choose licence as Apache Licence 2.0
7.  We are going to commit in this repo. We need to clone this repo into the local so that we will be able to commit on to it. In order to clone this repo
8.  Create a folder in local. Say we have created a folder named ‘ML End to end Project’ in D: drive.
9.  Goto CMD. Goto the path of folder using the commands. ‘D:’ ‘cd D:\\ML End to End Projects’
10. Goto github repo Code Local Copy the URL
11. Goto CMD Use command ‘git clone \<copied URL\>’
12. Copy the ipynb and pkl file we created to this cloned repo

## Git basic commands

**git config –global user.name “Bonny Philip”**

**git config –global user.email** [**philipbonny18@gmail.com**](mailto:philipbonny18@gmail.com)

\# The above two commands are first and for single time

**Git status** \# shows untracked files

**git add \<filename\>**

**git add .** \# this will add all files

-   Once we add the files which need to commit to repo, we will do the commit operation
-   git status \# will give all the files we need to commit
-   git add will track the files, git commit will move to the staging env
-   git push will push files from staging env to main branch

    **git commit -m "This commit contains all the necessary files"**

-   Once we done with commit, files are ready to be pushed to the repo.
-   Push command contain two terms remote and branch. We are basically pushing our code to main branch
-   Whatever commit we have made, it will be a specific environment named origin. From there we need to move to main branch

    **git push origin main**

-   Git add will move files to a staging location. Git commit will move the same from staging loc to origin. And form there ‘push’ will push this to our branch in repo
-   **Developer 1 needs to clone main branch to his new branch**
-   **git branch dev1** \# creates new branch along with ‘main’ branch
-   **git branch** \# shows all the available branches and the current branch we are in
-   **git checkout dev1** \# switches from main to dev1. Suppose we made some changes in README file. This change is visible only in dev1 branch README. Ie if we switch back to main branch, we wont be able to see that change in the same README.

Suppose we are in dev1 branch and made changes in code and files. Git status shows untracked files. Now add and commit.

-   **git add .**
-   **git commit -m “This is developer 1’s commit”**
-   **Merge branch with main**
-   **git checkout mai**n \# first move to main branch
-   **git merge dev1** \# Now check README file in main branch, we can see the changes made in dev1 README here.

Once the merging is done we don’t need to add or commit the files cos that is already done from dev1’s side. We just need to push from main branch.

-   **git push origin main \#** once we merged we will push the change to main.
-   **Delete the branch**
-   **git branch -d dev1** \#verify the deletion using ‘git branch’

## Other important git commands

-   **git branch** \# now the o/p would be master which is the default branch created while creating a repo.
-   **git branch -M main** \# now the o/p of ‘git branch’ would be main. Changed master to main branch
-   **git remote add origin** [**https://github.com/bonnyphilip/repo_name.git**](https://github.com/bonnyphilip/repo_name.git) \#we will do the committing into this url
-   \*\*git log \#\*\*for checking logs
-   **git restore –staged .** \# this will unstage the file

**Error Note :** Whenever we run a git command in CMD (windows or in visual studio code), if we face an error saying “‘git’ is not recognized as an internal or external command”, follow the steps.

1.  In the Start Menu or taskbar search, search for "environment variable".
2.  Select "Edit the system environment variables".
3.  Click the "Environment Variables" button at the bottom.
4.  Double-click the "Path" entry under "System variables".
5.  With the "New" button in the PATH editor, add C:\\Program Files\\Git\\bin\\ and C:\\Program Files\\Git\\cmd\\ to the end of the list.
6.  Close and re-open your console.

## How to participate in open source community ?

We have a repo (eg: bonny/deep_learning_project ) and we need 5-6 developers to work over here as collaborators. Settings Collaborators Add email id of a collaborator. Collaborator will receive an invitation request in mail. Suppose steffy is the collaborator. Once she accepts this invitation, she can see the repo in her git hub profile. She can use ‘fork’ feature to clone this repo to her’s. Resultant repo would be Steffy/deep_learning_project forked from bonny/deep_learning_project. Go to code copy the URL. Goto cmd clone the repo to local machine using git clone command. She can make some changes in the code. After the changes being made, she needs to go to terminal go to main branch do add, commit and push commands Go to git hub. It would be shown “This branch is 1 commit ahead of bonny:main” Go to pull request and create new pull request. Bonny will be able to see the pull request in his git hub. He can check the changes made by steffy. Then he can do merge pull request.

Now one scenario is , Bonny has made a change and committed. Now steffy can see that, “This branch is 1 commit behind Bonny from steffy:main”. Do sync fork update branch. Now Steffy can see updated main branch.

Conflict scenario 1 : Bonny has made changes. Now Bonny is one commit ahead of Steffy. Now steffy has made changes without fetching the main branch. And when she tries to add, commit and push to main branch, it will throw an error saying fetch main first. So she should initiate a pull request first.

-   **git pull origin main –** pulling main branch to her branch. Pull command does the pulling + merging
-   **git status -** will show the unmerged file from main
-   **git commit -m “merging main”** – merge steffy’s branch with main branch
-   **git push origin main –** now steffy pushing the changes made by her
-   **Go to git hub Sync Fork Discard commits –** Now she can see both the changes made by Bonny and herself.
-   **Steffy should raise pull request. -** Bonny will be able to see the pull request in his git hub. He can check the changes made by steffy. Then he can do merge pull request in git hub itself.
-   Once merging completed from Bonny’s side, main branch is updated with all the changes made by Bonny and Steffy. No Steffy’s branch needs to be in sync with Bonny’s main branch. So steffy needs to do **Synch Fork Update branch**

## Resolving conflict scenarios

Say I have a repo having main as default branch. Create a new branch dev ie we have taken a copy of main branch. When we make changes in dev env, we need to raise PR to the main in order to merge. But at the time of pull request, there might have changes happened with main branch cos other team members might have merged their code with the main. Which means dev branch is behind the main updates and dev is trying to merge with the main. This creates a conflict.

‘main’ branch to and fro updates. In CLI, I have created a file index.txt. Inorder to see this in desktop, we need to add, commit and push. Similarly say I have added a new line to index.txt or I have created another new file in main branch from desktop. Inorder to reflect the same in CLI, use command “**git pull origin main**”

In GitHub desktop, I have created a new branch dev. Inorder to see that branch in CLI, use command “**git branch -r** “. Use “**git switch dev**” to switch to that branch. Create new file dev.txt in dev branch without syncing the main branch.

![image](https://user-images.githubusercontent.com/106816732/213404004-92edb9fb-b219-468a-9093-0ea6f3dc5fbb.png)
Now go to desktop.

![image](https://user-images.githubusercontent.com/106816732/213404049-53666cc8-76c4-4cef-a73e-c428a9f1d91f.png)

![image](https://user-images.githubusercontent.com/106816732/213404083-03285057-a083-485c-acc6-10b012e34a6d.png)

![image](https://user-images.githubusercontent.com/106816732/213404127-93ecf320-1198-49e0-b825-1eee01824382.png)

We were able to raise the PR and merge it with main without any issue just cos, both file are different.

Now lets see both dev and main are working in same file index.txt. First lets merge dev with main in order to appear index.txt in dev as well. Lets say we have dev has edited the index.txt. Same time, main has edited the same file from desktop and committed. If we go to dev branch in desktop we can see “This branch is n commits behind main”

## Github operations in Linux

### Creating repository in Git

**There are 2 methods :**

1.  **Initializing a git repo in local machine**
-   mkdir my_repo
-   cd my_repo
-   git init - make this directory as git local repo
-   ls -a - contains .git/ which indicates this is my working or project directory. Also we can see (master) means master branch has been created.
-   git status

![image](https://user-images.githubusercontent.com/106816732/213404181-21996e88-261a-41b3-8cd5-bc5a9da22125.png)

-   vi file.txt - create file and check status

![image](https://user-images.githubusercontent.com/106816732/213404223-01fc27a7-b822-4220-ad2c-3612b64ef463.png)

1.  **Cloning a remote repo**
-   git clone \<URL\>

### Check Repository history

-   git log - show all the commits and other details. Enter q button to exit
-   git log --oneline - short version of logs
-   git show \<commit id\> - show details of specific commit
-   git log --stat - which all files has modified
-   git log --patch - detailed stat, ie lines which are modified in files.
-   **git log --oneline --graph –all - show all the commits and changes made in all branches**

### Doing Commits

git add – will move the modified file from working directory to the staging area

-   git add \<filename\>
-   git add .

git commit

-   git commit - opens a text editor to write about commits. Files added to staging location will be committed.
-   git commit -m “this ” - directly writing message instead opening an editor

### Git Restore

-   git restore - command will unstage or even discards uncommitted local changes
-   git restore --staged - removes the file from the staging area, but leaves its actual modifications untouched.

### Git Ignore

The .*gitignore* file is a text file that tells git which files or folders to ignore in a project. A local .gitignore file is usually placed in the root directory of a project. The entries in this file can also follow a matching pattern.

-   \* is used as a wildcard match
-   \# is used to add comments to a .gitignore file

### Tagging

Tagging is a mechanism used to create a snap shot of a git repository. It is traditionally used to create semantic version number identifier tags that correspond to software release cycles. Say we have 12 commits happened in a project and we want to make first 7 commits as v1.0 and upto 12 v2.0 then we will make use of tags. There are two types of tagging;

-   annotated tag - give information on commit, message, timestamp of tag, author etc
-   lightweight tag. – no extra info

Commands

-   git tag -a v1.0.0 : text editor will open, write like “Version 1.0.0 Release”
-   git tag : will show all the tag info

Suppose we have made some changes in files, and commited it. Git log shows, there is a commit happened after versioning.

![image](https://user-images.githubusercontent.com/106816732/213404285-3a3f1139-b7c2-42e8-b0df-a0e4e98543ac.png)

-   git tag v1.0.2 : this is light weighted tag without giving any message
-   If we want to tag a specific commit

    Say we want to tag ‘ce21591’

-   git tag -a v0.0.4 ce21591
-   git log --oneline - will show the details
-   git tag -d v0.0.4 - will delete the tag

### Branching

Branches allow you to work on different parts of the project without impacting the main branch. when the work is complete the branch can be merged with the main project. You can even switch between branches and work on different projects without them interfering with each other.

-   git branch - lists down all the available branches
-   git branch dev1 -creation of new branch dev1
-   git checkout dev1 – moving to dev1
-   git checkout -b dev2 - creation of new branch and moving there simultaneously
-   git switch main / git switch dev2 - switching between branches. We need to manually checkout to enter that branch. switch command works above git version 2.23
-   git switch -c dev3 - creation of new branch and switching there simultaneously
-   git branch -d dev3 - deleting a branch

### Merging

Note : Open both VS code and terminal to see changes.

![image](https://user-images.githubusercontent.com/106816732/213404323-ddae17bc-ed03-4529-b8a0-087b6f5815ae.png))

Explanation :

-   we have a main branch and dev branch
-   we have created a new branch ‘feature’ and directed to switched there. In VS code also switching will automatically happens
-   Make some edits in app.py (cloned from main) and created a new file feature.py. See the status. Note that we have made these changes in terminal.
-   Do add and commit. We can see the changes in VS code.
-   Switch to master.
-   **git log --oneline --graph –all - show all the commits and changes made in all branches**
-   git merge feature - doing the merge operation from master branch. VS code also switched back to master. Check the changes happened in VS code master. Ie changes made in feature branch will be reflected in the master once merging done

Note : before merging, HEAD was at master branch. Once we made 3 commits in feature branch, feature branch is commits ahead of master. Once we have done the merging, HEAD will shift from master to (master, feature) (This can be viewed by git log --oneline --graph --all)

![image](https://user-images.githubusercontent.com/106816732/213404365-a44ad965-c5ff-46c9-a13d-4728293e6bc8.png)

There are two types of merging; fast forward merging and regular merging. Here ‘feature’ branch is aligned with the master so merging done is called fast forward merging. Dev branch is diverged and merging of this branch to master is called as regular merging.

### Remote Repository cloning

1.  git clone \<connection string in the format of http\>
    1.  git clone \<ssh link in the format of git@...\>

        Before doing the ssh cloning, generate new SSH key using the command ssh-keygen -t ed25519 -C "your_email@example.com"

        Copy the new public key from the saved location in local system to ssh key in github

    2.  download as zip

### Working with remote directory

![image](https://user-images.githubusercontent.com/106816732/213404421-c6cd360c-88a2-441a-a0f7-b91bdceca9f6.png)

### Pull Requests

While working in a big team, its not a good practice to merge your work directly into the main branch. Once a pull request is opened you can discuss and review the potential changes with collaborators and add follow up commits before your changes are merged into the base or master branch.

-   Lets go to terminal. Suppose we are a developer and have cloned the repository.
-   cd my_repo - this is my working directory which contains few files and folders which is already been my master branch earlier
-   git checkout -b dev5 - created and checked into new branch dev5. All the data in master will be available here as well.
-   vim new_text.txt - I have created a new file in dev5 branch.
-   git add .
-   git commit -m “Raise Pull request”
-   git remote - shows the remote connections. Say we found test_origin branch.
-   git push test_origin dev5 - push is successful by asking to raise pull request from github URL
-   Go to github, we can see – “dev5 had recent pushes” “Compare and pull request”
-   After creating a pull request, check for conflicts and merge the pull request with master branch
-   Now we can see new_text.txt in both dev5 and master branches.

### Chery picking

This is for applying some commit from one branch into another branch. When we do cherry picking, it brings in changes from a specific commit or we choose one or more commits.

![image](https://user-images.githubusercontent.com/106816732/213404465-0a859b1c-1cb2-47be-9184-d6531019ad5c.png)

-   Say we have created two files cherry.txt and mango.txt in the test_branch. Do the commit one by one. Each commit will be having its own SHA id.
-   Switch to master. Run git log --oneline to find the recent commits and its respective SHA ids
-   Git cherry-pick \<sha id of required commit\> \<sha id of required commit\> …

## GitHub Actions

### Introduction

-   Platform to automate software development workflows
-   CI/CD is one of many workflows

![image](https://user-images.githubusercontent.com/106816732/213404495-bd863b0b-4f33-48b5-9eff-86051f2fbcb0.png)

So when you automate these flows, the concept is nothing but listen to the event and trigger workflow.

Eg: If someone creates an issue, we want to automatically sort the issue, label it, assign it or write a code to reproduce it etc. All thse can be automated using Actions. Each of these small tasks automatically trigger is a separate action. Combination of these actions makes up workflow.

![image](https://user-images.githubusercontent.com/106816732/213404533-a62a0f61-3a92-4dc7-8c69-f35a4179b77f.png)

Consider a private repository project on GitHub. The most common workflow for the repo is CICD pipeline.

![image](https://user-images.githubusercontent.com/106816732/213404578-9e8d0048-9137-43f9-a9fc-712600b00784.png)

**Why Git hub actions, why not Jenkins?**

![image](https://user-images.githubusercontent.com/106816732/213404613-f878227b-563e-4d28-9fdd-d85532f6f898.png)

Tool for developers means, team doesn’t need another resource for doing CICD pipeline, developers themselves can manage.

![image](https://user-images.githubusercontent.com/106816732/213404658-02538ee3-dc96-465e-abd0-bf474bbcddc4.png)

![image](https://user-images.githubusercontent.com/106816732/213404683-26213693-c8cc-4cad-a5e2-c12263371507.png))

Basically we may have different combinations of tools we are using in development process. We don’t need to sit there configure the CICD pipeline with all these tools, like installing Python, Docker, Configure integrations and plugins, AWS etc. Instead we can ask for an environment with node and docker available, with a version I specify, and simply connect to target and deploy. This is what possible through github Actions.

Step 1: Push all the project files into the repository

2: Either choose the predefined workflow file from Actions or create a custom one.

3: Once the yaml file is created, initiate commit changes (adviceable to create new branch for this commit and start a pull request). We can see the build happening status.

### Workflow file syntax

![image](https://user-images.githubusercontent.com/106816732/213404721-dc73b938-eb39-44ac-97c7-e30af17c87f0.png)

![image](https://user-images.githubusercontent.com/106816732/213404761-c0c7d545-2cd5-48e3-883a-6db197dbd67f.png)

![image](https://user-images.githubusercontent.com/106816732/213404794-6a97ff4d-a90f-49d2-a004-8d2e929853df.png)

Whenever any event or events happens we can trigger the workflow (which can be an action or combination of actions) defined inside ‘jobs’. Eg: Here if there is a ‘push’ or ‘pull’ happens wrt main branch, the workflow will initiate. Another example for events can be creating an issue or a contributor joining etc.

Another on condition :

![image](https://user-images.githubusercontent.com/106816732/213404865-a13931ed-c2b5-4555-a0bd-565ed3f66b92.png)

<https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows>

uses: actions/checkout@v2 - Whenever we want to build or test application, first we need to checkout the repo or code first. Actions/ path in github is where pre-created or predefined actions are hosted, so basically we can assume that everybody who uses a CICD pipeline in github actions will need to use checkout command. (Instead of letting everybody do that on their own, github has created an action called checkout that people can use).

Go to github.com/actions we can see predefined repositories.

### Jobs

![image](https://user-images.githubusercontent.com/106816732/213404904-939d9580-3b55-4192-84af-9802201221d9.png)

The codes will get checked out, java version gets installed, and build gradle. All these tasks will be done in same environment.

Note : each job in a workflow runs in a fresh virtual environment which will be managed by GitHub itself. Say we have a job for build an application another job for publishing it, all these jobs will run in parallel by default in different virtual env.

runs-on: ubuntu-latest

servers makes available for workflows by Github is available in ubuntu, windows and macOS. Say we have an application needs to be shipped into all three OS. We can test the releases or commits in all 3 OS.

![image](https://user-images.githubusercontent.com/106816732/213404942-22e4fd84-d42a-41f8-9d67-b6697c987453.png)

### Build docker image and push to private repo

Say we have a private repo in docker hub which already contains two images. **Now if we want to add one more image via git hub action, first include the job in yaml file.**

Here we have a choice of either running commands directly or using a predefined action. If we use run: then we should write all the commands to login, build and tag and push docker image. We can use multiline syntax in yaml which is pipe (\|)

Eg:

-   name: Build and push docker image

    run: \|

    docker login command

    docker build and tage command

    docker push command etc

Alternative way is to use an Action : <https://github.com/marketplace/actions/docker-build-push-action>

uses: mr-smithers-excellent/docker-build-push@v5.8

with:

image: docker-hub-repo/image-name

registry: docker.io

username: \${{ secrets.DOCKER_USERNAME }}

password: \${{ secrets.DOCKER_PASSWORD }}
