from http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013744142037508cf42e51debf49668810645e02887691000

* Create a repository
`git init <git dir>`

* add local repository to remote server  
`git remote add origin git@github.com:huyn/DemoGroup.git`  
then  
`git push -u origin master`

* Commit a file
use `git add file1 file2 file3` to add files to `index`  
use `git commit` to commit files to repository  
use `git commit -m "infomation about this commit"` to commit files with infomation  
use `git status` to check the status of current dir  
use `git diff` to display the changes between local and latest version  
use `git log` to show the commit logs, append `--pretty=oneline` to show distinct info  
use `git reset --hard <commit id>` to jump to the certain version  

In git, HEAD means current version, HEAD^ means last version, HEAD^^ means the version befor last version, etc.
For example, if last version id is `abcd1234`
`git reset --hard HEAD^` has the same effects like `git reset --hard abcd1234`

if you jump to a history version, and regret doing this and want to find a backup after this version, but you forget the commit id, this is the command to do show all the command you have executed:
`git reflog`
then you find your commit id and do `reset` operation

* Recover a file
use `git checkout -- <filename>` to revoke the changes on certain file  
use `rm filename` to delete a file beyond git
use `git rm filename` to delete a file under git control

* Connect to Remote Repository(Github)
`ssh-keygen -t rsa -C youremail@example.com`
