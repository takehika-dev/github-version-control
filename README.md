# Basics of Version Control with GitHub
A simple guide for GitHub version control. Learn how to create, merge, and delete branches.


## What is "Git Flow"?
Git Flow is a branching strategy that helps developers manage features, releases, and fixes efficiently. It organizes the development process using different branches:

- **`main`** → Stable branch containing production-ready code.
- **`develop`** → Active development branch where new features are merged.
- **`feature/*`** → Temporary branches for developing new features.
- **`release/*`** → Prepares a version for release, ensuring stability.
- **`hotfix/*`** → Emergency fixes applied directly to `main`.

Using this structured approach makes collaboration easier and keeps your codebase clean.


## How to start for beginners
1. Setup the Repository
Before we start coding, we need to initialize a Git repository and connect it to GitHub.
```
git init  # Initialize a new Git repository
git remote add origin https://github.com/<your-username>/<your-repo-name>.git  # Connect local repo to GitHub
```

<br>

2. Create `main` and `develop` Branches
To maintain a clean workflow, we separate stable and development code.
```
git checkout -b main  # Create and switch to the main branch
git commit --allow-empty -m "Initial commit on main"  # Create an empty commit for the main branch
git push -u origin main  # Push the main branch to GitHub

git checkout -b develop  # Create and switch to the develop branch
git commit --allow-empty -m "Initialize develop branch"  # Create an empty commit for the develop branch
git push -u origin develop  # Push the develop branch to GitHub
```
⚠️ `main` contains stable, production-ready code. `develop` is where new features and changes are tested before being released.

<br>

3. Work on a New `feature`
Every new functionality is developed in its own `feature` branch.
```
git checkout -b feature/new-feature develop  # Create and switch to a feature branch from develop
# Make changes to files, then stage and commit
git add .  # Stage all modified files
git commit -m "Implement new feature"  # Commit with a meaningful message
git push -u origin feature/new-feature  # Push the feature branch to GitHub
```
⚠️ Keeping each `feature` in its own branch prevents conflicts with other changes.

<br>

4. Merge the `feature` into `develop`
Once the `feature` is complete, it needs to be merged into `develop`.
```
git checkout develop  # Switch to the develop branch
git merge feature/new-feature  # Merge the completed feature into develop
git push origin develop  # Push the updated develop branch to GitHub
git branch -d feature/new-feature  # Delete the local feature branch
git push origin --delete feature/new-feature  # Delete the remote feature branch
```
⚠️ This keeps develop updated with the latest features.

<br>

5. Prepare for a `release`
Once the project is stable, we create a `release` branch to finalize the update.
```
git checkout -b release/1.0.0 develop  # Create a release branch from develop
# Finalize the release (fix minor issues, update documentation, etc.)
git add .  # Stage all changes
git commit -m "Final tweaks for release v1.0.0"  # Commit final updates
git push -u origin release/1.0.0  # Push the release branch to GitHub
```
⚠️ `release` locks the version so no new features are added. This branch is used for testing and last-minute fixes before deployment.

<br>

6. Merge `release` into `main` and `develop`
Once everything is ready, `release` is merged into `main` and `develop`.
```
git checkout main  # Switch to main
git merge release/1.0.0  # Merge the release into main
git push origin main  # Push the updated main branch
git checkout develop  # Switch back to develop
git merge release/1.0.0  # Merge the release back into develop
git push origin develop  # Push the updated develop branch
git branch -d release/1.0.0  # Delete the local release branch
git push origin --delete release/1.0.0  # Delete the remote release branch
```
⚠️ `main` is now updated with the stable release. Merging back into `develop` ensures all bug fixes stay in future versions.

<br>

7. Apply a `hotfix` (Urgent Bug Fix in Main)
If a critical issue is found in production, we need to fix it immediately.
```
git checkout -b hotfix/urgent-bug-fix main  # Create a hotfix branch from main
# Apply the fix, then commit and push
git add .  # Stage changes
git commit -m "Fix urgent bug in production"  # Commit the fix
git push -u origin hotfix/urgent-bug-fix  # Push the hotfix branch to GitHub
```
⚠️ `hotfix` skip `develop` and are applied directly to `main` to fix the issue quickly.

<br>

8. Merge Hotfix into `main` and `develop`
Once the fix is verified, it should be merged into both `main` and `develop`.
```
git checkout main  # Switch to main
git merge hotfix/urgent-bug-fix  # Merge the hotfix into main
git push origin main  # Push the updated main branch
git checkout develop  # Switch to develop
git merge hotfix/urgent-bug-fix  # Merge the hotfix into develop
git push origin develop  # Push the updated develop branch
git branch -d hotfix/urgent-bug-fix  # Delete the local hotfix branch
git push origin --delete hotfix/urgent-bug-fix  # Delete the remote hotfix branch
```
⚠️ `main` gets fixed immediately to prevent further issues. `hotfix` is also merged into `develop` to prevent regression in future updates.


## License
You are free to use this code for personal and educational purposes. Commercial use and redistribution are not allowed.
