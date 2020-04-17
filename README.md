# Github Tutorial

*What are github and git?* 

Git is a tool used to manage the versions of files, mostly code files. It is also a useful tool for collaborating on shared files. Github is a git cloud provider. They offer to store your code, manage permissions and provide additional collaboration functionality like pull requests.

## Setting-up

You'll install git, create an account on Github and set-up security credentials.

### 1. Install Git on Your Computer

You'll follow a few steps to install git. [Full instructions can be found on the git website](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

**Instructions for Mac**

1. Run `git --version` on your terminal. It will install `git` if it isn't already installed.

**Instructions for PC**

1. [Download the Git Shell](https://gitforwindows.org/)
    - This installs the git command line tool as well as a desktop app.
    - The below tutorials will only cover command line tools but the app works well if you want simpler, less-featered git tool.
1. Test that this installed correctly by opening the git bash tool

**An Alternative Install (Mac or PC)**

If you'd like to avoid using the command line you can also use the [Github Git App](https://desktop.github.com/) which provides a UI to use git. I'm not going to cover how to use this tool in the tutorial.

### 2. Setup Git on Your Computer

We'll follow the git setup steps from github. We'll add a [name](https://help.github.com/en/github/using-git/setting-your-username-in-git) and [email](https://help.github.com/en/github/setting-up-and-managing-your-github-user-account/setting-your-commit-email-address#setting-your-commit-email-address-in-git) to git.

1. Open your terminal (Mac) or git shell (PC).
    - You can check that git installed correctly by running `git --version`  which should return a version number.
1. Now you'll add your name. This should be your real name since it will be attached to your code.
    - Run `git config --global user.name "<YOUR NAME>"`
    - For example: `git config --global user.name "Mary Scott"`
    - Quotes are necessary if you have a space in your name
    - Check that this worked by running `git config --global user.name`
1. Now you'll add your email. It is recommended that you use your Berkeley email since you'll be working on lab projects.
    - Run `git config --global user.email "<YOUR EMAIL>"`
    - For example: `git config --global user.email "mary.scott@berkeley.edu"`
    - Check that this worked by running `git config --global user.email`

### 3. Register for a Github Account

1. Start by creating a Github account. If you already have an acocunt try to sign in again.
    - You're viewing this page on Github and you should find a `Sign Up` button in the upper right.
    - You'll sign-up with the email you used in step 2 when setting-up Git on your local computer. It is recommended that you use your Berkeley email since you'll be working on lab projects.
1. You can now fiddle with a few settings if you'd like. Navigate to `Settings` using the dropdown in the upper right.
    - You can add an additional email address (under the `Emails` heading) if you'd like Github to send emails to another address.
    - You can change notification settings (under the `Notifications` heading) if you'd like to get fewer emails. The security alerts in particular can get a little annoying so you may want to uncheck that box.
1. Contact Mary with your github usename so you can be added to the [Scott Lab Organization](https://github.com/ScottLabUCB)

### 4. Set-up SSH Credentials

Whenever you connect to Github from your local computer you need to provide some form of authentication. You have two choices. One is to connect to Github using your Github account password. This can however become cumbersome since you'll have to frequently reenter your password. The second option is an SSH key which requires more setup but doesn't require you to reenter a password every time you interact with Github using git.

[You'll follow the steps from these docs](https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh).

1. First check if you already have an existing SSH key.
    - Open your terminal (Mac) or git shell (PC). 
    - Run `ls -al ~/.ssh` to list all the files in the `.ssh` folder.
    - If you see a `id_rsa.pub` then you can skip the generate SSH key step.
2. If you don't have a key yet then you'll need to create one.
    - You'll use your terminal (Mac) or git shell (PC) again.
    - Run `ssh-keygen -t rsa -b 4096 -C "<YOUR EMAIL>"`.
    - For example `ssh-keygen -t rsa -b 4096 -C "mary.scott@berkeley.edu"`.
    - You'll want to use the same email you used to sign-up for github.
    - Press enter 3 times to first confirm creation of the default file (`id_rsa.pub`), assign an empty passcode and confirm the empty passcode.
    - SSH keys can be optionally secured with a passcode but since this key will only exist on your laptop it should be secure enough without a passcode.
3. Now you'll copy the contents of `id_rsa.pub` to Github. This gives Github the public version of your SSH key so that you can safely connect to Github.
    - Open the `~/.ssh/id_rsa.pub` file in a text editor and copy the contents.
    - Go to Github and navigate to [`settings -> SSH and GPG keys`](https://github.com/settings/keys).
    - Click `New SSH Key` and paste in the file.
4. Test that the credentials are setup correctly.
    - You'll use your terminal (Mac) or git shell (PC) again.
    - Go to a directory where you plan to keep code in the terminal. For example run the command `cd ~/Documents` (`cd` stands for change directory and `~` is the home directory).
    - You'll now run a git command to copy code from Github. Run `git clone git@github.com:ScottLabUCB/GithubDemo.git`.
    - You should now see a directory called `GithubDemo` in your folder. For example you can see this by running `ls`.

## Tutorial: Using Git on the Command Line to Create a Commit

In this tutorial we'll learn about the git basics on the command line. Key ideas are commits and branches.

1. Open your terminal (Mac) or git shell (PC).
1. If you have already cloned the `GithubDemo` then `cd` to that directory. Otherwise you'll perform the clone now.
    - Go to a directory where you plan to keep code in the terminal. (Ex. `cd ~/Documents`, [more info on the terminal here](https://maker.pro/linux/tutorial/basic-linux-commands-for-beginners))
    - Run `git clone git@github.com:ScottLabUCB/GithubDemo.git`.
    - Run `cd GithubDemo`
    - View the files by running `ls`.
1. Now we'll run a few commands to inspect the repo.
    - `git log` will show you all the commits.
    - `git branch` will show you you're on the `master` branch.
1. Now let's add a file and create a commit.
    - `git status` will show you nothing is staged
    - Now create a new file in this directory.
    - `git status` will show you there is a new untracked file.
    - `git diff` will show you what has changed
    - `git add <filename>` or `git add .` to respectively stage this new file or all the files in the directory for your commit.
    - `git status` will show you that the file is staged.
    - `git commit -m "Created new file"` to create a new commit containing the staged files.
    - `git status` will show you that your code is committed.
    - `git log` will show you your new commit.
1. Now let's update the file and create a new commit.
    - Edit the file you created.
    - `git diff` to see the changes
    - `git status` to see that the changes need to be added.
    - `git commit -a -m "Updated file"` will add and commit the new code. The `-a` is a shorthand for `git add`.
    - `git log` to see you new commit exists.

## Tutorial: Collaborating on Code Using Github

1. Save your new code to Github!
    -  You should have a new file and 2 commits from the tutuorial above.
    - `git push` to send your commits to github.
    - [You will likely get a `non-fast-forward` error.](https://help.github.com/en/github/using-git/dealing-with-non-fast-forward-errors)
    - [Checkout Github's commits to see what it looks like.](https://github.com/ScottLabUCB/GithubDemo/commits/master)
1. You'll need to update your branch before pushing
    - `git pull --rebase` will take the commits on Github and put yours on top
    - Checkout out `git log` now.
    - Try `git push` again.
    - You may need to repeat these steps since other people are also committing changes right now.
1. So the above process was a pain, enter branches! Let's create a branch for your work.
    - `git branch` will show you you're in the `master` branch
    - `git pull` to update the `master` branch with the latest commits from Github.
    - `git checkout -b first_branch` to create and checkout a new branch called `first_branch`
    - `git branch` will show you you're in the `first_branch` branch
1. Now modify the file that you created in the first tutorial and create a commit. (`git commit -a -m "Modified file"`)
    - `git log` will show you your new commit
1. You'll send you new changes up to github and create a pull request.
    - `git branch` to double check that you are in the `first_branch` branch
    - `git push` to send your new commits to github
    - The first time you run this it will fail and tell you to run a command.
    - Run that command. Ex. `git push --set-upstream origin first_branch`. This associates your local branch with one on 
1. Modify the readme



1. Review a pull request


    - `git log --all --pretty=format:"%h %ad | %s%d [%an]" --graph --date=short` 

1. TODO push branches
1. TODO create pull requests
1. TODO review pull requests
1. TODO merge pull requests
    
    - 

Github Tutorial
- Git clone repo
- Git log
- new file
- Git status
- Git add
- Git status
- Git commit
- Git status
- Git log, new she
- Github page
      - Look at commits, no change
- Git push
      - Uh oh, out of date
- Random
      - Aliases
      - Github security alerts

TODO

## Other Resources

**Git Commands Reference**

[Check out the documentation!](https://git-scm.com/docs) Remember you can always add `-h` to a command to see the help.

[Also if you're getting tired of typing long commands you can create aliases.](https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases)

- `git clone` to pull the repo from Github
- `git log` to view commits in your current branch
- `git branch` to view your active branch and other branches
- `git checkout -b <branch>` to create a new branch
- `git checkout <branch>` to checkout an existing branch
- `git diff` to see what changes you've made to your files
- `git status` to view file status
- `git add <file>` to stage the file or `git add .` to add all the files in the current directory
- `git commit -m <message>` to create a commit
- `git push` to push your changes to 
- `git pull` to pull changes from Github
- `git pull --rebase` will put your recent changes in front of the new changes from Github

**What to do if everything is messed up**

- `git fetch origin`
- `git reset --hard origin/master`

- `git commit -a -m "temp"`
- `git checkout -b backup`

- `git reset HEAD~1`

- `git reset <SHA>`

**Setting Up Repos on Github**

- [Check out gitignore files which helps git ignore files.](https://help.github.com/en/github/using-git/ignoring-files)
    - [Standard gitignore files can be found in Github!](https://github.com/github/gitignore)
- [Github will render all files in markdown.](https://guides.github.com/features/mastering-markdown/)

**How to administer organizations**
- Example organization https://github.com/orgs/sfbrigade
- Users are put in teams and teams are assigned permissions to repos. This ensures you have consistent permissions for the whole organization.
    - [Documentation on adding a user to a team](https://help.github.com/en/github/setting-up-and-managing-organizations-and-teams/adding-organization-members-to-a-team)
    - [Documentation on creating teams](https://help.github.com/en/github/setting-up-and-managing-organizations-and-teams/creating-a-team)
    - [Documentation on team permissions](https://help.github.com/en/github/setting-up-and-managing-organizations-and-teams/managing-team-access-to-an-organization-repository)
- External collaborators can be given access to specific repos.
