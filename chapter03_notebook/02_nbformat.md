[*第三章：掌握Jupyter Notebook*](./)

# 3.2. 用nbconvert将Jupyter Notebook转换为其他格式

一个Jupyter Notebook保存在一个JSON文本文件中。此文件包含NoteBook的全部内容：文本、代码和输出。matplotlib图形在NoteBook中被编码为base 64字符串，从而生成独立但有时很大的NoteBook文件。

> JSON是一种人类可读的、基于文本的、开放的标准格式，可以表示结构化数据.虽然它来自JavaScript，但它与语言无关。它的语法与Python字典有一些相似之处。JSON可以用许多语言进行解析，包括JavaScript和Python(使用Python标准库中的`json`模块)。

**nbConvert**(https://nbconvert.readthedocs.io/en/stable/)是一个工具，可以将NoteBook转换成其他格式：原始文本、Markdown、HTML、LaTeX/PDF，甚至还可以使用replal.js库进行幻灯片转换。您将在nbConvert文档中找到有关不同支持格式的更多信息。

通常使用**nbformat** (https://nbformat.readthedocs.io/en/latest/)库来操作NoteBook。然而，在这个参考手册中，我们将看到如何使用Python直接操作NoteBook(它只是一个纯文本JSON文件)的内容，以及如何使用nbconvert将其转换为其他格式。

## 准备工作

您需要安装pandoc，可以访问http://pandoc.org。此工具用于将markup文件转换为各种格式。在Ubuntu上，在终端输入`sudo apt-get安装pandoc`。

要将NoteBook转换为PDF，您需要一个LaTeX发行版，您可以从http://latex project.org/ftp.html下载和安装它。

## 怎么做...

1. 让我们下载并打开测试NoteBook。NoteBook只是一个纯文本文件(JSON):

```python
import io
import requests
```

```python
url = ('https://github.com/ipython-books/'
       'cookbook-2nd-data/blob/master/'
       'test.ipynb?raw=true')
```

```python
contents = requests.get(url).text
print(len(contents))
```

```{output:stdout}
3857
```

2. 下面是`test.ipynb`文件的摘录：

```python
print(contents[:345] + '...' + contents[-33:])
```

```{output:stdout}
{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# First chapter"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "my_field": [
     "value1",
     "2405"
    ]
   },
   "source": [
    "Let's write some *rich* **text** with
        [links](http://www.ipython.org) and lists:\n",
    "\n",
    "* item1...rmat": 4,
 "nbformat_minor": 4
}
```

3. 现在我们已经将NoteBook加载到一个字符串中，让我们用`json`模块解析它，如下所示：

```python
import json
nb = json.loads(contents)
```

4. 让我们看看NoteBook字典里的键:

```python
print(nb.keys())
print('nbformat %d.%d' % (nb['nbformat'],
                          nb['nbformat_minor']))
```

```{output:stdout}
dict_keys(['cells', 'metadata',
           'nbformat', 'nbformat_minor'])
nbformat 4.4
```

5. 每个单元格都有一个类型、可选元数据、一些内容(文本或代码)、一个或几个输出以及其他信息。让我们看一下标记单元格和代码单元格：

```python
nb['cells'][1]
```

```{output:result}
{'cell_type': 'markdown',
 'metadata': {'my_field': ['value1', '2405']},
 'source': ["Let's write some *rich* **text** with
        [links](http://www.ipython.org) and lists:\n",
  '\n',
  '* item1\n',
  '* item2\n',
  '    1. subitem\n',
  '    2. subitem\n',
  '* item3']}
```

```python
nb['cells'][2]
```

```{output:result}
{'cell_type': 'code',
 'execution_count': 1,
 'metadata': {},
 'outputs': [{'data': {'image/png': 'iVBOR...QmCC\n',
    'text/plain': ['<matplotlib Figure at ...>']},
   'metadata': {},
   'output_type': 'display_data'}],
 'source': ['import numpy as np\n',
  'import matplotlib.pyplot as plt\n',
  '%matplotlib inline\n',
  'plt.figure(figsize=(2,2));\n',
  "plt.imshow(np.random.rand(10,10),
              interpolation='none');\n",
  "plt.axis('off');\n",
  'plt.tight_layout();']}
```

6. 一旦被解析，NoteBook就被表示为Python字典。因此，在Python中操作它非常方便。在这里，我们按以下方式计算标记和代码单元格的数量：

```python
cells = nb['cells']
nm = len([cell for cell in cells
          if cell['cell_type'] == 'markdown'])
nc = len([cell for cell in cells
          if cell['cell_type'] == 'code'])
print((f"There are {nm} Markdown cells and "
       f"{nc} code cells."))
```

```{output:stdout}
There are 2 Markdown cells and 1 code cells.
```

7. 让我们用matplotlib图更仔细地查看单元格的图像输出:

```python
cells[2]['outputs'][0]['data']
```

```{output:result}
{'image/png': 'iVBOR...QmCC\n',
 'text/plain': ['<matplotlib.figure.Figure at ...>']}
```

通常，可以有0、1或多个输出。此外，每个输出可以有多个表示。在这里，matplotlib图有一个png表示(base 64编码的图像)和一个文本表示(图形的内部表示)。
8. 现在，我们使用nbconvert将我们的文本NoteBook转换为HTML:

```python
# We write the notebook to a file on disk.
with open('test.ipynb', 'w') as f:
    f.write(contents)
```

```python
!jupyter nbconvert --to html test.ipynb
```

```{output:stdout}
[NbConvertApp] Converting notebook test.ipynb to html
[NbConvertApp] Writing 253784 bytes to test.html
```

9. 让我们在`<iframe>`(在NoteBook中显示外部HTML文档的一个小窗口)中显示这个文档：

```python
from IPython.display import IFrame
IFrame('test.html', 600, 200)
```

![HTML export](02_nbformat_files/02_nbformat_30_0.png)

10. 我们也可以把NoteBook转换成乳胶和PDF。为了指定文档的标题和作者，我们需要扩展默认的LaTeX模板。首先，我们创建了一个名为`tem.tplx`的文件，它扩展了nbConvert提供的默认的`tracle.tplx`模板。我们将作者和标题块的内容指定如下：

```python
%%writefile temp.tplx
((*- extends 'article.tplx' -*))

((* block author *))
\author{Cyrille Rossant}
((* endblock author *))

((* block title *))
\title{My document}
((* endblock title *))
```

```{output:stdout}
Writing temp.tplx
```

11. 然后，我们可以通过如下所示的自定义模板来运行nbConvert：

```python
%%bash
jupyter nbconvert --to pdf --template temp test.ipynb
```

```{output:stderr}
[NbConvertApp] Converting notebook test.ipynb to pdf
[NbConvertApp] Support files will be in test_files/
[NbConvertApp] Making directory test_files
[NbConvertApp] Writing 16695 bytes to notebook.tex
[NbConvertApp] Building PDF
[NbConvertApp] Running xelatex 3 times:
    ['xelatex', 'notebook.tex']
[NbConvertApp] Running bibtex 1 time:
    ['bibtex', 'notebook']
[NbConvertApp] PDF successfully created
[NbConvertApp] Writing 16147 bytes to test.pdf
```

我们使用nbconvert将NoteBook转换为LaTeX，而使用pdflatex(与LaTeX发行版一起提供)将LaTeX文档编译为PDF。下面的截图显示了这个NoteBook的PDF版本:

![PDF output](02_nbformat_files/doc.png)

## 它是如何工作的.。

正如我们在这个参考手册中所看到的，`.ipynb`文件包含NoteBook的结构化表示。这个JSON文件可以很容易地用Python和其他语言进行解析和操作。然而，更好的做法是使用**nbformat**包来操作NoteBook。内部JSON格式可能会改变，而nbFormat API则不会改变。

nbConvert是一种将NoteBook转换成另一种格式的工具。转换可以通过多种方式进行定制。在这里，我们使用一个模板包Jinja2扩展了一个现有的模板(请参阅http://jinja.pocoo.org/docs/).

## 还有更多...

有一个免费的在线服务，**nbview**，它允许我们在云平台中动态地以HTML呈现Jupyter Notebook。我们的想法是向nbview提供一个指向原始NoteBook的URL(在JSON中)，并得到一个呈现出来的HTML输出。nbview的主页(http://nbviewer.jupyter.org/)包含一些示例。此服务由Jupyter开发人员维护，并托管在Rackspace(https://www.rackspace.com)上。

GitHub自动呈现存储在存储库中的Jupyter Notebook。

可以在https://mybinder.org上找到binder，它允许我们将GitHub存储库转换成云中交互式NoteBook的集合。该服务是免费的，代码是开源的，因此任何人都可以提供自己的活页夹服务。

以下是一些参考资料:

* Documentation of nbconvert, at https://nbconvert.readthedocs.io/en/stable/
* RISE, create interactive slideshows out of Jupyter notebooks, at https://damianavila.github.io/RISE/


