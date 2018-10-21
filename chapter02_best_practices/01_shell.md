[*第二章：交互计算之最佳实践*](../)

# 2.1. 学习Unix shell的基础知识

在交互式计算和数据分析中，学习如何使用命令行接口(或终端)与操作系统交互是必需的技能。我们将在本书的大多数参考手册中使用命令行界面。IPython和Jupyter Notebook一般从终端发射。安装Python包通常是在终端上完成的。

在这个参考手册中，我们将展示Unix shell的基本知识，它在Linux发行版(如Debian、Ubuntu等)和macOS中都可以直接使用。在Windows 10上，您可以为Linux**安装**Windows子系统，这是与Windows操作系统集成的Unix子系统的命令行接口(参见https://docs.microsoft.com/windows/wsl/about)。

## 准备工作

下面是在macOS、Linux和Windows上打开Unix shell的说明。**bash**是最常见的Unix shell，我们将在此参考手册中使用它。

在MacOS上，打开Spotlight搜索，键入`Terminal`，然后按Enter键。

在Windows上，遵循https://docs.microsoft.com/en-us/windows/wsl/install-win10.的说明。然后打开Windows菜单，输入`bash`，然后按回车。

在linux上，单击桌面上的左上角图标，键入`Terminal`，然后打开`Terminal‘应用程序来打开Dash。

如果您想在Jupyter中运行这个NoteBook，您需要安装`bash_kernel`，可在https://github.com/takluyver/bash_kernel中找到。打开终端，输入`pip install bash_kernel && python -m bash_kernel.install`。

这将在Jupyter中安装一个bash内核，并允许您直接在NoteBook中运行此参考手册的代码。

## 怎么做...

Unix Shell附带了数百条命令。我们会看到这个参考手册中最常见的。

1. 终端让我们用键盘写文本命令。我们通过按回车键执行，输出显示在命令下面。**工作目录**是当前在终端中`活动`的文件系统的目录。我们可以得到工作目录的绝对路径如下:

```bash
pwd
```

```{output:stdout}
~/git/cookbook-2nd/chapter02_best_practices
```

>  不能键入`$`符号:shell通常使用它来指示用户可以在何处开始键入。在此之前编写的信息可能显示用户名、计算机名和工作目录的一部分。在这里，在按回车键之前，应该只输入三个字符`pwd`。

2. 我们可以按以下方式列出工作目录中的所有文件和子目录：

```bash
ls
```

```{output:stdout}
00_intro.md  03_git.md           07_high_quality.md
01_shell.md  04_git_advanced.md  08_test.md
02_py3       05_workflows.md     09_debugging.md
02_py3.md    06_tips.md          images
```

```bash
ls -l
```

```{output:stdout}
total 100
-rw-rw-r-- 1 owner   769 Dec 12 10:23 00_intro.md
-rw-rw-r-- 1 owner  2473 Dec 12 14:21 01_shell.md
...
-rw-rw-r-- 1 owner  9390 Dec 12 11:46 08_test.md
-rw-rw-r-- 1 owner  5032 Dec 12 10:23 09_debugging.md
drwxrwxr-x 2 owner  4096 Aug  1 16:49 images
```

`-l`选项将目录内容显示为详细列表，显示文件的权限和所有者、文件大小以及最后修改的日期。大多数shell命令都带有许多选项，这些选项可以改变它们的行为，并且可以任意组合。

3. 我们使用`cd`命令在子目录之间导航。当前目录名为`.`(单点)，父目录名为`..`(双点)：

```bash
cd images
```

```bash
pwd
```

```{output:result}
~/git/cookbook-2nd/chapter02_best_practices/images
```

```bash
ls
```

```{output:stdout}
folder.png  github_new.png
```

```bash
cd ..
```

```bash
pwd
```

```{output:result}
~/git/cookbook-2nd/chapter02_best_practices
```

4. 路径可以指定为相对路径(取决于引用目录，通常是工作目录)或绝对路径。指定为`~‘的**主目录**包含用户的个人文件。配置文件通常存储在`~/.Programname‘这样的目录中。例如，`~/.ipyth`包含IPython的配置文件：

```bash
ls -la ~/.ipython
```

```{output:stdout}
total 20
drwxr-xr-x  5 cyrille 4096 Nov 14 16:16 .
drwxr-xr-x 93 cyrille 4096 Dec 12 10:50 ..
drwxr-xr-x  2 cyrille 4096 Nov 14 16:16 extensions
drwxr-xr-x  2 cyrille 4096 Nov 14 16:16 nbextensions
drwxr-xr-x  7 cyrille 4096 Dec 12 14:18 profile_default
```

> 在大多数终端中，我们可以使用键盘上的箭头键在过去的命令历史中导航。此外，Tab键启用选项卡完成，它自动完成命令或文件的第一个字符。例如，键入`ls-la~/.ipy`并按Tab将自动完成为`ls-la~/.ipython`，或者如果有几个以`~/.ipy‘开头的文件或目录，它将显示可能的选项列表。

5. 我们可以从终端创建、移动、重命名、复制、删除文件和目录：

```bash
# We create an empty directory:
mkdir md_files
# We copy all Markdown files into the new directory:
cp *.md md_files
# We rename the directory:
mv md_files markdown_files
ls markdown_files
```

```{output:stdout}
00_intro.md         05_workflows.md
01_shell.md         06_tips.md
02_py3.md           07_high_quality.md
03_git.md           08_test.md
04_git_advanced.md  09_debugging.md
```

```bash
rmdir markdown_files
```

```{output:stdout}
rmdir: failed to remove 'markdown_files':
    Directory not empty
```

```bash
rm markdown_files/*
```

```bash
rmdir markdown_files
```

> `rm`命令允许我们删除文件和目录。`rm-rf路径`递归删除给定路径，即使子目录不是空的。这是一个非常危险的命令，因为它无法撤消：文件被立即永久删除，它们不会首先进入垃圾目录。有关更多细节，请参见https：/github.com/sindsorhus/Guide/blob/master/How-Not-to-Rm-you.md。

6. 有几个有用的命令来处理文本文件:

```bash
# Show the first three lines of a text file:
head -n 3 01_shell.md
```

```{output:stdout}
# Learning the basics of the Unix shell

Learning how to interact with the operating system (...)
```

```bash
# Show the last line of a text file:
tail -n 1 00_intro.md
```

```{output:stdout}
We will also cover more general topics (...)
```

```bash
# We display some text:
echo "Hello world!"
```

```{output:stdout}
Hello world!
```

```bash
# We redirect the output of a command to
# a text file with `>`:
echo "Hello world!" > myfile.txt
```

```bash
# We display the entire contents of the file:
cat myfile.txt
```

```{output:stdout}
Hello world!
```

有几个命令行文本编辑器可用，例如`pico`、`nano`或`vi`。学习这些文本编辑器需要时间和精力，特别是vi。

7. `grep`命令允许我们在文本中搜索子字符串。在下面的示例中，我们发现`unix`的所有实例后面跟着一个单词(使用正则表达式)：

```bash
grep -Eo "Unix \w+" 01_shell.md
```

```{output:stdout}
Unix shell
Unix shell
Unix subsystem
Unix shell
(...)
Unix shell
Unix shell
```

8. Unix Shell的一个主要优点是可以将命令与**管道**组合起来：一个命令的输出可以直接传输到另一个命令的输入：

```bash
echo "This is a Unix shell" | grep -Eo "Unix \w+"
```

```{output:stdout}
Unix shell
```

## 还有更多...

在这个参考手册中，我们只触及了Unix shell的皮毛。有许多其他命令可以以无数种方式组合在一起。许多重复性的工作需要几个小时的手工工作，通过编写适当的命令可以在几分钟内完成。掌握Unix shell可能需要付出很多努力，但从长远来看，它会带来巨大的时间收益。

以下是一些参考资料：

* Linux教程 at https://ryanstutorials.net/linuxtutorial/
* Bash命令 at https://ss64.com/bash/
* 在Y分钟内学会Bash， at https://learnxinyminutes.com/docs/bash/
* 交互式地学习shell， at http://www.learnshell.org/
* 鱼壳， at https://fishshell.com/
* xonsh，一个由Python驱动的外壳， at http://xon.sh/
* 用于Linux的Windows子系统， at https://docs.microsoft.com/windows/wsl/about

## 另请参阅

* 进行可重复的交互式计算实验的十个技巧
