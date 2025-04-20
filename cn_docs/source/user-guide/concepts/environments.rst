.. _concepts-conda-environments:

============
环境
============

Environments

.. tab:: 中文

    环境是一个目录，包含你所安装的一组特定软件包。例如，你可以有一个包含 NumPy 1.7 及其依赖项的环境，也可以有另一个包含 NumPy 1.6 的环境用于旧版本测试。更改一个环境不会影响其他环境。你可以轻松激活或停用环境，这就是在环境间切换的方法。你还可以通过共享 ``environment.yaml`` 文件，将你的环境提供给他人。欲了解更多信息，请参阅 :doc:`../tasks/manage-environments`。

.. tab:: 英文

    An environment is a directory that contains a specific
    collection of packages that you have installed. For
    example, you may have one environment with NumPy 1.7 and its
    dependencies, and another environment with NumPy 1.6 for legacy
    testing. If you change one environment, your other environments
    are not affected. You can easily activate or deactivate
    environments, which is how you switch between them. You can also
    share your environment with someone by giving them a copy of your
    ``environment.yaml`` file. For more information, see
    :doc:`../tasks/manage-environments`.


Conda 目录结构
=========================

Conda directory structure

``ROOT_DIR``
------------

.. tab:: 中文

    这是 conda 分发版安装所在的目录。
    
    **示例：**
    
    .. code-block:: shell
    
       /opt/Anaconda  # Linux
       C:\Anaconda    # Windows

.. tab:: 英文

    The directory where the conda distribution was installed into.

    EXAMPLES:

    .. code-block:: shell

       /opt/Anaconda  #Linux
       C:\Anaconda    #Windows

``/pkgs``
---------

.. tab:: 中文

    这个目录也被称为 PKGS_DIR，包含了解压后的软件包，随时可以链接到 conda 环境中。每个软件包位于与其规范名称对应的子目录中。

.. tab:: 英文

    Also referred to as PKGS_DIR. This directory contains
    decompressed packages, ready to be linked in conda environments.
    Each package resides in a subdirectory corresponding to its
    canonical name.

``/envs``
---------

.. tab:: 中文

    这是用于创建其他 conda 环境的系统目录位置。

    以下子目录组成了默认 Anaconda 环境：

    | ``/bin``  
    | ``/include``  
    | ``/lib``  
    | ``/share``  
    |

    其他 conda 环境通常也包含与默认环境相同的子目录结构。

.. tab:: 英文

    The system location for additional conda environments to be
    created.

    The following subdirectories comprise the default Anaconda
    environment:

    | ``/bin``
    | ``/include``
    | ``/lib``
    | ``/share``
    |

    Other conda environments usually contain the same subdirectories
    as the default environment.

虚拟环境
====================

Virtual environments

.. tab:: 中文

    虚拟环境是一种工具，能够通过为不同项目创建隔离空间来将它们所需的依赖分开，每个空间只包含对应项目的依赖。
    
    用户可以使用多种工具来创建虚拟环境，如 Pipenv、Poetry，或 conda 虚拟环境。Pipenv 和 Poetry 基于 Python 内置的 `venv` 库，而 conda 则拥有自己的一套更底层的虚拟环境机制（Python 本身就是 conda 环境中的一个依赖项）。
    
    请向右滚动下表查看更多内容：
    
    .. list-table::
       :widths: 20 40 40
       :header-rows: 1
    
       * -
         - Python 虚拟环境
         - Conda 虚拟环境
       * - **库**
         - 静态链接、打包库进 wheel，或使用 apt/yum/brew 等工具安装
         - 将系统级库作为 conda 依赖项安装
       * - **系统依赖**
         - 依赖系统中已有的 Python 安装
         - Python 独立于系统安装
       * - **环境扩展**
         - 使用 pip 扩展环境
         - 使用 conda 或 pip 扩展环境
       * - **非 Python 依赖**
         -
         - 管理非 Python 依赖（如 R、Perl 或任意可执行程序）
       * - **依赖追踪**
         -
         - 显式追踪二进制依赖
    
    |

.. tab:: 英文

    A virtual environment is a tool that helps to
    keep dependencies required by different projects
    separate by creating isolated spaces for them that
    contain per-project dependencies for them.
    
    Users can create virtual environments
    using one of several tools such as
    Pipenv or Poetry, or a conda virtual
    environment. Pipenv and Poetry are based around Python's
    built-in venv library, whereas conda has its own notion of virtual
    environments that is lower-level (Python itself is a dependency provided
    in conda environments).
    
    Scroll to the right in the table below.
    
    Some other traits are:
    
    .. list-table::
       :widths: 20 40 40
       :header-rows: 1
    
       * -
         - Python virtual environment
         - Conda virtual environment
       * - **Libraries**
         - Statically link, vendor libraries in wheels,
           or use apt/yum/brew/etc.
         - Install system-level libraries as conda dependencies.
       * - **System**
         - Depend on base system install of Python.
         - Python is independent from system.
       * - **Extending environment**
         - Extend environment with pip.
         - Extended environment with conda or pip.
       * - **Non-Python dependencies**
         -
         - Manages non-Python dependencies (R, Perl,
           arbitrary executables).
       * - **Tracking dependencies**
         -
         - Tracks binary dependencies explicitly.
    
    |

为什么使用基于 venv 的虚拟环境
---------------------------------------

Why use venv-based virtual environments

.. tab:: 中文

    你可能会倾向使用 PyPI 或 conda，原因可能包括：

    - 你更喜欢它们的工作流程或规范格式；
    - 你希望使用系统自带的 Python 和库；
    - 你的项目维护者只发布到 PyPI，你更喜欢直接使用来自项目维护者的包，而不是由他人根据相同代码构建的版本；

.. tab:: 英文

    - You prefer their workflow or spec formats.
    - You prefer to use the system Python and libraries.
    - Your project maintainers only publish to PyPI, and
      you prefer packages that come more directly from the
      project maintainers, rather than someone else providing
      builds based on the same code.

为什么使用 conda 虚拟环境？
-----------------------------------

Why use conda virtual environments?

.. tab:: 中文

    - 你希望对二进制兼容性有更多控制；
    - 你需要使用更高版本的语言标准，如 C++17；
    - 你需要系统 Python 所不提供的库；
    - 你希望在同一个环境中管理多种语言的包，而不仅限于 Python。

.. tab:: 英文

    - You want control over binary compatibility choices.
    - You want to utilize newer language standards, such as C++ 17.
    - You need libraries beyond what the system Python offers.
    - You want to manage packages from languages other than Python
      in the same space.

工作流程差异
========================

Workflow differentiators

.. tab:: 中文

    在选择工作流和虚拟环境类型时，可以思考以下问题：

    - 你的环境是否被多个代码项目共享？
    - 环境是与代码存放在一起，还是放在单独位置？
    - 安装流程是否涉及安装外部库？
    - 你是否希望以某种归档形式打包整个环境并包含实际文件？

.. tab:: 英文

    Some questions to consider as you determine your preferred
    workflow and virtual environment:

    - Is your environment shared across multiple code projects?
    - Does your environment live alongside your code or in a separate place?
    - Do your install steps involve installing any external libraries?
    - Do you want to ship your environment as an archive of some sort
      containing the actual files of the environment?

软件包系统差异
==============================

Package system differentiators

.. tab:: 中文

    PyPI 和 conda 各有潜在优势：

    - **PyPI** 拥有一个全局命名空间，并由社区共同维护，这使得通过 PyPI 获取某个包的唯一来源更为直接，通常是项目的官方维护者；
    - **conda** 支持无限命名空间（即渠道 channel），每个渠道可以独立拥有其所有权。通过 conda 更容易在单个 channel 内确保二进制兼容性。

.. tab:: 英文

    There are potential benefits for choosing PyPI or conda.

    PyPI has one global namespace and distributed ownership of that namespace.
    Because of this, it is easier within PyPI to have single sources for a package
    directly from package maintainers.

    Conda has unlimited namespaces (channels) and distributed ownership of a
    given channel.
    As such, it is easier to ensure binary compatibility within a channel using
    conda.
