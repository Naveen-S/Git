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
    ![Screenshot_20220108-152808__01](https://user-images.githubusercontent.com/12951785/149866186-34d68038-847a-4e50-941d-581eab0ec7a4.jpg)

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
    ![Screenshot_20220115-080957__01__01](https://user-images.githubusercontent.com/12951785/149866266-e4c96159-632d-4c3b-ad7c-b92452180ce6.jpg)

    - When not to use Rebase? 
      - When a commit is already been shared with someone don't rebase, because Rebase rewrites history.
     
    
    - Interactive rebase
        - ![Screenshot_20220115-202729__01](https://user-images.githubusercontent.com/12951785/149865972-aa5b4ed1-fcf7-4ef9-bcf0-9d4389c4a7f8.jpg)
        
        - pick - Keep the commit.
        - reword - Reword the commit. 
        - fixup - delete a commit message of the commit and meld multiple(continous) commits to previous one.
        - drop - remove commit.
    
    - Tag
        ![image](https://user-images.githubusercontent.com/12951785/149866980-18bbc6be-ded5-46a0-bbf7-b4faf5c24062.png)
    
        - Type of tags
            - Lightweight Tag: Just the label. 
            - Annotated Tag: Includes meta data like author name, email date and tagging message.
    
        - View Tags
            - `git tag` : List all the tags.
            - `git tag -l "*beta*"` : Filter tags based on wild card.
            
        - Checking out tag
            - `git checkout <tagName>`
                - Note youll be detached head on doing this.
        
        - Making lightweight tags
            - `git tag <tagname>`
        
        - Making annotated tags
            - `git tag -a <tagname>`
            
            - How do I see the metadata of the annotated tag? 
                - `git show <tagname>`
        
        - Tagging previous commits
            - `git tag -a <tagname> <commit>`
    
        - Move tag / Force tag
            - If you want the tag to be moved to different commit use this. We can't have two same tags for two commit.
            - `git tag <tagname> <commit> -f`
    
        - Delete tag
            - `git tag -d <tagname>`
    
        - Push tag
            - Pushing single tag
                - `git push <remote> <tagname>`
            
            - Pushing all tags
                - `git push <remote> --tags`
            
     
    - Internals of Git
        - .git folder
            - Important files & folders: `config`,`HEAD`, `refs`, `objects`.
        
        - refs
            - heads
                - There will be a file for each local branch with content of its last commit.
            - tags
                - Similiar to heads, there will a file for each tag created with the content of its commit to which it is pointing. 
        
        - HEAD
            - Reference to the commit which I'm currently in. 
    
        - objects
            - commit
            - tree
            - blobs
            - annotated tags
            
            - Git uses SHA-1 for generating above hashes. 
            - Git is a key-value datastore. 
                ![image](https://user-images.githubusercontent.com/12951785/151353471-ec3725db-a5ea-4d42-8180-5cc48745efc0.png)
            
            
            - Truely internals
                - Trying Hashing
                    
                    - Hashing a text.
                    ![image](https://user-images.githubusercontent.com/12951785/151353858-e68f6b13-eaea-4839-ad1e-a9c06bacf627.png)
                    ![image](https://user-images.githubusercontent.com/12951785/151368418-6d4116c8-6be6-4556-b15b-1f629803acc7.png)

                    
                    - Retrieving Hashed data
                        `git cat-file -p <object-hash>`
                    
                    - Hash file
                        - `git hash-object <file-name>` -w
                            - `-w` to save the hash in objects.
                    
                    - Blobs - Stores file content
                        ![image](https://user-images.githubusercontent.com/12951785/151499729-64c5fd69-8000-45b8-bbc8-84fdcdc6c51c.png)
    
                    - Trees - Stores directory structure
                        ![image](https://user-images.githubusercontent.com/12951785/151501119-ed9ad5d8-731d-4db0-9dc9-b98f006f622f.png)
                        ![image](https://user-images.githubusercontent.com/12951785/151501405-4eeadde8-e1bc-46c6-97ca-148c006c550d.png)
                        ![image](https://user-images.githubusercontent.com/12951785/151501717-5c6e8f30-7e9f-4caf-9acb-3e90a7ba780d.png)
                        ![image](https://user-images.githubusercontent.com/12951785/151503740-d8fefab0-dffe-4709-8f8c-0cb9f46e9cdc.png)
                
                    - Commits
                        ![image](https://user-images.githubusercontent.com/12951785/151505612-ddc677a2-c463-4f50-98d9-a30d09830621.png)
                        ![image](https://user-images.githubusercontent.com/12951785/151505939-4b0b58fc-ca67-4bee-abd3-00460db0fd7c.png)
                        ![image](https://user-images.githubusercontent.com/12951785/151506339-9f623bf8-3cde-4078-be13-9116ac30d9d8.png)


            - Reflogs
                Git keeps the record of when the tips of the branches and other references were updated in the repo (Locally).
                `git reflog`
                
                - Present in `.git/logs/HEAD`
                    - Tracks the movement of HEAD.
    
                - ![image](https://user-images.githubusercontent.com/12951785/151545110-c0ad7425-9bd4-45a2-9388-3a867d3297b3.png)
                    - `git reflog show HEAD/<branch-name>`
                
                - Reflog references
                    `name@{qualifier}`
                    Ex: `git reflog show master@{2}`
                           - master two moves ago. 
    
                        - HEAD@{2} vs HEAD~2
                            - HEAD@{2} - HEAD two moves ago. 
                            - HEAD~2 - HEAD two commits ago. 
    
                
                - Timed references
                    ![image](https://user-images.githubusercontent.com/12951785/151546772-b8fbbcfc-4b87-4da2-9094-b8cb9933fede.png)
                    
                    - Ex: `git diff master master@{yesterday}`
    
        
            - Alias
                In global .gitconfig file. 
                
                ```
                    [alias]
                        s = status
                        d = diff
                    - Usage: 
                        `git s`
                        `git d`
                    
                        cm = commit -m 
                        // Note the arguments passed to git commit -m "commit message", will automatically passed. 
                        Usage: `git cm 'new commit'`

    
    * Aside: 
    * HEAD is a pointer pointing to the latest commit of the branch you are currently in. 
    * HEAD in .git folder would be pointing to `refs/heads/<branch-name>`.
    * Content of `refs/heads/<branch-name>` file would the latest commit hash of that branch `<branch-name>`.
    * In case of detached head HEAD in .git folder would be pointing to `refs/heads/<commit-hash>`
    * 
            
