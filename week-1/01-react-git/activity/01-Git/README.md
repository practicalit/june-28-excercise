### Creating and managing your own repo

Note: you can do all of this stuff from the command line! Open up a terminal and do the following:

#### Your initial commit

1. Create a directory named `git-basic-exercises`
2. `cd` into your new directory
3. look at what’s inside using `ls -a`. It should be empty
4. initialize your git repo using `git init`. Then check `ls -a` again. Can you spot the difference?
5. check the status of your repo by typing `git status`
6. type in `touch README.md`. This creates a new blank file. Then check `ls -a` and `git status` again.
7. type in `git log`. The output should make sense to you
8. Now add your readme file to your git staging area. Hint: use the `git add` command
9. Then check your `git status` again. Can you see the difference?
10. Try to unstage your file and check your `git status` again
11. Ok, now for your first commit: Make sure your readme file is staged then type in `git commit -m "initial commit"`
