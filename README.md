# gitflow


```
ticket-000 --> develop --> release --> master
                  \ [stage]     \ [relase]    \ [production]
```
- 依據票號, 從 develop 開分支 ticket-000

### 確保本地與遠端分支同步
```bash
# 獲取 git 遠端 repo
# -p --prune 清除遠端已經不存在的分支的追蹤分支
git fetch -p


git checkout develop

# 確認 develop 分支是否等高
git status
tig
```

### Feature 推送
```bash
# 建立新分支
git checkout -b ticket-000

...

# 程式碼修改完畢
git add
# commit-msg 請依循 .conf/.commit-msg (eg. <feat>: xxx)
git commit

# 推送
git push origin ticket-000
```


### 部署至 stage / release
```bash
# 確保本地與遠端分支同步後
# develop -> [stage] / release -> [release]
git checkout develop
# 使用非快進式合併, 保留commit歷程
git merge --no-ff ticket-000

git push origin develop
```

### 部署至 production
```bash
# 確保本地與遠端分支同步後
git checkout master
# 使用非快進式合併, 保留commit歷程
git merge --no-ff release

# 版本號參考: (https://keepachangelog.com/zh-TW/1.0.0/)
git tag -a v1.0.0

# 匯出 changelog
git-chglog -o CHANGELOG.md
git add CHANGELOG.md
git commit -m '<docs>: update CHANGELOG.md'

# 推版
git push origin master

# 推送 tag
git push origin --tags
```



# tools
- [tig](https://github.com/jonas/tig)
- [git-chglog](https://github.com/git-chglog/git-chglog)

