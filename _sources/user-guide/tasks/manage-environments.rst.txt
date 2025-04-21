=====================
管理环境
=====================

Managing environments

.. tab:: 中文

   使用 conda，可以创建、导出、列出、删除以及更新包含不同 Python 版本和/或不同软件包的环境。在环境之间切换或移动的操作称为激活环境。你还可以共享一个环境文件。

   本页所述命令支持许多选项。如需查看所有可用命令的详细参考，请参见 :doc:`commands <../../commands/index>`。

.. tab:: 英文

   With conda, you can create, export, list, remove, and update
   environments that have different versions of Python and/or
   packages installed in them. Switching or moving between
   environments is called activating the environment. You can also
   share an environment file.

   There are many options available for the commands described
   on this page. For a detailed reference on all available commands,
   see :doc:`commands <../../commands/index>`.

使用命令创建环境
=====================================

Creating an environment with commands

.. tab:: 中文

   以下步骤请在终端中执行：
   
   #. 创建一个环境：
   
      .. code::
   
         conda create --name <my-env>
   
      将 ``<my-env>`` 替换为你的环境名称。
   
   #. 当 conda 提示你是否继续时，输入 ``y``：
   
      .. code::
   
         proceed ([y]/n)?
   
      这将在 ``/envs/`` 目录中创建一个名为 myenv 的环境，尚未安装任何软件包。
   
   #. 创建一个指定 Python 版本的环境：
   
      .. code-block:: bash
   
         conda create -n myenv python=3.9
   
   #. 创建一个包含特定软件包的环境：
   
      .. code-block:: bash
   
         conda create -n myenv scipy
   
      或者：
   
      .. code-block:: bash
   
         conda create -n myenv python
         conda install -n myenv scipy
   
   #. 创建一个包含特定版本软件包的环境：
   
      .. code-block:: bash
   
         conda create -n myenv scipy=0.17.3
   
      或者：
   
      .. code-block:: bash
   
         conda create -n myenv python
         conda install -n myenv scipy=0.17.3
   
   #. 创建一个包含特定 Python 版本和多个软件包的环境：
   
      .. code-block:: bash
   
         conda create -n myenv python=3.9 scipy=0.17.3 astroid babel
   
      .. tip::
         建议在创建环境时一次性安装所有需要的程序，逐个安装可能会导致依赖冲突。
   
   若要在每次创建新环境时自动安装 pip 或其他程序，可将默认程序添加到 ``.condarc`` 配置文件的 :ref:`create_default_packages <config-add-default-pkgs>` 部分。默认软件包将在每次创建环境时自动安装。如果你不希望在某个环境中安装默认包，可使用 ``--no-default-packages`` 标志：
   
   .. code-block:: bash
   
     conda create --no-default-packages -n myenv python
   
   .. tip::
      你可以在 ``conda create`` 命令中添加更多内容。
      详情请运行 ``conda create --help``。

.. tab:: 英文

   Use the terminal for the following steps:
   
   #. To create an environment:
   
      .. code::
   
         conda create --name <my-env>
   
      Replace ``<my-env>`` with the name of your environment.
   
   #. When conda asks you to proceed, type ``y``:
   
      .. code::
   
         proceed ([y]/n)?
   
      This creates the myenv environment in ``/envs/``. No
      packages will be installed in this environment.
   
   #. To create an environment with a specific version of Python:
   
      .. code-block:: bash
   
         conda create -n myenv python=3.9
   
   #. To create an environment with a specific package:
   
      .. code-block:: bash
   
         conda create -n myenv scipy
   
      or:
   
      .. code-block:: bash
   
         conda create -n myenv python
         conda install -n myenv scipy
   
   #. To create an environment with a specific version of a package:
   
      .. code-block:: bash
   
         conda create -n myenv scipy=0.17.3
   
      or:
   
      .. code-block:: bash
   
         conda create -n myenv python
         conda install -n myenv scipy=0.17.3
   
   #. To create an environment with a specific version of Python and
      multiple packages:
   
      .. code-block:: bash
   
         conda create -n myenv python=3.9 scipy=0.17.3 astroid babel
   
      .. tip::
         Install all the programs that you want in this environment
         at the same time. Installing one program at a time can lead to
         dependency conflicts.
   
   To automatically install pip or another program every time a new
   environment is created, add the default programs to the
   :ref:`create_default_packages <config-add-default-pkgs>` section
   of your ``.condarc`` configuration file. The default packages are
   installed every time you create a new environment. If you do not
   want the default packages installed in a particular environment,
   use the ``--no-default-packages`` flag:
   
   .. code-block:: bash
   
     conda create --no-default-packages -n myenv python
   
   .. tip::
      You can add much more to the ``conda create`` command.
      For details, run ``conda create --help``.


.. _create-env-from-file:

通过 environment.yml 文件创建环境
====================================================

Creating an environment from an environment.yml file

.. tab:: 中文

   以下步骤请在终端中执行：
   
   #. 通过 ``environment.yml`` 文件创建环境：
   
      .. code::
   
         conda env create -f environment.yml
   
      ``yml`` 文件的第一行定义新环境的名称。
      详情请参见 :ref:`手动创建环境文件 <create-env-file-manually>`。
   
   #. 激活新环境： ``conda activate myenv``
   
   #. 验证新环境是否安装成功：
   
      .. code::
   
         conda env list
   
      你也可以使用 ``conda info --envs``。

.. tab:: 英文

   Use the terminal for the following steps:
   
   #. Create the environment from the ``environment.yml`` file:
   
      .. code::
   
         conda env create -f environment.yml
   
      The first line of the ``yml`` file sets the new environment's
      name. For details see :ref:`Creating an environment file manually
      <create-env-file-manually>`.
   
   
   #. Activate the new environment: ``conda activate myenv``
   
   #. Verify that the new environment was installed correctly:
   
      .. code::
   
         conda env list
   
      You can also use ``conda info --envs``.

.. _specifying-environment-platform:

为环境指定不同的目标平台
=========================================================

Specifying a different target platform for an environment

.. tab:: 中文

   默认情况下，``conda`` 会为当前运行平台创建环境。你可以通过运行 ``conda info`` 并查看 ``platform`` 字段来确认当前平台。
   
   不过在某些情况下，你可能希望为不同的目标平台或架构创建环境。为此，可以在 ``conda create`` 和 ``conda env create`` 命令中使用 ``--platform`` 选项。更多允许的取值请参见 :doc:`/commands/create` 中的 ``--subdir, --platform``。
   
   例如，在 Apple Silicon 平台上运行 macOS 的用户，可能希望为 Intel 处理器创建一个 ``python`` 环境，并通过 Rosetta 模拟可执行文件。命令如下：
   
   .. code::
   
      conda create --platform osx-64 --name python-x64 python
   
   .. note::
      无法对已存在的环境使用 ``--platform`` 参数。
      环境创建时将被注释上该自定义配置，后续操作将保留此目标平台设置。
   
   该选项还允许指定不同操作系统（如在 macOS 上创建 Linux 环境），但我们不建议将其用于 ``--dry-run`` 以外的操作。不匹配操作系统可能会导致以下问题：
   
   - 无法解析环境，因为缺少虚拟包。
     你可以通过设置必要的 ``CONDA_OVERRIDE_****`` 环境变量来解决。例如，在 macOS 上解析 Linux 环境时，可能需要设置 ``CONDA_OVERRIDE_LINUX=1`` 和 ``CONDA_OVERRIDE_GLIBC=2.17``。
   - 能够解析环境，但在提取和链接阶段失败，原因是文件系统限制（如大小写不敏感、不兼容路径等）。唯一的解决方案是使用 ``--dry-run --json`` 获取解决方案，并将其转换为锁文件，供目标机器使用。详情请参见 :ref:`dry-run-explicit`。

.. tab:: 英文

   By default, ``conda`` will create environments targeting the platform it's
   currently running on. You can check which platform you are currently on by running
   ``conda info`` and checking the ``platform`` entry.
   
   However, in some cases you might want to create an environment for a
   different target platform or architecture. To do so, use the
   ``--platform`` flag available in the ``conda create`` and
   ``conda env create`` commands. See ``--subdir, --platform``
   in :doc:`/commands/create` for more information about allowed values.
   
   For example, a user running macOS on the Apple Silicon platform
   might want to create a ``python`` environment for Intel processors
   and emulate the executables with Rosetta. The command would be:
   
   .. code::
   
      conda create --platform osx-64 --name python-x64 python
   
   .. note::
      You can't specify the ``--platform`` flag for existing environments.
      When created, the environment will be annotated with the custom configuration and
      subsequent operations on it will remember the target platform.
   
   This flag also allows specifying a different OS (e.g. creating a Linux
   environment on macOS), but we don't recommend its usage outside of
   ``--dry-run`` operations. Common problems with mismatched OSes include:
   
   - The environment cannot be solved because virtual packages are missing.
     You can workaround this issue by exporting the necessary
     ``CONDA_OVERRIDE_****`` environment variables. For example, solving
     for Linux from macOS, you will probably need ``CONDA_OVERRIDE_LINUX=1``
     and ``CONDA_OVERRIDE_GLIBC=2.17``.
   - The environment can be solved, but extraction and linking fails due
     filesystem limitations (case insensitive systems, incompatible paths,
     etc). The only workaround here is to use ``--dry-run --json`` to obtain
     the solution and process the payload into a lockfile that can be shared
     with the target machine. See :ref:`dry-run-explicit` for more details.

.. _specifying-location:

指定环境的位置
========================================

Specifying a location for an environment

.. tab:: 中文

   你可以通过为目标目录指定路径，在该目录中创建 conda 环境。例如，以下命令将在当前工作目录的 ``envs`` 子目录中创建一个新环境：
   
   ::
   
     conda create --prefix ./envs jupyterlab=3.2 matplotlib=3.5 numpy=1.21
   
   使用前缀创建的环境可以通过相同命令激活：
   
   ::
   
     conda activate ./envs
   
   在项目目录的子目录中创建环境具有如下好处：
   
   * 通过将环境作为子目录包含在项目中，可以轻松判断该项目是否使用隔离环境。
   * 项目更加自包含，所需软件全部包含在单一目录中。
   
   在项目子目录中创建环境的额外好处是，可以为所有环境使用相同名称。
   如果你将所有环境保存在 ``envs`` 文件夹中，则必须为每个环境指定不同名称。
   
   将 conda 环境放在默认 ``envs`` 文件夹之外时，有几点需要注意：
   
   #. Conda 不再能通过 ``--name`` 参数找到你的环境。
      通常需要使用 ``--prefix`` 参数并提供完整路径。
   #. 在创建环境时指定安装路径后，命令提示符将显示该环境的绝对路径前缀，而不是环境名称。
   
   使用前缀激活环境后，命令提示符类似于：
   
   ::
   
      (/absolute/path/to/envs) $
   
   这可能导致前缀过长：
   
   ::
   
      (/Users/USER_NAME/research/data-science/PROJECT_NAME/envs) $
   
   若要在 shell 提示符中移除该长前缀，可修改 ``.condarc`` 文件中的 env_prompt 设置：
   
   ::
   
      conda config --set env_prompt '({name})'
   
   如果你已有 ``.condarc`` 文件，该命令将编辑文件；否则将创建新文件。
   
   之后你的命令提示符将显示活跃环境的通用名称，即环境根目录的名称：
   
   .. code-block::
   
     $ cd project-directory
     $ conda activate ./env
     (env) project-directory $

.. tab:: 英文

   You can control where a conda environment lives by providing a path
   to a target directory when creating the environment. For example,
   the following command will create a new environment in a subdirectory
   of the current working directory called ``envs``::
   
     conda create --prefix ./envs jupyterlab=3.2 matplotlib=3.5 numpy=1.21
   
   You then activate an environment created with a prefix using the same
   command used to activate environments created by name::
   
     conda activate ./envs
   
   Specifying a path to a subdirectory of your project directory when
   creating an environment has the following benefits:
   
   * It makes it easy to tell if your project uses an isolated environment
     by including the environment as a subdirectory.
   * It makes your project more self-contained as everything, including
     the required software, is contained in a single project directory.
   
   An additional benefit of creating your project’s environment inside a
   subdirectory is that you can then use the same name for all your
   environments. If you keep all of your environments in your ``envs``
   folder, you’ll have to give each environment a different name.
   
   There are a few things to be aware of when placing conda environments
   outside of the default ``envs`` folder.
   
   #. Conda can no longer find your environment with the ``--name`` flag.
      You’ll generally need to pass the ``--prefix`` flag along with the
      environment’s full path to find the environment.
   #. Specifying an install path when creating your conda environments
      makes it so that your command prompt is now prefixed with the active
      environment’s absolute path rather than the environment’s name.
   
   After activating an environment using its prefix, your prompt will
   look similar to the following::
   
   (/absolute/path/to/envs) $
   
   This can result in long prefixes::
   
   (/Users/USER_NAME/research/data-science/PROJECT_NAME/envs) $
   
   To remove this long prefix in your shell prompt, modify the env_prompt
   setting in your ``.condarc`` file::
   
   conda config --set env_prompt '({name})'
   
   This will edit your ``.condarc`` file if you already have one
   or create a ``.condarc`` file if you do not.
   
   Now your command prompt will display the active environment’s
   generic name, which is the name of the environment's root folder:
   
   .. code-block::
   
      $ cd project-directory
      $ conda activate ./env
      (env) project-directory $

.. _update-env:

更新环境
=======================

Updating an environment

.. tab:: 中文

   你可能出于多种原因需要更新环境。例如：

   * 某个核心依赖项发布了新版本（依赖项版本号更新）；
   * 你需要一个额外的数据分析软件包（添加新依赖项）；
   * 你发现了更好的软件包，不再需要旧的软件包（添加新依赖项并移除旧依赖项）。

   如果发生这些情况，只需相应地更新你的 ``environment.yml`` 文件内容，并运行以下命令：

   .. code::

      conda env update --file environment.yml  --prune

   .. note::
      ``--prune`` 选项会使 conda 移除环境中不再需要的依赖项。

.. tab:: 英文

   You may need to update your environment for a variety of reasons.
   For example, it may be the case that:
   
   * one of your core dependencies just released a new version
     (dependency version number update).
   * you need an additional package for data analysis
     (add a new dependency).
   * you have found a better package and no longer need the older
     package (add new dependency and remove old dependency).
   
   If any of these occur, all you need to do is update the contents of
   your ``environment.yml`` file accordingly and then run the following
   command:
   
   .. code::
   
      conda env update --file environment.yml  --prune
   
   .. note::
      The ``--prune`` option causes conda to remove any dependencies
      that are no longer required from the environment.


克隆环境
======================

Cloning an environment

.. tab:: 中文

   请在终端中执行以下步骤：

   你可以通过克隆已有环境来创建一个环境的精确副本：

   .. code::

      conda create --name myclone --clone myenv

   .. note::
      将 ``myclone`` 替换为新环境的名称。
      将 ``myenv`` 替换为你要复制的已有环境名称。

   要验证副本是否创建成功：

   .. code::

      conda info --envs

   在显示的环境列表中，你应能看到源环境和新复制的环境。

.. tab:: 英文

   Use the terminal for the following steps:
   
   You can make an exact copy of an environment by creating a clone
   of it:
   
   .. code::
   
      conda create --name myclone --clone myenv
   
   .. note::
      Replace ``myclone`` with the name of the new environment.
      Replace ``myenv`` with the name of the existing environment that
      you want to copy.
   
   To verify that the copy was made:
   
   .. code::
   
      conda info --envs
   
   In the environments list that displays, you should see both the
   source environment and the new copy.

.. _identical-conda-envs:

构建相同的 conda 环境
=====================================

Building identical conda environments

.. tab:: 中文

   你可以使用显式规范文件，在相同操作系统平台上（无论是在同一台机器还是另一台机器上）构建一个完全相同的 conda 环境。
   
   请在终端中执行以下步骤：
   
   #. 运行 ``conda list --explicit`` 来生成如下规范列表：
   
      .. code::
   
         # This file may be used to create an environment using:
         # $ conda create --name <env> --file <this file>
         # platform: osx-64
         @EXPLICIT
         https://repo.anaconda.com/pkgs/free/osx-64/mkl-11.3.3-0.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/numpy-1.11.1-py35_0.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/openssl-1.0.2h-1.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/pip-8.1.2-py35_0.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/python-3.5.2-0.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/readline-6.2-2.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/setuptools-25.1.6-py35_0.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/sqlite-3.13.0-0.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/tk-8.5.18-0.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/wheel-0.29.0-py35_0.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/xz-5.2.2-0.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/zlib-1.2.8-3.tar.bz2
   
   #. 若要在当前工作目录中将此规范列表保存为文件，请运行：
   
      ::
   
        conda list --explicit > spec-file.txt
   
      .. note::
         你可以使用 ``spec-file.txt`` 作为文件名，或替换为你选择的其他文件名。
   
      显式规范文件通常不具备跨平台兼容性，因此文件顶部会有类似 ``# platform: osx-64`` 的注释，表明该文件在哪个平台上创建，并已知可用。在其他平台上，某些软件包可能不可用，或关键依赖可能缺失。
   
      使用规范文件创建相同环境的命令如下：
   
      ::
   
        conda create --name myenv --file spec-file.txt
   
      若要将文件中列出的软件包安装到已有环境中：
   
      ::
   
        conda install --name myenv --file spec-file.txt
   
      Conda 在从规范文件安装软件包时不会检查架构或依赖关系。为确保软件包正确运行，请确保该文件来自可正常运行的环境，并在相同的架构、操作系统和平台（如 linux-64 或 osx-64）上使用。

.. tab:: 英文

   You can use explicit specification files to build an identical
   conda environment on the same operating system platform, either
   on the same machine or on a different machine.
   
   Use the terminal for the following steps:
   
   #. Run ``conda list --explicit`` to produce a spec list such as:
   
      .. code::
   
         # This file may be used to create an environment using:
         # $ conda create --name <env> --file <this file>
         # platform: osx-64
         @EXPLICIT
         https://repo.anaconda.com/pkgs/free/osx-64/mkl-11.3.3-0.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/numpy-1.11.1-py35_0.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/openssl-1.0.2h-1.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/pip-8.1.2-py35_0.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/python-3.5.2-0.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/readline-6.2-2.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/setuptools-25.1.6-py35_0.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/sqlite-3.13.0-0.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/tk-8.5.18-0.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/wheel-0.29.0-py35_0.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/xz-5.2.2-0.tar.bz2
         https://repo.anaconda.com/pkgs/free/osx-64/zlib-1.2.8-3.tar.bz2
   
   
   #. To create this spec list as a file in the current working
      directory, run::
   
        conda list --explicit > spec-file.txt
   
      .. note::
         You can use ``spec-file.txt`` as the filename or replace
         it with a filename of your choice.
   
      An explicit spec file is not usually cross platform, and
      therefore has a comment at the top such as ``# platform: osx-64``
      showing the platform where it was created. This platform is the
      one where this spec file is known to work. On other platforms,
      the packages specified might not be available or dependencies
      might be missing for some of the key packages already in the
      spec.
   
      To use the spec file to create an identical environment on the
      same machine or another machine::
   
        conda create --name myenv --file spec-file.txt
   
      To use the spec file to install its listed packages into an
      existing environment::
   
        conda install --name myenv --file spec-file.txt
   
      Conda does not check architecture or dependencies when installing
      from a spec file. To ensure that the packages work correctly,
      make sure that the file was created from a working environment,
      and use it on the same architecture, operating system, and
      platform, such as linux-64 or osx-64.


.. _activate-env:

激活环境
=========================

Activating an environment

.. tab:: 中文
   
   激活环境是使环境中软件正常工作的关键。激活操作主要包含两个方面：将环境路径添加到 PATH 中，以及运行环境中可能包含的激活脚本。通过激活脚本，软件包可以设置它们运行所需的任意环境变量。你也可以使用 :ref:`配置 API 设置环境变量 <set-env-vars>`。
   
   激活会将环境路径前置添加到 PATH 中。这种更改仅在当前终端会话中有效，不具有全局作用。
   
   .. note::
   
      当你 `安装 Anaconda <http://docs.anaconda.com/anaconda/install.html>`_ 时，可以选择 “Add Anaconda to my PATH environment variable”。  
      *不建议这样做*，因为它会将 Anaconda *追加* 到 PATH。
      安装程序在追加 PATH 时，并不会调用激活脚本。
   
   .. note::
   
      在 Windows 上，PATH 分为 *系统 PATH* 和 *用户 PATH* 两部分，系统 PATH 总是优先生效。当你选择 “仅为我安装” 时，Anaconda 会添加到 *用户 PATH*；当你选择 “为所有用户安装” 时，会添加到 *系统 PATH*。前者可能导致系统 PATH 中的值优先生效，后者则不会。
      *我们不推荐* 进行 `多用户安装 <https://docs.anaconda.com/anaconda/install/multi-user/>`__。
   
   激活环境： ``conda activate myenv``
   
   .. note::
   
      将 ``myenv`` 替换为你的环境名称或路径。
   
   Conda 会将 ``myenv`` 的路径前置添加到系统命令中。
   
   如果你未激活环境，可能会看到如下警告信息：
   
   .. code-block:: Python
   
      Warning:
      This Python interpreter is in a conda environment, but the environment has
      not been activated. Libraries may fail to load. To activate this environment
      please see https://conda.io/activation.
   
   如果出现此类警告，你需要激活环境。Windows 用户可在终端中运行：  
   ``c:\Anaconda3\Scripts\activate``。
   
   Windows 对激活要求极为严格。这是因为其库加载机制不支持“知道依赖路径”的可执行文件或库（RPATH）。相反，Windows 依赖的是其自身的 `动态链接库搜索顺序 <https://docs.microsoft.com/en-us/windows/win32/dlls/dynamic-link-library-search-order>`_。
   
   如果未激活环境，可能会导致库加载失败，并产生大量错误。例如，如果某个子环境中的 Python 无法找到所需的 OpenSSL 库，就可能出现 HTTP 或 SSL 错误。
   
   Conda 自身做了一些特殊处理，可以自动添加必要的 PATH 条目。这使得即使未激活环境或在子环境中，也能调用 conda 命令。但通常情况下，若未激活环境直接运行其中的可执行文件，很可能会失败。
   
   若想在已激活的环境中运行可执行程序，可以使用 ``conda run`` 命令。
   
   如果遇到 PATH 相关错误，可参考我们的 :ref:`疑难解答 <path-error>`。

.. tab:: 英文

   Activating environments is essential to making the software in the environments
   work well. Activation entails two primary functions: adding entries to PATH for
   the environment and running any activation scripts that the environment may
   contain. These activation scripts are how packages can set arbitrary
   environment variables that may be necessary for their operation. You can also
   :ref:`use the config API to set environment variables <set-env-vars>`.
   
   Activation prepends to PATH. This only takes effect
   when you have the environment active so it is local to a terminal session,
   not global.
   
   .. note::
      When `installing Anaconda <http://docs.anaconda.com/anaconda/install.html>`_,
      you have the option to “Add Anaconda to my PATH environment variable.”
      *This is not recommended* because it *appends* Anaconda to PATH.
      When the installer appends to PATH, it does not call the activation scripts.
   
   .. note::
      On Windows, PATH is composed of two parts, the *system* PATH and the
      *user* PATH. The system PATH always comes first. When you install
      Anaconda for "Just Me", we add it to the *user* PATH. When you install
      for "All Users", we add it to the *system* PATH. In the former case,
      you can end up with system PATH values taking precedence over
      your entries. In the latter case, you do not. *We do not recommend*
      `multi-user installs <https://docs.anaconda.com/anaconda/install/multi-user/>`__.
   
   To activate an environment: ``conda activate myenv``
   
   .. note::
      Replace ``myenv`` with the environment name or directory path.
   
   Conda prepends the path name ``myenv`` onto your system command.
   
   You may receive a warning message if you have not activated your environment:
   
   .. code-block:: Python
   
      Warning:
      This Python interpreter is in a conda environment, but the environment has
      not been activated. Libraries may fail to load. To activate this environment
      please see https://conda.io/activation.
   
   If you receive this warning, you need to activate your environment. To do
   so on Windows, run: ``c:\Anaconda3\Scripts\activate`` in a terminal window.
   
   Windows is extremely sensitive to proper activation. This is because
   the Windows library loader does not support the concept of libraries
   and executables that know where to search for their dependencies
   (RPATH). Instead, Windows relies on a `dynamic-link library search order <https://docs.microsoft.com/en-us/windows/win32/dlls/dynamic-link-library-search-order>`_.
   
   If environments are not active, libraries won't be found and there
   will be lots of errors. HTTP or SSL errors are common errors when the
   Python in a child environment can't find the necessary OpenSSL library.
   
   Conda itself includes some special workarounds to add its necessary PATH
   entries. This makes it so that it can be called without activation or
   with any child environment active. In general, calling any executable in
   an environment without first activating that environment will likely not work.
   For the ability to run executables in activated environments, you may be
   interested in the ``conda run`` command.
   
   If you experience errors with PATH, review our :ref:`troubleshooting <path-error>`.

Conda init
----------

Conda init

.. tab:: 中文

   早期版本的 conda 引入了脚本，用于在不同操作系统之间统一激活行为。从 Conda 4.4 开始支持 ``conda activate myenv`` 命令。Conda 4.6 增加了更全面的初始化支持，使 conda 能在各种 shell（bash、zsh、csh、fish、xonsh 等）中运行得更快且更少产生干扰。现在这些 shell 都可以使用 ``conda activate`` 命令。由于无需手动修改 PATH，这种方式也使得 conda 对系统上其他软件的干扰更小。要了解更多信息，请查看 ``conda init --help`` 命令的输出。

   在使用 ``conda init`` 时，以下设置可能对你有用::

      auto_activate: bool

   该设置用于控制 conda 启动时是否自动激活默认环境。无论该选项是否启用，你都可以使用 ``conda`` 命令，但如果未激活环境，则该默认环境中的其他程序在激活前是不可用的，需通过 ``conda activate`` 激活环境。

   你可以通过以下配置指定默认要激活的环境::

      default_activation_env: str

   有些用户会选择关闭该设置，以加快 shell 启动速度，或避免 conda 安装的软件自动屏蔽他们原有的软件。

.. tab:: 英文

   Earlier versions of conda introduced scripts to make activation
   behavior uniform across operating systems. Conda 4.4 allowed
   ``conda activate myenv``. Conda 4.6 added extensive initialization
   support so that conda works faster and less disruptively on
   a wide variety of shells (bash, zsh, csh, fish, xonsh, and more).
   Now these shells can use the ``conda activate`` command.
   Removing the need to modify PATH makes conda less disruptive to
   other software on your system. For more information, read the
   output from ``conda init --help``.

   One setting may be useful to you when using ``conda init`` is::

      auto_activate: bool

   This setting controls whether or not conda activates the given default
   environment when it first starts up. You'll have the ``conda``
   command available either way, but without activating the environment,
   none of the other programs in the default environment will be available until
   the environment is activated with ``conda activate``.

   The environment to be activated by default can be configured with::

      default_activation_env: str

   People sometimes choose this setting to speed up the time their shell takes
   to start up or to keep conda-installed software from automatically
   hiding their other software.

嵌套激活
-----------------

Nested activation

.. tab:: 中文

   默认情况下， ``conda activate`` 会在激活新环境之前先停用当前环境，并在停用新环境后重新激活原环境。但在某些场景下，你可能希望保留当前环境的 PATH 设置，以便继续访问第一个环境中提供的命令行工具。这种需求通常出现在默认环境中安装了一些常用命令行工具时。若要保留当前环境路径，可使用如下命令激活新环境::

      conda activate --stack myenv

   若你希望在从最外层环境（通常是默认环境）进入其它环境时始终使用 stack 模式，可以设置 ``auto_stack`` 配置选项::

      conda config --set auto_stack 1

   你也可以将该值设置为更大的数字，以支持更深层级的自动堆叠，但这并不推荐，因为堆叠层级越深越容易引发混乱。

.. tab:: 英文

   By default, ``conda activate`` will deactivate the current environment
   before activating the new environment and reactivate it when
   deactivating the new environment. Sometimes you may want to leave
   the current environment PATH entries in place so that you can continue
   to easily access command-line programs from the first environment.
   This is most commonly encountered when common command-line utilities
   are installed in the default environment. To retain the current environment
   in the PATH, you can activate the new environment using::

      conda activate --stack myenv

   If you wish to always stack when going from the outermost environment,
   which is typically the default environment, you can set the ``auto_stack``
   configuration option::

      conda config --set auto_stack 1

   You may specify a larger number for a deeper level of automatic stacking,
   but this is not recommended since deeper levels of stacking are more likely
   to lead to confusion.

用于 DLL 加载验证的环境变量
-------------------------------------------------

Environment variable for DLL loading verification

.. tab:: 中文

   如果你不想激活环境、但又希望 Python 能正确执行 DLL 加载验证，请参阅 :ref:`故障排查说明 <mkl_library>`。

   .. warning::

      如果你选择不激活环境，那么加载和设置用于激活的脚本中的环境变量将不会执行。我们仅支持通过激活方式来加载环境。

.. tab:: 英文

   If you don't want to activate your environment and you want Python
   to work for DLL loading verification, then follow the
   :ref:`troubleshooting directions <mkl_library>`.

   .. warning::
      If you choose not to activate your environment, then
      loading and setting environment variables to activate
      scripts will not happen. We only support activation.

停用环境
===========================

Deactivating an environment

.. tab:: 中文

   若要停用当前环境，请输入： ``conda deactivate``

   此命令会将当前激活环境的路径从系统命令中移除。

   .. note::

      若你只是想返回默认环境，推荐直接使用不带参数的 ``conda activate`` 命令，而非尝试执行 deactivate。如果你在 base 环境中执行 ``conda deactivate``，可能会导致无法再运行 conda。别担心，这个影响只限于当前终端会话——重新打开一个新的终端即可。不过，如果是使用 ``--stack`` 参数（或自动堆叠）激活的环境，则推荐使用 ``conda deactivate`` 来退出。

.. tab:: 英文

   To deactivate an environment, type: ``conda deactivate``

   Conda removes the path name for the currently active environment from
   your system command.

   .. note::
      To simply return to the default environment, it's better to call ``conda
      activate`` with no environment specified, rather than to try to deactivate. If
      you run ``conda deactivate`` from your base environment, you may lose the
      ability to run conda at all. Don't worry, that's local to this shell - you can
      start a new one. However, if the environment was activated using ``--stack``
      (or was automatically stacked) then it is better to use ``conda deactivate``.


.. _determine-current-env:

确定当前环境
====================================

Determining your current environment

.. tab:: 中文

   请在终端中执行以下操作。

   默认情况下，当前正在使用的活跃环境会以括号（）或中括号 [] 的形式显示在命令提示符的开头::

      (myenv) $

   如果你没有看到这样的提示，请运行：

   .. code::

      conda info --envs

   在显示的环境列表中，当前所处的环境将以星号（*）标记。

   默认情况下，命令提示符会显示当前激活环境的名称。若要关闭该行为::

      conda config --set changeps1 false

   若要重新启用该行为::

      conda config --set changeps1 true

.. tab:: 英文

   Use the terminal for the following steps.

   By default, the active environment---the one you are currently
   using---is shown in parentheses () or brackets [] at the
   beginning of your command prompt::

      (myenv) $

   If you do not see this, run:

   .. code::

      conda info --envs

   In the environments list that displays, your current environment
   is highlighted with an asterisk (*).

   By default, the command prompt is set to show the name of the
   active environment. To disable this option::

      conda config --set changeps1 false

   To re-enable this option::

      conda config --set changeps1 true


查看环境列表
===================================

Viewing a list of your environments

.. tab:: 中文

   若要查看你的所有环境，在终端窗口中运行：

   .. code::

      conda info --envs

   或

   .. code::

      conda env list

   将显示如下类似的列表：

   .. code::

      conda environments:
      myenv                 /home/username/miniconda/envs/myenv
      snowflakes            /home/username/miniconda/envs/snowflakes
      bunnies               /home/username/miniconda/envs/bunnies

   如果该命令由管理员用户执行，则会显示所有用户拥有的环境列表。

.. tab:: 英文

   To see a list of all of your environments, in your terminal window, run:

   .. code::

      conda info --envs

   OR

   .. code::

      conda env list

   A list similar to the following is displayed:

   .. code::

      conda environments:
      myenv                 /home/username/miniconda/envs/myenv
      snowflakes            /home/username/miniconda/envs/snowflakes
      bunnies               /home/username/miniconda/envs/bunnies

   If this command is run by an administrator, a list of all environments
   belonging to all users will be displayed.

查看环境中的软件包列表
================================================

Viewing a list of the packages in an environment

.. tab:: 中文

   要查看特定环境中已安装的所有包：
   
   * 如果环境尚未激活，请在终端中运行：
   
     .. code-block:: bash
   
        conda list -n myenv
   
   * 如果环境已激活，请在终端中运行：
   
     .. code-block:: bash
   
        conda list
   
   * 若要查看某个特定包是否已安装在某个环境中，请在终端中运行：
   
     .. code-block:: bash
   
        conda list -n myenv scipy

.. tab:: 英文
   
   To see a list of all packages installed in a specific environment:
   
   * If the environment is not activated, in your terminal window, run:
   
     .. code-block:: bash
   
        conda list -n myenv
   
   * If the environment is activated, in your terminal window, run:
   
     .. code-block:: bash
   
        conda list
   
   * To see if a specific package is installed in an environment, in your
     terminal window, run:
   
     .. code-block:: bash
   
       conda list -n myenv scipy


.. _pip-in-env:

在环境中使用 pip
===========================

Using pip in an environment

.. tab:: 中文

   若要在你的环境中使用 pip，请在终端中运行：
   
   .. code-block:: bash
   
      conda install -n myenv pip
      conda activate myenv
      pip <pip_subcommand>
   
   同时使用 pip 和 conda 时可能会遇到问题。推荐的做法是在一个隔离的 conda 环境中使用 pip。在使用 pip 安装剩余软件之前，应尽可能使用 conda 安装所需的软件包。如果需要对环境进行修改，建议新建一个环境，而不是在 pip 安装包之后再运行 conda。适当时，应将 conda 和 pip 的依赖需求分别保存在文本文件中。
   
   我们推荐以下做法：
   
   **仅在 conda 之后使用 pip**
     - 尽可能使用 conda 安装所有依赖，再使用 pip。
     - pip 应使用 ``--upgrade-strategy only-if-needed`` （默认策略）运行。
     - 不要使用 pip 的 ``--user`` 参数，避免全局安装。
   
   **使用 conda 环境实现隔离**
     - 创建一个 conda 环境，用于隔离 pip 带来的改动。
     - 由于采用硬链接，环境本身占用空间很小。
     - 应避免在 root 环境中运行 pip。
   
   **如需修改环境，建议重新创建**
     - 一旦使用 pip 安装了软件，conda 将无法感知这些改动。
     - 若需安装额外的 conda 包，建议重新创建该环境。
   
   **将 conda 和 pip 的依赖写入文本文件**
     - conda 可使用 ``--file`` 参数读取包依赖。
     - pip 可使用 ``-r`` 或 ``--requirements`` 参数读取 Python 包列表。
     - ``conda env`` 可以基于包含 conda 与 pip 依赖的文件导出或创建环境。

.. tab:: 英文
   
   To use pip in your environment, in your terminal window, run:
   
   .. code-block:: bash
   
      conda install -n myenv pip
      conda activate myenv
      pip <pip_subcommand>
   
   Issues may arise when using pip and conda together. When combining conda and pip,
   it is best to use an isolated conda environment. Only after conda has been used to
   install as many packages as possible should pip be used to install any remaining
   software. If modifications are needed to the environment, it is best to create a
   new environment rather than running conda after pip. When appropriate, conda and
   pip requirements should be stored in text files.
   
   We recommend that you:
   
   **Use pip only after conda**
     - Install as many requirements as possible with conda then use pip.
     - Pip should be run with ``--upgrade-strategy only-if-needed`` (the default).
     - Do not use pip with the ``--user`` argument, avoid all users installs.
   
   **Use conda environments for isolation**
     - Create a conda environment to isolate any changes pip makes.
     - Environments take up little space thanks to hard links.
     - Care should be taken to avoid running pip in the root environment.
   
   **Recreate the environment if changes are needed**
     - Once pip has been used, conda will be unaware of the changes.
     - To install additional conda packages, it is best to recreate
       the environment.
   
   **Store conda and pip requirements in text files**
     - Package requirements can be passed to conda via the ``--file`` argument.
     - Pip accepts a list of Python packages with ``-r`` or ``--requirements``.
     - Conda env will export or create environments based on a file with
       conda and pip requirements.

.. _set-env-vars:

设置环境变量
=============================

Setting environment variables

.. tab:: 中文

   如果你希望将环境变量与某个环境关联，推荐使用配置 API。这是一种更安全的替代方案，优于使用激活与停用脚本执行任意代码的做法。
   
   首先，创建并激活你的环境::
   
      conda create -n test-env
      conda activate test-env
   
   若要列出当前的环境变量，运行 ``conda env config vars list``。
   
   若要设置环境变量，运行 ``conda env config vars set my_var=value``。
   
   设置完成后，需要重新激活环境：``conda activate test-env``。
   
   要检查环境变量是否已设置，可运行 ``echo $my_var`` （Windows 下为 ``echo %my_var%``）或 ``conda env config vars list``。
   
   当你停用环境后，再运行上述命令，即可看到环境变量已被移除。
   
   你可以通过 ``-n`` 或 ``-p`` 参数指定要操作的环境。其中 ``-n`` 用于指定环境名称，``-p`` 用于指定环境路径。
   
   若要取消某个环境变量，运行：``conda env config vars unset my_var -n test-env``。
   
   当你停用环境后，可重新运行 ``echo my_var`` 或 ``conda env config vars list``，确认变量已不再存在。
   
   通过 ``conda env config vars`` 设置的环境变量会被包含在 ``conda env export`` 的导出结果中。此外，你也可以在 `environment.yml` 文件中声明环境变量，如下所示::
   
       name: env-name
       channels:
         - conda-forge
         - defaults
       dependencies:
         - python=3.7
         - codecov
       variables:
         VAR1: valueA
         VAR2: valueB

.. tab:: 英文

   If you want to associate environment variables with an environment,
   you can use the config API. This is recommended as an alternative to
   using activate and deactivate scripts since those are an execution of
   arbitrary code that may not be safe.
   
   First, create your environment and activate it::
   
      conda create -n test-env
      conda activate test-env
   
   To list any variables you may have, run ``conda env config vars list``.
   
   To set environment variables, run ``conda env config vars set my_var=value``.
   
   Once you have set an environment variable, you have to reactivate your environment:
   ``conda activate test-env``.
   
   To check if the environment variable has been set, run
   ``echo $my_var`` (``echo %my_var%`` on Windows)  or ``conda env config vars list``.
   
   When you deactivate your environment, you can use those same commands to see that
   the environment variable goes away.
   
   You can specify the environment you want to affect using the ``-n`` and ``-p`` flags. The ``-n`` flag allows you to name the environment and ``-p`` allows you to specify the path to the environment.
   
   To unset the environment variable, run ``conda env config vars unset my_var -n test-env``.
   
   When you deactivate your environment, you can see that environment variable goes away by rerunning
   ``echo my_var`` or ``conda env config vars list`` to show that the variable name
   is no longer present.
   
   Environment variables set using ``conda env config vars`` will be retained in the output of
   ``conda env export``. Further, you can declare environment variables in the environment.yml file
   as shown here::
   
       name: env-name
       channels:
         - conda-forge
         - defaults
       dependencies:
         - python=3.7
         - codecov
       variables:
         VAR1: valueA
         VAR2: valueB


保存环境变量
============================

Saving environment variables

.. tab:: 中文

   Conda 环境支持保存环境变量。

   假设你希望为环境 "analytics" 保存一个登录服务器所需的密钥和一个配置文件路径。以下章节说明了如何分别在 :ref:`Windows <win-save-env-variables>` 与 :ref:`macOS 或 Linux <macos-linux-save-env-variables>` 上编写名为 ``env_vars`` 的脚本来实现这一目标。

   这类脚本文件可以作为 conda 包的一部分。当包含该脚本的包被激活时，环境变量将自动生效。

   你可以自由命名这些脚本。但由于多个包可能会创建脚本文件，因此请务必使用具有描述性的、不易与其他包冲突的名称。一种常见做法是使用类似 ``packagename-scriptname.sh`` 的命名方式，在 Windows 上则使用 ``packagename-scriptname.bat``。

.. tab:: 英文

   Conda environments can include saved environment variables.

   Suppose you want an environment "analytics" to store both a
   secret key needed to log in to a server and a path to a
   configuration file. The sections below explain how to write a
   script named ``env_vars`` to do this on :ref:`Windows
   <win-save-env-variables>` and :ref:`macOS or Linux
   <macos-linux-save-env-variables>`.

   This type of script file can be part of a conda package, in
   which case these environment variables become active when an
   environment containing that package is activated.

   You can name these scripts anything you like. However, multiple
   packages may create script files, so be sure to use descriptive
   names that are not used by other packages. One popular option is
   to give the script a name in the form
   ``packagename-scriptname.sh``, or on Windows,
   ``packagename-scriptname.bat``.

.. _win-save-env-variables:

Windows
-------

Windows

.. tab:: 中文

   #. 在终端中通过运行 ``%CONDA_PREFIX%`` 命令定位 conda 环境的目录。
   
   #. 进入该目录，并创建如下子目录与文件::
   
        cd %CONDA_PREFIX%
        mkdir .\etc\conda\activate.d
        mkdir .\etc\conda\deactivate.d
        type NUL > .\etc\conda\activate.d\env_vars.bat
        type NUL > .\etc\conda\deactivate.d\env_vars.bat
   
   #. 编辑 ``.\etc\conda\activate.d\env_vars.bat``，内容如下::
   
        set MY_KEY='secret-key-value'
        set MY_FILE=C:\path\to\my\file
   
   #. 编辑 ``.\etc\conda\deactivate.d\env_vars.bat``，内容如下::
   
        set MY_KEY=
        set MY_FILE=
   
   运行 ``conda activate analytics`` 后，环境变量 ``MY_KEY`` 与 ``MY_FILE`` 将被设置为你在文件中定义的值。运行 ``conda deactivate`` 后，这些变量会被清除。

.. tab:: 英文

   #. Locate the directory for the conda environment in your
      terminal window by running in the command shell ``%CONDA_PREFIX%``.
   
   #. Enter that directory and create these subdirectories and
      files::
   
       cd %CONDA_PREFIX%
       mkdir .\etc\conda\activate.d
       mkdir .\etc\conda\deactivate.d
       type NUL > .\etc\conda\activate.d\env_vars.bat
       type NUL > .\etc\conda\deactivate.d\env_vars.bat
   
   #. Edit ``.\etc\conda\activate.d\env_vars.bat`` as follows::
   
        set MY_KEY='secret-key-value'
        set MY_FILE=C:\path\to\my\file
   
   #. Edit ``.\etc\conda\deactivate.d\env_vars.bat`` as follows::
   
        set MY_KEY=
        set MY_FILE=
   
   When you run ``conda activate analytics``, the environment variables
   ``MY_KEY`` and ``MY_FILE`` are set to the values you wrote into the file.
   When you run ``conda deactivate``, those variables are erased.

.. _macos-linux-save-env-variables:

macOS 和 Linux
---------------

macOS and Linux

.. tab:: 中文
   
   #. 在终端中运行 ``echo $CONDA_PREFIX`` 来定位 conda 环境的目录。
   
   #. 进入该目录，并创建如下子目录与文件::
   
        cd $CONDA_PREFIX
        mkdir -p ./etc/conda/activate.d
        mkdir -p ./etc/conda/deactivate.d
        touch ./etc/conda/activate.d/env_vars.sh
        touch ./etc/conda/deactivate.d/env_vars.sh
   
   #. 编辑 ``./etc/conda/activate.d/env_vars.sh``，内容如下::
   
        #!/bin/sh
   
        export MY_KEY='secret-key-value'
        export MY_FILE=/path/to/my/file/
   
   #. 编辑 ``./etc/conda/deactivate.d/env_vars.sh``，内容如下::
   
        #!/bin/sh
   
        unset MY_KEY
        unset MY_FILE
   
   运行 ``conda activate analytics`` 后，环境变量 ``MY_KEY`` 与 ``MY_FILE`` 将被设置为你写入文件的值。运行 ``conda deactivate`` 后，这些变量将被清除。

.. tab:: 英文

   #. Locate the directory for the conda environment in your terminal window by running in the terminal ``echo $CONDA_PREFIX``.
   
   #. Enter that directory and create these subdirectories and
      files::
   
        cd $CONDA_PREFIX
        mkdir -p ./etc/conda/activate.d
        mkdir -p ./etc/conda/deactivate.d
        touch ./etc/conda/activate.d/env_vars.sh
        touch ./etc/conda/deactivate.d/env_vars.sh
   
   #. Edit ``./etc/conda/activate.d/env_vars.sh`` as follows::
   
        #!/bin/sh
   
        export MY_KEY='secret-key-value'
        export MY_FILE=/path/to/my/file/
   
   #. Edit ``./etc/conda/deactivate.d/env_vars.sh`` as follows::
   
        #!/bin/sh
   
        unset MY_KEY
        unset MY_FILE
   
   When you run ``conda activate analytics``, the environment
   variables ``MY_KEY`` and ``MY_FILE`` are set to the values you wrote into
   the file. When you run ``conda deactivate``, those variables are
   erased.


共享环境
=======================

Sharing an environment

.. tab:: 中文

   你可以将环境分享给其他人，例如让他们复现你所做的测试。为了让他们快速复现你的环境及其所有包和版本，你可以将你的 ``environment.yml`` 文件复制给他们。

.. tab:: 英文

   You may want to share your environment with someone else---for
   example, so they can re-create a test that you have done. To
   allow them to quickly reproduce your environment, with all of its
   packages and versions, give them a copy of your
   ``environment.yml`` file.

导出 environment.yml 文件
----------------------------------

Exporting the environment.yml file

.. tab:: 中文

   .. note::
      如果你当前目录中已有 ``environment.yml`` 文件，本操作会覆盖它。

   #. 激活要导出的环境：``conda activate myenv``

      .. note::
         请将 ``myenv`` 替换为你的环境名称。

   #. 将当前激活的环境导出为新文件::

      conda env export > environment.yml

      .. note::
         此文件会同时记录环境中的 pip 包和 conda 包。

   #. 通过电子邮件或其他方式将导出的 ``environment.yml`` 文件发送给对方。

.. tab:: 英文

   .. note::
      If you already have an ``environment.yml`` file in your
      current directory, it will be overwritten during this task.

   #. Activate the environment to export: ``conda activate myenv``

      .. note::
         Replace ``myenv`` with the name of the environment.

   #. Export your active environment to a new file::

        conda env export > environment.yml

      .. note::
         This file handles both the environment's pip packages
         and conda packages.

   #. Email or copy the exported ``environment.yml`` file to the
      other person.

.. _export-platform:

跨平台导出环境文件
----------------------------------------------

Exporting an environment file across platforms

.. tab:: 中文

   如果你希望环境文件在多个平台间通用，可以使用 ``conda env export --from-history`` 选项。该选项只会导出你**明确指定**安装的包，而不会导出为满足依赖而自动安装的全部内容。

   例如，创建一个环境并安装 Python 和某个包::

      conda install python=3.7 codecov

   这会自动安装许多额外包以解决依赖关系，可能会引入在不同平台上不兼容的内容。

   使用 ``conda env export`` 会导出所有这些包；而使用 ``conda env export --from-history`` 则只会导出你显式安装的内容：

   .. code-block::

      (env-name) ➜  ~ conda env export --from-history
      name: env-name
      channels:
      - conda-forge
      - defaults
      dependencies:
      - python=3.7
      - codecov
      prefix: /Users/username/anaconda3/envs/env-name

   .. note::
      如果你在 macOS 上安装的是 Anaconda 2019.10，前缀可能是
      ``/Users/username/opt/envs/env-name``。

.. tab:: 英文

   If you want to make your environment file work across platforms,
   you can use the ``conda env export --from-history`` flag. This
   will only include packages that you’ve explicitly asked for,
   as opposed to including every package in your environment.

   For example, if you create an environment and install Python and a package::

     conda install python=3.7 codecov

   This will download and install numerous additional packages to solve
   for dependencies. This will introduce packages that may not be compatible
   across platforms.

   If you use ``conda env export``, it will export all of those packages.
   However, if you use ``conda env export --from-history``, it will
   only export those you specifically chose:

   .. code-block::

      (env-name) ➜  ~ conda env export --from-history
      name: env-name
      channels:
        - conda-forge
        - defaults
      dependencies:
        - python=3.7
        - codecov
      prefix: /Users/username/anaconda3/envs/env-name

   .. note::
      If you installed Anaconda 2019.10 on macOS, your prefix may be
      ``/Users/username/opt/envs/env-name``.

.. _create-env-file-manually:

手动创建环境文件
-------------------------------------

Creating an environment file manually

.. tab:: 中文

   你也可以手动编写一个 ``environment.yml`` 文件用于分享环境。

   **示例：一个简单的环境文件**

   .. code::

      name: stats
      dependencies:
         - numpy
         - pandas

   **示例：一个复杂的环境文件**

   .. code::

      name: stats2
      channels:
      - javascript
      dependencies:
      - python=3.9
      - bokeh=2.4.2
      - conda-forge::numpy=1.21.*
      - nodejs=16.13.*
      - flask
      - pip
      - pip:
         - Flask-Testing

   .. note::
      **使用通配符**

      注意使用了 ``*`` 通配符来定义部分版本。固定主版本和次版本的同时允许补丁版本变化，可帮助你在维护环境一致性的同时获得 bug 修复。有关包安装版本语法，详见 :doc:`../concepts/pkg-search`。

      **为特定包指定安装源**

      有时你可能希望指定 conda 从特定源安装某个包。你可以使用 `channel::package` 语法来实现，如上述例子中的 `conda-forge::numpy` （可选指定版本）。此处的源可以无需写入 `channels:` 列表，这在只希望部分包从特定社区源安装时非常有用。

   你可以通过在 ``channels`` 列表中加入 ``nodefaults`` 来排除默认源：

   .. code::

      channels:
      - javascript
      - nodefaults

   这相当于对多数 ``conda`` 命令使用 ``--override-channels`` 参数。

   在 ``environment.yml`` 中添加 ``nodefaults`` 类似于从 ``.condarc`` 配置文件中移除默认源 ``defaults``，不过前者只影响当前环境，后者影响所有环境。

   有关如何根据 ``environment.yml`` 文件创建环境的说明，参见 :ref:`create-env-from-file`。


.. tab:: 英文

   You can create an environment file (``environment.yml``) manually
   to share with others.

   EXAMPLE: A simple environment file:

   .. code::

       name: stats
       dependencies:
         - numpy
         - pandas

   EXAMPLE: A more complex environment file:

   .. code::

      name: stats2
      channels:
        - javascript
      dependencies:
        - python=3.9
        - bokeh=2.4.2
        - conda-forge::numpy=1.21.*
        - nodejs=16.13.*
        - flask
        - pip
        - pip:
          - Flask-Testing

   .. note::
      **Using wildcards**

      Note the use of the wildcard ``*`` when defining a few of the
      versions in the complex environment file. Keeping the major and
      minor versions fixed while allowing the patch to be any number
      allows you to use your environment file to get any bug fixes
      while still maintaining consistency in your environment. For
      more information on package installation values,
      see :doc:`../concepts/pkg-search`.

      **Specifying channels outside of "channels"**

      You may occasionally want to specify which channel conda will
      use to install a specific package. To accomplish this, use the
      `channel::package` syntax in `dependencies:`, as demonstrated
      above with `conda-forge::numpy` (version numbers optional). The
      specified channel does not need to be present in the `channels:`
      list, which is useful if you want some—but not *all*—packages
      installed from a community channel such as `conda-forge`.

   You can exclude the default channels by adding ``nodefaults``
   to the channels list.

   .. code::

      channels:
        - javascript
        - nodefaults

   This is equivalent to passing the ``--override-channels`` option
   to most ``conda`` commands.

   Adding ``nodefaults`` to the channels list in ``environment.yml``
   is similar to removing ``defaults`` from the :ref:`channels
   list <config-channels>` in the ``.condarc`` file. However,
   changing ``environment.yml`` affects only one of your conda
   environments while changing ``.condarc`` affects them all.

   For details on creating an environment from this
   ``environment.yml`` file, see :ref:`create-env-from-file`.

恢复环境
========================

Restoring an environment

.. tab:: 中文

   Conda 会记录环境中的所有更改历史，你可以轻松“回滚”至旧版本。列出当前环境的修改历史：

   ``conda list --revisions``

   回滚到某个历史版本：

   ``conda install --revision=REVNUM``  
   或  
   ``conda install --rev REVNUM``

   .. note::
      请将 REVNUM 替换为修订号。

   示例：  
   若要回滚至修订号为 8 的版本，运行 ``conda install --rev 8``。

.. tab:: 英文

   Conda keeps a history of all the changes made to your environment,
   so you can easily "roll back" to a previous version. To list the history of each change to the current environment:
   ``conda list --revisions``

   To restore environment to a previous revision: ``conda install --revision=REVNUM``
   or ``conda install --rev REVNUM``.

   .. note::
      Replace REVNUM with the revision number.

   Example:
   If you want to restore your environment to revision 8, run ``conda install --rev 8``.

删除环境
=======================

Removing an environment

.. tab:: 中文

   要移除一个环境，在终端中运行：

   .. code::

      conda remove --name myenv --all

   你也可以使用：

   ``conda env remove --name myenv``

   验证环境是否已移除：

   .. code::

      conda info --envs

   输出的环境列表中不应再包含该已删除环境。

.. tab:: 英文

   To remove an environment, in your terminal window, run:

   .. code::

      conda remove --name myenv --all

   You may instead use ``conda env remove --name myenv``.

   To verify that the environment was removed, in your terminal window, run:

   .. code::

      conda info --envs

   The environments list that displays should not show the removed
   environment.

.. _dry-run-explicit:

在不创建环境的情况下创建显式锁文件
=========================================================

Create explicit lockfiles without creating an environment

.. tab:: 中文

   ``@EXPLICIT`` 锁定文件允许你无需解析依赖（不启用 solver）就能重建环境。该文件包含一个 ``@EXPLICIT`` 头部，后接一组 conda 包的 URL，可选附加其 MD5 或 SHA256 校验值。

   你可以通过 ``conda list --explicit`` 从现有环境生成它，如 :ref:`identical-conda-envs` 所示。

   但如果你只想获得锁定文件，是否必须先临时创建一个环境再删除它？答案是：不需要。你可以使用 JSON 模式运行 ``conda``，并使用 ``jq`` 工具处理输出。

   .. tip::

      你需要系统中安装 ``jq``。如果尚未安装，可以通过 ``conda`` （例如 ``conda create -n jq jq``）或系统包管理器进行安装。

   Linux 和 macOS 下命令如下（将 ``MATCHSPECS_GO_HERE`` 替换为你想指定的包）：

   .. code-block:: shell

      echo "@EXPLICIT" > explicit.txt
      CONDA_PKGS_DIRS=$(mktemp -d) conda create --dry-run MATCHSPECS_GO_HERE --json | jq -r '.actions.FETCH[] | .url + "#" + .md5' >> explicit.txt

   Windows 下只需稍作调整：

   .. code-block:: shell

      echo "@EXPLICIT" > explicit.txt
      set "CONDA_PKGS_DIRS=%TMP%\conda-%RANDOM%"
      conda create --dry-run MATCHSPECS_GO_HERE --json | jq -r '.actions.FETCH[] | .url + "#" + .md5' >> explicit.txt
      set "CONDA_PKGS_DIRS="

   然后你就可以使用该 ``explicit.txt`` 文件创建新环境：

   .. code::

      conda create -n new-environment --file explicit.txt

.. tab:: 英文

   ``@EXPLICIT`` lockfiles allow you to (re)create environments without invoking the solver.
   They consist of an ``@EXPLICIT`` header plus a list of conda package URLs, optionally followed
   by their MD5 or SHA256 hash.

   They can be obtained from existing environments via ``conda list --explicit``, as seen in
   :ref:`identical-conda-envs`.

   But what if you only need the lockfile? Would you need create to a temporary environment first just
   to delete it later? Fortunately, there's a way: you can invoke ``conda`` in JSON mode and then
   process the output with ``jq``.

   .. tip::

      You'll need ``jq`` in your system. If you don't have it yet, you can install it via
      ``conda`` (e.g. ``conda create -n jq jq``) or via your system package manager.

   The command looks like this for Linux and macOS (replace ``MATCHSPECS_GO_HERE`` with the relevant
   packages you want):

   .. code-block:: shell

      echo "@EXPLICIT" > explicit.txt
      CONDA_PKGS_DIRS=$(mktemp -d) conda create --dry-run MATCHSPECS_GO_HERE --json | jq -r '.actions.FETCH[] | .url + "#" + .md5' >> explicit.txt

   The syntax in Windows only needs some small changes:

   .. code-block:: shell

      echo "@EXPLICIT" > explicit.txt
      set "CONDA_PKGS_DIRS=%TMP%\conda-%RANDOM%"
      conda create --dry-run MATCHSPECS_GO_HERE --json | jq -r '.actions.FETCH[] | .url + "#" + .md5' >> explicit.txt
      set "CONDA_PKGS_DIRS="

   The resulting ``explicit.txt`` can be used to create a new environment with:

   .. code::

      conda create -n new-environment --file explicit.txt
