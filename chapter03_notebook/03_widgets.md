[*第三章：掌握Jupyter Notebook*](./)

# 3.3. 掌握Jupyter Notebook中的小部件

**ipywidgets**包提供了许多通用的用户界面控件，用于交互式地研究代码和数据。可以组装和定制这些控件，以创建复杂的图形用户界面。在这个参考手册中，我们将介绍使用ipywidgets创建用户界面的各种方法。

## 准备工作

默认情况下，应该在Anaconda中安装ipywidget包，但您也可以使用`conda install ipywidgets`手动安装它。

或者，您可以使用`pip install ipywidgets`安装ipywidgets，但是您还需要输入以下命令，以便在Jupyter Notebook中启用扩展:

```bash
jupyter nbextension enable --py --sys-prefix widgetsnbextension
```

## 怎么做...

1. 让我们导入这些包:

```python
import ipywidgets as widgets
from ipywidgets import HBox, VBox
import numpy as np
import matplotlib.pyplot as plt
from IPython.display import display
%matplotlib inline
```

2. `@interact`装饰符显示了一个小部件，用于控制函数的参数。在这里，函数`f()`接受一个整数作为参数。默认情况下，`@interact‘装饰器显示一个滑块来控制传递给函数的值：

```python
@widgets.interact
def f(x=5):
    print(x)
```

![Interact](03_widgets_files/03_widgets_6_0.png)

每当滑块值发生变化时，都会调用函数`f()`。

3. 我们可以定制滑块参数。这里，我们为滑块指定一个最小和最大整数范围:

```python
@widgets.interact(x=(0, 5))
def f(x=5):
    print(x)
```

![Interact](03_widgets_files/03_widgets_9_0.png)

4. 还有一个`@Interactive_manual‘装饰符，它提供了一个按钮来手动调用函数。对于不应该每次小部件值更改时运行的长时间计算来说，这是非常有用的。在这里，我们创建了一个简单的用户界面，用于控制显示一个图的函数的四个参数。有两个浮点滑块，一个下拉菜单，用于在几个预定义的选项中选择一个值，以及一个用于布尔值的复选框：

```python
@widgets.interact_manual(
    color=['blue', 'red', 'green'], lw=(1., 10.))
def plot(freq=1., color='blue', lw=2, grid=True):
    t = np.linspace(-1., +1., 1000)
    fig, ax = plt.subplots(1, 1, figsize=(8, 6))
    ax.plot(t, np.sin(2 * np.pi * freq * t),
            lw=lw, color=color)
    ax.grid(grid)
```

![Interact manual](03_widgets_files/03_widgets_11_0.png)

5. 除了`@interact`和`@interactivemanual`装饰器之外，ipywidget还提供了一个简单的API来创建各个小部件。在这里，我们创建了一个浮点滑块：

```python
freq_slider = widgets.FloatSlider(
    value=2.,
    min=1.,
    max=10.0,
    step=0.1,
    description='Frequency:',
    readout_format='.1f',
)
freq_slider
```

![Interact manual](03_widgets_files/03_widgets_13_0.png)

6. 下面是选择数字对的滑块示例，比如间隔和范围:

```python
range_slider = widgets.FloatRangeSlider(
    value=[-1., +1.],
    min=-5., max=+5., step=0.1,
    description='xlim:',
    readout_format='.1f',
)
range_slider
```

![Range slider](03_widgets_files/03_widgets_15_0.png)

7. 切换按钮可以控制一个布尔值:

```python
grid_button = widgets.ToggleButton(
    value=False,
    description='Grid',
    icon='check'
)
grid_button
```

![Toggle button widget](03_widgets_files/03_widgets_17_0.png)

8. 下拉菜单和切换按钮在从预定义的选项中选择值时非常有用：

```python
color_buttons = widgets.ToggleButtons(
    options=['blue', 'red', 'green'],
    description='Color:',
)
color_buttons
```

![Toggle buttons](03_widgets_files/03_widgets_19_0.png)

9. 文本小部件允许用户编写字符串:

```python
title_textbox = widgets.Text(
    value='Hello World',
    description='Title:',
)
title_textbox
```

![Text widget](03_widgets_files/03_widgets_21_0.png)

10. 我们可以让用户使用内置的系统颜色选择器选择颜色:

```python
color_picker = widgets.ColorPicker(
    concise=True,
    description='Background color:',
    value='#efefef',
)
color_picker
```

![Color picker](03_widgets_files/03_widgets_23_0.png)

11. 我们也可以简单地创建一个按钮:

```python
button = widgets.Button(
    description='Plot',
)
button
```

![Button widget](03_widgets_files/03_widgets_25_0.png)

12. 现在，我们将看到如何将这些小部件组合成复杂的图形用户界面，以及如何对与这些控件的用户交互作出反应。我们创建一个函数来显示由创建的控件定义的绘图。我们可以使用小部件的`value`属性访问控件值：

```python
def plot2(b=None):
    xlim = range_slider.value
    freq = freq_slider.value
    grid = grid_button.value
    color = color_buttons.value
    title = title_textbox.value
    bgcolor = color_picker.value

    t = np.linspace(xlim[0], xlim[1], 1000)
    f, ax = plt.subplots(1, 1, figsize=(8, 6))
    ax.plot(t, np.sin(2 * np.pi * freq * t),
            color=color)
    ax.grid(grid)
```

13. 按钮小部件的`on_click`装饰器允许我们对单击事件做出反应。在这里，我们简单地声明当按下按钮时应该调用绘图函数：

```python
@button.on_click
def plot_on_click(b):
    plot2()
```

14. 为了在统一的图形界面中显示所有小部件，我们定义了一个带有两个选项卡的布局。第一个选项卡显示与绘图本身相关的小部件，而第二个选项卡显示与绘图样式相关的小部件。每个选项卡都包含一个由`VBox`类定义的垂直部件堆栈:

```python
tab1 = VBox(children=[freq_slider,
                      range_slider,
                      ])
tab2 = VBox(children=[color_buttons,
                      HBox(children=[title_textbox,
                                     color_picker,
                                     grid_button]),
                                     ])
```

15. 最后，我们用两个选项卡创建`Tab‘实例，设置选项卡的标题，并在选项卡下面添加绘图按钮：

```python
tab = widgets.Tab(children=[tab1, tab2])
tab.set_title(0, 'plot')
tab.set_title(1, 'styling')
VBox(children=[tab, button])
```

![Complex widget](03_widgets_files/03_widgets_33_0.png)

## 还有更多...

ipywidget的文档演示了包的许多其他特性。可以定制小部件的样式。可以通过编写Python和JavaScript代码来创建新的小部件(请参见用Python、HTML和JavaScript*创建定制的Jupyter Notebook小部件)。小部件还可以在静态NoteBook导出中至少部分保持功能。

以下是一些参考资料：

* ipywidgets用户指南 at https://ipywidgets.readthedocs.io/en/stable/user_guide.html
* 构建自定义小部件 at https://ipywidgets.readthedocs.io/en/stable/examples/Widget%20Custom.html

## 另请参阅

* 用Python、HTML和JavaScript创建定制的Jupyter Notebook小部件


