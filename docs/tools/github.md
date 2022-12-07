## Introduction to GitHub

```
cd /path/to/your/project

# initialize the repository
git init

# add files to be tracked
git add main.py input.txt 

# commit the files to the repository, creating the first snapshot
git commit -m "Initial Commit"

git config --global user.name "Your Name"
git config --global user.email "your.email@yale.edu"

git remote add origin git@github.com:user_name/my_new_repo.git
git push -u origin master
```
