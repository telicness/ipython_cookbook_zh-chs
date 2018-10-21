# 第一章：Jupyter与IPython互动计算之旅

在本章中，我们将涵盖以下主题:

* [1.1. 介绍IPython和Jupyter Notebook](01_notebook.md)
* [1.2. 从Jupyter Notebook的探索性数据分析开始](02_pandas.md)
* [1.3. 在NumPy中引入多维数组以实现快速数组计算](03_numpy.md)
* [1.4. 使用定制的magic命令创建一个IPython扩展](04_magic.md)
* [1.5. 掌握IPython配置系统](05_config.md)
* [1.6. 为Jupyter创建一个简单的内核](06_kernel.md)

在这篇引言中，我们将对Python、IPython、Jupyter和科学Python生态系统进行全面概述。

## Python是什么? 

Python是一种高级的、开源的、通用的编程语言，最初是由Guido van Rossum在20世纪80年代后期构思出来的(这个名字的灵感来自英国喜剧Monty Python的飞行马戏团*)。这种易于使用的语言通常被系统管理员用作粘合语言，将各种系统组件连接在一起。它也是用于大规模软件开发的健壮语言。此外，Python还提供了一个非常丰富的标准库(其中包含了一些哲学思想)，它涵盖了字符串处理、Internet协议、操作系统接口和许多其他领域。

在过去的二十年中，Python也越来越多地被用于科学计算和数据分析。其他竞争平台包括MATLAB、Maple、Mathematica、Excel、SPSS、SAS等商业软件。竞争的开源平台包括Julia，R，Octave和Scilab.这些工具专门用于科学计算，而Python是一种通用的编程语言，最初不是为科学计算而设计的。

然而，已经开发了一个广泛的工具生态系统，使Python达到了其他科学计算系统的水平。今天，Python的主要优势，也是它如此受欢迎的主要原因之一，是它为通用语言带来了科学计算特性，这种通用语言在许多研究领域和行业中都使用。这使得从研究到生产的转变更加容易。

## 什么是IPython? 

IPython**是一个Python库，最初的目的是改进Python提供的默认交互控制台，并使其对科学友好。2011年，在首次发布IPython 10年后，推出了**IPythonNoteBook**。这个基于web的IPython接口结合了代码、文本、数学表达式、内联图、交互式图形、小部件、图形界面和独立的可共享web文档中的其他富媒体。该平台为交互式科学计算和数据分析提供了理想的门户。IPython对于研究人员、工程师、数据科学家、教师和学生来说已经变得非常重要。

## 什么是Jupyter? 

几年内，IPython在科学和工程社区中获得了难以置信的普及。NoteBook开始支持Python以外的越来越多的编程语言。2014年，IPython开发人员宣布了**Jupyter**项目，这是一个旨在改进NoteBook的实现并通过设计使其语言不可知论的倡议。该项目的名称反映了NoteBook所支持的三种主要科学计算语言的重要性：Julia、Python和R。

今天，Jupyter本身就是一个生态系统，它包含了几个可供选择的NoteBook接口(JupyterLab、nteract、Hydrogen等)、交互式可视化库、与NoteBook兼容的创作工具。Jupyter有自己的会议叫JupyterCon。该项目获得了几家公司以及阿尔弗雷德·p·斯隆基金会(Alfred P. Sloan Foundation)和戈登·贝蒂·摩尔基金会(Gordon and Betty Moore Foundation)的资助。

## 什么是SciPy生态系统?

SciPy是用于科学计算的Python包的名称，但更广泛地说，它还提到了为将科学计算特性引入Python而开发的所有Python工具的集合。

在20世纪90年代后期，Travis Oliphant和其他人开始构建高效的工具来处理Python中的数字数据:Numeric, Numarray，最后是**NumPy**。实现了许多数值计算算法的SciPy也在NumPy的基础上创建。在本世纪初，John Hunter创建了**matplotlib**，将科学图形引入Python。同时，Fernando Perez创建了**IPython**以提高Python的交互性和生产力。在2000年代后期，Wes McKinney创造了**panda **用于操纵和分析数字表格和时间序列。此后，数百名工程师和研究人员在这个平台上通力合作，使SciPy成为领先的开放源码科学计算和数据科学平台之一。

> 许多SciPy工具都得到了NumFOCUS的支持，NumFOCUS是一个非营利组织，作为促进生态系统可持续发展的法律结构。NumFOCUS得到了包括微软、IBM和英特尔在内的几家大公司的支持。

SciPy也有自己的会议，SciPy(在美国)和EuroSciPy(在欧洲)(参见https://conference.scipy.org/)。

## SciPy生态系统有什么新变化?

自2014年出版这本书的第一版以来，SciPy生态系统中的一些主要变化是什么? 我们在这里作了一个非常简短的选择。

> 如果您是这个平台的新手，请随意跳过这一部分。

撰写本文时，IPython的最后一个版本是IPython 6.0，于2017年4月发布。它是第一个不再兼容Python 2的IPython版本。这个决定使开发人员能够使内部代码更简单，并更好地使用语言的新特性。

IPython现在有一个基于Web的终端接口，可以与NoteBook一起使用。键盘快捷键可以直接从NoteBook界面编辑。可以选择多个单元格，并在NoteBook之间复制/粘贴。在NoteBook中有一个新的`重新启动和运行`按钮和`查找和替换`选项。有关更多细节，请参见http：/ipython.readthedocs.io/en/稳定器/WhatsNew/version6.html。

NumPy上一个版本1.13是在2017年6月发布的，现在支持矩阵之间的`@`矩阵乘法运算符(以前可以通过`np.dot()`函数访问)。`a + b + c`之类的操作在某些系统上占用的内存更少，而且速度更快(暂时省略)。新的`np.block()`函数允许定义块矩阵。新的`np.stack()`函数将一系列数组连接到一个新的轴上。有关详细信息，请参阅https://docs.scipy.org/doc/numpy-1.13.0/release.html。

SciPy1.0于2017年10月发布。对于开发人员来说，1.0版本意味着经过16年的开发，库已经达到了一定的稳定性和成熟度。有关更多细节，请参见https：/docs.sciy.org/doc/s枕/Reference/Relase.html。

Matplotlib的2.1版本于2017年10月发布，它改进了样式，使用**viridis**彩色地图而不是jet提供了更好的默认调色板。有关详细信息，请参阅https://github.com/matplotlib/matplotlib/release。

Pandas0.21于2017年10月发行。Pandas现在支持分类数据。在过去的几年中，已经完成了几次反对，取消了`.ix‘语法和面板(这可以通过xArray库来替换)。有关更多细节，请参见https：/panadas.pydata.org/pans-docs/稳定化/Relase.html。

## 如何安装Python? 

在本书中，我们使用**Anaconda发行版**，可在https://www.anaconda.com/download/找到。Anaconda 可以在Linux、macOS和Windows上工作。您应该安装最新版本的Anaconda(在编写时为5.0.1)和最新64位版本的Python(在编写时为3.6)。Python 2.7是一个旧版本，将在2020年正式不受支持。

Anaconda附带Python、IPython、Jupyter、NumPy、SciPy、Pandas、matplotlib以及我们将在本书中使用的几乎所有其他科学软件包。所有包的列表都可以在https：/docs.anaconda.com/anaconda/Packages/pkg-docs上找到。

> Miniconda是Anaconda的轻量级版本，只有Python和其他一些重要的包。您只能使用Anaconda的`conda`包管理器逐一安装所需的包。

在本书中，我们不会介绍安装科学Python发行版的各种其他方法。

Anaconda网站应该给您提供安装Anaconda系统的所有指示。要安装新包，可以使用Anaconda附带的`conda`包管理器。例如，要安装ipyParallyPackage(Anaconda中目前没有默认安装)，请在系统外壳中键入`condainstall ipypeling`。

> 在*第2章，学习Unix Shell的基础知识*中有关于系统shell的简短介绍。

安装包的另一种方法是使用**conda-forge**，可以在https://conda-forge.org/上找到。这是一个由社区驱动的工作，目的是自动构建GitHub上可用的最新版本的包，并让它们使用`conda`。如果`conda install somepackage`中的包不可用，那么如果`conda install—channel conda-forge somepackage`可以用`conda install—channel conda-forge somepackage`代替。

> GitHub是一个为软件存储库提供免费和付费托管的商业服务。它是最流行的开源协作开发平台之一。

**Pip**是Python系统管理器。与`conda`相反，`pip‘适用于任何Python发行版，而不仅仅是Anaconda。pip可安装的包存储在https://pypi.python.org/pypi.提供的PythonPackageIndex上

conda中几乎所有可用的Python包都可以在pip中使用，但反之则不然。实际上，如果一个包在conda或conda-forge中不可用，那么它应该与`pip install somepackage`一起可用。Conda包通常包括为最常见平台编译的二进制文件，而pip包则不一定如此。pip包可能包含必须在本地编译的源代码(这需要安装和配置兼容的编译器)，但它们也可能包含编译后的二进制文件。

## 参考文献

以下是一些参考资料：

* Python的网页 at https://www.python.org
* 维基百科上的Python at https://en.wikipedia.org/wiki/Python_%28programming_language%29
* Python标准库 at https://docs.python.org/3/library/
* 与Guido van Rossum关于Python诞生的对话 at http://www.artima.com/intv/pythonP.html
* 提供科学Python的历史 at http://fr.slideshare.net/shoheihido/sci-pyhistory
* Jupyter Notebook的历史 at http://blog.fperez.org/2012/01/ipython-notebook-historical.html

这里有一些关于科学Python的资源:

* 计算科学和工程Python简介， at https://github.com/fangohr/introduction-to-python-for-computational-science-and-engineering
* 统计计算与计算， at http://people.duke.edu/~ccc14/sta-663-2017/
* SciPy 2017 视频 https://www.youtube.com/playlist?list=PLYx7XA2nY5GfdAFycPLBdUDOUtdQIVoMf
