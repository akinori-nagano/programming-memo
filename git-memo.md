# git memo

## Git config  
http://sgry.jp/blog/2014/11/24/1811/

## Git で現在チェックアウトしているコミットのID
```
git show -s --format=%H
　　or
git log -n 1 --format=%H
```

## tig のコミットグラフがズレちゃう人のための対処法
https://qiita.com/Balacker/items/9c0f937a1faf1317c71b

----
## よく使うGitコマンド 

### Branch
```
git branch
git checkout -b ROSADEV-3
```

### add commit した後の push, merge
```
git push origin ROSADEV-3
git checkout master
git branch
git pull
git merge ROSADEV-3
git push
```

### Ignore file
```
git update-index --assume-unchanged [file path]
git update-index --no-assume-unchanged [file path]
```

### 一時的にコミットして変更を保存して、他のブランチを開始する
```
git checkout -b BRANCH-A
git commit -m "suspend"
    # 違う枝を触ることにしたので一時保存してBに切り替え
git checkout -b ROSADEV-B
git commit -m "completed"
    # Bは完了、ここで元の枝Aに戻る
git checkout ROSADEV-A
git commit --amend -m "completed"
    # 最終コミット時に一つ前のコミットを無効にする（らしい？）
    # 直前の commit と今回の commit を1つにまとめることができます。
```

### checkout tag
```
git checkout -b sprint_42_complete refs/tags/sprint_42_complete
                ~~~~~~~~~~~~~~~~~~           ~~~~~~~~~~~~~~~~~~
git fetch --all --tags --prune
```

### stash
```
git stash
git stash list
git stash drop stash_name
git stash pop stash_name
```
