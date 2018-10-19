[*Chapter 3 : Mastering the Jupyter Notebook*](../)
[*第三章：掌握Jupyter Notebook*](../)

# Introduction
# 介绍

In this chapter, we will see several advanced features and usage examples of the Jupyter Notebook. As we have only seen basic features in the previous chapters, we will dive deeper into the architecture of the Notebook here.
在本章中，我们将看到Jupyter Notebook的一些高级特性和使用示例。由于我们在前几章中只看到了基本特性，我们将在这里深入研究NoteBook的体系结构。

## The Notebook ecosystem
## NoteBook的生态系统

Jupyter notebooks are represented as **JavaScript Object Notation (JSON)** documents. JSON is a language-independent, text-based file format for representing structured documents. As such, notebooks can be processed by any programming language, and they can be converted to other formats such as Markdown, HTML, LaTeX/PDF, and others.
Jupyter Notebook被表示为**JavaScript Object Notetion(JSON)**文档。JSON是一种独立于语言的、基于文本的文件格式，用于表示结构化文档.因此，任何编程语言都可以处理NoteBook，并且可以将它们转换为其他格式，如Markdown、HTML、LaTeX/PDF等。

There is an ecosystem of tools around the Notebook. Notebooks are being used to create slides, teaching materials, blog posts, research papers, and even books. In fact, this very book is entirely written in the Notebook using the Markdown format and a custom-made Python tool.
NoteBook周围有一个工具生态系统。NoteBook正被用来制作幻灯片，教材，博客文章，研究论文，甚至书籍。实际上，这本书完全是用Markdown格式和定制的Python工具在NoteBook中编写的。

**JupyterLab** is the next generation of the Jupyter Notebook. It is still in an early stage of development at the time of this writing. We cover it in the last recipe of this chapter.
**JupyterLab**是Jupyter Notebook的下一代。在写这篇文章的时候，它还处于发展的早期阶段。我们在这一章的最后一部分会讲到。

## Architecture of the Jupyter Notebook
## Jupyter Notebook的架构

Jupyter implements a two-process model, with a **kernel** and a **client**. The client is the interface offering the user the ability to send code to the kernel. The kernel executes the code and returns the result to the client for display. In the **Read-Evaluate-Print Loop (REPL)** terminology, the kernel implements the *Evaluate*, whereas the client implements the *Read* and the *Print* of the process.
Jupyter实现了一个具有**内核(kernel)**和**客户端(client)**的双进程模型。客户端是为用户提供向内核发送代码的接口。内核执行代码并将结果返回给客户端以供显示。在**读取(Read)-求值(Evaluate)-打印(Print)循环(REPL)**术语中，内核实现**求值(Evaluate)**，而客户端实现进程的**读取(read)**和**打印(print)**。

The client can be a Qt widget if we run the Qt console, or a browser if we run the Jupyter Notebook. In the Jupyter Notebook, the kernel receives entire cells at once, so it has no notion of a notebook. There is a strong decoupling between the linear document containing the notebook, and the underlying kernel.
如果我们运行Qt控制台，客户端可以是一个QT小部件，如果我们运行Jupyter Notebook，客户端可以是一个浏览器。在Jupyter Notebook中，内核同时接收整个单元格，因此它没有NoteBook的概念。包含NoteBook的线性文档与底层内核之间存在很强的解耦关系。

All communication procedures between the different processes are implemented on top of the **ZeroMQ** (or **ZMQ**) messaging protocol (http://zeromq.org). The Notebook communicates with the underlying kernel using **WebSocket**, a TCP-based protocol implemented in modern web browsers.
不同进程之间的所有通信过程都是在**ZeroMQ**(或**ZMQ**)消息传递协议(http://zeromq.org).)之上实现的。Notebook使用**WebSocket**与底层内核通信，这是一种在现代Web浏览器中实现的基于TCP的协议。

### Connecting multiple clients to one kernel
### 将多个客户端连接到一个内核

In a notebook, typing `%connect_info` in a cell gives the information we need to connect a new client (such as a Qt console) to the underlying kernel:
在NoteBook中，在单元格中输入`%connect_info`就可以得到连接新客户端(比如Qt控制台)到底层内核所需的信息:

```python
%connect_info
```

```{output:stdout}
{
  "shell_port": 58645,
  "iopub_port": 47422,
  "stdin_port": 60550,
  "control_port": 39092,
  "hb_port": 49409,
  "ip": "127.0.0.1",
  "key": "2298f955-7020b0ce534e7a8d81053d43",
  "transport": "tcp",
  "signature_scheme": "hmac-sha256",
  "kernel_name": ""
}

Paste the above JSON into a file, and connect with:
    $> jupyter <app> --existing <file>
or, if you are local, you can connect with just:
    $> jupyter <app> --existing kernel-4342f625-a8...
or even just:
    $> jupyter <app> --existing
if this is the most recent Jupyter kernel you
    have started.
```

Here, `<app>` is `console`, `qtconsole`, or `notebook`
在这里，`<app>`是`console`，`qtconsole`，或`notebook`

### JupyterHub

**JupyterHub**, available at https://jupyterhub.readthedocs.io/en/latest/, is a Python library that can be used to serve notebooks to a set of end-users, for example students of a particular class, or lab members in a research group. It handles user authentication and other low-level details.
**JupyterHub**，可在https://jupyterhub.readthedocs.io/en/latest/上找到。是一个Python库，可用于为一组终端用户(例如某个班级的学生或研究小组的实验室成员)提供NoteBook。它处理用户身份验证和其他低级细节。

## Security in notebooks
## NoteBook的安全性

It is possible for an attacker to put malicious code in a Jupyter notebook. Since notebooks may contain hidden JavaScript code in a cell output, it is theoretically possible for malicious code to execute surreptitiously when the user opens a notebook.
攻击者有可能将恶意代码放入Jupyter Notebook中。由于NoteBook可能在单元格输出中包含隐藏的JavaScript代码，理论上，恶意代码可能在用户打开NoteBook时偷偷执行。

For this reason, Jupyter has a security model where HTML and JavaScript code in a notebook can be either trusted or untrusted. Outputs generated by the user are always trusted. However, outputs that were already there when the user first opened an existing notebook are untrusted.
因此，Jupyter有一个安全模型，其中NoteBook中的HTML和JavaScript代码可以是可信的，也可以是不可信的。用户生成的输出总是可信的。然而，当用户第一次打开现有的NoteBook时已经存在的输出是不可信的。

The security model is based on a cryptographic signature present in every notebook. This signature is generated using a secret key owned by every user.
安全模型是基于每个NoteBook中的加密签名。此签名使用每个用户拥有的密钥生成。

## References
## 参考文献

The following are some references about the Notebook architecture:
以下是有关NoteBook架构的一些参考资料：

* Overview of IPython at http://ipython.readthedocs.io/en/stable/overview.html
* IPython概述 at http://ipython.readthedocs.io/en/stable/overview.html
* Documentation of the Jupyter Notebook, available at https://jupyter.readthedocs.io/en/latest/
* Jupyter Notebook文档 https://jupyter.readthedocs.io/en/latest/
* Security in the Notebook, described at http://jupyter-notebook.readthedocs.io/en/stable/security.html
* NoteBook中的安全性，描述 at http://jupyter-notebook.readthedocs.io/en/stable/security.html
* The Jupyter messaging protocol, at http://jupyter-client.readthedocs.io/en/latest/messaging.html
* Jupyter通讯协议， at http://jupyter-client.readthedocs.io/en/latest/messaging.html
* Wrapper kernels at http://jupyter-client.readthedocs.io/en/latest/wrapperkernels.html
* 包装内核 at http://jupyter-client.readthedocs.io/en/latest/wrapperkernels.html

Here are a few kernels in non-Python languages for the Notebook:
下面是一些用非python语言编写的NoteBook内核:

* IJulia, available at https://github.com/JuliaLang/IJulia.jl
* IRkernel, available at https://github.com/IRkernel/IRkernel
* IHaskell, available at https://github.com/gibiansky/IHaskell
* Dozens of kernels are referenced at https://github.com/jupyter/jupyter/wiki/Jupyter-kernels
