===============
管理 Python
===============

Managing Python

.. tab:: 中文

    Conda 将 Python 视为与其他软件包相同的实体，因此可以轻松管理和更新多个安装版本。

    Conda 支持 Python 3.9、3.10、3.11 和 3.12。

.. tab:: 英文

    Conda treats Python the same as any other package, so it is easy
    to manage and update multiple installations.

    Conda supports Python 3.9, 3.10, 3.11 and 3.12.

查看可用的 Python 版本列表
===========================================

Viewing a list of available Python versions

.. tab:: 中文

    要列出可供安装的 Python 版本，请在终端窗口中运行::

        conda search python

    该命令会列出所有名称中包含 ``python`` 的软件包。

    若只想列出名称完全为 ``python`` 的软件包，请添加 ``--full-name`` 选项。在终端窗口中运行::

        conda search --full-name python

.. tab:: 英文

    To list the versions of Python that are available to install,
    in your terminal window, run::

        conda search python

    This lists all packages whose names contain the text ``python``.

    To list only the packages whose full name is exactly ``python``,
    add the ``--full-name`` option. In your terminal window, run::

        conda search --full-name python


安装其他版本的 Python
=========================================

Installing a different version of Python

.. tab:: 中文

    要在不覆盖当前版本的情况下安装其他版本的 Python，可创建一个新环境，并在其中安装目标 Python 版本：
    
    #. 创建新环境：
    
       * 要为 Python 3.9 创建新环境，请在终端窗口中运行：
    
         .. code-block:: bash
    
            conda create -n py39 python=3.9
    
         .. note::
            将 ``py39`` 替换为你想创建的环境名称。``python=3.9`` 表示你希望在该新环境中安装的包及其版本。也可以是任意其他软件包，例如 ``numpy=1.19``，或 :ref:`多个软件包 <installing multiple packages>`。
    
    #. :ref:`激活新环境 <activate-env>`。
    
    #. 验证新环境是否为你的 :ref:`当前环境 <determine-current-env>`。
    
    #. 若要确认当前环境使用的是新版本的 Python，请在终端窗口中运行：
    
       .. code::
    
          python --version

.. tab:: 英文

    To install a different version of Python without overwriting the
    current version, create a new environment and install the second
    Python version into it:
    
    #. Create the new environment:
    
       * To create the new environment for Python 3.9, in your terminal
         window run:
    
         .. code-block:: bash
    
            conda create -n py39 python=3.9
    
         .. note::
            Replace ``py39`` with the name of the environment you
            want to create. ``python=3.9`` is the package and version you
            want to install in this new environment. This could be any
            package, such as ``numpy=1.19``, or :ref:`multiple packages
            <installing multiple packages>`.
    
    #. :ref:`Activate the new environment <activate-env>`.
    
    #. Verify that the new environment is your :ref:`current
       environment <determine-current-env>`.
    
    #. To verify that the current environment uses the new Python
       version, in your terminal window, run:
    
       .. code::
    
          python --version

安装 PyPy
===============

Installing PyPy

.. tab:: 中文

    若要使用 PyPy 版本，可执行以下操作::

        conda config --add channels conda-forge
        conda config --set channel_priority strict
        conda create -n pypy pypy
        conda activate pypy

.. tab:: 英文

    To use the PyPy builds you can do the following::

        conda config --add channels conda-forge
        conda config --set channel_priority strict
        conda create -n pypy pypy
        conda activate pypy


使用其他版本的 Python
====================================

Using a different version of Python

.. tab:: 中文

    若要切换到包含不同版本 Python 的环境，请 :ref:`激活该环境 <activate-env>`。

.. tab:: 英文

    To switch to an environment that has different version of Python,
    :ref:`activate the environment <activate-env>`.


更新 Python
===============

Updating Python

.. tab:: 中文

    若要将当前环境中的 Python 更新到最新版本，请运行::

        conda update python

    该命令会将 Python 更新至最新的主版本（例如从 ``python=3.10`` 升级到 ``python=3.12``）。

    若希望保持在某个次版本上，请改用 ``conda install`` 命令::

        conda install python=3.10

.. tab:: 英文

    To update Python to the latest version in your environment, run::

        conda update python

    This command will update you to the latest major release (e.g. from ``python=3.10`` to ``python=3.12``).

    If you would like to remain on a minor release, use the ``conda install`` command instead::

        conda install python=3.10
