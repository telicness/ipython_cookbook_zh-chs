; [*Chapter 2 : Best practices in Interactive Computing*](./)
[*第二章：交互计算之最佳实践*](../)

; # 2.1. Learning the basics of the Unix shell
# 2.1. 学习Unix shell的基础知识

; Learning how to interact with the operating system using a command-line interface (or terminal) is a required skill in interactive computing and data analysis. We will use a command-line interface in most recipes of this book. IPython and the Jupyter Notebook are typically launched from a terminal. Installing Python packages is typically done from a terminal.
在交互式计算和数据分析中，学习如何使用命令行接口(或终端)与操作系统交互是必需的技能。我们将在本书的大多数参考手册中使用命令行界面。IPython和Jupyter Notebook一般从终端发射。安装Python包通常是在终端上完成的。

; In this recipe, we will show the very basics of the Unix shell, which is natively available in Linux distributions (such as Debian, Ubuntu, and so on) and macOS. On Windows 10, one can install the **Windows Subsystem for Linux**, a command-line interface to a Unix subsystem integrated with the Windows operating system (see https://docs.microsoft.com/windows/wsl/about).
在这个参考手册中，我们将展示Unix shell的基本知识，它在Linux发行版(如Debian、Ubuntu等)和macOS中都可以直接使用。在Windows 10上，您可以为Linux**安装**Windows子系统，这是与Windows操作系统集成的Unix子系统的命令行接口(参见https://docs.microsoft.com/windows/wsl/about)。

; ## Getting ready
## 准备工作

; Here are the instructions to open a Unix shell on macOS, Linux, and Windows. **bash** is the most common Unix shell and this is what we will use in this recipe.
下面是在macOS、Linux和Windows上打开Unix shell的说明。**bash**是最常见的Unix shell，我们将在此参考手册中使用它。

; On macOS, bring up the Spotlight Search, type `terminal`, and press Enter.
在MacOS上，打开Spotlight搜索，键入`Terminal`，然后按Enter键。

; On Windows, follow the instructions at https://docs.microsoft.com/en-us/windows/wsl/install-win10. Then, open the Windows menu, type `bash`, and press Enter.
在Windows上，遵循https://docs.microsoft.com/en-us/windows/wsl/install-win10.的说明。然后打开Windows菜单，输入`bash`，然后按回车。

; On Linux, open the Dash by clicking on the top-left icon on the desktop, type `terminal`, and open the `Terminal` application.
在linux上，单击桌面上的左上角图标，键入`Terminal`，然后打开`Terminal‘应用程序来打开Dash。

; If you want to run this notebook in Jupyter, you need to install `bash_kernel`, available at https://github.com/takluyver/bash_kernel. Open a terminal and type `pip install bash_kernel && python -m bash_kernel.install`.
如果您想在Jupyter中运行这个NoteBook，您需要安装`bash_kernel`，可在https://github.com/takluyver/bash_kernel中找到。打开终端，输入`pip install bash_kernel && python -m bash_kernel.install`。

; This will install a bash kernel in Jupyter, and it will allow you to run this recipe's code directly in the Notebook.
这将在Jupyter中安装一个bash内核，并允许您直接在NoteBook中运行此参考手册的代码。

; ## How to do it...
## 怎么做...

; The Unix shell comes with hundreds of commands. We will see the most common ones in this recipe.
Unix Shell附带了数百条命令。我们会看到这个参考手册中最常见的。

; 1. The terminal lets us write text commands with the keyboard. We execute them by pressing Enter, and the output is displayed below the command. The **working directory** is the directory of our file system that is currently "active" in the terminal. We can get the absolute path of the working directory as follows:
1. 终端让我们用键盘写文本命令。我们通过按回车键执行，输出显示在命令下面。**工作目录**是当前在终端中`活动`的文件系统的目录。我们可以得到工作目录的绝对路径如下:

```bash
pwd
```

```{output:stdout}
~/git/cookbook-2nd/chapter02_best_practices
```

> the dollar `$` sign must not be typed: it is typically used by the shell to indicate where the user can start typing. The information written before it may show the user name, the computer name, and part of the working directory. Here, only the three characters `pwd` should be typed before pressing Enter.
>  不能键入`$`符号:shell通常使用它来指示用户可以在何处开始键入。在此之前编写的信息可能显示用户名、计算机名和工作目录的一部分。在这里，在按回车键之前，应该只输入三个字符`pwd`。

; 2. We can list all files and subdirectories in the working directory as follows:
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

; The `-l` option displays the directory contents as a detailed list, showing the permissions and owner of the files, the file sizes, and the last modified dates. Most shell commands come with many options that alter their behavior and that can be arbitrarily combined.
`-l`选项将目录内容显示为详细列表，显示文件的权限和所有者、文件大小以及最后修改的日期。大多数shell命令都带有许多选项，这些选项可以改变它们的行为，并且可以任意组合。

; 3. We use the `cd` command to navigate between subdirectories. The current directory is named `.` (single dot), and the parent directory is named `..` (double dot):
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

; 4. Paths can be specified as relative (depending on a reference directory, generally the working directory) or absolute. The **home directory**, specified as `~`, contains the user's personal files. Configuration files are often stored in a directory like `~/.program_name`. For example, `~/.ipython` contains configuration files of IPython:
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

; > in most terminals, we can use the arrow keys on the keyboard to navigate in the history of past commands. Also, the Tab key enables tab completion, which automatically completes the first characters of a command or a file. For example, typing `ls -la ~/.ipy` and pressing Tab would automatically complete to `ls -la ~/.ipython`, or it would present the list of possible options if there are several files or directories that begin with `~/.ipy`.
> 在大多数终端中，我们可以使用键盘上的箭头键在过去的命令历史中导航。此外，Tab键启用选项卡完成，它自动完成命令或文件的第一个字符。例如，键入`ls-la~/.ipy`并按Tab将自动完成为`ls-la~/.ipython`，或者如果有几个以`~/.ipy‘开头的文件或目录，它将显示可能的选项列表。

; 5. We can create, move, rename, copy, delete files and directories from the terminal:
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

; > The `rm` command lets us delete files and directories. The `rm -rf path` deletes the given path recursively, even if subdirectories are not empty. It is an extremely dangerous command as it cannot be undone: the files are immediately and permanently deleted, they do not go into a trash directory first. See https://github.com/sindresorhus/guides/blob/master/how-not-to-rm-yourself.md for more details.
> `rm`命令允许我们删除文件和目录。`rm-rf路径`递归删除给定路径，即使子目录不是空的。这是一个非常危险的命令，因为它无法撤消：文件被立即永久删除，它们不会首先进入垃圾目录。有关更多细节，请参见https：/github.com/sindsorhus/Guide/blob/master/How-Not-to-Rm-you.md。

; 6. There are several useful commands to deal with text files:
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
; # We redirect the output of a command to
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

; Several command-line text editors are available, such as `pico`, `nano`, or `vi`. Learning these text editors requires time and effort, especially vi.
有几个命令行文本编辑器可用，例如`pico`、`nano`或`vi`。学习这些文本编辑器需要时间和精力，特别是vi。

; 7. The `grep` command lets us search substrings in text. In the following example, we find all instances of `Unix` followed by a word (using regular expressions):
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

; 8. A major strength of the Unix shell is that commands can be combined with **pipes**: the output of one command can be directly transferred to the input of another command:
8. Unix Shell的一个主要优点是可以将命令与**管道**组合起来：一个命令的输出可以直接传输到另一个命令的输入：

```bash
echo "This is a Unix shell" | grep -Eo "Unix \w+"
```

```{output:stdout}
Unix shell
```

; ## There's more...
## 还有更多...

; We only scratched the surface of the Unix shell in this recipe. There are many other commands that can be combined in an infinite number of ways. Many repetitive tasks that would take hours of manual work can be done in a few minutes by writing the appropriate commands. Mastering the Unix shell may take a lot of effort, but it leads to dramatic time gains in the long term.
在这个参考手册中，我们只触及了Unix shell的皮毛。有许多其他命令可以以无数种方式组合在一起。许多重复性的工作需要几个小时的手工工作，通过编写适当的命令可以在几分钟内完成。掌握Unix shell可能需要付出很多努力，但从长远来看，它会带来巨大的时间收益。

; Here are a few references:
以下是一些参考资料：

; * Linux tutorial at https://ryanstutorials.net/linuxtutorial/
* Linux教程 at https://ryanstutorials.net/linuxtutorial/
; * Bash commands at https://ss64.com/bash/
* Bash命令 at https://ss64.com/bash/
; * Learn Bash in Y minutes, at https://learnxinyminutes.com/docs/bash/
* 在Y分钟内学会Bash， at https://learnxinyminutes.com/docs/bash/
; * Learn the shell interactively, at http://www.learnshell.org/
* 交互式地学习shell， at http://www.learnshell.org/
; * The fish shell, at https://fishshell.com/
* 鱼壳， at https://fishshell.com/
; * xonsh, a Python-powered shell, at http://xon.sh/
* xonsh，一个由Python驱动的外壳， at http://xon.sh/
; * Windows Subsystem for Linux, at https://docs.microsoft.com/windows/wsl/about
* 用于Linux的Windows子系统， at https://docs.microsoft.com/windows/wsl/about

; ## See also
## 另请参阅

; * Ten tips for conducting reproducible interactive computing experiments
* 进行可重复的交互式计算实验的十个技巧
