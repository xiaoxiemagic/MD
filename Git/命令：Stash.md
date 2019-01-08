#### Stash 命令的使用

---

- 删除`stash`记录后找回

  ~~~
  #执行如下命令
  git fsck --lost-found
  
  #会得到类似于如下的输出
  dangling blob afc02fb30cc94f6ffd0cb2f524d7d349afa5f0dc
  dangling commit dc41434caa510da8b0bb8fc40bb53041d0693945
  dangling commit df053c06f6cac001cbe6a2c58da0bf972552fb26
  
  #找到你想要的记录后，执行如下命令，这样就还原了你git stash drop, git stash clear 的内容
  git merge 7010e0447be96627fde29961d420d887533d7796
  ~~~

  > 上面的记录中可以通过如下命令查看具体的内容
  > git show <id>
  >
  > 记录中会描述日期和摘要， 日期是你git stash 的日期， 摘要会记录你是在哪一条commit 上进行git stash操作的， 类似（WIP on integration-xf: 2e205ac Merge branch ‘release’ into develop）， 貌似只能一条记录一条记录的查看

