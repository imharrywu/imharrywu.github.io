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

读者可能有一个疑问：
在expr分支上，是否可以reset到master分支的c2？
答：当然可以，分支具体指在什么gittree的什么位置没有要求，分支可以指向任何位置，可以变动。
比如这个例子中，完全可以把expr分支reset到c2，在fast-forward到master的c3。有何不可？

读者可能还有一个疑问：
以master为base进行rebase之后，expr的确得到了master分支上c2到c3的diff，master怎么办？
答：如果希望master也得到expr的diff，就站到master分支上进行fast-forward到expr即可，即merge expr。


从这里我们也可以看出rebase一词的原始意义：本来expr分支上，c4到c2的diff，是以c2为base的。现在把这个diff从expr上‘剪’下来，并把expr分支reset到c4，以c4为base进行重放这个diff（即replay changes）。

