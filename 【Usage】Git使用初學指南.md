# Git使用初學指南
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
![git-bash](https://github.com/roy-tsai-tw/Reconfigurable-Architecture/blob/main/images/git_bash.png)
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
* Reference:
  *  [新手也能懂的Git教學](https://medium.com/@flyotlin/%E6%96%B0%E6%89%8B%E4%B9%9F%E8%83%BD%E6%87%82%E7%9A%84git%E6%95%99%E5%AD%B8-c5dc0639dd9)
  *  [1.6 開始 - 初次設定 Git](https://git-scm.com/book/zh-tw/v2/%E9%96%8B%E5%A7%8B-%E5%88%9D%E6%AC%A1%E8%A8%AD%E5%AE%9A-Git)
  *  [2.5 Git 基礎 - 與遠端協同工作](https://git-scm.com/book/zh-tw/v2/Git-%E5%9F%BA%E7%A4%8E-%E8%88%87%E9%81%A0%E7%AB%AF%E5%8D%94%E5%90%8C%E5%B7%A5%E4%BD%9C)
  *  [Git 常见错误 之 error: src refspec xxx does not match any / error: failed to push some refs to 简单解决方法](https://blog.csdn.net/u014361280/article/details/109703556)
  *  [github上传时出现error: src refspec master does not match any解决办法继续海阔天空](https://www.jianshu.com/p/8d26730386f3)
  *  [Git & GitHub (1) 最初階的基本操作](https://ithelp.ithome.com.tw/articles/10285329)
  *  [Git 與 Github 版本控制基本指令與操作入門教學](https://blog.techbridge.cc/2018/01/17/learning-programming-and-coding-with-python-git-and-github-tutorial/)
  *  



##














