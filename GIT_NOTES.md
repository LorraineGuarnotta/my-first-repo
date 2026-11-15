# Git exercise – notes

 Setup & config
- Check the version: `git --version`
- Configure username and email:
```bash
git config --global user.name "Lorraine Guarnotta"
git config --global user.email "my-email@essec.edu"
```

 Create my first repository
- Create the folder: `mkdir my-first-repo`
- Go into it: `cd my-first-repo`
- Initialize Git: `git init`
- Create the file: `touch readme.txt`

 First commit
- Show the current state: `git status`
- Stage the file: `git add readme.txt`
- Commit: `git commit -m "Add readme file"`
- Show the history: `git log`

Make changes
- I edited the file with `nano readme.txt` and added a line.
-  readme.txt appears as "modified" in red: Git already tracks the file
  and noticed it changed since the last commit, but the change is not staged yet.
- Stage and commit:
```bash
git add readme.txt
git commit -m "Add project description to readme"
```
- I now have 2 commits (checked with `git log`).

 Exploration
- `git diff` shows the changes that are not staged yet: added lines in green with a `+`, the line in an neutral color is the line that was already on the document (that didn’t change). If I’d remove one line, the line will turn red.
  with a `-`. `a/` is the old version and `b/` is the new version.
- `git log --oneline` shows the history in a short format: one line per commit and there is no user nor date
  (no author, no date).

Branches
- List all branches: `git branch` (the `*` shows the current branch)
- Create a branch: `git branch feature-script`
- Switch to it: `git switch feature-script`
- Create and switch in one command: `git switch -c dev`
- Switch back: `git switch feature-script`
- Verify: `git branch` (or `git status`, which says "On branch feature-script")

Bash script on a branch
On the feature-script branch:
```bash
touch install.sh
nano install.sh
```
Content of `install.sh`:
```bash
#!/bin/bash
echo "Starting installation..."
brew update
brew install tree
echo "Installation complete!"
```
```bash
chmod +x install.sh
git add install.sh
git commit -m "Add install script"
git log --oneline
```

Merge branches
- Switch back to main: `git switch main`
- No. It was committed only on the feature-script branch; each branch has
  its own version of the files, so main doesn't have it before the merge.
- Merge: `git merge feature-script`
- After the merge, `install.sh` is present on main, and the commit "Add install script" is in main's history.
- Delete the branch: `git branch -d feature-script`

 Push to GitHub
- Link the local repo to GitHub: `git remote add origin https://github.com/LorraineGuarnotta/my-first-repo.git`
- Push: `git push -u origin main`
- On GitHub, I can see my files (readme.txt, install.sh) and my commits.
- Note: GitHub requires a personal access token instead of the password to push.

Delete and clone
```bash
cd ..
rm -rf my-first-repo
git clone https://github.com/LorraineGuarnotta/my-first-repo.git
cd my-first-repo
ls
```
All my files and commits came back from GitHub.

Full workflow practice
This repository (bash-installer) is the result:
```bash
cd bash-installer
git init
touch README.md
nano README.md
git add README.md
git commit -m "Add README explaining the project"
git switch -c feature-install
git add env_install.sh
git commit -m "Add environment install script"
git switch main
git merge feature-install
git branch -d feature-install
git remote add origin https://github.com/LorraineGuarnotta/Bash-installer.git
git push -u origin main
```
I also added a `.gitignore` to ignore the `.ipynb_checkpoints/` folder created by Jupyter.
And I did use AI to help me understand every command so for the bash exercise I can do it myself. AI help rewrite properly my answers for this document.

 Reflection questions

1. Why is version control useful?
It is really useful, because if you lose something important and want to get it back, version control lets you take back what you deleted or go back to a previous version.

2. What is the difference between staging and committing?
Staging is choosing what you put in your next save: you put the changes "in the suitcase" with `git add`. Committing is really saving them: it records a snapshot of the staged changes in the history, with a message. Uploading to GitHub is a separate step, done with `git push`.

3. When should you make a commit?
We need to make a commit after every small change that works, for example adding the first line or the second line of a file, so that each save corresponds to one clear modification.

4. What is the difference between git init and git clone?
`git init` initializes a new, empty repository in a folder. `git clone` makes a copy of an existing repository from GitHub, with all its files and its history.

5. Why should you write good commit messages?
Because it is important that when people see our project, they know exactly what we did and how we modified it. In one sentence, they can understand the change without even opening the file.

6. What is the purpose of using branches?
It is like having saves: you have the main save (main) and smaller saves (the other branches). If something is not done properly on a branch, it is still okay, because main is not affected. You can go back to main and only bring in your work when it is ready.

7. When would you create a new branch instead of working on main?
When you want to work on something new without touching main. If it works and it is important to have it in main, you merge it into main. It is better not to merge it right away, only once it is ready.
