[*第二章：交互计算之最佳实践*](../)

# 2.7. 编写高质量的Python代码

编写代码很容易。编写高质量的代码要难得多。质量应该从实际代码(变量名、注释、文档字符串等)和体系结构(函数、模块和类)两方面来理解。一般来说，设计一个设计良好的代码体系结构比实现本身更具挑战性。

在这个参考手册中，我们将给出一些关于如何编写高质量代码的技巧。这是学术界一个特别重要的话题，因为越来越多没有软件开发经验的科学家需要编写代码。

## 怎么做...

1. 花时间认真学习Python语言。查看标准库中的所有模块列表--您可能会发现您实现的函数已经存在。学习编写Python代码，不要将Java或c++等其他语言的编程习惯用法翻译成Python。
2. 学习公共设计模式*；这些是软件工程中常见问题的通用可重用解决方案。
3. 在代码中使用断言(`assert`关键字)来防止将来的错误(**防御性编程**)。
4. 开始使用自底向上的方法编写代码;编写独立的Python函数来实现专注的任务。
5. 不要犹豫定期重构您的代码。如果您的代码变得过于复杂，请考虑如何简化它。
6. 尽可能避免使用Class。如果可以使用函数而不是类，请选择该函数。只有在需要在函数调用之间存储持久状态时，类才会有用。使你的功能尽可能纯净(没有副作用)。
7. 通常，与定制类型(类)相比，更喜欢Python本机类型(列表、元组、字典和来自Python集合模块的类型)。本机类型会导致更高效、更可读和更可移植的代码。
8. 在函数中选择关键字参数而不是位置参数。参数名比参数排序更容易记住。它们使你的函数自我记录。
9. 认真为变量命名。函数和方法的名称应该以动词开头。变量名应该描述它是什么。函数名应该描述它所做的事情。正确命名事物的重要性怎么强调也不为过。
10. 每个函数都应该有一个docstring来描述它的用途、参数和返回值，如下例所示。您还可以查看在诸如NumPy等流行库中选择的约定。确切的约定并不重要，关键是在代码中保持一致。您可以使用标记语言，如Markdown或REST：

```python
def power(x, n):
    """Compute the power of a number.

    Arguments:
    * x: a number
    * n: the exponent

    Returns:
    * c: the number x to the power of n

    """
    return x ** n
```

11. 遵循(至少部分遵循)Guido van Rossum的Python风格指南，也被称为**Python增强建议8 (PEP8)**，可用 at http://www.python.org/dev/peps/pep-0008/. It is a long read, but it will help you write well-readable Python code. It covers many little things such as spacing between operators, naming conventions, comments, and docstrings. For instance, you will learn that it is considered a good practice to limit any line of your code to 79 or 99 characters. This way, your code can be correctly displayed in most situations (such as in a command-line interface or on a mobile device) or side by side with another file. Alternatively, you can decide to ignore certain rules. In general, following common guidelines is beneficial on projects involving many developers.
12. 您可以使用**pycodestyle**Python包(https://github.com/PyCQA/pycodestyle).)根据PEP 8中的大多数样式约定自动检查代码。您还可以自动使您的代码PEP 8与**AUTOPE 8**包(https://github.com/hhatto/autopep8).)兼容。
13. 使用工具进行静态代码分析，例如**flake8**(http://flake8.pycqa.org/en/latest/)或**Pylint**(https://www.pylint.org).)它允许您静态地查找潜在的错误或低质量的代码，也就是说，不运行您的代码。
14. 使用空行来避免代码混乱(参见PEP8)。您还可以用类似这样的突出注释在长Python模块中划分部分:

```python
# Imports
# -------
import numpy

# Utility functions
# -----------------

def fun():
    pass
```

15. Python模块不应该包含超过几百行代码。在一个模块中有太多的代码行可能表明您需要将其分解为多个模块。
16. 将重要的项目(包含数十个模块)组织到子程序包(子目录)中。
17. 看看主要的Python项目是如何组织的。例如，IPython的代码被很好地组织成具有重点角色的子包的层次结构。阅读代码本身也很有指导意义。
18. 学习创建和分发新的Python包的最佳实践。确保您了解setuptools、pip、wheels、virtualenv、PyPI等等。此外，我们还鼓励您认真研究conda (http://conda.pydata.org)，这是由Anaconda创建的一个功能强大的通用打包系统。在Python中，打包一直是一个快速发展的主题，所以只阅读最近的参考资料。有一些参考文献在**有更多…**部分。

## 它是如何工作的.。

编写可读的代码意味着其他人(或者你)在几个月或几年之后会更快地理解它，并且更愿意使用它。它还有助于bug跟踪。

模块化代码也更容易理解和重用。在独立的函数中实现程序的功能，这些函数被组织成包和模块的层次结构，这是实现高代码质量的极好方法。

使用函数而不是类时，保持代码松散耦合更容易。意大利面条式的代码真的很难理解、调试和重用。

在处理新项目时，在自下而上和自顶向下的方法之间迭代。从自下而上的方法开始，在开始考虑程序的总体架构之前，您可以获得使用代码的体验。尽管如此，通过考虑组件将如何协同工作，确保您知道要做什么。

## 还有更多...

关于如何编写漂亮的代码，已经写了很多-参见下面的参考资料。你可以找到许多关于这个主题的书。在下一个参考手册中，我们将介绍标准技术，以确保我们的代码不仅看上去不错，而且工作正常：单元测试、代码覆盖和持续集成。

以下是一些参考资料：

* Python Cookbook, by David Beazley and Brian K. Jones, with many Python advanced recipes, available at http://shop.oreilly.com/product/0636920027072.do
* *The Hitchhiker's Guide to Python!*, available at http://docs.python-guide.org/en/latest/
* Design patterns on Wikipedia, available at https://en.wikipedia.org/wiki/Software_design_pattern
* Coding standards of Tahoe-LAFS, available at https://tahoe-lafs.org/trac/tahoe-lafs/wiki/CodingStandards
* *How to be a great software developer*, by Peter Nixey, available at http://peternixey.com/post/83510597580/how-to-be-a-great-software-developer
* *Why you should write buggy software with as few features as possible*, a talk by Brian Granger, available at http://www.youtube.com/watch?v=OrpPDkZef5I
* *Python Packaging User Guide*, available at https://packaging.python.org/

;## See also
## 另请参阅

* 进行可重复交互计算实验的十个技巧
* 用pytest编写单元测试


