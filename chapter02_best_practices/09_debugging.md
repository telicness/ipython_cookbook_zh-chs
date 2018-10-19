[*Chapter 2 : Best practices in Interactive Computing*](./)
[*第二章：交互计算之最佳实践*](../)

# 2.9. Debugging code with IPython
# 2.9. 使用IPython调试代码


Debugging is an integral part of software development and interactive computing. A widespread debugging technique consists of placing `print()` functions in various places in the code. Who hasn't done this? It is probably the simplest solution, but it is certainly not the most efficient (it is the poor man's debugger).
调试是软件开发和交互计算的重要组成部分。一种广泛的调试技术是在代码中的不同位置放置`print()`函数。谁没做过这件事? 这可能是最简单的解决方案，但肯定不是最有效的(这是穷人的调试器)。

IPython is perfectly adapted for debugging, and the integrated debugger is quite easy to use (actually, IPython merely offers a nice interface to the native Python debugger **pdb**). In particular, tab completion works in the IPython debugger. This recipe describes how to debug code with IPython.
IPython非常适合调试，集成调试器非常容易使用(实际上，IPython只是为本地Python调试器**PDB**提供了一个很好的接口)。特别是，选项卡完成在IPython调试器中工作。此配方描述如何使用IPython调试代码。

## How to do it...
## 怎么做...

There are two not-mutually exclusive ways of debugging code in Python. In the post-mortem mode, the debugger steps into the code as soon as an exception is raised so that we can investigate what caused it. In the step-by-step mode, we can stop the interpreter at a breakpoint and resume its execution step by step. This process allows us to check carefully the state of our variables as our code is executed.
在Python中有两种非互斥的调试代码的方法。在事后分析模式中，调试器在引发异常时就会进入代码，这样我们就可以调查是什么导致了异常。在分步模式中，我们可以在断点处停止解释器，并逐步恢复其执行。这个过程允许我们在执行代码时仔细检查变量的状态。

Both methods can actually be used simultaneously; we can do step-by-step debugging in the post-mortem mode.
两种方法实际上可以同时使用;我们可以在事后分析模式下进行逐步调试。

### The post-mortem mode
### 事后模式

When an exception is raised within IPython, execute the `%debug` magic command to launch the debugger and step into the code. Also, the `%pdb on` command tells IPython to launch the debugger automatically as soon as an exception is raised.
当在IPython中引发异常时，执行`%%debug`魔法命令来启动调试器并进入代码。此外，`%pdb on`命令告诉IPython，在出现异常时自动启动调试器。

Once you are in the debugger, you have access to several special commands, the most important ones being listed here:
一旦进入调试器，您就可以访问几个特殊的命令，其中最重要的命令列在这里:

* `p varname` **prints** the value of a variable
* `p varname`**打印**变量的值
* `w` shows your current location within the stack
* `w`显示堆栈中的当前位置
* `u` goes **up** in the stack
* `u` 进入**up**在堆栈中
* `d` goes **down** in the stack
* `u` 进入**down**在堆栈中
* `l` shows the **lines** of code around your current location
* `l` 表示围绕当前位置的**行**代码
* `a` shows the **arguments** of the current function
* `a`显示当前函数的**参数**

The call stack contains the list of all active functions at a given location in the code's execution. You can easily navigate up and down the stack to inspect the values of the function arguments. Although quite simple to use, this mode should let you resolve most of your bugs. For more complex problems, you may need to do step-by-step debugging.
调用堆栈包含代码执行过程中给定位置的所有活动函数的列表。您可以轻松地向上和向下浏览堆栈，以检查函数参数的值。虽然使用起来很简单，但是这种模式应该可以解决大多数bug。对于更复杂的问题，您可能需要进行逐步调试。

### Step-by-step debugging
### 单步调试

You have several options to start the step-by-step debugging mode. First, in order to put a breakpoint somewhere in your code, insert the following command:
您有几个选项可以开始单步调试模式。首先，为了在代码中的某个地方放置一个断点，请插入以下命令：

```
import pdb
pdb.set_trace()
```

Second, you can run a script from IPython with the following command:
其次，可以使用以下命令从IPython运行脚本：

```
%run -d -b extscript.py:20 script
```

This command runs the `script.py` file under the control of the debugger with a breakpoint on line 20 in `extscript.py` (which is imported by `script.py`). Finally, you can do step-by-step debugging as soon as you are in the debugger.
这个命令在调试器的控制下运行`script.py`文件，其中第20行在`extscript.py`(由`script.py`导入)中有一个断点。最后，您可以在调试器中一步地调试.

Step-by-step debugging consists of precisely controlling the course of the interpreter. Starting from the beginning of a script or from a breakpoint, you can resume the execution of the interpreter with the following commands:
单步调试包括精确控制解释器的运行过程.从脚本开始或从断点开始，您可以使用以下命令继续执行解释器：

* `s` executes the current line and stops as soon as possible afterwards (step-by-step debugging, that is, the most fine-grained execution pattern)
* `s` 执行当前行，然后尽快停止(单步调试，也就是最细粒度的执行模式)。
* `n` continues the execution until the **next** line in the current function is reached
* `N` 继续执行，直到到达当前函数中的**Next**行为止
* `r` continues the execution until the current function **returns**
* `r` 继续执行，直到当前函数**返回**为止
* `c` **continues** the execution until the next breakpoint is reached
* `c `**继续执行**，直到到达下一个断点为止
* `j 30` brings you to line 30 in the current file
* `j 30`将在当前文件中显示第30行

You can add breakpoints dynamically from within the debugger using the `b` command or with `tbreak` (temporary breakpoint). You can also clear all or some of the breakpoints, enable or disable them, and so on. You can find the full details of the debugger at https://docs.python.org/3/library/pdb.html.
您可以在调试器中使用`b`命令或使用`t以外`(临时断点)动态添加断点。您还可以清除所有或部分断点，启用或禁用它们，等等。您可以在https://docs.python.org/3/library/pdb.html.上找到调试器的详细信息。

## There's more...
## 还有更多...

To debug your code with IPython, you typically need to execute it first with IPython, for example, with `%run`. However, you may not always have an easy way of doing this. For instance, your program may run with a custom command-line Python script, it may be launched by a complex bash script, or it may be integrated within a GUI. In these cases, you can embed an IPython interpreter at any point in your code (launched by Python), instead of running your whole program with IPython (which may be overkill if you just need to debug a small portion of your code).
要使用IPython调试代码，通常需要首先使用IPython执行它，例如，使用`%run`。然而，您可能并不总是有一个简单的方法来做到这一点。例如，您的程序可以使用定制的命令行Python脚本运行，可以使用复杂的bash脚本启动，或者集成到GUI中。在这些情况下，您可以在代码中的任何位置嵌入一个IPython解释器(由Python启动)，而不是使用IPython运行整个程序(如果您只需要调试一小部分代码，那么使用IPython运行整个程序可能有些过火)。

To embed IPython within your program, simply insert the following commands somewhere in your code:
要在程序中嵌入IPython，只需在代码中插入以下命令:

```
from IPython import embed
embed()
```

When your Python program reaches this code, it will pause and launch an interactive IPython terminal at this specific point. You will then be able to inspect all local variables, run any code you want, and possibly debug your code before resuming normal execution.
当Python程序到达此代码时，它将暂停并在此特定点启动交互式IPython终端。然后，您将能够检查所有局部变量，运行任何您想要的代码，并可能在恢复正常执行之前调试您的代码。

Most Python IDEs offer graphical debugging features (see the *Efficient interactive computing workflows with IPython* recipe). A GUI can sometimes be more convenient than a command-line debugger. A list of Python debuggers is available at https://wiki.python.org/moin/PythonDebuggingTools.
大多数Python ide都提供图形化调试功能(请参阅带有IPython**参考手册的**高效交互计算工作流)。GUI有时比命令行调试器更方便。Python调试器列表可以在https://wiki.python.org/moin/PythonDebuggingTools找到。

