# Stash introduction
什麼是 stash ?
當你正在進行專案中某一部分的工作，裡面的東西處於一個比較雜亂的狀態，而你想轉到其他分支上進行一些工作。不想只為了待會要回到這個工作點，就把做到一半的工作進行提交。git stash 就是解決這個問題的命令。
Stash 取得你工作目錄的 dirty state——也就是你修改過的被追蹤檔和暫存的變更——並將它保存到一個未完成變更的堆疊(stack)中，隨時可以重新套用。

執行  git status，你可以看到你的 dirty state：

>	 $ git status  
>	 On branch master  
>	 Changes to be committed:  
>	 	(use "git restore --staged <file>..." to unstage)  
>			modified:   test  

想切換分支，但還不想提交你正在進行中的工作，執行 git stash :  

>	 $ git stash  
>	　Saved working directory and index state WIP on master: 4a69ae7 git is hard  

工作目錄就乾淨了 :

>	 $ git status  
>	 On branch master  
>	 nothing to commit, working tree clean  

## git stash list:
git stash 後再輸入git status 會出現"nothing to commit,working tree clean"的字。
那到底剛剛那些檔案存到哪兒?  這時候輸入git stash list會出現以下字樣

>	 stash@{0}: WIP on master: ed7654c index test  
>	 stash@{1}: WIP on master: 2b47536 start  

看起來目前只有二份狀態被存起來，最前面的 stash@{0} 是這個 stash 的代名詞，而後面的 WIP 字樣是「Work In Progress」，就是工作進行中的意思
	
>	 stash@{0}: WIP on master: ed7654c index test  
>	 stash@{1}: WIP on master: 2b47536 start  

## git stash apply:
目的:從現有的儲藏中重新套用(#如果無指定，git預設使用最近的儲藏)
如果你想應用較舊的儲藏，你可以通過名字指定他  ex:git stash apply stash@{1}

>	 $ git stash apply  
>	 On branch master  
>	 Changes not staged for commit:  
>	 (use "git add <file>..." to update what will be committed)  
>	 (use "git restore <file>..." to discard changes in working directory)  
>	      modified:   test  

>	 no changes added to commit (use "git add" and/or "git commit -a")  

## git stash drop / pop / clear: 
如果想要移除已經 stash 的東西，
可以執行 git stash drop 加上希望刪除的stash的名字 :
	
>	 $ git stash list  
>	 stash@{0}: WIP on master: f0c9ca2 :thinking:  
>	 stash@{1}: WIP on master: e0d6928 I need shue fun  
>	 stash@{2}: WIP on master: a442e54 too much HW  
>	 stash@{3}: WIP on master: 2a30843 Zzzz  
>	 stash@{4}: WIP on master: 4a69ae7 git is hard  
>	 stash@{5}: WIP on master: ed7654c index test  
>	 stash@{6}: WIP on master: 2b47536 start  
>	 $ git stash drop stash@{5}  
>	 Dropped stash@{5} (4f6c34964d5e84e2968907e03c0e8c554e6ed58a)  
>	 $ git stash list  
>	 stash@{0}: WIP on master: f0c9ca2 :thinking:  
>	 stash@{1}: WIP on master: e0d6928 I need shue fun  
>	 stash@{2}: WIP on master: a442e54 too much HW  
>	 stash@{3}: WIP on master: 2a30843 Zzzz  
>	 stash@{4}: WIP on master: 4a69ae7 git is hard  
>	 stash@{5}: WIP on master: 2b47536 start  

想要先 apply 再 drop ， 可以執行  git  stash  pop 加上檔名，
這樣就會有相同的效果 :

>	 $ git stash list  
>	 stash@{0}: WIP on master: cebb4b6 final  
>	 stash@{1}: WIP on master: e0d6928 I need shue fun  
>	 stash@{2}: WIP on master: a442e54 too much HW  
>	 stash@{3}: WIP on master: 2a30843 Zzzz  
>	 stash@{4}: WIP on master: 4a69ae7 git is hard  
>	 stash@{5}: WIP on master: 2b47536 start  
>	 $ git stash pop  
>	 On branch master  
>	 Changes not staged for commit:  
>	   (use "git add <file>..." to update what will be committed)  
>	   (use "git restore <file>..." to discard changes in working directory)  
>	         modified:   test  

>	 no changes added to commit (use "git add" and/or "git commit -a")  
>	 Dropped refs/stash@{0} (dbd595b1e3ec424585a13f058eb4bf943caa02cd)  
>	 $ git stash list  
>	 stash@{0}: WIP on master: e0d6928 I need shue fun  
>	 stash@{1}: WIP on master: a442e54 too much HW  
>	 stash@{2}: WIP on master: 2a30843 Zzzz  
>	 stash@{3}: WIP on master: 4a69ae7 git is hard  
>	 stash@{4}: WIP on master: 2b47536 start  

想要刪除所有 stash 可以不用一個一個慢慢git stash drop，
可以執行 git status clear 這樣就可以刪除所有 stash : 

>	 $ git stash list  
>	 stash@{0}: WIP on master: e0d6928 I need shue fun  
>	 stash@{1}: WIP on master: a442e54 too much HW  
>	 stash@{2}: WIP on master: 2a30843 Zzzz  
>	 stash@{3}: WIP on master: 4a69ae7 git is hard  
>	 stash@{4}: WIP on master: 2b47536 start  
>	 $ git stash clear  
>	 $ git stash list  
>	 $  


