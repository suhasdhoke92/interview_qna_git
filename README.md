# interview_qna_git 
# Git Interview Preparation Guide

1. ### What is the difference between `git clone` and `git fork`?  
   - **Git clone** creates a local copy of a remote repository on your machine, allowing you to work locally with the entire history.  
   - **Git fork** creates a personal copy of a repository on a hosting platform (e.g., GitHub). This enables making changes independently and submitting them back via pull requests without affecting the original repo directly.

2. ### What is the difference between `git fetch` and `git pull`?  
   - `git fetch` downloads new data from the remote repository but **does not** alter your working files or current branch.  
   - `git pull` is essentially a `git fetch` followed by an automatic `git merge`, which updates your current branch with the fetched changes.

3. ### How does `git merge` differ from `git rebase`?  
   - `git merge` combines the histories of two branches by creating a new merge commit, preserving the complete branch history.  
   - `git rebase` moves your commits on top of another base tip, creating a linear, cleaner history by rewriting commit hashes.

4. ### What Git branching strategy did you introduce in your previous organization?  
   - Introduced a **trunk-based branching** strategy with the following types of branches:  
     - `main`: The stable production branch  
     - `feature` branches: For developing new features  
     - `release` branches (tagged): For preparing production releases  
     - `hotfix` branches (tagged): For urgent fixes directly from released versions  
   - Conducted team training and presentations to ensure adoption.

5. ### What were the three main Git challenges faced?  
   1. **Branching Strategies:** Lack of a defined strategy led to chaotic merges; resolved by introducing trunk-based branching.  
   2. **Access Control:** Granular role definitions for read, write, branch creation, reviews, maintainers, and admins were missing; implemented via configurations and branch protections.  
   3. **Repository Configuration & Hooks:** Need to manage `.gitignore`, implement pre-commit and post-commit hooks to prevent unwanted file pushes, and troubleshoot push failures by checking `.gitconfig`.

6. ### How did you handle access control and role management recently?  
   - Applied fine-grained permissions using `CODEOWNERS.yaml` and branch protection rules.  
   - Roles included reviewers, maintainers, and admins with clearly defined responsibilities and access levels.

7. ### How do you handle merge conflicts in Git?  
   - Conflicts occur when two branches modify the same lines in a file.  
   - Steps:  
     - Notify and collaborate with developers who caused conflicts.  
     - Manually resolve conflicts by choosing all changes carefully.  
     - Test thoroughly before merging or creating pull requests.  
   - Git cannot auto-decide which change to keep, requiring manual resolutions.

8. ### Have you used Git tags? Why?  
   - Yes, to mark **specific points in history** as releases, helping QA and customers refer to stable versions.  
   - Examples:  
     - `v1.33` tagged for a release.  
     - Patches or hotfixes tagged as `v1.33.1` to represent incremental updates.

9. ### How do you combine multiple commits into a single commit?  
   - Using interactive rebasing:  
     ```bash
     git rebase -i HEAD~3
     ```
   - Change "pick" to "squash" on the commits you want to combine.
   - Edit the commit message to summarize changes.
   - Save and close the editor to complete the rebase.
     ```bash
     git log
     ```

11. ### What are your 10 commonly used Git commands?  
    `git clone`, `git status`, `git add`, `git commit -m`, `git push`, `git pull`, `git checkout`, `git branch -a`, `git fetch`, `git merge`, `git rebase`, `git log`.

12. ### How do you ignore certain files or folders in Git?  
    - Define file patterns or specific files in `.gitignore`. Common examples include environment or secret files such as `.env`.

13. ### What is the purpose of the `.git` folder?  
    - Contains the full repository metadata: commits, branches, tags, configuration, and remotes.  
    - It enables all Git operations; without it, the directory is not recognized as a Git repository.

14. ### Can you restore a deleted `.git` folder?  
    - Yes, if a backup or clone of the repository exists. Otherwise, the repo needs to be recloned, which may cause local un-pushed commits to be lost.

15. ### What should you do if a Kubernetes secret is accidentally committed?  
    - Immediately revoke and rotate the compromised secret.  
    - Remove it from Git history with tools like **BFG Repo Cleaner** or `git filter-branch`.  
    - Introduce pre-commit hooks and update `.gitignore` to prevent recurrence.  
    - Train the team on security best practices regarding secrets management.

16. ### Additional best practices for Git usage  
    - Regularly prune and delete stale branches to keep the repository clean.  
    - Use signed commits and tags for enhanced security where applicable.  
    - Encourage code reviews through branch protection rules and mandatory PR approvals.  
    - Automate checks via CI/CD pipelines integrated with Git hooks to maintain code quality.

