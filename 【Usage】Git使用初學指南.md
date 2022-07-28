#Git使用初學指南
## Contents


## Git & GitHubs
### Git vs. GitHub
* Git is a version control system.
* GitHub is a cloud space where you could put everything on it.
### How to start using Git
* Download Git (for Windows) installation packages on the official website: (git-Downloads)[https://git-scm.com/downloads].
* Install Git.
* Create a folder where your codes are in it.
* Right click and click "Git Bash Here":
()[]
* Enter the followings in the git bash:
  ```
  git init                    (Initialize a git repository in your local machine.)
  git status                  (Check all files in the folder and the repository.)
  git add XXX.txt / git add . (Add a text file / all files  into the repository.)
  git commit -m "v1"          (Save this version without start the text editor.)
  ```

### How to connect Git & GitHub
* Check your user name and email on the GitHub. 
* Set your name and email in the git bash:
  ```
  git config -- global user.name "John" ("John" is the user name on your github account.)
  git config -- global user.email "john@google.com" ("john@google.com" is the email on your github account.)
  ```
* Eneter the following in the git bash:
  ```
  git remote add origin https://github.com/yourname/repository_name
  git branch -m master main   (Change branch name: The oldBranch name is master, and the new branch nameis main.)
  git commit -m "v2"          (Save your current version first.)
  git push -u origin main     (The default branch name on GitHub now is main.)
  ```
* Then you will see all files in the repository on the github.
 
##














