# public-repo-test

 1. Create a bare clone of the repository.
    (This is temporary and will be removed so just do it wherever.)
    ```bash
    git clone --bare git@github.com:philip-ellis-sp/public-repo-test.git
    ```

 2. [Create a new private repository on Github](https://help.github.com/articles/creating-a-new-repository/) and name it `private-repo-test`.

 3. Mirror-push your bare clone to your new `easytrace` repository.
    > Replace `<your_username>` with your actual Github username in the url below.
    
    ```bash
    cd public-repo-test.git
    git push --mirror git@github.com:<your_username>/private-repo-test.git
    ```

 4. Remove the temporary local repository you created in step 1.
    ```bash
    cd ..
    rm -rf public-repo-test.git
    ```
    
 5. You can now clone your `private-repo-test` repository on your machine (in my case in the `git` folder).
    ```bash
    cd ~/git
    git clone git@github.com:<your_username>/private-repo-test.git
    ```
   
 6. Now add the original repo as remote to fetch (potential) future changes.
    Make sure you also disable push on the remote (as you are not allowed to push to it anyway).
    ```bash
    git remote add upstream git@github.com:philip-ellis-sp/public-repo-test.git
    git remote set-url --push upstream DISABLE
    ```
    You can list all your remotes with `git remote -v`. You should see:
    ```
    origin	git@github.com:<your_username>/private-repo-test.git (fetch)
    origin	git@github.com:<your_username>/private-repo-test.git (push)
    upstream	git@github.com:philip-ellis-sp/public-repo-test.git (fetch)
    upstream	DISABLE (push)
    ```
    > When you push, do so on `origin` with `git push origin`.
   
    > When you want to pull changes from `upstream` you can just fetch the remote and rebase on top of your work.
    ```bash
      git fetch upstream
      git rebase upstream/main
      ```
      And solve the conflicts if any
