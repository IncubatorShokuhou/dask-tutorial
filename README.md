# Dask 教程

本教程最后一次在 SciPy 2020上提供，这是一个虚拟会议。
[SciPy 2020教程的视频可在线获取](https://www.youtube.com/watch?v=EybGGLbLipI).

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/dask/dask-tutorial/main?urlpath=lab)
[![Build Status](https://github.com/dask/dask-tutorial/workflows/CI/badge.svg)](https://github.com/dask/dask-tutorial/actions?query=workflow%3ACI)

Dask提供一种在大于内存的数据集上多核运行的方法。

我们可以从高阶和低阶两个层次考虑：

* **高阶集合：** Dask提供了高阶的Array，Bag和DataFrame, 它们模仿了NumPy，List和Pandas，但可以在不适合主内存的数据集上并行操作。 
    Dask的高阶集合是NumPy和Pandas在大型数据集的替代品。
* **低阶计划程序：** Dask提供了动态任务计划程序，可并行执行任务图。 这些执行引擎为上述高阶集合提供支持，但也可以为用户定义的自定义工作负载提供支持。 这些调度器的等待时间很短（大约1毫秒），并且努力在较小的内存占用空间中运行计算。 Dask的调度器是在复杂情况或其他任务调度系统（如`Luigi`或`IPython parallel`）中直接使用`threading`或`multiprocessing`库的替代方法。

不同的用户在不同的级别上进行操作，但了解两者都有帮助。 本教程将在`dask.array`和`dask.dataframe`的高阶使用（偶数章节）和dask图和调度器的低阶使用（奇数章节）之间进行交错。

## 准备工作

#### 1. 你需要克隆这个仓库

    git clone http://github.com/IncubatorShokuhou/dask-tutorial

然后安装必要的包。
有三种方法可以安装这些包。选择最适合你的方法，且 ***只需选择其中一个***。
他们分别是（按推荐顺序）: 

#### 2a) 创建一个conda环境(推荐)

在主仓库目录

    conda env create -f binder/environment.yml
    conda activate dask-tutorial
    jupyter labextension install @jupyter-widgets/jupyterlab-manager
    jupyter labextension install @bokeh/jupyter_bokeh

#### 2b) 在一个已有的环境中安装

您将需要以下核心库

    conda install numpy pandas h5py pillow matplotlib scipy toolz pytables snakeviz scikit-image dask distributed -c conda-forge

您可能会发现以下库对某些练习有帮助

    conda install python-graphviz -c conda-forge

请注意，此选项将更改您的现有环境，可能会更改您已经安装的软件包的版本。

#### 2c) 使用Dockerfile

您可以从提供的Dockerfile中构建Docker映像。

    $ docker build . # 这将构建a)中相同的环境

运行一个容器，将ID替换为先前命令的输出值

    $ docker run -it -p 8888:8888 -p 8787:8787 <container_id_or_tag>

上述命令会生成一个链接(`例如 http://(container_id or 127.0.0.1):8888/?token=<sometoken>`) ，可用于从浏览器访问notebook。 您可能需要用`localhost`或`127.0.0.1`替换为给定的主机名。

#### 你只需要执行上述选项中的一个!

### 启动notebook

从仓库目录执行

    jupyter notebook

或

    jupyter lab

该步骤已在选项 c) 中执行，不需要再重复。

## 链接

*  参考
    *  [文档](https://dask.org/)
    *  [示例](https://examples.dask.org/)
    *  [代码](https://github.com/dask/dask/)
    *  [博客](https://blog.dask.org/)
*  求助
    *   Stack Overflow上的[`dask`](http://stackoverflow.com/questions/tagged/dask)标签, 针对用法问题
    *   [github issues](https://github.com/dask/dask/issues/new) 针对错误报告和功能请求
    *   [gitter chat](https://gitter.im/dask/dask) 针对一般问题、非错误问题、讨论
    *   参加现场教程

## 大纲

0. [概述](00_overview.ipynb) - dask在宇宙中的地位。

1. [延迟执行](01_dask.delayed.ipynb) - 并行化一般python代码的单函数方法。

1x. [惰性执行](01x_lazy.ipynb) - 惰性执行背后的一些原则，供感兴趣的人参考。

2. [Bag](02_bag.ipynb) - 第一个高级集合：用于函数式编程风格和清理杂乱数据的通用迭代器。

3. [Array](03_array.ipynb) - 分块化的类numpy功能，包含分布在集群中的 numpy 数组集合。

4. [Dataframe](04_dataframe.ipynb) - 对分布在集群中的许多Pandas Dataframe的并行操作。

5. [分布式](05_distributed.ipynb) - Dask的集群调度器，以及如何查看UI的详细信息。

6. [进阶分布式](06_distributed_advanced.ipynb) - 关于分布式计算的更多细节，包括如何调试。

7. [Dataframe存储](07_dataframe_storage.ipynb) - 将Dataframe读写到磁盘的有效方法。

8. [机器学习](08_machine_learning.ipynb) - 将dask应用于机器学习问题。
