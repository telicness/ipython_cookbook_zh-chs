[*第二章：交互计算之最佳实践*](../)

# 2.8. 使用py.test编写单元测试

未经测试的代码不是好代码。手动测试对于确保我们的软件按预期工作，并且不包含关键错误是必不可少的。但是，手动测试受到严重限制，因为在代码中的任何时候都可能引入bug。

现在，自动化测试是软件工程的标准实践。在这个参考手册中，我们将简要介绍自动化测试的重要方面:单元测试、测试驱动开发、测试覆盖和持续集成。遵循这些实践是生产高质量软件的基础。

## 准备工作

Python有一个本机单元测试模块，您可以很容易地使用它(unittest)。还有其他第三方单元测试包。在这个参考手册中，我们将使用**py.test**。它默认安装在Anaconda中，但是你也可以用`conda install pytest`手动安装它。

## 怎么做...

1. 让我们在一个`first.py‘文件中编写一个返回列表的第一个元素的简单函数。

```python
%%writefile first.py
def first(l):
    return l[0]
```

```{output:stdout}
Overwriting first.py
```

2. 为了测试这个函数，我们编写了另一个函数**unit test**，它使用示例和断言检查我们的第一个函数:

```python
%%writefile -a first.py

# This is appended to the file.
def test_first():
    assert first([1, 2, 3]) == 1
```

```{output:stdout}
Appending to first.py
```

```python
%cat first.py
```

```{output:stdout}
def first(l):
    return l[0]

# This is appended to the file.
def test_first():
    assert first([1, 2, 3]) == 1
```

3. 要运行单元测试，我们使用`pytest`可执行文件(`!`意味着从IPython调用外部程序)：

```python
!pytest first.py
```

```{output:stdout}
============= test session starts ==============
platform linux -- Python 3.6.3, pytest-3.2.1, py-1.4.34
rootdir: ~/git/cookbook-2nd/chapter02_best_practices:
plugins: cov-2.5.1

collecting 0 items
collecting 1 item
collected 1 item

first.py .

=========== 1 passed in 0.00 seconds ===========
```

4. 我们的测试通过!让我们添加另一个空列表示例。在这种情况下，我们希望函数返回`None`:

```python
%%writefile first.py
def first(l):
    return l[0]

def test_first():
    assert first([1, 2, 3]) == 1
    assert first([]) is None
```

```{output:stdout}
Overwriting first.py
```

```python
!pytest first.py
```

```{output:stdout}
============= test session starts ==============
platform linux -- Python 3.6.3, pytest-3.2.1, py-1.4.34
rootdir: ~/git/cookbook-2nd/chapter02_best_practices:
plugins: cov-2.5.1

collecting 0 items
collecting 1 item
collected 1 item

first.py F

=================== FAILURES ===================
__________________ test_first __________________

    def test_first():
        assert first([1, 2, 3]) == 1
>       assert first([]) is None

first.py:6:
 _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _

l = []

    def first(l):
>       return l[0]
E       IndexError: list index out of range

first.py:2: IndexError
=========== 1 failed in 0.02 seconds ===========
```

5. 这次我们的测试失败了。让我们通过修改`first()`函数来修正它：

```python
%%writefile first.py
def first(l):
    return l[0] if l else None

def test_first():
    assert first([1, 2, 3]) == 1
    assert first([]) is None
```

```{output:stdout}
Overwriting first.py
```

```python
!pytest first.py
```

```{output:stdout}
============= test session starts ==============
platform linux -- Python 3.6.3, pytest-3.2.1, py-1.4.34
rootdir: ~/git/cookbook-2nd/chapter02_best_practices:
plugins: cov-2.5.1

collecting 0 items
collecting 1 item
collected 1 item

first.py .

=========== 1 passed in 0.00 seconds ===========
```

测试又通过了！

## 它是如何工作的…

根据定义，单元测试必须集中在一个特定的功能上。所有单元测试都应该是完全独立的。将程序编写为经过良好测试的、大部分是解耦的单元的集合，会迫使您编写更易于维护的模块化代码。

在Python包中，一个`test_xxx.py`模块应该与每个名为`xxx.py‘的Python模块一起使用。这个测试模块包含在`xxx.py‘模块中实现的测试功能的单元测试。

有时候，模块的功能需要进行初步的工作才能运行(例如，设置环境、创建数据文件或设置web服务器)。单元测试框架可以通过**fixture**处理这个问题。在测试模块运行之前和之后，系统环境的状态应该完全相同。如果您的测试影响到文件系统，它们应该在一个临时目录中这样做，这个临时目录在测试结束时被自动删除。测试框架，如py.test为这个用例提供了方便的工具。

测试通常涉及许多断言。使用py.test可以简单地使用内置的`assert`关键字。NumPy还提供了更方便的断言函数(请参见http：/docs.sciy.org/doc/numpy/Reference/实务.testing.html)。它们在处理数组时特别有用。例如，`np.testing.ASSERT_ALCLOSE(x，y)‘断言`x`和`y‘数组几乎相等，直到可以指定的给定精度为止。

编写完整的测试套件需要时间。它对代码的体系结构施加了强大(但很好的)约束。这是一项真正的投资，但从长远来看总是有利可图的。另外，知道您的项目是由完整的测试套件支持的，这将真正减轻您的负担。

首先，从一开始就考虑单元测试迫使您考虑模块化架构。为一个相互依赖的整体程序编写单元测试是非常困难的。

第二，单元测试使您更容易找到和修复bug。如果在程序中引入更改后单元测试失败，那么隔离和复制bug就变得非常简单。

第三，单元测试可以帮助您避免回归，也就是说，修正了在以后版本中悄然重新出现的bug。当您发现一个新的错误时，您应该为它编写一个特定的失败的单元测试。要解决这个问题，就要通过这个测试。现在，如果bug稍后再次出现，此单元测试将失败，您将立即能够解决它。

当您编写基于相互依赖的API的复杂程序时，对一个模块具有良好的测试覆盖率意味着您可以在其他模块中安全地依赖它，而不必担心它的行为不符合其规范。

单元测试只是一种自动化测试。其他重要的测试类型包括集成测试(确保程序的不同部分一起工作)和功能测试(测试典型用例)。

## 还有更多...

自动化测试是一个广泛的话题，我们在这个参考手册中只触及了皮毛。我们在此提供进一步的信息。

### 测试覆盖率

使用单元测试很好。但是，测量**测试覆盖率**更好：它量化了测试套件覆盖了多少代码。**overage.py**模块(https://coverage.readthedocs.io/)正是这样做的。它与py.test集成得很好。

**coveralls.io**服务为持续集成服务器带来测试覆盖特性(请参阅**单元测试和持续集成**部分)。它与GitHub无缝连接。

### 单元测试的工作流

注意我们在本例中使用的特定工作流。在编写完我们的函数之后，我们创建了第一个通过的单元测试。然后我们创建了第二个测试，失败了。我们研究了这个问题并修正了函数。第二次考试通过了。我们可以继续编写越来越复杂的单元测试，直到我们确信该函数在大多数情况下都能正常工作。

> 运行`pytest --pdb`，在失败时进入Python调试器。这很方便快速找出单元测试失败的原因。

我们甚至可以在函数本身之前编写测试。这是**测试驱动开发**，它包括在编写实际代码之前编写单元测试。这个工作流迫使我们考虑我们的代码做什么以及如何使用它，而不是如何实现它。

### 单元测试和连续集成

一个好的习惯是在每次提交时运行项目的完整测试套件。事实上，甚至可以通过**连续集成**完全透明和自动地做到这一点。我们可以设置一个服务器，在每次提交时自动在云中运行我们的测试套件。如果测试失败，我们会收到一封自动的电子邮件，告诉我们问题是什么，以便我们能够修复它。

有许多连续集成系统和服务：Jenkins/Hudson，TraVisCI(https://travis-ci.org)，Codeship(http://codeship.com/)，等)。他们中的一些人和GitHub玩得很好。例如，若要在GitHub项目中使用Travis CI，请在Travis CI上创建一个帐户，将您的GitHub项目链接到此帐户，然后添加一个`.travis.yml`文件，其中包含存储库中的各种设置(请参阅下面参考资料中的其他详细信息)。

总之，单元测试、代码覆盖和持续集成是应该在所有重要项目中使用的标准实践。

以下是一些参考资料：

* 测试驱动的开发， at https://en.wikipedia.org/wiki/Test-driven_development
* 用Python编写Travis CI的文档， at http://about.travis-ci.org/docs/user/languages/python/


