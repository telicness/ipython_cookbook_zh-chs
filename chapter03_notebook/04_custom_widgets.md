[*第三章：掌握Jupyter Notebook*](./)

# 3.4. 用Python、HTML和JavaScript创建定制的Jupyter Notebook小部件

ipywidget包提供了许多内置的控件小部件，可以与Jupyter Notebook中的代码和数据进行交互。在这个参考手册中，我们将展示如何从头开始构建一个定制的交互式小部件，在内核端使用Python，在客户端(前端)使用HTML/JavaScript。小部件只显示两个按钮来增加和减少一个数字。可以从内核(Python代码)或客户机(浏览器)访问和更新数字。

## 怎么做...

1. 让我们导入包：

```python
import ipywidgets as widgets
from traitlets import Unicode, Int, validate
```

2. 我们创建了一个从`DOMWidget`派生出来的`CounterWidget`类：

```python
class CounterWidget(widgets.DOMWidget):
    _view_name = Unicode('CounterView').tag(sync=True)
    _view_module = Unicode('counter').tag(sync=True)
    value = Int(0).tag(sync=True)
```

这个类表示小部件的Python部分。`_view_name`和`_view_module`属性引用JavaScript部分的名称和模块。我们使用traitlet包来指定变量的类型。`value`属性是计数器值，初始化为整数0。所有这些属性的值都是在Python和JavaScript之间同步的，因此使用了`sync=True`选项。

3. 现在我们转到小部件的JavaScript端。我们可以使用`%%javascript` cell魔法在NoteBook中直接编写代码。小部件框架依赖于几个JavaScript库:jQuery(表示为`$`变量)、require.js(模块和依赖项)和Backbone.js(模型视图控制器框架)：

```python
%%javascript
// We make sure the `counter` module is defined
// only once.
require.undef('counter');

// We define the `counter` module depending on the
// Jupyter widgets framework.
define('counter', ["@jupyter-widgets/base"],
       function(widgets) {

    // We create the CounterView frontend class,
    // deriving from DOMWidgetView.
    var CounterView = widgets.DOMWidgetView.extend({

        // This method creates the HTML widget.
        render: function() {
            // The value_changed() method should be
            // called when the model's value changes
            // on the kernel side.
            this.value_changed();
            this.model.on('change:value',
                          this.value_changed, this);

            var model = this.model;
            var that = this;

            // We create the plus and minus buttons.
            this.bm = $('<button/>')
            .text('-')
            .click(function() {
                // When the button is clicked,
                // the model's value is updated.
                var x = model.get('value');
                model.set('value', x - 1);
                that.touch();
            });

            this.bp = $('<button/>')
            .text('+')
            .click(function() {
                var x = model.get('value');
                model.set('value', x + 1);
                that.touch();
            });

            // This element displays the current
            // value of the counter.
            this.span = $('<span />')
            .text('0')
            .css({marginLeft: '10px',
                  marginRight: '10px'});

            // this.el represents the widget's DOM
            // element. We add the minus button,
            // the span element, and the plus button.
            $(this.el)
            .append(this.bm)
            .append(this.span)
            .append(this.bp);
        },

        value_changed: function() {
            // Update the displayed number when the
            // counter's value changes.
            var x = this.model.get('value');
            $($(this.el).children()[1]).text(x);
        },
    });

    return {
        CounterView : CounterView
    };
});
```

4. 让我们显示这个小部件：

```python
w = CounterWidget()
w
```

![Custom widget](04_custom_widgets_files/04_custom_widgets_11_0.png)

5. 按下按钮将立即更新该值。

![Custom widget](04_custom_widgets_files/widget2.png)

6. 计数器的值在内核端自动更新：

```python
print(w.value)
```

```{output:stdout}
4
```

7. 相反，我们可以从Python中更新值，并且在前端更新:

```python
w.value = 5
```

![Custom widget](04_custom_widgets_files/04_custom_widgets_17_0.png)

## 还有更多...

以下是一些参考资料：

* 自定义小部件教程 at https://ipywidgets.readthedocs.io/en/stable/examples/Widget%20Custom.html
* Backbone.js库 at http://backbonejs.org/

## 另请参阅

* 掌握Jupyter Notebook中的小部件
