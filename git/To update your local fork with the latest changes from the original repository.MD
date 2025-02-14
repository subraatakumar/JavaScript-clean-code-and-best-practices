# Updating Your Forked Repository

If you've forked a repository and cloned it to your local machine, you might need to update it when the original repository (upstream) changes. Follow these steps to sync your fork with the latest updates.

## 🚀 Steps to Update Your Fork

### 1️⃣ Add the Original Repository as an Upstream Remote
Check if the original repository (upstream) is already added:

```sh
git remote -v
```

If `upstream` is not listed, add it using:

```sh
git remote add upstream <original-repo-url>
```

Example:

```sh
git remote add upstream https://github.com/original-owner/repo.git
```

### 2️⃣ Fetch the Latest Changes from Upstream

Get the latest updates from the original repository:

```sh
git fetch upstream
```

### 3️⃣ Merge or Rebase the Changes into Your Branch

If you are on your main branch (`main` or `master`), merge the updates:

```sh
git checkout main  # Switch to main branch
git merge upstream/main  # Merge changes
```

Or, if you prefer rebasing to keep a cleaner history:

```sh
git rebase upstream/main
```

### 4️⃣ Push the Updated Code to Your Fork

Once merged or rebased, push the changes to your GitHub fork:

```sh
git push origin main
```

🎉 **Your fork is now up-to-date with the original repository!**
