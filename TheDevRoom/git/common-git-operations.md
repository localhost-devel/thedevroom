
## 1. Git Merge vs Git Rebase
- Git Merge
```bash
git clone https://github.com/localhost-devel/git-test-repository.git
cd git-test-repository/
ls
git checkout -b "test"
echo "Git merge" > file.txt
git add . && git commit -m "added new txt for git merge scenario"
git log --oneline
git checkout master
git log --oneline
git merge test --no-ff
git log --oneline
```
- Explain git merge use case here

- Git Rebase: 
```bash
  git clone https://github.com/localhost-devel/git-test-repository.git
  cd git-test-repository/
  ls
  git checkout -b "test"
  echo "Git Rebase" > file2.txt
  git add . && git commit -m "added new txt for git rebase scenario"
  git log --oneline
  git checkout master
  git log --oneline
  git rebase test
  git log --oneline
```
- Explain git rebase use case scenario here
- Prepare A table to explain git merge vs rebase


## 2. Git Fetch Vs Git Pull
```bash
mkdir git-fetch && cd git-fetch
git clone https://github.com/localhost-devel/git-test-repository.git
cd .. && ls
mkdir git-pull && cd git-pull
git clone https://github.com/localhost-devel/git-test-repository.git
cd .. && ls
cd git-fetch && ls && cd git-test-repository && ls
echo "fetch scenario" >> file.txt
git add . && git commit -m "Updated fetch scenario" && git push origin master
git log --oneline
cd ../.. && cd git-pull && d git-test-repository/ && ls
git fetch origin
git log master..origin/master
git pull origin master
ls && git log --oneline
```

## Git stash, List, Apply
```bash
mkdir git-stash && cd git-stash
git clone https://github.com/localhost-devel/git-test-repository.git && cd git-test-repository
echo "stash example" > stash.txt
git add . && git commit -m "stash example commit 1"
echo "stash example work in progress">> stash.txt
cat stash.txt
git status
git stash && git status && cat stash.txt
git stash list
git stash apply
cat stash.txt
```

## Git Branching Strategy
Explain scenario and example of branching stratergy here using main, feauture, hotfix include env dev-test-prod


## Git Revert vs Git Reset
git rebase
```bash
mkdir rev-res && cd rev-res
git clone https://github.com/localhost-devel/git-test-repository.git && cd git-test-repository
e cho "line1 - rev-res example" > rev-res.txt
git add . && git commit -m "rev-res example commit 1"
echo "line2 - rev-res example" >> rev-res.txt
git add . && git commit -m "rev-res example commit 2"
echo "line3 - rev-res example" >> rev-res.txt
git add . && git commit -m "rev-res example commit 3"
cat rev-res.txt
git log --oneline
git revert HEAD
cat rev-res.txt
git log --oneline

## Resetting the last commit
cat rev-res.txt
git log --oneline
git reset --soft HEAD~1
git status
git log --oneline
git reset --mixed HEAD~1
git status
git log --oneline
cat rev-res.txt
git reset --hard HEAD~1
git status
cat rev-res.txt
git log --oneline
```







