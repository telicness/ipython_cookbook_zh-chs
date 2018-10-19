[*第一章：Jupyter与IPython互动计算之旅*](./)

# 1.5. 掌握IPython的配置系统

源自IPython的**traitlet **包(https://traitlets.readthedocs.io/en/stable/)实现了一个强大的配置系统。这个系统在整个项目中都使用，但是它也可以被IPython扩展使用。它甚至可以用于全新的应用程序。

在这个参考手册中，我们展示了如何使用这个系统来编写一个可配置的IPython扩展。我们将创建一个显示随机数的简单魔法命令。这个神奇的命令具有可配置的参数，用户可以在他们的IPython配置文件中设置这些参数。

## 怎么做...

1. 我们在`random_magics.py`中创建了一个IPython扩展。让我们从导入一些对象开始:

```python
%%writefile random_magics.py

from traitlets import Int, Float, Unicode, Bool
from IPython.core.magic import (Magics, magics_class,
                                line_magic)
import numpy as np
```

```{output:stdout}
Writing random_magics.py
```

2. 我们创建了一个从`wagics`派生出来的`RandomMagics`类。这个类包含一些可配置的参数：

```python
%%writefile random_magics.py -a

@magics_class
class RandomMagics(Magics):
    text = Unicode(u'{n}', config=True)
    max = Int(1000, config=True)
    seed = Int(0, config=True)
```

```{output:stdout}
Appending to random_magics.py
```

3. 我们需要调用父构造函数。然后，我们用种子初始化一个随机数生成器：

```python
%%writefile random_magics.py -a

    def __init__(self, shell):
        super(RandomMagics, self).__init__(shell)
        self._rng = np.random.RandomState(
            self.seed or None)
```

```{output:stdout}
Appending to random_magics.py
```

4. 我们创建一个`%random`行魔法显示一个随机数:

```python
%%writefile random_magics.py -a

    @line_magic
    def random(self, line):
        return self.text.format(
            n=self._rng.randint(self.max))
```

```{output:stdout}
Appending to random_magics.py
```

5. 最后，我们在加载扩展时注册这个魔法:

```python
%%writefile random_magics.py -a

def load_ipython_extension(ipython):
    ipython.register_magics(RandomMagics)
```

```{output:stdout}
Appending to random_magics.py
```

6. 让我们在NoteBook中测试我们的扩展：

```python
%load_ext random_magics
```

```python
%random
```

```{output:result}
'430'
```

```python
%random
```

```{output:result}
'305'
```

7. 我们的magic命令有一些可配置参数。在启动IPython时，用户应该在IPython配置文件或控制台中配置这些变量。要在终端中配置这些变量，我们可以在系统shell中输入以下命令:

```
ipython --RandomMagics.text='Your number is {n}.' \
        --RandomMagics.max=10 \
        --RandomMagics.seed=1
```

在该会话中，`%random`将显示一个字符串，比如`Your number is 5.'`。

8. 为了配置IPython配置文件中的变量，我们打开`~/.IPython /profile_default/ipython_config`。的文件，并添加以下一行:

```
c.RandomMagics.text = 'random {n}'
```

在启动IPython之后，`%random`打印一个字符串，比如`random 652`。

## 它是如何工作的.。

IPython的配置系统定义了几个概念：

* **用户配置文件**是一组特定于用户的参数、日志和命令历史记录。在处理不同的项目时，用户可以拥有不同的配置文件。`xx`配置文件存储在`~/.ipython/profile_xx`中，其中`~‘是用户的主目录。
    * 在Linux上，路径应该是`/home/youname/.ipython/profile_xxx`
    * 在macOS上，路径应该是`/Users/yourname/.ipython/profile_xxx`
    * 在Windows上，路径应该是`C: Users\YourName\.ipython\profile_xxx`
* 一个**configuration 对象**，或`Config`，是一个包含键-值对的特殊Python字典。`Config`类源自Python的`dict`类。
* `HasTraits`类是一个可以具有特殊`trait`属性的类。**字符**是具有特定类型和默认值的复杂Python属性。此外，当特征的值发生变化时，会自动透明地调用回调函数。这种机制允许在特征属性发生更改时通知类。
* `Configurable`类是希望从配置系统中受益的所有类的基类。`Configurable`类可以具有可配置的属性。这些属性的默认值直接在类定义中指定。`Configurable`类的主要特性是，这些特征的默认值可以在类逐个类的基础上被配置文件覆盖。然后，Configurable实例可以在空闲时更改这些值。
* **配置文件**是包含`Configurable`类参数的Python或JSON文件。

`Configurable`类和配置文件支持继承模型。`Configurable`类可以从另一个`Configurable`类派生并重写其参数。同样，配置文件也可以包含在另一个文件中。

### 可配置类

下面是`Configurable`类的一个简单示例：

```
from traitlets.config import Configurable
from traitlets import Float

class MyConfigurable(Configurable):
    myvariable = Float(100.0, config=True)
```

默认情况下，`myconfigure`类的一个实例的`myvariable`属性将等于100。现在，让我们假设我们的IPython配置文件包含以下几行:

```
c = get_config()
c.MyConfigurable.myvariable = 123.
```

然后，`myvariable`属性将默认为123。实例在实例化之后可以随意更改这个默认值。

`get_config()`函数是一个在任何配置文件中都可用的特殊函数。

此外，可以在命令行接口中指定`Configurable`参数，就像我们在这个参考手册中看到的那样。

所有IPython应用程序都使用这个配置系统(特别是`console`、`qtconsole`和`notebook`)。这些应用程序具有许多可配置的属性。您将在概要文件的配置文件中找到这些属性的列表。

### 魔法类

**magics**类派生于`Configurable`，可以包含可配置属性。此外，魔法命令可以由`@line_magic`或`@cell_magic‘修饰的方法定义。定义类魔法而不是函数魔法的优点是我们可以在多个神奇调用之间保持状态(因为我们使用的是类而不是函数)。

## 还有更多...

以下是一些参考资料：

* Configuring and customizing IPython at http://ipython.readthedocs.io/en/stable/config/
* Defining custom magics available at http://ipython.readthedocs.io/en/stable/config/custommagics.html
* Detailed overview of the configuration system at https://traitlets.readthedocs.io/en/stable/config.html

## 另请参阅

* 使用自定义魔法命令创建IPython扩展
