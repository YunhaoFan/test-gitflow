# test-gitflow 一个测试gitflow的破玩意儿

### Master

用于保存发布历史，使用版本号为master上的所有提交打上标签

### Hotfix

唯一一个可以基于master创建的分支，是用于修复bug的分支，解决bug后合并入master和develop分支后，需要在master分支上打上tag。

```shell
// 发现bug
git checkout -b issue-#001 master

// 修复bug完成
git checkout master
git merge issue-#001
git push
git checkout develop
git merge issue-#001
git push
git branch -d issue-#001
```

### Release

develop分支功能足够了，或者临近发布，则需要基于develop分支建立一个release分支用于产品发布，这个分支意味着发布周期的开始（只能修复bug，不能再新增新的功能）。所有准备结束后可以合并master分支了，然后打上tag记录版本信息。

```shell
// 准备发布
git checkout -b release-0.1 develop

// 完成发布
git checkout master 
git merge release-0.1
git push
git checkout develop
git merge release-0.1
git push 
git branch -d release-0.1

// 打标签
git tag -a 0.1 -m"Init version 0.1" master
git push --tags
```

### Develop

用于集成各种功能开发

```shell
// 创建者
git branch develop
git push -u origin develop

// 其余开发者
git clone xxxxxx.git
git checkout -b develop origin/develop
```

### Feature

创建新功能开发分支的时候，创建分支的父分支应该选择develop分支，功能开发完毕时，代码应当被合并（merge）到develop分支。

```shell
// 开发新功能
git checkout -b some-feature develop
git status
git add <new files>
git commit -m "xxxx"

// 开发终了
git pull origin develop
git checkout develop
git merge some-feature
git push
git branch -d some-feature
```

