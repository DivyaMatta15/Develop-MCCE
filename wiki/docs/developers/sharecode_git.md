# Collaborate through GIT

## Git/github Cheat Sheet

!!! Tip
    If you need a quick reference of setting up and using git/github, find git cheat sheet [here](https://github.com/newbooks/Develop-MCCE/raw/master/doc/gitcards.pdf).

## Sample workflow

To collaborate with others on this project, please fork from the [GunnerLab Develop-MCCE repository](https://github.com/GunnerLab/Develop-MCCE). The detailed steps are illustrated in the following example:

### Create an issue on group repo
Tell others what you are working on by creating an issue.

To create an issue, go to [https://github.com/GunnerLab/Develop-MCCE](https://github.com/GunnerLab/Develop-MCCE), and create a new issue. After an issue is created, a number will be returned.

### Create a branch on local repo
Suppose I am going to write code to address the issue created by someone else or myself, and the issue number is #30. The issue title is "Develop script to install Mkdocs and recommended plugins"

Now I go to the forked repo directory on my local computer, make sure I have remote referenc set up correctly:
```bash
(base) jmao@vivo:~/projects/Develop-MCCE$ git remote -v
origin	https://github.com/newbooks/Develop-MCCE.git (fetch)
origin	https://github.com/newbooks/Develop-MCCE.git (push)
upstream	https://github.com/GunnerLab/Develop-MCCE.git (fetch)
upstream	https://github.com/GunnerLab/Develop-MCCE.git (push)
```

Before I create a branch, update the master from upstream so all existing code is up to date.
```bash
(base) jmao@vivo:~/projects/Develop-MCCE$ git checkout master
Already on 'master'
Your branch is ahead of 'origin/master' by 7 commits.
  (use "git push" to publish your local commits)
(base) jmao@vivo:~/projects/Develop-MCCE$ git pull upstream master
From https://github.com/GunnerLab/Develop-MCCE
 * branch            master     -> FETCH_HEAD
Already up to date.
``` 

It's time to create a new local branch that matches the issue number:
```bash
(base) jmao@vivo:~/projects/Develop-MCCE$ git checkout -b issue#30
```

### Develop code under branch
In this example, I create a file install_mkdocs.sh under bin.
``` bash
#!/bin/bash

pip install --upgrade pip
pip install bs4
pip install unicode
pip install mkdocs
pip install mkdocs-material
pip install pymdown-extensions
pip install markdown-blockdiag
pip install markdown-include
```

Go to wiki directory and run
```
mkdocs serve
```
Then point browser to URL http://localhost:8000 to monitor mkdocs page.

If everything goes well, the documentation site should be up. Any edits under wiki will be reflected by the above page.

When it is ready to deploy as a github page, run
```
mkdocs gh-deploy
```

This will create another branch, which is a special branch linked to Github page, and pushed to Github automatically. So in this example, I actually end up with two branches:

   1. issue#30
   2. gh-pages   (already pushed to Github by ```mkdocs gh-deploy```)
  
We only need to manually commit and push branch issue#30
```bash
git add bin/
git commit -a -m "Added script to install mkdocs. closes #30"
```
 

### Create pull request 
