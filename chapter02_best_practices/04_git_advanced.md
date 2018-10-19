[*Chapter 2 : Best practices in Interactive Computing*](./)
[*第二章：交互计算之最佳实践*](../)

# 2.4. A typical workflow with Git branching
# 2.4. Git分支的典型工作流

A distributed version control system such as Git is designed for the complex and nonlinear workflows that are typical in interactive computing and exploratory research. A central concept is **branching**, which we will discuss in this recipe.
分布式版本控制系统(如Git)是针对交互式计算和探索性研究中典型的复杂和非线性工作流而设计的。一个核心概念是**分支**，我们将在这个参考手册中讨论这个概念。

## Getting ready
## 准备工作

You need to work in a local Git repository for this recipe (see the previous recipe, *Learning the basics of the distributed version control system Git*).
您需要在本地Git存储库中为这个参考手册工作(请参阅前面的参考手册，**学习分布式版本控制系统Git**的基础知识)。

## How to do it...
## 怎么做...

1. We go to the `myproject` repository and we create a new branch named `newidea`:
1. 我们进入`myproject`存储库，创建一个名为`newidea`的新分支:

```bash
pwd
```

```{output:stdout}
/home/cyrille/git/cookbook-2nd/chapter02
```

```bash
cd myproject
```

```bash
git branch newidea
```

```bash
git branch
```

```{output:stdout}
* master
  newidea
```

As indicated by the star `*`, we are still on the master branch.
如星号`*`所示，我们仍然在主分支上。

2. We switch to the newly-created `newidea` branch:
2. 我们切换到新创建的`newidea`分支:

```bash
git checkout newidea
```

```{output:stdout}
Switched to branch 'newidea'
```

```bash
git branch
```

```{output:stdout}
  master
* newidea
```

3. We make changes to the code, for instance, by creating a new file:
3. 例如，通过创建一个新文件，我们对代码进行了更改：

```bash
echo "print('new')" > newfile.py
```

```bash
cat newfile.py
```

```{output:stdout}
print('new')
```

4. We add this file to the staging area and we commit our changes:
4. 我们将此文件添加到暂存区域，并提交更改：

```bash
git add newfile.py
git commit -m "Testing new idea"
```

```{output:stdout}
[newidea 8ebee32] Testing new idea
 1 file changed, 1 insertion(+)
 create mode 100644 newfile.py
```

```bash
ls
```

```{output:stdout}
file.txt  newfile.py
```

5. If we are happy with the changes, we merge the branch to the master branch (the default):
5. 如果我们对更改满意，我们将分支合并到主分支(默认):

```bash
git checkout master
```

```{output:stdout}
Switched to branch 'master'
```

On the master branch, our new file is not there:
在主分支上，我们的新文件不在那里:

```bash
ls
```

```{output:stdout}
file.txt
```

If we merge the new branch into the master branch, the file appears:
如果将新分支合并到主分支中，则文件将显示：

```bash
git merge newidea
```

```{output:stdout}
Updating 045df6a..8ebee32
Fast-forward
 newfile.py | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 newfile.py
```

```bash
ls
```

```{output:stdout}
file.txt  newfile.py
```

6. If we are not happy with the changes, we can just delete the branch, and the new file will be deleted. Here, since we have just merged the branch, we need to undo the last commit:
6. 如果我们对修改不满意，我们可以删除分支，新的文件将被删除。在这里，由于我们刚刚合并了分支，我们需要撤销最后一次提交:

```bash
git reset --hard HEAD~1
```

```{output:stdout}
HEAD is now at 045df6 Add exclamation mark to file.txt
```

We are still on the master branch, but before we merged the `newidea` branch:
我们还在主分支上，但在合并`newidea`分支之前:

```bash
git branch
```

```{output:stdout}
* master
  new idea
```

We can delete the branch as follows:
我们可以删除以下分支:

```bash
git branch -D newidea
```

```{output:stdout}
Deleted branch newidea (was 8ebee32).
```

The Python file is gone:
Python文件不见了：

```bash
ls
```

```{output:stdout}
file.txt
```

7. It may happen that while we are halfway through some work, we need to make some other change in another commit or another branch. We could commit our half-done work, but this is not ideal. A better idea is to stash our working copy in a secure location so that we can recover all of our uncommitted changes later. We save our uncommitted changes with the following command:
7. 当我们完成一些工作时，可能会发生这样的情况，我们需要在另一个commit或另一个分支中进行一些其他更改。我们可以完成一半的工作，但这并不理想。更好的方法是将工作副本存储在一个安全的位置，以便稍后可以恢复所有未提交的更改。我们用以下命令保存未提交的更改:

```bash
echo "new line" >> file.txt
```

```bash
cat file.txt
```

```{output:stdout}
Hello world!
new line
```

```bash
git stash
```

```{output:stdout}
Saved working directory and index state WIP on master:
045df6a Add exclamation mark to file.txt
HEAD is now at 045df6 Add exclamation mark to file.txt
```

```bash
cat file.txt
```

```{output:stdout}
Hello world!
```

We can do anything we want with the repository: checkout a branch, commit changes, pull or push from a remote repository, and so on. When we want to recover our uncommitted changes, we type the following command:
对于存储库，我们可以做任何我们想做的事情:签出分支、提交更改、从远程存储库提取或推送等等。当我们想要恢复未提交的更改时，我们输入以下命令:

```bash
git stash pop
```

```{output:stdout}
On branch master
Changes not staged for commit:

    modified:   file.txt

no changes added to commit
    (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (c9071a)
```

```bash
cat file.txt
```

```{output:stdout}
Hello world!
new line
```

We can have several stashed states in the repository. More information about stashing can be found with `git stash --help`.
我们可以在存储库中存储多个状态。有关存储的更多信息可以在`git stash—help`中找到。

## How it works...
## 它是如何工作的.。

Let's imagine that in order to test a new idea, you need to make non-trivial changes to your code in multiple files. You create a new branch, test your idea, and end up with a modified version of your code. If this idea was a dead end, you switch back to the original branch of your code. However, if you are happy with the changes, you **merge** it into the main branch.
让我们想象一下，为了测试一个新的想法，您需要对多个文件中的代码进行一些重要的更改。您创建一个新分支，测试您的想法，最后得到一个修改过的代码版本。如果这个想法是死胡同的话，你可以切换回原来的代码分支。但是，如果您对这些更改感到满意，那么您将其合并到主分支中。

The strength of this workflow is that the main branch can evolve independently from the branch with the new idea. This is particularly useful when multiple collaborators are working on the same repository. However, it is also a good habit to have, even when there is a single contributor.
该工作流的优点在于，主分支可以独立于分支进化。并具有新的思想。当多个协作者在同一个存储库上工作时，这一点尤其有用。然而，这也是一个好习惯，即使有一个单一的贡献者。

Merging is not always a trivial operation, as it can involve two divergent branches with potential conflicts. Git tries to resolve conflicts automatically, but it is not always successful. In this case, you need to resolve the conflicts manually.
合并并不总是一个简单的操作，因为它可能涉及两个可能存在冲突的分支。Git试图自动解决冲突，但并不总是成功的。在这种情况下，您需要手动解决冲突。

An alternative to merging is **rebasing**, which is useful when the main branch has changed while you were working on your branch. Rebasing your branch on the main branch allows you to move your branching point to a more recent point. This process may require you to resolve conflicts.
合并的另一种替代方法是**rebasing**，当您在处理分支时主分支发生更改时，这很有用。将分支重新基于主分支，可以将分支点移动到最近的点。这个过程可能需要您解决冲突。

Git branches are lightweight objects. Creating and manipulating them is cheap. They are meant to be used frequently. It is important to perfectly grasp all related notions and Git commands (notably `checkout`, `merge`, and `rebase`). The previous recipe contains many references.
Git分支是轻量级对象。创建和操作它们代价很小。它们应该经常使用。完美地掌握所有相关的概念和Git命令(特别是`checkout`、`merge`和`rebase`)非常重要。前面的参考手册包含了许多参考资料。

## There's more...
## 还有更多...

Many people have thought about effective workflows. For example, a common but complex workflow, called git-flow, is described at http://nvie.com/posts/a-successful-git-branching-model/. However, it may be preferable to use a simpler workflow in small and mid-size projects, such as the one described at http://scottchacon.com/2011/08/31/github-flow.html. The latter workflow elaborates on the simplistic example shown in this recipe.
许多人都考虑过有效的工作流程。例如，在http://nvie.com/posts/a-success -git-branch -model/中描述了一个常见但复杂的工作流，称为git-flow。但是，在中小型项目中使用更简单的工作流可能更好，例如http://scottchacon.com/2011/08/31/github-flow.html。后一个工作流详细介绍了这个参考手册中所示的简单示例。

A related notion to branching is **forking**. There can be multiple copies of the same repository on different servers. Imagine that you want to contribute to IPython's code stored on GitHub. You probably don't have the permission to modify their repository, but you can make a copy into your personal account—this is called forking. In this copy, you can create a branch and propose a new feature or a bug fix. Then, you can propose the IPython developers to merge your branch into their master branch with a **pull request**. They can review your changes, propose suggestions, and eventually merge your work (or not). GitHub is built around this idea and thereby offers a clean way to collaborate on open source projects.
与分支相关的一个概念是**forking**。在不同的服务器上可以有相同存储库的多个副本。假设您希望对存储在GitHub上的IPython代码作出贡献。您可能没有修改其存储库的权限，但是您可以将其复制到您的个人帐户中--这称为分叉。在这个副本中，您可以创建一个分支，并提出一个新特性或bug修复。然后，您可以建议IPython开发人员使用**pull request**将分支合并到主分支中。他们可以检查您的变更，提出建议，并最终合并您的工作(或不合并)。GitHub就是围绕着这个想法构建的，因此它提供了一种在开源项目上进行协作的干净方式。

Performing code reviews before merging pull requests leads to higher code quality in a collaborative project. When at least two people review any piece of code, the probability of merging bad or wrong code is reduced.
在合并pull请求之前执行代码审查，可以提高协作项目中的代码质量。当至少有两个人检查某段代码时，合并错误或错误代码的可能性就降低了。

There is, of course, much more to say about Git. Version control systems are complex and quite powerful in general, and Git is no exception. Mastering Git requires time and experimentation. The previous recipe contains many excellent references.
当然，关于Git还有更多要说的。一般来说，版本控制系统是复杂而强大的，Git也不例外。掌握Git需要时间和实验。前面的参考手册包含了许多优秀的参考资料。

Here are a few further references about branches and workflows:
下面是一些关于分支和工作流的进一步参考：

* Git workflows available at http://www.atlassian.com/git/workflows
* Git工作流 at http://www.atlassian.com/git/workflows
* Learn Git branching at http://pcottle.github.io/learnGitBranching/
* 学习Git分支 at http://pcottle.github.io/learnGitBranching/
* The Git workflow recommended on the NumPy project (and others), described at http://docs.scipy.org/doc/numpy/dev/gitwash/development_workflow.html
* 对NumPy项目(和其他项目)推荐的Git工作流进行了描述 at http://docs.scipy.org/doc/numpy/dev/gitwash/development_workflow.html
* A post on the IPython mailing list about an efficient Git workflow, by Fernando Perez, available at http://mail.scipy.org/pipermail/ipython-dev/2010-October/006746.html
* 费尔南多•佩雷斯(Fernando Perez)在IPython邮件列表中发布了一篇关于高效Git工作流的文章 at http://mail.scipy.org/pipermail/ipython-dev/2010-October/006746.html

## See also
## 另请参阅

* Learning the baics of the distributed version control system Git
* 学习分布式版本控制系统Git基础
