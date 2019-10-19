# Stash introduction

##git stash list:
git stash 後再輸入git status 會出現"nothing to commit,working tree clean"的字。
那到底剛剛那些檔案存到哪兒?  這時候輸入git stash list會出現以下字樣
>stash@{0}: WIP on master: ed7654c index test
>stash@{1}: WIP on master: 2b47536 start
目前只有二份狀態被存起來，最前面的 stash@{0} 是這個 stash 的代名詞，而後面的 WIP 字樣是「Work In Progress」，就是工作進行中的意思


##git stash apply:
  目的:從現有的儲藏中重新套用(#如果無指定，git預設使用最近的儲藏)
  如果你想應用較舊的儲藏，你可以通過名字指定他  ex:git stash apply stash@{1}

  >$ git stash apply
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   test

no changes added to commit (use "git add" and/or "git commit -a")

