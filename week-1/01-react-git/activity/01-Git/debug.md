# Debug fixes from Week 1

### Problem:
```
ashlees-MacBook-Pro:~ ashleesstuff$ git --version

Agreeing to the Xcode/iOS license requires admin privileges, please run “sudo xcodebuild -license” and then retry this command.
```

### Reason:
Git on a Mac is managed by Apple themselves through Xcode. Every new Xcode or iOS license update requres you to agree to the license again.

### Fix:
1. Copy code `sudo xcodebuild -license accept`
2. Enter computer password and press enter
3. Rerun `git --version`


### Problem:
```
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

   git config --global user.name "Your Name"
   git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

   git commit --amend --reset-author
```

### Reason:
Git needs to be configured to your email that you use on github or gitlab so that they are aware of who is uploading to git

### Fix:
1. Copy code `git config --global user.email "your@example.com"`
2. Replace where the `"your@example.com"` with your email (note: make sure to keep the quotation marks)

### Problem:
```
remote: Counting objects: 45, done.
remote: Compressing objects: 100% (45/45), done.
remote: Total 45 (delta 14), reused 0 (delta 0)
Unpacking objects: 100% (45/45), done.
From http://gw.bootcampcontent.com/GW-Coding-Boot-Camp/10-16-2017-GW-Arlington-Class-Repository-FSF-FT
   d987b9b..9aee9a6  master     -> origin/master
Updating d987b9b..9aee9a6
error: Your local changes to the following files would be overwritten by merge:
    01-Week/02-html-git/01-Activities/08-GoogleFontDemo/Unsolved/index.html
Please commit your changes or stash them before you merge.
Aborting
```

### Reason:
Changes have been made to files that you are trying to be pull from git. If you continued with the pull your local changes will be over written with the remote changes on git.
### [RTFM](https://git-scm.com/book/en/v1/Git-Tools-Stashing)

### Fix:
Depending on whether or not you want the changes there are two ways to go about it:

#### Fix 1 (Need the changed files):
1. `git stash` This command stores your files in a "vault" that can be accessed later and reverts your files to how they were from the pull
2. `git pull` allows you to pull the new files down locally
3. `git stash apply` this will reapply your changed files to the newly pulled files

#### Fix 2 (Don't need the changed files):
1. `git stash` This command stores your files in a "vault" that can be accessed later and reverts your files to how they were from the pull
2. `git pull` allows you to pull the new files down locally
3. `git stash drop` this will remove the changed files from your "vault"
