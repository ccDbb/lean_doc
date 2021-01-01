远程强制覆盖本地

1. git fetch *--all*

2. git reset *--hard origin/master*

3. git pull

4. git remote prune origin 远程分支名和本地同步。修剪掉远程删掉的，但是通过Git branch -a还能看到的

5. git push origin --delete 0723  删除远程分支名

6. git branch -d （-d是删除本地分支，如果没有合并不删除。-D即使没有合并也会删除）

   



