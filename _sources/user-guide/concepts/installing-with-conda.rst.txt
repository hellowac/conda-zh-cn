=====================
使用 conda 安装
=====================

Installing with conda

.. _installing-with-conda:

.. tab:: 中文

    可以使用以下命令安装 Conda 软件包::
    
      conda install <package>
    
    当 conda 安装一个软件包时，它会自动添加到你当前激活的环境中。这些软件包是文件和目录的集合，包含使用该库或软件所需的一切。对于 Python 软件包而言，主要是可以被导入到其他 Python 应用程序中的 Python 文件；而对于如 ``ffmpeg`` 这样的已编译软件包，则通常是可以直接在电脑上使用的二进制可执行文件。
    
    .. admonition:: 注意
    
        如果你想进一步了解环境的结构，请参阅 :doc:`conda environments<../concepts/environments>`。
    
    以下是一个更精确的说明，展示了安装单个软件包时发生的完整流程：
    
    * 当前配置的渠道（如 ``defaults`` 或 ``conda-forge``）会按优先级顺序被读取；
    * 从这些已配置的渠道中下载并读取索引数据（repodata）；
    * 从 repodata 中搜索目标软件包，优先从最高优先级的渠道开始；
    * 一旦找到该软件包，conda 会发起单独的下载请求并进行安装；
    * 如果该软件包有依赖项，conda 会对每个依赖重复上述流程。
    
    下图展示了这一过程的图示说明：
    
    .. image:: /img/installing-with-conda.png
        :align: center

.. tab:: 英文

    Conda packages can be installed by running the following command::

        conda install <package>

    When conda installs a package, it is automatically added to your active
    environment. These packages are collections of files and directories
    that make up everything you need to use that particular
    library or software. For Python packages, these are primarily Python
    files that can be imported into other Python applications, but for compiled
    software packages, such as ``ffmpeg``, these are typically binary executables
    you use directly on your computer.

    .. admonition:: Note

        If you would like to learn more about how environments are structured,
        head over to :doc:`conda environments<../concepts/environments>`.

    Below is a more precise overview of everything that happens during the installation
    process for a single package:

    * Currently configured channels (e.g. ``defaults`` or ``conda-forge``) are read in order of priority
    * Repodata for these configured channels is downloaded and read
    * The repodata is searched for the package, starting with the highest priority channel first
    * Once the package is found, conda makes a separate download request and then installs it
    * This process then repeats for each of the package's dependencies, if there are any

    A graphic illustration of this process is shown below:

    .. image:: /img/installing-with-conda.png
       :align: center

Conda 更新与 conda 安装
=================================

Conda update versus conda install

.. tab:: 中文

    使用 ``conda update`` 可以将软件包更新为最新的兼容版本；而使用 ``conda install`` 可以安装任何指定版本。

    **示例：**

    * 如果当前已安装的是 Python 2.7.0，且 Python 2 的最新版本是 2.7.5，则执行 ``conda update python`` 会安装 Python 2.7.5，而不会安装 Python 3；
    * 如果当前已安装的是 Python 3.7.0，且 Python 的最新版本是 3.9.0，则执行 ``conda install python=3`` 会安装 Python 3.9.0。

    Conda 对其他软件包也使用相同的规则。``conda update`` 始终会安装相同主版本号下的最高版本，而 ``conda install`` 则始终安装该软件包可用的最高版本。

.. tab:: 英文

    ``conda update`` updates packages to the latest compatible version.
    ``conda install`` can be used to install any version.

    Example:

    * If Python 2.7.0 is currently installed, and the latest version of Python 2 is 2.7.5, then ``conda update python`` installs Python 2.7.5. It does not install Python 3.

    * If Python 3.7.0 is currently installed, and the latest version of Python is 3.9.0, then ``conda install python=3`` installs Python 3.9.0.

    Conda uses the same rules for other packages. ``conda update`` always installs the highest version with the same major version number, whereas ``conda install`` always installs the highest version.


离线安装 conda 软件包
=================================

Installing conda packages offline

.. tab:: 中文

    要在离线状态下安装 conda 软件包，可执行以下命令：
    ``conda install /path-to-package/package-filename.tar.bz2/``

    如果需要，也可以将多个 conda 软件包打包成一个 `.tar` 归档文件，并使用一条命令统一安装：
    ``conda install /packages-path/packages-filename.tar``

    .. note::
       如果某个已安装的软件包无法正常工作，可能是缺失了某些依赖项，需要手动解决。

    从文件直接安装软件包不会自动解析其依赖项。

.. tab:: 英文

    To install conda packages offline, run:
    ``conda install /path-to-package/package-filename.tar.bz2/``

    If you prefer, you can create a /tar/ archive file containing
    many conda packages and install them all with one command:
    ``conda install /packages-path/packages-filename.tar``

    .. note::
        If an installed package does not work, it may be missing
        dependencies that need to be resolved manually.

    Installing packages directly from the file does not resolve
    dependencies.


使用特定版本号安装 conda 软件包
======================================================

Installing conda packages with a specific build number

.. tab:: 中文

    如果你希望使用正确的软件包规范安装 conda 软件包，可尝试如下格式：
    ``pkg_name=version=build_string``。  
    详细了解请参阅：  
    - `构建字符串与包命名规范 <https://docs.conda.io/projects/conda-build/en/latest/concepts/package-naming-conv.html#index-2>`_  
    - `软件包规范与元数据 <https://docs.conda.io/projects/conda-build/en/latest/resources/package-spec.html#package-metadata>`_
    
    例如，如果你想在 Python 3.7.8 上安装 llvmlite 的 0.31.0dev0 版本，可以运行：
    
    ```
    conda install -c numba/label/dev llvmlite=0.31.0dev0=py37_8
    ```

.. tab:: 英文

    If you want to install conda packages with the correct package specification, try
    ``pkg_name=version=build_string``. Read more about `build strings and package naming conventions <https://docs.conda.io/projects/conda-build/en/latest/concepts/package-naming-conv.html#index-2>`_.
    Learn more about `package specifications and metadata <https://docs.conda.io/projects/conda-build/en/latest/resources/package-spec.html#package-metadata>`_.

    For example, if you want to install llvmlite 0.31.0dev0 on Python 3.7.8, you
    would enter::

        conda install  -c numba/label/dev llvmlite=0.31.0dev0=py37_8
