=================
创建项目
=================

Creating projects

.. tab:: 中文

    在本教程中，我们将演示如何使用 ``environment.yml`` 文件，在 conda 中设置一个新的 Python 项目。此文件可帮助你追踪依赖项，并便于与他人共享项目。我们将介绍如何创建项目、添加简单的 Python 程序，以及如何随着需求增加更新依赖项。

.. tab:: 英文

    In this tutorial, we will walk through how to set up a new Python project in conda
    using an ``environment.yml`` file. This file will help you keep track of your
    dependencies and share your project with others. We cover how to create your
    project, add a simple Python program and update it with new dependencies.

需求
============

Requirements

.. tab:: 中文

    要跟随本教程操作，你需要一个已安装且可用的 conda 环境。如果尚未安装，请参考我们的 :doc:`安装指南 <../install/index>` 获取安装说明。

    本教程大量依赖使用终端（在 Windows 上是命令提示符或 PowerShell），因此你应熟悉如 ``cd`` 和 ``ls`` 等基本命令的使用。

.. tab:: 英文

    To follow along, you will need a working conda installation. Please head
    over to our :doc:`installation guide <../install/index>` for instructions on how
    to get conda installed if you do not have it.

    This tutorial relies heavily on using your computer's terminal (Command Prompt or PowerShell
    on Windows), so it is also important to have a working familiarity with using basic commands
    such as ``cd`` and ``ls``.

创建项目文件
============================

Creating the project's files

.. tab:: 中文

    首先，我们需要一个目录来存放项目的所有文件。可以使用以下命令创建该目录::

        mkdir my-project

    在该目录下，我们将创建一个新的 ``environment.yml`` 文件，用于声明该 Python 项目的依赖项。请使用你偏好的文本编辑器（如 VSCode、PyCharm、vim 等）创建此文件，并添加以下内容：

    .. code-block:: yaml

        name: my-project
        channels:
        - defaults
        dependencies:
        - python

    我们来简单解释一下该文件的各个部分：

    .. glossary::

        Name
            环境名称。在这里我们使用了 "my-project"，但你可以根据需要自定义名称。

        Channels
            指定 conda 搜索软件包的通道。我们这里使用了 ``defaults``，你也可以添加如 ``conda-forge`` 或 ``bioconda`` 等其他通道。

        Dependencies
            声明项目所需的所有依赖项。目前我们仅添加了 ``python``，后续会继续补充。

.. tab:: 英文

    To start off, we will need a directory that will contain the files for our project. This can
    be created with the following command::

        mkdir my-project

    In this directory, we will now create a new ``environment.yaml`` file, which will hold the
    dependencies for our Python project. In your text editor (e.g. VSCode, PyCharm, vim, etc.),
    create this file and add the following:

    .. code-block:: yaml

        name: my-project
        channels:
        - defaults
        dependencies:
        - python

    Let's briefly go over what each part of this file means.

    .. glossary::

        Name
            The name of your environment. Here, we have chosen the name "my-project", but this can
            be anything you want.

        Channels
            Channels specify where you want conda to search for packages. We have chosen the
            ``defaults`` channel, but others such as ``conda-forge`` or ``bioconda`` are also possible
            to list here.

        Dependencies
            All the dependencies that you need for your project. So far, we have just added ``python``
            because we know it will be a Python project. We will add more later.


创建环境
========================

Creating our environment

.. tab:: 中文

    现在我们已经编写了一个基础的 ``environment.yml`` 文件，可以基于它创建并激活一个环境。运行以下命令::

        conda env create --file environment.yml
        conda activate my-project

.. tab:: 英文

    Now that we have written a basic ``environment.yml`` file, we can create and activate an environment
    from it. To do so, run the following commands::

        conda env create --file environment.yml
        conda activate my-project


创建 Python 应用程序
===============================

Creating our Python application

.. tab:: 中文

    此时我们拥有了一个已安装 Python 的新环境，可以开始编写一个简单的 Python 程序。在项目目录中，创建一个 ``main.py`` 文件，并添加如下内容：

    .. code-block:: python

        def main():
            print("Hello, conda!")


        if __name__ == "__main__":
            main()

    可以通过以下命令运行该程序::

        python main.py
        Hello, conda!

.. tab:: 英文

    With our new environment with Python installed, we can create a simple Python program.
    In your project folder, create a ``main.py`` file and add the following:

    .. code-block:: python

        def main():
            print("Hello, conda!")


        if __name__ == "__main__":
            main()

    We can run our simple Python program by running the following command::

        python main.py
        Hello, conda!


使用新的依赖项更新项目
==========================================

Updating our project with new dependencies

.. tab:: 中文

    如果你希望项目功能超出上面的简单示例，可以使用 conda 通道中的数千个可用软件包。接下来我们将添加一个新依赖项，从网络获取数据并进行简单分析。

    本例中我们使用 `Pandas <https://pandas.pydata.org/docs/index.html>`_ 软件包进行数据分析。要将其添加至项目，需要更新 ``environment.yml`` 文件如下：

    .. code-block:: yaml

        name: my-project
        channels:
        - defaults
        dependencies:
        - python
        - pandas  # <-- 这是我们新增的依赖项

    编辑完成后，运行以下命令安装新依赖项::

        conda env update --file environment.yml

    现在依赖项已安装完毕，我们将下载一份用于分析的数据。我们选用的是美国环保署的
    `Walkability Index <https://catalog.data.gov/dataset/walkability-index1>`_ 数据集，可从 `data.gov <https://data.gov>`_ 网站获取。使用以下命令下载::

        curl -O https://edg.epa.gov/EPADataCommons/public/OA/EPA_SmartLocationDatabase_V3_Jan_2021_Final.csv

    .. admonition:: 提示

        如果你没有安装 ``curl``，也可以通过浏览器访问上述链接手动下载文件。

    我们的分析目标是了解多少比例的美国居民生活在高可步行性区域。我们可以借助 ``pandas`` 库轻松完成这一分析。以下是可能的实现代码：

    .. code-block:: python

        import pandas as pd


        def main():
            """
            回答以下问题：

            有多少比例的美国居民生活在高可步行性的社区？

            “15.26” 是被认为高可步行区域的指数阈值。
            """
            csv_file = "./EPA_SmartLocationDatabase_V3_Jan_2021_Final.csv"
            highly_walkable = 15.26

            df = pd.read_csv(csv_file)

            total_population = df["TotPop"].sum()
            highly_walkable_pop = df[df["NatWalkInd"] >= highly_walkable]["TotPop"].sum()

            percentage = (highly_walkable_pop / total_population) * 100.0

            print(
                f"{percentage:.2f}% of U.S. residents live in highly" "walkable neighborhoods."
            )


        if __name__ == "__main__":
            main()

    将上述代码更新到你的 ``main.py`` 文件并运行，你应该能看到如下输出::

        python main.py
        10.69% of Americans live in highly walkable neighborhoods

.. tab:: 英文

    If you want your project to do more than the simple example above, you can use one of the thousands
    of available packages on conda channels. To demonstrate this, we will add a new dependency
    so that we can pull in some data from the internet and perform a basic analysis.

    To perform the data analysis, we will be relying on the `Pandas <https://pandas.pydata.org/docs/index.html>`_
    package. To add this to our project, we will need to update our ``environment.yml`` file:

    .. code-block:: yaml

        name: my-project
        channels:
        - defaults
        dependencies:
        - python
        - pandas  # <-- This is our new dependency

    Once we have done that, we can run the ``conda env update`` command to install the new package::

        conda env update --file environment.yml


    Now that our dependencies are installed, we will download some data to use for our analysis.
    For this, we will use the U.S. Environmental Protection Agency's
    `Walkability Index <https://catalog.data.gov/dataset/walkability-index1>`_ dataset
    available on `data.gov <https://data.gov>`_. You can download this with the following command::

        curl -O https://edg.epa.gov/EPADataCommons/public/OA/EPA_SmartLocationDatabase_V3_Jan_2021_Final.csv


    .. admonition:: Tip

        If you do not have ``curl``, you can visit the above link with a web browser to download it.

    For our analysis, we are interested in knowing what percentage of U.S. residents live in highly
    walkable areas. This is a question that we can easily answer using the ``pandas`` library.
    Below is an example of how you might go about doing that:

    .. code-block:: python

        import pandas as pd


        def main():
            """
            Answers the question:

            What percentage of U.S. residents live highly walkable neighborhoods?

            "15.26" is the threshold on the index for a highly walkable area.
            """
            csv_file = "./EPA_SmartLocationDatabase_V3_Jan_2021_Final.csv"
            highly_walkable = 15.26

            df = pd.read_csv(csv_file)

            total_population = df["TotPop"].sum()
            highly_walkable_pop = df[df["NatWalkInd"] >= highly_walkable]["TotPop"].sum()

            percentage = (highly_walkable_pop / total_population) * 100.0

            print(
                f"{percentage:.2f}% of U.S. residents live in highly" "walkable neighborhoods."
            )


        if __name__ == "__main__":
            main()

    Update your ``main.py`` file with the code above and run it. You should get the following
    answer::

        python main.py
        10.69% of Americans live in highly walkable neighborhoods


结论
==========

Conclusion

.. tab:: 中文

    你已经学会了如何借助 ``environment.yml`` 文件在 conda 中创建自己的数据分析项目。随着项目的发展，你可能还会添加更多依赖项，并将 Python 代码拆分为多个文件和模块以便组织。

    如需了解更多关于管理环境与 ``environment.yml`` 文件的信息，请参阅 :doc:`管理环境 <manage-environments>`。

.. tab:: 英文

    You have just been introduced to creating your own data analysis project by using
    the ``environment.yml`` file in conda. As the project grows, you may wish to add more dependencies
    and also better organize the Python code into separate files and modules.

    For even more information about working with environments and ``environment.yml`` files,
    please see :doc:`Managing Environments <manage-environments>`.
