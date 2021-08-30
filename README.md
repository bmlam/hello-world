# hello-world - hook repos on my machine to GitHub
My first-step project to get myself familiary with GitHub

I just succeeded in configuring git on my Unix desktop to use my first github account as remote repository, not in the default way that is meant for new users who normally work with one single github remote. The default way saves new users a lot of configuration work. But in my case I plan to work with multiple github remotes / accounts, so I did this config exercise with my first account.

These are the steps:

Step 1: put my ssh public key from .ssh/id_rsa into github as per
    https://gist.github.com/JoaquimLey/e6049a12c8fd2923611802384cd2fb4a

step 2:
    created file .ssh/config with this content:

    Host <ssh_host_alias>
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa
    
step 3:
    Created repo multilingual in the target github account
    
step 4:
    Created the local multilingual repo with "git init ."
    
step 5:
    git remote add <origin_alias> git@<ssh_host_alias>:<top_level_dir_at_github_alias_account_name>/multilingual.git
    
step 6:
    git push <origin_alias> master
    
"multilingual" is just an example, I could have used "<repo_name>" as placeholder. <ssh_host_alias>, <origin_alias> are placeholders named intentionally so to express their purposes.

Note that when you enter "git remote -v" in the newly created repository, it will output:

<origin_alias> git@<ssh_host_alias>:<top_level_dir_at_github_alias_account_name>/multilingual (fetch)
<origin_alias> git@<ssh_host_alias>:<top_level_dir_at_github_alias_account_name>/multilingual (push)

To clone the repository in another location - you probably want to do that on another machine - use this command (mind the string .git at the end!)

git clone  git@<ssh_host_alias>:<top_level_dir_at_github_alias_account_name>/multilingual.git 

Of course this is assuming that you have done the same git/ssh configuration, if it is on another machine.

At some point of time, the local repositories which I created when first started off with github no longer could push to remote, getting error similar to "password authentication no longer allowed". Those are the one where "git remote -v" shows 

    https//github.com/bmlam/<repo-name>.git

bmlam is my first github "account" name. Since I have added a public ssh key in this account for my PC and created an ssh_host_alias a while ago, I just needed to replace the remote URL with 
    git@<ssh_host_alias>:bmlam/<repo-name>.gi
    
Thereafter, "git push" worked again.
