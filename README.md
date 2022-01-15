# Git
My Git Journey

## Basics

### To check if git is already installed
    - git version

### Initial configurations

    - git config --global user.name "yourusername"
    - git config --global email "youremailaddress"
    
    - git config --global list
    
    
    - git config --global core.editor "vim/subl -w"
    - git config --global e



2021 update:

- How to configure your favorite editor with the Git? 
https://git-scm.com/book/en/v2/Appendix-C%3A-Git-Commands-Setup-and-Config

* commit
    * `git commit -a -m <msg>`
       Add all files and commit. 

- Branching in Git:
    - `git branch` 
        Shows you a list of branches. 
    -  `git branch <branch-name>`
        Create a new branch with that name but you won't to switched/checkedout to that branch.
    -  `git switch <branch-name>`
        Takes you to that branch. Similar to checkout.        
    -  `git switch -c <branch-name>`
       Create a new branch with that name and switches/checks you out to that branch.
    - `git branch -d <branch-name>`
        To delete a branch. 
    - `git branch -D <branch-name>`
        To forcefully delete a branch.
    - `git branch -m <new-name>`
       To rename the branch you are in. 

- Diff in git
    - `git diff`
       Diff between the working directory and staging area.
    - `git diff HEAD`
       Difference between working directory and the last commit.
    - `git diff --staged` / `git diff --cached`
      Difference between staged area and last commit. 
    - `git diff <filename>`
      Targeting specific file change.
    - `git diff branch1..branch2` / `git diff branch1 branch2`
       Compare changes between two branches.
    - `git diff commit1..commit2`
       Compare changes between commmits.
    - `git diff HEAD HEAD~1` / `git diff HEAD~1`
       Compare current HEAD and previous HEAD. or Current commit and the previous commit. 

- Stash
    - `git stash apply`
     If you want to apply stashed changes in multiple branches.
    - `git stash drop stash{2}`
     If you want to delete a stash, from stash list.
    - `git stash clear`
    To clear out the stash list, removes all stashes.

 - Time travel
    - What is detached head? 
      When you checkout a commit `git checkout <commit-hash>`,  `HEAD`  pointer will no longer point to a branch instead it points to a commit hash, this is called detached head.
    - `git checkout HEAD~1` 
       Accessing parent and grandparent commits, parent (1 commit previous) grandparent(2 commits back). Basically you want to go back one commit or two commit without knowing the commit hash. 
    - `git checkout -`
        Switch to previous branch you accessed. 
    - `git checkout HEAD filename` / `git checkout -- filename` / `git checkout filename` or `git restore filename`
        To discard the changed made in working directory so that it is now as our HEAD or last commit.

 - Restore
    - `git restore filename` 
       Same as `git checkout filename`. But you can do more with git restore.
    - `git restore --source HEAD~2 filename`
       File goes back to content of `HEAD~2`.
   - `git restore --staged filename`
      To unstage the staged file.

- Reset
    - `git reset <commit hash>`
        Say you want to remove couple of commits and go back in time. I.E. If you have 5 commits and decide that you don't need last two commits, you can do `git reset 3rdCommitHash` this will bring back those two commit changes to your working directory, so that you can take that changes elsewhere. 
    - `git reset --hard <commit hash>`
       If you don't want those changes in your working directory also.

- Revert
   - `git revert <commit hash>`
      Same as `git reset` but it doesn't alter the history instead it create a new commit that undoes the changes you don't need. 
        Ex: Assume you have 4(A -> B -> C -> D) commit and you decide you don't need the last commit(D), `git reset D` will make the history look like this: 
        A -> B -> C
        (altering the history) Which can cause some serious problem if other collaborators already have that commit.
        Instead we should `git revert D`:
        A -> B -> c -> D -> D'
        This create a new commit (D') which undoes the changes of D. 
        ( Useful link: https://stackoverflow.com/questions/1463340/how-to-revert-multiple-git-commits)    

- Remote
    - What's remote? 
        - Remote is nothing but to say which github/gitLab/bitbucket link in the remote it is connected to.
            - `git remote -v` (lists the remotes its connected to.) 

- Push
    ![Screenshot_20220108-152808](https://user-images.githubusercontent.com/12951785/149617844-d851e798-bc2d-4c66-85fb-2955c579b122.jpg)

    - git push <remote> <local-branch>:<remote-branch>
      git push origin   dog:cat
        This mean push the content of local branch dog to remote cat.
        
    Default behavior is to: git push origin dog
    This pushes local branch dog to remote dog.    
    
- git push by setting upstream
    git push -u origin dog  --> Sets the upstream to origin dog. 
    After this `git push` to origin dog by default.

- Remote tracking branch
    Pointer to tell where remote branch is.
    `git branch -r`
    
    
  - Before making any changes on master branch as soon as you clone. 
  
   ``` 
              master
              |
    A -> B -> C
              |
              origin/master  --> remote tracking branch
    ```


  - After making local commits.
    
    
    ```
                        master
                        |
    A -> B -> C -> D -> E
              |
              origin/master  --> remote tracking branch doesn't move. 
    (Your branch is ahead of `origin/master` by 2 commits)
    ```
    
    Once we push master and origin/master will point to same commit.
    
    To see content of origin/master --> `git checkout origin/master`
 
 - Fork and Clone
    - You will have 2 remotes one to forked version of the repo.
    - And second one to original repo from where you forked.
    
        - `git remote add upstream <.git clone>`
    
   - Rebase
        - What's Rebase? Rebase is nothing but a mechanism to merge code similar to merge but with merge commits.
        - Why use Rebase?
            - If you want a clean git history without merge commits.
        - What does Rebase do? 
            - It change the base from original base to tip the new branch for clean git history. Because of this it rewrites history. 
    ![Screenshot_20220115-080957](https://user-images.githubusercontent.com/12951785/149617750-a953ee86-8891-4272-98c2-80ad7caeb408.jpg)
           
    - When not to use Rebase? 
      - When a commit is already been shared with someone don't rebase, because Rebase rewrites history.
     
    * Aside: 
    * HEAD is a pointer pointing to the latest commit of the branch you are currently in. 
    * HEAD in .git folder would be pointing to `refs/heads/<branch-name>`.
    * Content of `refs/heads/<branch-name>` file would the latest commit hash of that branch `<branch-name>`.
    * In case of detached head HEAD in .git folder would be pointing to `refs/heads/<commit-hash>`
    * 
            
