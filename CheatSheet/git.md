# Git/github

#### Configure

**If you not setup the `user.email`, mostly your commits won't count as contributions.**

```shell
git config --global user.name "[name]"
git ocnfig --global user.email "[email]"
```

##Git Workflow

![image-20190206194020094](/Users/crystal/Library/Application Support/typora-user-images/image-20190206194020094.png)

###Create a Repository

####Remote Repository (GitHub)

Download a project and its entire version history.

```shell
git clone [url]
```

####Local Repository

```shell
git init
```

### Track a File

```shell
git add <filename>
git add <filename_1> <filename_2>
git add --all # add all the file under current repository to track.
```

```shell
git commit
-m "message" # followed by a message
```

### Backtrack

```shell
git show HEAD # show the current commit
git checkout HEAD <filename> # restore the file to last commit
git reset HEAD <filename> # 
```



## Other Useful Command

`git status`: check the status of changes.

`git diff <filename>`: check the differences since last `git commit`.

`git log`: view all commits.

