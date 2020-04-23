无论是开发、运维，还是测试，大家都知道Git在日常工作中的地位。所以，也是大家的必学、必备技能之一。之前公众号也发过很多git相关的文章：

[Git这些高级用法，喜欢就拿去用！](http://mp.weixin.qq.com/s?__biz=MzI0MDQ4MTM5NQ==&mid=2247492361&idx=2&sn=56c8cc90d6018805e5770eb3df4f54ed&chksm=e9188615de6f0f0375c35dcfecc14e88faa7b96485a79ba18fbd0d94864fc44a47272a882c3e&scene=21#wechat_redirect) 
[一文速查Git常用命令，搞定版本控制照做就ok](http://mp.weixin.qq.com/s?__biz=MzI0MDQ4MTM5NQ==&mid=2247490976&idx=2&sn=f2d1c9e39375c1235a7c96191e6cc8be&chksm=e91b78bcde6cf1aa82eab8c794b0b155bec7afdffe0fe354c8553c306e676e4ee560c0fc7c15&scene=21#wechat_redirect) 
[大牛总结的Git使用技巧，写得太好了！](http://mp.weixin.qq.com/s?__biz=MzI0MDQ4MTM5NQ==&mid=2247490468&idx=2&sn=c0ffd551fc6be91334c07391339dc96b&chksm=e91b7eb8de6cf7aef37a926dbac8ca6295e148fd79ca61ffcbf8988f543302b6e1d3aec2f921&scene=21#wechat_redirect) 
[掌握这10条规范，轻松搞定Git！](http://mp.weixin.qq.com/s?__biz=MzI0MDQ4MTM5NQ==&mid=2247486125&idx=1&sn=ce871dd581b847ce8d6418f616d208ef&chksm=e91b6fb1de6ce6a7129022c167e46b780a0a4a91d7e54c6c3de63b1121c3f487bf561f9c13c5&scene=21#wechat_redirect)

但是呢，民工哥，也经常在后台看到读者说，命令太多了不好记啊，时间长了不用又忘记了等等的吐槽。是啊，要学一门技术真难，何况现在技术更新、迭代这么快.....

所以，对于学习Git这门技术，要是有一个一看就懂，一学就会的入门资料就好了。前不久，国外的一位小姐姐写了一篇这样的文章《CS Visualized: Useful Git Commands》。作者是来自英属哥伦比亚的小姐姐 Lydia Hallie，在这篇文章里面，她通过生动形象的动画，以更加直观的方式，向开发者展示 Git 命令中的 merge、rebase、reset、revert、cherry-pick 等常用骚操作的具体原理。

**下面就给大家带来一些实例分享：**

**1、git merge**

fast-forward模式

![640.gif](https://segmentfault.com/img/bVbGazO)

no-fast-forward模式

![640 (1).gif](https://segmentfault.com/img/bVbGazQ)

合并冲突修复的过程 ，动画演示如下：

![640 (2).gif](https://segmentfault.com/img/bVbGazR)

**2、git rebase**

git rebase 指令会复制当前分支的所有最新提交，然后将这些提交添加到指定分支提交记录之上。

![640 (4).gif](https://segmentfault.com/img/bVbGazU)

git rebase还提供了 6 种操作模式：

- reword：修改提交信息
- edit：修改此提交
- squash：将当前提交合并到之前的提交中
- fixup：将当前提交合并到之前的提交中，不保留提交日志消息
- exec：在每一个需要变基的提交上执行一条命令
- drop：删除提交

以 drop 为例：
![640 (5).gif](https://segmentfault.com/img/bVbGazW)

以 squash 为例：

![640 (7).gif](https://segmentfault.com/img/bVbGazW)

**3、git reset**

以下图为例：9e78i 提交添加了 style.css 文件，035cc 提交添加了 index.js 文件。使用软重置，我们可以撤销提交记录，但是保留新建的 style.css 和 index.js 文件。

![640 (6).gif](https://segmentfault.com/img/bVbGaz6)

### **Hard reset硬重置**

硬重置时：无需保留提交已有的修改，直接将当前分支的状态恢复到某个特定提交下。需要注意的是，硬重置还会将当前工作目录（working directory）中的文件、已暂存文件（staged files）全部移除！如下图所示：

![640 (8).gif](https://segmentfault.com/img/bVbGaAk)

**4、git revert**

举个例子，我们在 ec5be 上添加了 index.js 文件。之后发现并不需要这个文件。那么就可以使用 git revert ec5be 指令还原之前的更改。如下图所示：
![640 (9).gif](https://segmentfault.com/img/bVbGaAn)

**5、git cherry-pick**

举个例子：dev 分支上的 76d12 提交添加了 index.js 文件，我们需要将本次提交更改加入到 master 分支，那么就可以使用 git cherry-pick 76d12 单独检出这条记录修改。如下图所示：

![640 (10).gif](https://segmentfault.com/img/bVbGaAp)

**6、git fetch**

使用 git fetch 指令将远程分支上的最新的修改下载下来。

![640 (11).gif](https://segmentfault.com/img/bVbGaAr)
**7、git pull**

git pull 指令实际做了两件事：git fetch 和 git merge。

如下图所示：

![640 (12).gif](https://segmentfault.com/img/bVbGaAs)
**8、git reflog**

git reflog 用于显示所有已执行操作的日志！包括合并、重置、还原，也就是记录了对分支的一切更改行为。

![ ](https://segmentfault.com/img/bVbGaAw)

如果，你不想合并 origin/master 分支了。就需要执行 git reflog 命令，合并之前的仓库状态位于 HEAD@{1} 这个地方，所以我们使用 git reset 指令将 HEAD 头指向 HEAD@{1}就可以了。
![640 (14).gif](https://segmentfault.com/img/bVbGaAG)

以上就是民工哥今天给大家带来的分享，如果本文对你有所帮助，请点个在看与转发分享支持一下，感谢大家。我们一起学习，共同进步！！！

> *原作者：莉迪亚·哈莉（Lydia Hallie）*
> *原文：[https://dev.to/lydiahallie/cs...](https://dev.to/lydiahallie/cs-visualized-useful-git-commands-37p1)*
> *民工哥通过翻译作者原文再加上一些个人理解总结而成，版权归原作者所有，纯属技术分享，不作为商业目的。*