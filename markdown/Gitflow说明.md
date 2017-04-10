# Gitflow说明 #

Gitflow工作流为功能开发，发布准备和维护这三个分配了独立的分支。它定义了一个围绕项目发布的严格流程。它将项目开发过程分配在独立的分支中。

它包含几个重要的分支：

1、 主分支和开发分支

> master ，发布的分支
> develop ，功能开发的分支

这两个分支共同包含了项目开发的历史，其中master只包括发布的历史，而develop分支包含了功能的所有开发历史；

2、功能分支

基于develop分支，前缀为feature/，是属于具体的开发功能的分支，新功能开发完之后，merge到develop上，从来不和master分支交互。

3、发布分支

当需要发布的时候，基于develop新建一个发布分支，前缀为release/，开始一个发布流程，当一切工作完成之后，将分支合并到master和develop，并且将master搭上Tag。

4、维护分支

当master分支有bug时，基于master创建一个维护分支，前缀为hotfix/，用于快速修复错误，完毕之后合并到master和develop，然后将master分支打上Tag

