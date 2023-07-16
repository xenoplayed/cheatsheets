# GIT

## Basics

```bash
# create a new repository on the command line
echo "# my-project" >> README.md
git init
git add README.md
git commit -m "initial commit"
git remote add origin https://github.com/username/my-project.git
git push -u origin main

# push an existing repository from the command line
git remote add origin https://github.com/username/my-project.git
git push -u origin main
```

## Advanced

```bash
git branch -d branchname                            # delete fully merged branch
git commit --allow-empty # allow empty commit
git reset --soft # keep your files, and stage all changes back automatically
git reset --hard # completely destroy any changes and remove them from the local directory.
git reset --mixed # (default) keeps all files the same but unstages the changes. 
```

## git config

```bash
    git config --global --add color.ui true # enable colored output
```
