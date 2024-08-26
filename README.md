# GIT

## merge conflict


**Git Merge Conflict Example**  

This example walks you through the steps to create and resolve a merge conflict in Git using a file named `abc.txt`. Two users will be working on different branches to simulate the conflict.

-  **Prerequisites**  

  - Git installed on your local machine.

  - A GitHub account (or any other Git hosting service).

  - Basic understanding of Git and terminal commands.

###   Step 1: Clone the Repository  

First, clone the repository where you want to simulate the conflict.

```bash
git clone <repository-url>
cd <repository-directory>
```

###   Step 2: Create and Switch to a New Branch  

  User 1:   Create and switch to a new branch named `user1-branch`.

```bash
git checkout -b user1-branch
```

  User 2:   Create and switch to a new branch named `user2-branch`.

```bash
git checkout -b user2-branch
```

###   Step 3: Make Changes to `abc.txt`  

  User 1:  

1. Open `abc.txt` and make some changes.
2. Save the changes.
3. Stage and commit the changes.

```bash
echo "User 1's changes" >> abc.txt
git add abc.txt
git commit -m "User 1's changes to abc.txt"
```

  User 2:  

1. Open `abc.txt` and make different changes.
2. Save the changes.
3. Stage and commit the changes.

```bash
echo "User 2's changes" >> abc.txt
git add abc.txt
git commit -m "User 2's changes to abc.txt"
```

###   Step 4: Merge the Changes and Create a Conflict  

  User 1:   Merge the changes from `user1-branch` into the main branch.

```bash
git checkout main
git merge user1-branch
```

  User 2:   Try to merge the changes from `user2-branch` into the main branch.

```bash
git checkout main
git merge user2-branch
```

At this point, you will encounter a merge conflict because `abc.txt` has conflicting changes from `user1-branch` and `user2-branch`.


###   Step 5: Resolve the Merge Conflict  

When you attempt to merge the changes from `user2-branch` into `main`, Git will detect a conflict in `abc.txt`. This conflict occurs because the same lines in the file were modified differently in the two branches. Git cannot automatically determine which changes to keep, so you need to resolve the conflict manually.

  1. Open `abc.txt` to View the Conflict

Open the `abc.txt` file in a text editor. You will see conflict markers indicating the conflicting changes from the two branches:

```diff
<<<<<<< HEAD
User 1's changes
=======
User 2's changes
>>>>>>> user2-branch
```

- `<<<<<<< HEAD`: This marks the beginning of the changes from the current branch (`main`).
- `=======`: This separator divides the changes from the two branches.
- `>>>>>>> user2-branch`: This marks the beginning of the changes from the branch being merged (`user2-branch`).

  2. Choose How to Resolve the Conflict

You have several options to resolve the conflict:

  - Option 1: Accept Current Changes

If you want to keep the changes from the current branch (`main`) and discard the changes from the incoming branch (`user2-branch`), you can remove the conflict markers and the incoming changes.

Example:

```bash
User 1's changes
```

  - Option 2: Accept Incoming Changes

If you prefer to keep the changes from the incoming branch (`user2-branch`) and discard the changes from the current branch (`main`), remove the conflict markers and the current changes.

Example:

```bash
User 2's changes
```

  - Option 3: Accept Both Changes

If both changes are valuable and you want to keep them, you can manually edit the file to include both sets of changes. Remove the conflict markers and combine the changes in a way that makes sense.

Example:

```bash
User 1's changes
User 2's changes
```

  - Option 4: Manual Edit

Sometimes, neither of the automatic options (current, incoming, or both) are ideal. In such cases, you can manually edit the file to create a custom resolution. Carefully combine or modify the conflicting lines to produce the desired outcome.

  3. Save the Resolved File

After making the necessary edits to resolve the conflict, save the file.

  4. Stage the Resolved File

Once the conflict is resolved, you need to stage the resolved file to mark it as resolved:

```bash
git add abc.txt
```

  5. Complete the Merge

Finally, complete the merge by committing the resolved changes:

```bash
git commit -m "Resolved merge conflict in abc.txt"
```

This commit finalizes the merge and integrates the resolved changes into the `main` branch.

###   Step 6:  Push the Changes  

After resolving the conflict and committing the changes, push the updated branch to the remote repository:

```bash
git push origin main
```

You have successfully created and resolved a merge conflict in Git using `abc.txt`. This process is common when multiple people collaborate on the same project, and understanding how to resolve conflicts is an essential skill in software development.


## .gitignore
---------------------

- When sharing your code with others, there are often files or parts of your project, you do not want to share.

- Git can specify which files or parts of your project should be ignored by Git using a .gitignore file.


### Step 1: Create a `.gitignore` File

1. **Navigate to your project directory**:

   Open your terminal and navigate to the root directory of your project where you want to create the `.gitignore` file.

   ```bash
   cd /path/to/your/project
   ```

2. **Create a `.gitignore` file**:

   Use a text editor or the command line to create a `.gitignore` file in the root of your project.

   ```bash
   touch .gitignore
   ```

### Step 2: Define Patterns in `.gitignore`

1. **Open the `.gitignore` file**:

   Use any text editor to open the `.gitignore` file.

   ```bash
   nano .gitignore
   ```

2. **Add patterns to ignore**:

   Add the files or directories you want to exclude from your Git repository. For example:

   ```bash
   # Ignore node_modules directory
   node_modules/

   # Ignore environment variables file
   .env

   # Ignore compiled files
   *.o
   *.pyc

   # Ignore log files
   logs/
   *.log

   # Ignore IDE or editor files
   .vscode/
   *.swp
   ```

3. **Save and close the file**:

   Save the changes and close the text editor(Ctrl+X).

### Step 3: Verify `.gitignore` is Working

1. **Check ignored files**:

   Use the `git status` command to verify that the files or directories you specified are not tracked by Git.

   ```bash
   git status
   ```

   The files listed in `.gitignore` should not appear in the untracked files section.

### Step 4: Add and Commit Changes

1. **Stage the `.gitignore` file**:

   Add the `.gitignore` file to your Git staging area.

   ```bash
   git add .gitignore
   ```

2. **Commit the changes**:

   Commit the `.gitignore` file to your repository.

   ```bash
   git commit -m "Add .gitignore file"
   ```

3.**Push the changes**:

   ```bash
   git push
   ```

### Step 5: Resolve Issues with `.gitignore`

1. **If files are already tracked**:

   If you have files that are already tracked by Git and you want to ignore them, you need to untrack them first.

   ```bash
   git rm -r --cached <file_or_directory>
   ```

   For example, to untrack the `node_modules` directory:

   ```bash
   git rm -r --cached node_modules
   ```

2. **Commit the changes**:

   After untracking the files, commit the changes.

   ```bash
   git commit -m "Remove node_modules from tracking"
   ```

3.**Push the changes**:

   ```bash
   git push
   ```

### Example Patterns

- **node_modules/**: Ignores the `node_modules` directory.
- **.env**: Ignores environment variables files.
- **logs/** and **.log**: Ignores logs directories and files.
- **.vscode/**: Ignores Visual Studio Code configuration files.


## rebase
---------------------

This demonstrates how to perform and resolve a `git rebase`. `git rebase` is a powerful tool that allows you to integrate changes from one branch into another, creating a cleaner project history.

**Prerequisites**

Ensure you have the following installed:

- Git (version 2.0 or above)
- A GitHub account (optional for pushing to a remote repository)



### Step 1: Clone the Repository

First, clone the repository to your local machine:

```bash
git clone https://github.com/your-username/git-rebase-example.git
cd git-rebase-example
```

### Step 2: Create a New Branch

Create a new branch from the `main` branch to work on:

```bash
git checkout -b feature-branch
```

### Step 3: Make Changes in the Feature Branch

Edit some files or add new commits:

```bash
echo "Feature A" >> feature.txt
git add feature.txt
git commit -m "Add Feature A"
```

### Step 4: Push the Feature Branch

Push the feature branch to the remote repository:

```bash
git push origin feature-branch
```

### Step 5: Switch Back to the Main Branch

Switch back to the `main` branch:

```bash
git checkout main
```

### Step 6: Make Changes in the Main Branch

Simulate changes in the `main` branch:

```bash
echo "Hotfix" >> hotfix.txt
git add hotfix.txt
git commit -m "Apply hotfix"
```

### Step 7: Push the Main Branch

Push the changes in the `main` branch to the remote repository:

```bash
git push origin main
```

### Step 8: Rebase the Feature Branch onto Main

Rebase your `feature-branch` onto `main`:

```bash
git checkout feature-branch
git rebase main
```

### Step 9: Resolve Conflicts (If Any)

If there are conflicts, Git will pause the rebase process. You can resolve them as follows:

1. **Identify Conflicts**: Git will mark conflicts in the affected files.
2. **Edit Files**: Manually resolve conflicts by editing the files.
3. **Mark as Resolved**: Once conflicts are resolved, mark them as resolved:

    ```bash
    git add <resolved_file>
    ```

4. **Continue the Rebase**: After resolving all conflicts, continue the rebase:

    ```bash
    git rebase --continue
    ```

### Step 10: Force Push the Rebased Branch

After a successful rebase, you need to force push the `feature-branch` to the remote repository to update it with the rebased commits:

```bash
git push --force-with-lease origin feature-branch
```

### Step 11: Verify the History

After a successful rebase and push, verify the history to ensure that the commits have been properly applied:

```bash
git log --oneline --graph --all
```

This command should display a linear commit history, reflecting the rebased changes.

### Step 12: Merge the Rebased Branch

Finally, merge the `feature-branch` into the `main` branch:

```bash
git checkout main
git merge feature-branch
```

This will result in a fast-forward merge, preserving the clean history.

### Step 13: Push the Merged Changes

Push the merged changes to the remote repository:

```bash
git push origin main
```

### Step 14: Delete the Feature Branch

After merging, you can delete the feature branch both locally and remotely:

```bash
git branch -d feature-branch
git push origin --delete feature-branch
```


## Cherry Picking in Git

Cherry picking in Git allows you to apply the changes from a specific commit in one branch to another branch. This is useful when you need to integrate specific changes without merging entire branches.


**Prerequisites**

- Basic knowledge of Git and version control.

- Git installed on your system.

- Access to a repository with multiple branches.

### Step 1: Clone the Repository

First, clone the repository that you want to work on.

```bash
git clone <repository-url>
cd <repository-directory>
```

### Step 2: Create a New Branch

Let's create a new branch where we will make some changes.

```bash
git checkout -b feature-branch
```

### Step 3: Make Some Commits

Create a new file and commit it. For example:

```bash
echo "Hello, World!" > hello.txt
git add hello.txt
git commit -m "Add hello.txt with initial content"
```

Make another commit:

```bash
echo "This is a feature" > feature.txt
git add feature.txt
git commit -m "Add feature.txt with feature content"
```

### Step 4: Push the Feature Branch

Push the new branch with the commits to the remote repository:

```bash
git push origin feature-branch
```

### Step 5: Switch to Another Branch

Now, switch to another branch (e.g., `main` or `develop`).

```bash
git checkout main
```

### Step 6: Cherry-Pick a Commit

Suppose you want to apply the commit that added `feature.txt` to the `main` branch. You can cherry-pick this commit by using its commit hash.

First, find the commit hash:

```bash
git log --oneline feature-branch
```

Then cherry-pick the commit:

```bash
git cherry-pick <commit-hash>
```

### Step 7: Resolve Conflicts (if any)

If there are conflicts when applying the cherry-pick, Git will pause and allow you to resolve them.

1. Git will indicate the files that are in conflict. Open those files in a text editor.

2. Look for conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`) and resolve the conflicts by editing the file.

3. After resolving the conflicts, add the resolved files:

    ```bash
    git add <resolved-file>
    ```

4. Continue the cherry-pick process:

    ```bash
    git cherry-pick --continue
    ```

### Step 8: Verify the Changes

After successfully cherry-picking the commit, you can verify the changes by viewing the file or using `git log`:

```bash
cat feature.txt
git log --oneline
```

### Step 9: Push the Changes

Finally, push the changes to the remote repository:

```bash
git push origin main
```


## Staging in git
----------------------------

The Git staging area (or index) allows you to prepare changes before committing them.

**Prerequisites**

- Basic knowledge of Git and version control.

- Git installed on your system.

- Access to a Git repository.

### Example Scenario

Suppose you have a repository with the following setup:

- `main` branch: The primary branch where changes are finalized.
- `feature-branch`: A branch where you are making updates or new features.

You want to stage changes on `feature-branch`, review them, and then commit those changes to `main`.

### Step 1: Clone the Repository

If you haven't already cloned the repository, do so:

```bash
git clone https://github.com/username/repository-name.git
cd repository-name
```

### Step 2: Create a New Branch

Create and switch to a new branch for your changes:

```bash
git checkout -b feature-branch
```

### Step 3: Make Changes

Edit the files in your project as needed. For instance, you might update existing files or add new ones.

### Step 4: Stage Changes

Add specific changes to the staging area using `git add`:

- To stage a specific file:

  ```bash
  git add path/to/your/file
  ```

- To stage all changes:

  ```bash
  git add .
  ```

### Step 5: Check Staged Changes

Review the changes you have staged:

```bash
git status
```

This command will display which files are staged and ready to be committed.

### Step 6: Commit Changes

Once you are satisfied with the staged changes, commit them with a descriptive message:

```bash
git commit -m "Your descriptive commit message"
```

### Step 7: Push Changes

Push your changes to the remote repository:

```bash
git push origin feature-branch
```

### Step 8: Resolve Staging Issues

If you face issues while staging changes, here’s how to resolve them:

1. **Untracked Files**

   To add untracked files, use:

   ```bash
   git add path/to/file
   ```

2. **Forgotten Files**

   If you forgot to stage a file, add it with:

   ```bash
   git add path/to/file
   ```

   Then commit again if needed.

3. **Undo Staged Changes**

   To unstage a file, use:

   ```bash
   git reset HEAD path/to/file
   ```

4. **Review Changes Before Staging**

   To review changes before staging, use:

   ```bash
   git diff
   ```

5. **Check for Conflicts**

   If you encounter merge conflicts, resolve them manually:

   - Check the status:

     ```bash
     git status
     ```

   - Open the files with conflicts, resolve the issues, and mark them as resolved:

     ```bash
     git add path/to/resolved-file
     ```

### Step 9: Merge Changes

To merge changes from another branch into your current branch:

```bash
git merge branch-name
```

### Step 10: Clean Up

After merging and pushing changes, you might want to delete the feature branch:

```bash
git checkout main
```

```bash
git pull
```

```bash
git branch -d feature-branch
```

## temp branches
----------------------

### Step 1: Initialize a Git Repository

If you haven’t already, initialize a Git repository in your project directory.

```bash
git init
```

### Step 2: Create and Commit the Initial File

Create a file named `abc.txt` and commit it to the `main` branch.

```bash
echo "Initial content" > abc.txt
git add abc.txt
git commit -m "Add initial abc.txt"
```

### Step 3: Create a Temporary Branch

Create a new branch for temporary changes. For example, `temp-branch`.

```bash
git checkout -b temp-branch
```

### Step 4: Make Changes in the Temporary Branch

Modify `abc.txt` in the temporary branch.

```bash
echo "Temporary changes" >> abc.txt
git add abc.txt
git commit -m "Add temporary changes to abc.txt"
```

### Step 5: Merge Changes to Main Branch

Switch back to the `main` branch and merge the temporary branch.

```bash
git checkout main
git merge temp-branch
```

### Step 6: Resolve Conflicts (if any)

If there are conflicts during the merge, Git will prompt you to resolve them. Open the conflicting files, edit them to resolve conflicts, thenadd and commit the resolved changes.

```bash
# Edit conflicted files
git add abc.txt
git commit -m "Resolve merge conflicts in abc.txt"
```

### Step 7: Delete the Temporary Branch

After the changes are merged and conflicts are resolved, you can delete the temporary branch.

```bash
git branch -d temp-branch
```

## when to create branches - feature level  


### Step 1: Create a Feature Branch

- Update your local `main` branch: 

```bash
git checkout main
git pull origin main
```

- Create a new feature branch:

```bash
  git checkout -b feature/<feature-name>
```

### Step 2: Work on Your Feature

- Make changes and commit them:

  ```bash
  git add <files>
  git commit -m "Implement feature: <brief description>"
  ```

### Step 3: Resolve Conflicts and Push Changes

   - Update your feature branch with the latest `main`:

```bash
git checkout main
git pull origin main
git checkout feature/<feature-name>
git merge main
```

- Resolve any conflicts if necessary.

- Push the feature branch:

```bash
git push origin feature/<feature-name>
```

### Step 4: Create and Merge Pull Request

- Create a pull request on your Git hosting service.

- Review and merge the pull request into `main`.

- Delete the feature branch:

```bash
git branch -d feature/<feature-name>
git push origin --delete feature/<feature-name>
```

### Step 5: Update Local Repository

- Update your `main` branch:

```bash
git checkout main
git pull origin main
```

This workflow helps manage feature development efficiently and ensures that the main branch remains stable.