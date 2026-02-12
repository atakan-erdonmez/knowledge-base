- git commit \<name> -> creates a commit, which is a save of like
- git branch \<name> -> creates a branch, which is like a different version
- git checkout \<name> -> changes to a branch, which makes it do commits in that specific branch
	- git checkout -b \<name> -> create branch and switchover to that

- git merge \<branch_name> -> merge the selected branch with the \<branch_name>, which makes the selected branch the new merged one. \<branch_name> stays alone if left. To make both the same merged, you gotta checkout and merge again, cross over merge

- git rebase \<branch> -> similar to merge. However, they don't combine. Instead, the selected branch appears under the \<branch>.

- git checkout \<branch/commit> -> Changes the HEAD (where you are) to a commit instead of a branch.


# Relative Refs
^ -> Means 1 parent up
	main^ - > means the first parent of main
	main^^ -> means the greatparent

You can also reference `HEAD` as a relative ref

~\<number> -> Specifies how many times you want to go up
`git checkout HEAD~4`

git branch -f \<branch> HEAD^ -> Moves the \<branch> 3 times up (forcefully)
`git branch -m \<name>` -> rename the branch
# Reset & Reverting

git reset -> Goes back to the commit. It acts like last commits didn't happened
git revert -> It creates a new commit while resetting the commits. It is used for remote stuff or if someone else is using


# Cherry-pick
Similar to rebase, 