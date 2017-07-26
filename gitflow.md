### 长期分支
- master:主分支，负责记录上线版本的迭代，该分支代码与线上代码是完全一致的

> 所有在Master分支上的Commit应该Tag

- dev:开发分支，该分支记录相对稳定的版本，所有的feature分支和bugfix分支都从该分支创建

### 短期分支
- feature/*：特性（功能）分支，用于开发新的功能，不同的功能创建不同的功能分支，功能分支开发完成并自测通过之后，需要合并到dev分支，之后删除该分支
> 功能分支的分支名称应该为能够准确描述该功能的英文简要表述
> 
>> feature/分支名称
> 
>例如，开发的功能为蒲公英市集活动，则可以创建名称为 feature/marketing的分支

- release/*:发布分支，用于代码上线准备,该分支从dev分支创建，创建之后由测试发布到测试环境进行测试，测试过程中发现的bug需要开发人员在该release分支上进行bug修复，所有bug修复完成后，上线之后，合并该release分支到master分支和dev分支（一旦打了release分支之后不要从dev分支上合并新的改动到Release分支）
> release分支为预发布分支，命名为本次发布的主要功能英文简称
> 
>>release/分支名称
> 
>比如，本次上线蒲公英市集活动的功能，则分支名称可以为release/marketing

- hotfix/*:紧急bug修复分支，该分支只有在紧急情况下使用，从master分支创建，修复完成后需要合并到master分支和dev分支，并master上打一个tag
> bug修复分支的分支名称为bug代码
> > bugfix/分支名称
> 
> > bugfix/分支名称

### Git Flow代码示例
- 创建develop分支
	
	git branch develop  
	git push -u origin develop

- 开始新Feature开发
	git checkout -b some-feature develop  	
	git push -u origin some-feature  
	git status  
	git add some-file  
	git commit  

- 完成Feature

	git pull origin develop  
	git checkout develop  
	git merge --no-ff some-feature  
	git push origin develop  

	git branch -d some-feature  

	git push origin --delete some-feature  
- 开始release

	git checkout -b release-0.1.0 develop

- 完成release

	git checkout master  
	git merge --no-ff release-0.1.0  
	git push  

	git checkout develop  
	git merge --no-ff release-0.1.0  
	git push  

	git branch -d release-0.1.0 
 
	git push origin --delete release-0.1.0 

  
	git tag -a v0.1.0 master  
	git push --tags  
- 开始Hotfix

	git checkout -b hotfix-0.1.1 master

- 完成Hotfix
	
	git checkout master  
	git merge --no-ff hotfix-0.1.1  
	git push  

	git checkout develop  
	git merge --no-ff hotfix-0.1.1  
	git push  

	git branch -d hotfix-0.1.1  

	git tag -a v0.1.1 master  
	git push --tags  

