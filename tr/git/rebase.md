(https://git-scm.com/book/en/v2/Git-Branching-Rebasing)[https://git-scm.com/book/en/v2/Git-Branching-Rebasing]


```
This operation works by going to the common ancestor of the two branches (the one you’re on and the one you’re rebasing onto), 
getting the diff introduced by each commit of the branch you’re on, 
saving those diffs to temporary files, resetting the current branch to the same commit as the branch you are rebasing onto, 
and finally applying each change in turn.
```

git-rebase是如何工作的呢？

如图所示，exprement和master两个chain在c2之后产生了分叉（fork）。

我们可以站在master，来调用merge exprement，在master这个chain上产生一个c5的合并提交。

也可以如本文即将介绍的站在experment上，在master上做rebase，产生一个c5。

```
该操作先找到一个分叉的公共位置，比如本例中的c2，计算当前坐在链到c2之间的差异diff，把这个diff保存到临时文件，把当前exprement链reset到c4的位置，
即，和master上的最新位置一致，最后在这个位置重放replay刚才保存的diff。
```
