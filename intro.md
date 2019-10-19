# Stash introduction

##git stash list:
git stash 後再輸入git status 會出現"nothing to commit,working tree clean"的字。
那到底剛剛那些檔案存到哪兒?  這時候輸入git stash list會出現以下字樣
stash@{0}: WIP on master: ed7654c index test
stash@{1}: WIP on master: 2b47536 start
看起來目前只有二份狀態被存起來，最前面的 stash@{0} 是這個 stash 的代名詞，而後面的 WIP 字樣是「Work In Progress」，就是工作進行中的意思



