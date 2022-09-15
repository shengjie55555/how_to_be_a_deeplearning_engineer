# Learn Git from Scratch
## rebase
![git_graph](materials/git_tutorial/git_graph.png)
1. 解释
   1. 当执行rebase操作时，git会从两个分支的共同祖先开始提取待变基分支（一般是特性分支）上的修改，然后将待变基分支指向基分支（一般是主分支）的最新提交，最后将刚才提取的修改应用到基分支的最新提交的后面。
   2. rebase，变基，可以直接理解为改变基底。在主分支上新开了一个特性分支，但是主分支更新了，那么我们的特性分支和主分支的公共祖先就不是主分支的最新提交了，这样子提交pr比较麻烦，可以在特性分支上git rebase master，这样子就可以改变特性分支的基底为master的最新提交。结果如下：![git_graph_rebase](materials/git_tutorial/git_graph_rebase.png)
2. 和merge的区别
   1. rebase可以对我们要操作的分支历史进行修改，比如上述在特性分支执行git rebase master之后，对于特性分支而言，它的历史提交发生了改变，新增了master分支上的改动。
      * 会合并之前的commit历史，得到更简洁的项目历史，去掉了merge commit。
      * 如果合并出现代码问题不容易定位，因为改变了history。
   2. merge会自动创建一个新的commit，如果合并的时候遇到conflict，仅需要修改后重新commit。结果如下![git_graph_merge](materials/git_tutorial/git_graph_merge.png)
      * 记录了真实的commit情况，包括每个分支的详情。
      * 因为每次merge会自动产生一个merge commit，所以在使用一些git的GUI tools，特别是commit比较频繁时，看到分支很杂乱。
3. **The Golden Rule of Rebasing rebase**
   1. 千万不要再公共分支上使用rebase，如果在主分支上git rebase feature，结果如下![git_graph_rebase_master](materials/git_tutorial/git_graph_rebase_master.png) rebase将所有master的commit移动到你的feature的顶端。问题是：其他人还在original master上开发，由于你使用了rebase移动了master，git会认为你的主分支的历史与其他人的有分歧，会产生冲突。
4. rebase解决冲突
   1. 如果git rebase master的时候提示出现冲突，可以在解决冲突后，git add，然后再git rebase --continue。
   2. 提示冲突后，.git目录下会产生一个.COMMIT_EDITMSG.swp 的交换文件，只有 git rebase --continue 或者 --skip 或者 --abort 后，交换文件才会删掉。**所以最好有始有终，不然swg文件不太好删！**