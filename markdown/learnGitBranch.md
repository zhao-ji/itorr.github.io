##[learnGitBranch](http://http://pcottle.github.io/learnGitBranching/) 刷题总结

- commit 做一次提交
- commit --amend 修改最近一次的提交

- branch *branch early branch often*
- git branch newImage 新建分支并留在原分支
- git checkout -b newImage 新建分支并跳到新分支
- git checkout -b newImage origin/newImage 新建分支然后跳到新分支并跟踪远程origin/newImage分支
- git checkout -u origin/newImage newImage 同上
- git checkout --track origin/newImage 新建与远程跟踪分支同名分支

- git merge 合并分支
- git rebase 与 git merge 相比分支看起来是一条直线没有分叉 更干净
   `Rebasing essentially takes a set of commits, 'copies' then and plops then down somewhere else`
- git rebase basebranch highbranch 以basebranch最后一个commit为起点把highbranch分支上不同的commit按序拼接上 原来的highbranch commit历史还存在

- HEAD 一个指向当前所处commit的指针 checkout到哪里HEAD就跟到哪里

- ^<num> 移动到更古老的一个commit上 如果当前commit上有多个父commit 选择第num个父commit
- ~<num> 移动到第一个父commit上更加古老的num个commit
- git checkout HEAD^2 HEAD指针向第二个父分支移动一个提交
- git checkout HEAD~3 HEAD指针向第一个父分支移动三个提交
- git branch -f master HEAD~3 master分支向更古老方向移动三个提交

- git reset 撤销提交 保留文件修改
- git reset --hard 撤销提交 丢弃文件修改
- git revert 提交抵消commit

- git cherry-pick <commit-hash> <commit-hash>将其他分支的commit按顺序放到本分支来
- git rebase -i basebranch 打开编辑器重新编辑commit 选择pick 删除（删除对应行） 合并(squash) 重新对提交排序
- git rebase -i HEAD~4 编辑最近的四次提交

- git tag <version-num> <commit-hash> 打标签
- git describe <commit-hash> 返回距离那次提交最近的标签还有距最近标签多少个提交 <tag>_<numCommits>_g<hash>

- git push origin <local-branch>:<remote-branch>
- git fetch origin <remote-branch>
:<local-branch>