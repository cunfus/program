# git


## 其他

- `git restore --staged <file>` 不该加的 add 了，撤销撤销
- `git blame` fuck，这该死的代码是谁写的
- `git show` 等等，这个人提交了哪些东西
- `git add -p file` 代码有风险，添加需谨慎，一个片段一个片段来

## git tag
- `git tag <version>` 这次提交后，整体像个样子了，打个 tag 吧，指不定用来发布
- `git push origin <version>` 喂，远程的中心仓库，接受一下俺的 tag
- `git tag -d <version>` 不行，这个 tag 不行，删掉吧
- `git push origin :refs/tags/<version>` 喂，远程，同步一下，刚刚那个 tag 被俺删了

## git rebase

- `git rebase -i HEAD~2` 提交历史太乱了，得整理下
    - 这个 commit 不用改， pick；那几个合并下，
    - 好了好了，保存 :wq
    - 这啥，哦，这次修订的 commit 信息，refractor，:wq 
    - 喂， 远程中心，修改岁月史书了 `git push origin branch-name --force`        
- 上面真麻烦，能不能粗暴一点
    - 俺来创建一个孤儿分支 `git checkout --orphan new-branch`
    - 文件加进来，都加进来 `git add -A`
    - 提交提交 `git commit -m " "`
    - 你不是正统，俺才是正统 `git branch -D master`
    - 嘿嘿，俺就是正统了 `git branch -m master`
    - 喂，远程中心，修改岁月史书了 `git push origin master --force`


## git init

```bash
#!/bin/bash
repo_name=$1
git init --bare  ${repo_name}.git  # 裸仓库
chown -R git:git ${repo_name}.git
```