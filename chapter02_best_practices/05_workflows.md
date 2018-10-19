[*Chapter 2 : Best practices in Interactive Computing*](./)
[*第二章：交互计算之最佳实践*](../)

# 2.5. Efficient interactive computing workflows with IPython
# 2.5. 基于IPython的高效交互计算工作流

There are multiple ways of using IPython for interactive computing. Some of them are better in terms of flexibility, modularity, reusability, and reproducibility. We will review and discuss them in this recipe.
使用IPython进行交互计算有多种方法。其中一些在灵活性、模块化、可重用性和可重现性方面更好。我们将在这个参考手册中回顾和讨论它们。

Any interactive computing workflow is based on the following cycle:
任何交互式计算工作流都基于以下周期：

* Write some code
* 编写一些代码
* Execute it
* 执行它
* Interpret the results
* 解释结果
* Repeat
* 重复

This fundamental loop (also known as **Read-Eval-Print Loop** or **REPL**) is particularly useful when doing exploratory research on data or model simulations, or when building a complex algorithm step by step. A more classical workflow (the edit-compile-run-debug loop) would consist of writing a full-blown program, and then performing a complete analysis. This is generally more tedious. It is more common to build an algorithmic solution iteratively, by doing small-scale experiments and tweaking the parameters, and this is precisely what interactive computing is about.
这个基本循环(也称为**Read-Eval-Print Loop**或**REPL**)在对数据或模型模拟进行探索性研究或逐步构建复杂算法时特别有用。一个更经典的工作流(编辑-编译-运行-调试循环)将包括编写一个完整的程序，然后执行一个完整的分析。这通常是比较乏味的。通过进行小规模的实验和调整参数来迭代地构建一个算法解决方案更为常见，而这正是交互计算的意义所在。

**Integrated Development Environments (IDEs)**, providing comprehensive facilities for software development (such as a source code editor, compiler, and debugger), are widely used for classical workflows. However, when it comes to interactive computing, alternatives to IDEs exist. We will review them here.
**集成开发环境(IDE)**为软件开发提供了全面的便利(例如源代码编辑器、编译器和调试器)，在经典工作流中广泛使用。然而，当涉及到交互计算时，IDE的替代方案是存在的。我们将在这里回顾它们。

## How to do it...
## 怎么做...

Here are a few possible workflows for interactive computing, by increasing order of complexity. Of course, IPython is at the core of all of these methods.
这里有一些可能用于交互计算的工作流，通过增加复杂性的顺序。当然，IPython是所有这些方法的核心。

### The IPython terminal
### IPython终端

IPython is the de facto standard for interactive computing in Python. The IPython terminal (the `ipython` command) offers a command-line interface specifically designed for REPLs. It is a much more powerful tool than the native Python interpreter (the `python` command). The IPython terminal is a convenient tool for quick experiments, simple shell interactions, and to find help. Forgot the input arguments of NumPy's `savetxt` function? Just type in `numpy.savetxt?` in IPython (you will first need to use import numpy, of course). Some people even use the IPython terminal as a (sophisticated) calculator!
IPython是Python中交互计算的事实上的标准。IPython终端(`ipython`命令)提供了专门为REPL设计的命令行接口。它是一个比本机Python解释器(`python`命令)更强大的工具。IPython终端是一个方便的工具，用于快速实验、简单的shell交互和查找帮助。忘记了NumPy的`Savetxt`函数的输入参数? 只需在IPython中键入`numpy.savetxt? `(当然，您首先需要使用import numpy)。有些人甚至使用IPython终端作为(复杂的)计算器！

Yet, the terminal quickly becomes limited when it is used alone. The main issue is that the terminal is not a code editor, and thus entering more than a few lines of code can be inconvenient. Fortunately, there are various ways of solving this problem, as detailed in the following sections.
然而，当终端单独使用时，它很快就会受到限制。主要问题是终端不是代码编辑器，因此输入几行以上的代码可能会不方便。幸运的是，解决这个问题的方法有很多种，详见下面几节。

### IPython and text editor
### IPython和文本编辑器

The simplest solution to the not-a-text-editor problem is to use IPython along with a text editor. The `%run` magic command then becomes the central tool in this workflow:
解决非文本编辑器问题的最简单的解决方案是使用IPython和文本编辑器。`%%run`魔法命令随后成为此工作流中的中心工具：

* Write some code in your favorite text editor and save it in a `myscript.py` Python script file.
* 在您最喜欢的文本编辑器中编写一些代码，并将其保存到一个`myscript.py`Python脚本文件中。
* In IPython, assuming you are in the right directory, type in `%run myscript.py`.
* 在IPython中，假设您在正确的目录中，输入`%run myscript.py`。
* The script is executed. The standard output is displayed in real time in the IPython terminal along with possible errors. Top-level variables defined in the script are accessible in the IPython terminal at the end of the script's execution.
* 执行脚本。在IPython终端中实时显示标准输出以及可能的错误。脚本中定义的顶级变量可以在脚本执行结束时的IPython终端中访问。
* If code changes are required in the script, repeat the process.
* 如果脚本中需要更改代码，请重复此过程。

With a good text editor, this workflow can be quite efficient. As the script is reloaded when you execute `%run`, your changes will be taken into account automatically. Things become more complicated when your script imports other Python modules that you modify, as these won't be reloaded with `%run`. To overcome this problem, you can use the `autoreload` IPython extension as described at http://ipython.readthedocs.io/en/stable/config/extensions/autoreload.html.
有了一个好的文本编辑器，这个工作流就会非常高效。在执行`%Run`时重新加载脚本时，将自动考虑您的更改。当脚本导入您修改的其他Python模块时，情况会变得更加复杂，因为这些模块不会用`%Run`重新加载。为了克服这个问题，您可以使用`autoreload`IPython扩展`，如http：/ipython.readthedocs.io/en/稳态/config/Exments/autoreload.html所述。

### The Jupyter Notebook
### Jupyter Notebook

The Jupyter Notebook plays a central role in efficient interactive workflows. It is a well-designed mix between a code editor and a terminal, bringing the best of both worlds within a unified environment.
Jupyter Notebook在高效的交互工作流中起着核心作用。它是代码编辑器和终端之间的一个精心设计的混合体，在一个统一的环境中将两个世界的优点结合在一起。

You can start writing all your code in your notebook's cells. You write, execute, and test your code at the same place, thereby improving your productivity. You can put long comments in Markdown cells and structure your notebook with Markdown headers.
您可以开始在NoteBook的单元格中编写所有代码。在同一个地方编写、执行和测试代码，从而提高了工作效率。您可以在标记单元格中放置较长的注释，并使用Markdown标题构造您的NoteBook。

Once portions of your code become mature enough and do not require further changes, you refactor them into reusable Python components (functions, classes, and modules). In practice, you copy and paste the code into Python scripts (files with the `.py` extension). Jupyter notebooks are currently not easily reusable by third-party code. They are designed for preliminary analyses and exploratory research, not for production-ready code.
一旦代码的部分变得足够成熟并且不需要进一步的更改，就可以将它们重构为可重用的Python组件(函数、类和模块)。实际上，您可以将代码复制并粘贴到Python脚本中(扩展名为`.py`的文件)。Jupyter Notebook目前不容易被第三方代码重用。它们是为初步分析和探索性研究而设计的，而不是为开发用于生产的代码而设计的。

A major advantage of notebooks is that they give you documents retracing everything you did with your code, which is particularly useful for reproducible research. Since notebooks are saved in human-readable JSON documents, they don't work that well with version control systems such as Git.
NoteBook的一个主要优点是，它们会让您的文档重新跟踪您使用代码所做的一切，这对于可重复的研究尤其有用。由于NoteBook被保存在人类可读的JSON文档中，而它们在版本控制系统(如Git)中不能很好地工作。

The **ipymd** module, available at https://github.com/rossant/ipymd/, and the more recent **podoc** module, available at https://github.com/podoc/podoc, allow you to use Markdown instead of JSON for notebooks. In podoc, images are saved in external files instead of being embedded in the JSON notebook, which is more convenient when working with a version control system.
https://github.com/rossant/ipymd/，提供的**ipymd**模块和最近在https://github.com/podoc/podoc，上使用的**podoc**模块允许您在NoteBook上使用Markdown而不是JSON。在podoc中，图像保存在外部文件中，而不是嵌入到JSONNoteBook中，这在使用版本控制系统时更方便。

**JupyterLab**, the next generation of the Jupyter Notebook, bridges the gap between the Jupyter Notebook and IDEs. It is covered in the last recipe of Chapter 3.
**JupyterLab**，下一代Jupyter Notebook，架起Jupyter Notebook与IDE之间的桥梁。它在第三章的最后一个参考手册中讨论过。

### Integrated Development Environments
### 集成开发环境

IDEs are particularly well-adapted for classic software development, but they can also be used for interactive computing. A good Python IDE combines a powerful text editor (for example, one that includes features such as syntax highlighting and tab completion), an IPython terminal, and a debugger within a unified environment.
IDE特别适合于经典的软件开发，但它们也可以用于交互式计算。好的Python IDE结合了强大的文本编辑器(例如，包含语法突出显示和选项卡完成等特性的文本编辑器)、IPython终端和统一环境中的调试器。

There are multiple open-source and commercial IDEs. **Rodeo** is an IDE for data analysis made by ŷhat. **Spyder** is another open source IDE with good integration of IPython and matplotlib. **Eclipse/PyDev** is a popular (although slightly heavy) open source cross-platform environment.
有多种开放源代码和商业IDE。**rodeo**是ŷHAT开发的用于数据分析的IDE。**Spyder**是另一个具有IPython和matplotlib良好集成的开源IDE。**Eclipse/PyDev**是一个流行的(尽管稍微重)的开源跨平台环境。

**PyCharm** is one of many commercial environments that support IPython.
**PyCharm**是许多支持IPython的商业环境之一。

Microsoft's IDE for Windows, Visual Studio, has an open source plugin named **Python Tools for Visual Studio (PTVS)**. This tool brings Python support to Visual Studio. PTVS natively supports IPython. You don't necessarily need a paid version of Visual Studio; you can download a free package bundling PTVS with Visual Studio.
Microsoft的IDE for Windows，Visual Studio有一个名为**Python Tools for Visual Studio(PTV)**的开源插件。该工具为VisualStudio提供Python支持。PTVS本机支持IPython。您不一定需要付费版本的VisualStudio；您可以下载一个免费包，将PTV与VisualStudio捆绑在一起。

## There's more...
## 还有更多...

Here are a few links to various IDEs for Python:
下面是一些Python各种ide的链接:

* Rodeo at https://www.yhat.com/products/rodeo
* Spyder at https://github.com/spyder-ide/spyder
* PyDev at http://pydev.org
* PyCharm at http://www.jetbrains.com/pycharm/
* PyTools for Microsoft Visual Studio at https://microsoft.github.io/PTVS/
* MicrosoftVisualStudio的PyTools at https://microsoft.github.io/PTVS/
* PyTools for Microsoft Visual Studio at https://microsoft.github.io/PTVS/

## See also
## 另请参阅

* Learning the basics of the distributed version control system Git
* 学习分布式版本控制系统Git的基础知识
* Debugging your code with IPython
* 用IPython调试代码
