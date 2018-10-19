# IPython 操作指引, 第二版 (2018年)

## 译序
本书简直是一部关于Ipython交互式计算的百科全书。虽然每一部分都没有深入，但这更有助于读者了解Ipython生态的全貌。

## 目录 


### [第1章: 使用Jupyter和IPython的交互式计算之旅](chapter01_basic)

* [1.1. 介绍IPython与Jupyter Notebook](chapter01_basic/01_notebook.md)
* [1.2. 开始在Jupyter Notebook中进行探索性数据分析](chapter01_basic/02_pandas.md)
* [1.3. 在NumPy中引入多维数组，用于快速数组计算](chapter01_basic/03_numpy.md)
* [1.4. 使用自定义魔法命令创建IPython扩展](chapter01_basic/04_magic.md)
* [1.5. 掌握IPython的配置系统](chapter01_basic/05_config.md)
* [1.6. 为Jupyter创建一个简单的内核](chapter01_basic/06_kernel.md)


### [第2章：交互计算的最佳实践](chapter02_best_practices)

* [2.1. 学习Unix Shell的基础知识](chapter02_best_practices/01_shell.md)
* [2.2. 使用Python 3的最新特性](chapter02_best_practices/02_py3.md)
* [2.3. 学习分布式版本控制系统Git的基础知识](chapter02_best_practices/03_git.md)
* [2.4. Git分支的典型工作流程](chapter02_best_practices/04_git_advanced.md)
* [2.5. 基于IPython的高效交互计算工作流程](chapter02_best_practices/05_workflows.md)
* [2.6. 进行可重复交互计算实验的十个技巧](chapter02_best_practices/06_tips.md)
* [2.7. 编写高质量的Python代码](chapter02_best_practices/07_high_quality.md)
* [2.8. 使用py.test编写单元测试](chapter02_best_practices/08_test.md)
* [2.9. 使用IPython调试代码](chapter02_best_practices/09_debugging.md) *


### [第3章：掌握Jupyter Notebook](chapter03_notebook)

* [3.1. 使用IPython块在NoteBook中进行编程教学](chapter03_notebook/01_blocks.md)
* [3.2. 使用nbconvert将Jupyter Notebook转换为其他格式](chapter03_notebook/02_nbformat.md)
* [3.3. 掌握Jupyter Notebook中的小部件](chapter03_notebook/03_widgets.md)
* [3.4. 在Python、HTML和JavaScript中创建自定义Jupyter Notebook小部件](chapter03_notebook/04_custom_widgets.md)
* [3.5. 配置Jupyter Notebook](chapter03_notebook/05_custom_notebook.md) *
* [3.6. 介绍JupyterLab](chapter03_notebook/06_jupyterlab.md)

<!-- 

### [Chapter 4 : Profiling and Optimization](chapter04_optimization)
### [第4章: 分析与优化](chapter04_optimization)

* [4.1. Evaluating the time taken by a command in IPython](chapter04_optimization/01_timeit.md) *
* [4.1. 在IPython中估算一条指令的执行时间](chapter04_optimization/01_timeit.md) *
* [4.2. Profiling your code easily with cProfile and IPython](chapter04_optimization/02_profile.md)
* [4.2. 使用cProfile和IPython轻松分析代码](chapter04_optimization/02_profile.md)
* [4.3. Profiling your code line-by-line with line_profiler](chapter04_optimization/03_linebyline.md)
* [4.3. 使用line_profiler逐行分析代码](chapter04_optimization/03_linebyline.md)
* [4.4. Profiling the memory usage of your code with memory_profiler](chapter04_optimization/04_memprof.md)
* [4.4. 使用memory_profiler分析代码的内存使用情况](chapter04_optimization/04_memprof.md)
* [4.5. Understanding the internals of NumPy to avoid unnecessary array copying](chapter04_optimization/05_array_copies.md)
* [4.5. 了解NumPy的内部结构以避免不必要的数组复制](chapter04_optimization/05_array_copies.md)
* [4.6. Using stride tricks with NumPy](chapter04_optimization/06_stride_tricks.md)
* [4.6. 使用与NumPy的步幅(stride)技巧](chapter04_optimization/06_stride_tricks.md)
* [4.7. Implementing an efficient rolling average algorithm with stride tricks](chapter04_optimization/07_rolling_average.md)
* [4.7. 使用步幅(stride)技巧实现高效的滚动平均算法](chapter04_optimization/07_rolling_average.md)
* [4.8. Processing large NumPy arrays with memory mapping](chapter04_optimization/08_memmap.md)
* [4.8. 使用内存映射处理大型NumPy数组](chapter04_optimization/08_memmap.md)
* [4.9. Manipulating large arrays with HDF5](chapter04_optimization/09_hdf5_array.md) *
* [4.9. 使用HDF5操作大数组](chapter04_optimization/09_hdf5_array.md) *


### [Chapter 5 : High-Performance Computing](chapter05_hpc)
### [第5章：高性能计算](chapter05_hpc)

* [5.1. Knowing Python to write faster code](chapter05_hpc/01_slow.md)
* [5.1. 了解Python以便更快编写代码](chapter05_hpc/01_slow.md)
* [5.2. Accelerating pure Python code with Numba and just-in-time compilation](chapter05_hpc/02_numba.md)
* [5.2. 用Numba和即时编译技术加速纯Python代码](chapter05_hpc/02_numba.md)
* [5.3. Accelerating array computations with Numexpr](chapter05_hpc/03_numexpr.md)
* [5.3. 使用Numexpr加速数组计算](chapter05_hpc/03_numexpr.md)
* [5.4. Wrapping a C library in Python with ctypes](chapter05_hpc/04_ctypes.md)
* [5.4. 使用ctypes包裹c语音编写的代码库](chapter05_hpc/04_ctypes.md)
* [5.5. Accelerating Python code with Cython](chapter05_hpc/05_cython.md)
* [5.5. 使用Cython加速Python代码](chapter05_hpc/05_cython.md)
* [5.6. Optimizing Cython code by writing less Python and more C](chapter05_hpc/06_ray.md)
* [5.6. 多写C代码少些Python以优化Cython代码](chapter05_hpc/06_ray.md)
* [5.7. Releasing the GIL to take advantage of multi-core processors with Cython and OpenMP](chapter05_hpc/07_openmp.md)
* [5.7. 释放GIL以便用Cython和OpenMP利用多核处理器](chapter05_hpc/07_openmp.md)
* [5.8. Writing massively parallel code for NVIDIA graphics cards (GPUs) with CUDA](chapter05_hpc/08_cuda.md)
* [5.8. 用CUDA为NVIDIA显卡(GPU)编写大规模并行代码](chapter05_hpc/08_cuda.md)
* [5.9. Distributing Python code across multiple cores with IPython](chapter05_hpc/09_ipyparallel.md)
* [5.9. 使用IPython把Python代码分发到多个处理器内核上](chapter05_hpc/09_ipyparallel.md)
* [5.10. Interacting with asynchronous parallel tasks in IPython](chapter05_hpc/10_async.md)
* [5.10. 与IPython中的异步并行任务交互](chapter05_hpc/10_async.md)
* [5.11. Performing out-of-core computations on large arrays with Dask](chapter05_hpc/11_dask.md)
* [5.11. 使用Dask对大数组执行核外计算](chapter05_hpc/11_dask.md)
* [5.12. Trying the Julia programming language in the Jupyter Notebook](chapter05_hpc/12_julia.md) *
* [5.12. 在Jupyter Notebook中尝试使用Julia编程语言](chapter05_hpc/12_julia.md) *


### [Chapter 6 : Data Visualization](chapter06_viz)
### [第6章：数据可视化](chapter06_viz)

* [6.1. Using matplotlib styles](chapter06_viz/01_styles.md)
* [6.1. 使用matplotlib样式](chapter06_viz/01_styles.md)
* [6.2. Creating statistical plots easily with seaborn](chapter06_viz/02_seaborn.md)
* [6.2. 使用seaborn轻松创建统计图](chapter06_viz/02_seaborn.md)
* [6.3. Creating interactive Web visualizations with Bokeh and HoloViews](chapter06_viz/03_bokeh.md)
* [6.3. 使用Bokeh和HoloViews创建交互式Web可视化](chapter06_viz/03_bokeh.md)
* [6.4. Visualizing a NetworkX graph in the Notebook with D3.js](chapter06_viz/04_d3.md)
* [6.4. 在Notebook中用D3.js对NetworkX图进行可视化处理](chapter06_viz/04_d3.md)
* [6.5. Discovering interactive visualization libraries in the Notebook](chapter06_viz/05_widgets.md) *
* [6.5. 在NoteBook中探索交互式可视化库](chapter06_viz/05_widgets.md) *
* [6.6. Creating plots with Altair and the Vega-Lite specification](chapter06_viz/06_altair.md)
* [6.6. 利用Altair和Vega-Lite规范生成图表](chapter06_viz/06_altair.md)


### [Chapter 7 : Statistical Data Analysis](chapter07_stats)
### [第7章：统计数据分析](chapter07_stats)

* [7.1. Exploring a dataset with pandas and matplotlib](chapter07_stats/01_pandas.md)
* [7.1. 用Pandas和matplotlib解析数据集](chapter07_stats/01_pandas.md)
* [7.2. Getting started with statistical hypothesis testing — a simple z-test](chapter07_stats/02_z_test.md)
* [7.2. 从统计假设检验开始——一个简单的z检验](chapter07_stats/02_z_test.md)
* [7.3. Getting started with Bayesian methods](chapter07_stats/03_bayesian.md)
* [7.3. 开始使用贝叶斯方法](chapter07_stats/03_bayesian.md)
* [7.4. Estimating the correlation between two variables with a contingency table and a chi-squared test](chapter07_stats/04_correlation.md)
* [7.4. 用列联表和卡方检验估计两个变量之间的相关性](chapter07_stats/04_correlation.md)
* [7.5. Fitting a probability distribution to data with the maximum likelihood method](chapter07_stats/05_mlfit.md)
* [7.5. 用最大似然法拟合数据的概率分布](chapter07_stats/05_mlfit.md)
* [7.6. Estimating a probability distribution nonparametrically with a kernel density estimation](chapter07_stats/06_kde.md)
* [7.6. 用核密度估计非参数概率分布](chapter07_stats/06_kde.md)
* [7.7. Fitting a Bayesian model by sampling from a posterior distribution with a Markov Chain Monte Carlo method](chapter07_stats/07_pymc.md)
* [7.7. 用马尔可夫链蒙特卡罗方法从后验分布中抽样拟合贝叶斯模型](chapter07_stats/07_pymc.md)
* [7.8. Analyzing data with the R programming language in the Jupyter Notebook](chapter07_stats/08_r.md) *
* [7.8. 使用R编程语言在Jupyter Notebook上分析数据](chapter07_stats/08_r.md) *


### [Chapter 8 : Machine Learning](chapter08_ml)
### [第8章: 机器学习](chapter08_ml)

* [8.1. Getting started with scikit-learn](chapter08_ml/01_scikit.md)
* [8.1. scikit-learn入门](chapter08_ml/01_scikit.md)
* [8.2. Predicting who will survive on the Titanic with logistic regression](chapter08_ml/02_titanic.md) *
* [8.2. 通过logistic回归预测谁能在泰坦尼克号上生存下来](chapter08_ml/02_titanic.md) *
* [8.3. Learning to recognize handwritten digits with a K-nearest neighbors classifier](chapter08_ml/03_digits.md)
* [8.3. 学习使用K近邻分类器识别手写数字](chapter08_ml/03_digits.md)
* [8.4. Learning from text — Naive Bayes for Natural Language Processing](chapter08_ml/04_text.md)
* [8.4. 从文本中学习--用于自然语言处理的朴素贝叶斯算法](chapter08_ml/04_text.md)
* [8.5. Using support vector machines for classification tasks](chapter08_ml/05_svm.md)
* [8.5. 分类任务中使用支持向量机](chapter08_ml/05_svm.md)
* [8.6. Using a random forest to select important features for regression](chapter08_ml/06_random_forest.md)
* [8.6. 用随机森林选择回归的重要特征](chapter08_ml/06_random_forest.md)
* [8.7. Reducing the dimensionality of a dataset with a principal component analysis](chapter08_ml/07_pca.md) *
* [8.7. 用主分量分析法降低数据集的维度](chapter08_ml/07_pca.md) *
* [8.8. Detecting hidden structures in a dataset with clustering](chapter08_ml/08_clustering.md)
* [8.8. 利用集群探测数据中隐藏的结构](chapter08_ml/08_clustering.md)


### [第9章 : Numerical Optimization](chapter09_numoptim)
### [第9章 : 数值优化](chapter09_numoptim)

* [9.1. Finding the root of a mathematical function](chapter09_numoptim/01_root.md) *
* [9.1. 求数学函数的根](chapter09_numoptim/01_root.md) *
* [9.2. Minimizing a mathematical function](chapter09_numoptim/02_minimize.md)
* [9.2. 最小化数学函数](chapter09_numoptim/02_minimize.md)
* [9.3. Fitting a function to data with nonlinear least squares](chapter09_numoptim/03_curvefitting.md)
* [9.3. 用非线性最小二乘法将数据拟合成函数](chapter09_numoptim/03_curvefitting.md)
* [9.4. Finding the equilibrium state of a physical system by minimizing its potential energy](chapter09_numoptim/04_energy.md)
* [9.4. 通过最小化其势能求出物理系统的平衡态](chapter09_numoptim/04_energy.md)


### [第10章: Signal Processing](chapter10_signal)
### [第10章: 信号处理](chapter10_signal)

* [10.1. Analyzing the frequency components of a signal with a Fast Fourier Transform](chapter10_signal/01_fourier.md)
* [10.1. 用快速傅里叶变换分析信号的频率分量](chapter10_signal/01_fourier.md)
* [10.2. Applying a linear filter to a digital signal](chapter10_signal/02_filter.md)
* [10.2. 将线性滤波器应用于数字信号](chapter10_signal/02_filter.md)
* [10.3. Computing the autocorrelation of a time series](chapter10_signal/03_autocorrelation.md)
* [10.3. 计算时间序列的自相关](chapter10_signal/03_autocorrelation.md)


### [第11章: Image and Audio Processing](chapter11_image)
### [第11章: 图像与音频处理](chapter11_image)

* [11.1. Manipulating the exposure of an image](chapter11_image/01_exposure.md)
* [11.1. 操纵图像的曝光](chapter11_image/01_exposure.md)
* [11.2. Applying filters on an image](chapter11_image/02_filters.md)
* [11.2. 在图像上应用过滤器](chapter11_image/02_filters.md)
* [11.3. Segmenting an image](chapter11_image/03_segmentation.md)
* [11.3. 分割图像](chapter11_image/03_segmentation.md)
* [11.4. Finding points of interest in an image](chapter11_image/04_interest.md)
* [11.4. 在图像中找到感兴趣的点](chapter11_image/04_interest.md)
* [11.5. Detecting faces in an image with OpenCV](chapter11_image/05_faces.md) *
* [11.5. 用OpenCV检测图像中的人脸](chapter11_image/05_faces.md) *
* [11.6. Applying digital filters to speech sounds](chapter11_image/06_speech.md)
* [11.6. 把数字滤波器运用于语音](chapter11_image/06_speech.md)
* [11.7. Creating a sound synthesizer in the Notebook](chapter11_image/07_synth.md)
* [11.7. 在Notebook中创建声音合成器](chapter11_image/07_synth.md)


### [第12章: Deterministic Dynamical Systems](chapter12_deterministic)
### [第12章: 确定性动力系统](chapter12_deterministic)

* [12.1. Plotting the bifurcation diagram of a chaotic dynamical system](chapter12_deterministic/01_bifurcation.md)
* [12.1. 绘制混沌动力系统的分岔图](chapter12_deterministic/01_bifurcation.md)
* [12.2. Simulating an elementary cellular automaton](chapter12_deterministic/02_cellular.md)
* [12.2. 模拟基本元胞自动机](chapter12_deterministic/02_cellular.md)
* [12.3. Simulating an ordinary differential equation with SciPy](chapter12_deterministic/03_ode.md)
* [12.3. 用SciPy模拟一个常微分方程](chapter12_deterministic/03_ode.md)
* [12.4. Simulating a partial differential equation — reaction-diffusion systems and Turing patterns](chapter12_deterministic/04_turing.md)
* [12.4. 模拟偏微分方程--反应扩散系统和图灵模式](chapter12_deterministic/04_turing.md)


### [第13章: Stochastic Dynamical Systems](chapter13_stochastic)
### [第13章: 随机动力系统](chapter13_stochastic)

* [13.1. Simulating a discrete-time Markov chain](chapter13_stochastic/01_markov.md)
* [13.1. 模拟离散时马尔可夫链](chapter13_stochastic/01_markov.md)
* [13.2. Simulating a Poisson process](chapter13_stochastic/02_poisson.md) *
* [13.2. 模拟泊松过程](chapter13_stochastic/02_poisson.md) *
* [13.3. Simulating a Brownian motion](chapter13_stochastic/03_brownian.md)
* [13.3. 模拟布朗运动](chapter13_stochastic/03_brownian.md)
* [13.4. Simulating a stochastic differential equation](chapter13_stochastic/04_sde.md)
* [13.4. 模拟随机微分方程](chapter13_stochastic/04_sde.md)


### [第14章 : Graphs, Geometry, and Geographic Information Systems](chapter14_graphgeo)
### [第14章 : 图形,几何和地理信息系统](chapter14_graphgeo)

* [14.1. Manipulating and visualizing graphs with NetworkX](chapter14_graphgeo/01_networkx.md) *
* [14.1. 用NetworkX对图形进行操作和可视化](chapter14_graphgeo/01_networkx.md) *
* [14.2. Drawing flight routes with NetworkX](chapter14_graphgeo/02_airports.md)
* [14.2. 用NetworkX绘制航线](chapter14_graphgeo/02_airports.md)
* [14.3. Resolving dependencies in a directed acyclic graph with a topological sort](chapter14_graphgeo/03_dag.md)
* [14.3. 用拓扑排序解决有向无环图中的依赖关系](chapter14_graphgeo/03_dag.md)
* [14.4. Computing connected components in an image](chapter14_graphgeo/04_connected.md)
* [14.4. 计算图像中的连接组件](chapter14_graphgeo/04_connected.md)
* [14.5. Computing the Voronoi diagram of a set of points](chapter14_graphgeo/05_voronoi.md)
* [14.5. 计算一组点的Voronoi图](chapter14_graphgeo/05_voronoi.md)
* [14.6. Manipulating geospatial data with Cartopy](chapter14_graphgeo/06_gis.md)
* [14.6. 用Cartopy操纵地理空间数据](chapter14_graphgeo/06_gis.md)
* [14.7. Creating a route planner for a road network](chapter14_graphgeo/07_gps.md)
* [14.7. 为路网创建路径规划器](chapter14_graphgeo/07_gps.md)


### [第15章 : Symbolic and Numerical Mathematics](chapter15_symbolic)
### [第15章 : 符号和数值数学](chapter15_symbolic)

* [15.1. Diving into symbolic computing with SymPy](chapter15_symbolic/01_sympy_intro.md)
* [15.1. 用SymPy深入符号计算](chapter15_symbolic/01_sympy_intro.md)
* [15.2. Solving equations and inequalities](chapter15_symbolic/02_solvers.md)
* [15.2. 解方程与不等式](chapter15_symbolic/02_solvers.md)
* [15.3. Analyzing real-valued functions](chapter15_symbolic/03_function.md)
* [15.3. 分析实值函数](chapter15_symbolic/03_function.md)
* [15.4. Computing exact probabilities and manipulating random variables](chapter15_symbolic/04_stats.md)
* [15.4. 精确概率的计算与随机变量的操纵](chapter15_symbolic/04_stats.md)
* [15.5. A bit of number theory with SymPy](chapter15_symbolic/05_number_theory.md)
* [15.5. 一点关于SymPy的数论](chapter15_symbolic/05_number_theory.md)
* [15.6. Finding a Boolean propositional formula from a truth table](chapter15_symbolic/06_logic.md)
* [15.6. 从真值表中寻找布尔命题公式](chapter15_symbolic/06_logic.md)
* [15.7. Analyzing a nonlinear differential system — Lotka-Volterra (predator-prey) equations](chapter15_symbolic/07_lotka.md)
* [15.7. 非线性微分系统分析 -- Lotka-Volterra方程](chapter15_symbolic/07_lotka.md)
* [15.8. Getting started with Sage](chapter15_symbolic/08_sage.md) *
* [15.8. Sage入门](chapter15_symbolic/08_sage.md) *

-->

## 说明 

Python是数据科学和数值计算领域开源平台之一。IPython和相应的Jupyter Nodebook为Python提供了高效的数据分析和交互可视化接口，
它们构成了通往数据科学和数值计算平台理想入口。

IPython交互式计算和可视化手册第二版, 包含了许多现成的、专注于高性能科学计算和数据分析的实例代码。从最新的Ipython Jupyter特性到最先进的技巧，
以帮助您编写更好、更快的代码。你可以把这些最先进的方法应用到各种现实世界的例子中，比如应用数学、科学建模和机器学习方面。

本书的第一部分包括编程技术：代码质量和再现性、代码优化、通过实时编译、并行计算和图形卡编程实现高性能计算。
第二部分涉及数据科学、统计、机器学习、信号和图像处理、动力系统、纯数学和应用数学。

