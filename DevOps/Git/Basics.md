### git init
`git init <reponame>` -> create a repo

Git init creates a folder when you create a repo

.git : It is a folder in the repo that contains everything that makes that folder a repository. If no `.git` file, that is not a repo. The config file can be helpful 

### git status
`git status` commands shows you the status of the repo. You should be inside the repo. It will show changes

- **Untracked files**: You have to add newly created files to the git. Just being inside the directory doesn't mean it is a part of version control. Untracked files shows this.

You have to use `git add <file_name>` to add to version control

### git add
This commands add the files from "untracked files" to "changes to be committed".

### git config
This commands adjust the git stuff. We will use with --global flag for now, which edits all the repos.

| Command                                           | Explanation                          |
| ------------------------------------------------- | ------------------------------------ |
| `git config --global user.name "atakan"`          | Adds the 'atakan' username as global |
| `git config --global user.email` "atakan@example" | Adds the email as global             |
|                                                   |                                      |

### git commit

`git commit -m "message"` -> commits the changes

### git diff
`git diff <file>` shows the differences between current and last comit

### git log
`git log --oneline` shows the logs

### git revert
`git revert <last commit you want to revert, hash value>` -> it creates another commit with the fixed & old commit

### git clone
Copy an existing repo to local

### git remote
`git remote add origin <url>` -> it adds a remote repo. You can see the changes in .git/config

To push, you need a personal access token. In github, go to settings -> developer -> personal access token and create one.

You will use this token as password

#### git push origin master
- This commands push master to the remote origin

#### For ssh login
- git remote set-url origin git@github.com:USERNAME/REPO.git
# Something about SSH and HTTP

When you use http commands, you need username/password

```
git clone https://github.com/username/repo.git
git remote add origin https://github.com/username/repo.git
```

When you use SSH versions of those, you don't have to put password.

```
git clone git@github.com:username/repo.git
git remote set-url origin git@github.com:username/repo.git
```

You can see it with `git remote -v`.