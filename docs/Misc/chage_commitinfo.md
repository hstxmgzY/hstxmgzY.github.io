# Git 修改提交的邮箱或用户名

今天已经被气死了，因为发现我的commit全部没有小绿点，然后查了一堆blog，全部有问题,完全没办法实现，最终终于找到了一个大佬写的

感谢大佬

大佬[白路tcatche](https://github.com/tcatche)


**原文地址：[Git 修改提交的邮箱或用户名](https://github.com/tcatche/tcatche.github.io/issues/113).**
>
## 修改全局的 commit 的用户名和邮箱
如果需要以后 commit 默认的用户名和邮箱为指定的内容，可以通过 `git config --global`命令:
>
```shell
git config --global user.email "global@example.com"
git config --global user.name "example"
```
>
然后编辑提交后可以看到修改已生效：
>
```shell
git log
# 输出
commit d4a341f8aab5acd0468cbe3d029fc1801f62678d (HEAD -master)
Author: example <global@example.com>
Date:   Tue Jan 26 14:34:48 2021 +0800

    test
```
>
## 对某个仓库设置特定的用户名和邮箱
如果想针对某个仓库设置特定的用户名和邮箱，比如工作项目使用工作邮箱，个人项目使用个人邮箱，可以去掉 `--global` 在特定代码仓库运行：
>
```shell
cd my-work-repo
git config user.email "work@example.com"
git config user.name "work"
```
>
然后重新提交 commit ,可以看到此时最新的的提交的用户名已经修改了：
>
```shell
git log
# 输出
commit 65a152b75e6c3748eb086830b836d6ec18e3baee (HEAD -master)
Author: work <work@example.com>
Date:   Tue Jan 26 14:38:04 2021 +0800

    test2

commit d4a341f8aab5acd0468cbe3d029fc1801f62678d
Author: example <global@example.com>
Date:   Tue Jan 26 14:34:48 2021 +0800

    test
```
>
而全局的用户信息仍为 `example 和 global@example.com `：
>
```shell
git config --global user.email
global@example.com # 输出

git config --global user.name
example # 输出
```
>
## 修改最新提交中的用户信息
上面的内容只针对新提交的记录，如果想要修改以前的提交中的用户信息，则上面的方式并不生效，需要采用其他方式。
>
如果需要修改最近一次提交的信息，通常可以使用 `git commit --amend --author="example <global@example.com>"`，此时会弹窗 vim 编辑器，可以进一步编辑其它提交信息（注意在 vim 修改用户信息并不生效。）：
>
```shell
git commit --amend --author="example <global@example.com>"

#vim 弹出提示修改 git 信息
test2

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Author:    example <global@example.com>
# Date:      Tue Jan 26 14:38:04 2021 +0800
#
# On branch master
# Changes to be committed:
#       new file:   test2
#
```
>
如果不需要编辑其它提交信息，只需要增加个 `--no-edit` 参数即可：
>
```shell
git commit --amend --author="example <global@example.com>" --no-edit
```
>
## git rebase 修改多个指定的历史提交
如果有多个历史提交，类似的，可以使用 `git rebase` 命令，和 rebase 操作类似，只是在 `git commit --amend ` 时加上 `--author="example <global@example.com>"`，不再详细说明。
>
## 使用 git filter-branch 修改全部历史提交
git filter-branch 可以重写分支信息，如果需要修改全部的提交信息，可以使用。
>
```shell
git filter-branch -f --env-filter "GIT_AUTHOR_NAME='Example'; GIT_AUTHOR_EMAIL='example@test.com'"

# 输出
Proceeding with filter-branch...
Rewrite d4a341f8aab5acd0468cbe3d029fc1801f62678d (1/2) (0 seconds passed, remaining 0 predicted)
Rewrite 559892effdc205a2315589b0199fff158a2cd1f8 (2/2) (1 seconds passed, remaining 0 predicted)
Ref 'refs/heads/master' was rewritten
```
>
运行 `git log` 可以看到，变更已经生效。
>
```shell
#运行
git log

#输出
commit bf98e0e451072d9e46955e4e779fec0097a51bff (HEAD -master)
Author: Example <example@test.com>
Date:   Tue Jan 26 14:38:04 2021 +0800

    test2

    Author:    global <global-test@example.com>
    Date:      Tue Jan 26 14:38:04 2021 +0800

commit 05aa39b6ce9126ea84caa1be00d6f8b0c742ad9f
Author: Example <example@test.com>
Date:   Tue Jan 26 14:34:48 2021 +0800

    test
```
>
## 使用 git filter-branch 修改特定的历史提交
可以使用脚本，增加判断，只修改特定的历史提交，如下示例：
>
```shell
# filter-branch.sh

#!/bin/sh

git filter-branch -f --env-filter '
OLD_EMAIL="example@test.com"
CORRECT_NAME="Example-New"
CORRECT_EMAIL="example-new@test.com"
if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi' HEAD
```
>
新提交一个 `commit` 作为区分，然后运行脚本:
>
```shell
# 运行
git config user.email "example-not-change@test.com"
git commit -m "test3" --allow-empty
bash filter-branch.sh
git log

# 输出
commit 292062018b88641f3233efa08dfd23df04e8dc3c (HEAD -master)
Author: work <example-not-change@test.com>
Date:   Tue Jan 26 15:23:08 2021 +0800

    test

commit 4dc68a1ebfd8c2600f09ed7de307c1a4aa3acf52
Author: Example-New <example-new@test.com>
Date:   Tue Jan 26 14:38:04 2021 +0800

    test2

    Author:    global <global-test@example.com>
    Date:      Tue Jan 26 14:38:04 2021 +0800

commit b3761e99006c662cca4a8285842eeca3232f70d0
Author: Example-New <example-new@test.com>
Date:   Tue Jan 26 14:34:48 2021 +0800

    test
```
>
可以看到，第一个 log 并没有修改。
>
在使用 `git filter-branch` 时，可能会注意到控制台有个**警告**输出：
>
```shell
WARNING: git-filter-branch has a glut of gotchas generating mangled history
         rewrites.  Hit Ctrl-C before proceeding to abort, then use an
         alternative filtering tool such as 'git filter-repo'
         (https://github.com/newren/git-filter-repo/) instead.  See the
         filter-branch manual page for more details; to squelch this warning,
         set FILTER_BRANCH_SQUELCH_WARNING=1.
```
>
翻译过来就是说而且 `filter-branch` 有很多缺陷，可能会对预期的历史重写造成不明显的破坏。而且它的速度非常慢，推荐使用[git filter-repo](https://github.com/newren/git-filter-repo/)替代。
>
## 注意
需要注意的是，如果使用上面的方法更改历史提交的用户信息，历史提交的 commit hash，也会随之改变，如果一个仓库是多人协作的，需要慎重使用。
>
To change the name and/or email address recorded in existing commits, you must rewrite the entire history of your Git repository.
>
Warning: This action is destructive to your repository's history. If you're collaborating on a repository with others, it's considered bad practice to rewrite published history. You should only do this in an emergency.
>
提交后如果推动到远端，需要加上 `--force` 或 `-f`:
>
```shell
git push --force
```
>
## 参考
* [git commit](https://git-scm.com/docs/git-commit)
* [git filter-branch](https://git-scm.com/docs/git-filter-branch)


