# hello-world - connect local repositories to GitHub using ssh host alias

I first worked with local repository connected to a single github account using the default method. That means the remote URL is analogue to what you would enter into the browser address fieled. The default way saves new users a lot of configuration work. But when one has to work with multiple github remotes / accounts, the game became a bit more complex. Basically one has to configure each remote account as ssh host alias on the local machine.

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

I have created other repositories using the default authentication method, i.e., "git remote -v" will display the URL matching the one you would use in a web browser. I decided to no longer use this default method. So I added another host alias in ~/.ssh/config. This is also a good idea because at some point of time, Github depricated this method and the local repositories which I had created with this method no longer could push to remote, getting error similar to "password authentication no longer allowed". I needed to change the repositority which had this remote URL 

    https//github.com/bmlam/<repo-name>.git
    
to something else. bmlam was my first github account. Besides adding an alias entry in .ssh/config, I had to store the public key in the github account. Next step was to replace in each repository the remote URL with 

    git remote set-url origin git@<ssh_host_alias>:bmlam/<repo-name>
    
Thereafter, "git push" worked again. Below is an example git command that did the magic:

    git remote set-url origin git@my-github1:bmlam/apex_konten_bewegungen
    
This same hack/command is applicable when I clone the repository afresh from https://github.com/bmlam/apex_konten_bewegung. The cloning would work with a personal access token and a local repo created. But thereafter pull and push would not work until this hack has been applied.
