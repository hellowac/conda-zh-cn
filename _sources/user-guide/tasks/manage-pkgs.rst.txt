=================
管理软件包
=================

Managing packages

.. tab:: 中文

   .. note::
      本页描述的命令有很多可用选项。详情请参阅 :doc:`commands <../../commands/index>`。

.. tab:: 英文

   .. note::
      There are many options available for the commands described
      on this page. For details, see :doc:`commands <../../commands/index>`.


搜索软件包
======================

Searching for packages

.. tab:: 中文

   使用终端完成以下步骤。

   要查看某个特定软件包（例如 SciPy）是否可供安装：

   .. code-block:: bash

      conda search scipy

   要查看某个特定软件包（例如 SciPy）是否可以从 Anaconda.org 安装：

   .. code-block:: bash

      conda search --override-channels --channel defaults scipy

   要查看某个特定软件包（例如 iminuit）是否存在于某个特定的渠道（例如 http://conda.anaconda.org/mutirri）中，并可供安装：

   .. code-block:: bash

      conda search --override-channels --channel http://conda.anaconda.org/mutirri iminuit

.. tab:: 英文

   Use the terminal for the following steps.

   To see if a specific package, such as SciPy, is available for
   installation:

   .. code-block:: bash

      conda search scipy

   To see if a specific package, such as SciPy, is available for
   installation from Anaconda.org:

   .. code-block:: bash

      conda search --override-channels --channel defaults scipy

   To see if a specific package, such as iminuit, exists in a
   specific channel, such as http://conda.anaconda.org/mutirri,
   and is available for installation:

   .. code-block:: bash

      conda search --override-channels --channel http://conda.anaconda.org/mutirri iminuit


安装软件包
===================

Installing packages

.. tab:: 中文使用终端完成以下步骤。

   要将特定软件包（如 SciPy）安装到已有的环境 "myenv" 中：

   .. code-block:: bash

      conda install --name myenv scipy

   如果未指定环境名称（在此例中通过 ``--name myenv`` 指定），该软件包将安装到当前环境中：

   .. code-block:: bash

      conda install scipy

   要安装特定版本的软件包（如 SciPy）：

   .. code-block:: bash

      conda install scipy=0.15.0

   .. _`installing multiple packages`:

   要一次性安装多个软件包，例如 SciPy 和 cURL：

   .. code-block:: bash

      conda install scipy curl

   .. note::
      最好一次性安装所有软件包，以便所有依赖项能同时被正确安装。

   要一次性安装多个软件包并指定版本号：

   .. code-block:: bash

      conda install scipy=0.15.0 curl=7.26.0

   要为特定 Python 版本安装某个软件包：

   .. code-block:: bash

      conda install scipy=0.15.0 curl=7.26.0 -n py34_env

   如果希望使用特定的 Python 版本，建议创建使用该版本的环境。有关更多信息，请参阅 :doc:`../troubleshooting`。

.. tab:: 英文

   Use the terminal for the following steps.

   To install a specific package such as SciPy into an existing
   environment "myenv":

   .. code-block:: bash

      conda install --name myenv scipy

   If you do not specify the environment name, which in this
   example is done by ``--name myenv``, the package installs
   into the current environment:

   .. code-block:: bash

      conda install scipy

   To install a specific version of a package such as SciPy:

   .. code-block:: bash

      conda install scipy=0.15.0

   To install multiple packages at once, such as SciPy and cURL:

   .. code-block:: bash

      conda install scipy curl

   .. note::
      It is best to install all packages at once, so that all of
      the dependencies are installed at the same time.

   To install multiple packages at once and specify the version of
   the package:

   .. code-block:: bash

      conda install scipy=0.15.0 curl=7.26.0

   To install a package for a specific Python version:

   .. code-block:: bash

      conda install scipy=0.15.0 curl=7.26.0 -n py34_env

   If you want to use a specific Python version, it is best to use
   an environment with that version. For more information,
   see :doc:`../troubleshooting`.

安装类似软件包
===========================

Installing similar packages

.. tab:: 中文

   安装名称相似、功能相近的软件包可能会产生意外结果。通常，后安装的软件包会决定最终的行为，这种行为可能并非所期望的。
   如果这两个软件包名称不同，或你正在构建软件包变体并需要协调栈中其它软件，我们建议使用 :ref:`mutex-metapackages`。

.. tab:: 英文

   Installing packages that have similar filenames and serve similar
   purposes may return unexpected results. The package last installed
   will likely determine the outcome, which may be undesirable.
   If the two packages have different names, or if you're building
   variants of packages and need to line up other software in the stack,
   we recommend using :ref:`mutex-metapackages`.

从 Anaconda.org 安装软件包
=====================================

Installing packages from Anaconda.org

.. tab:: 中文

   使用 ``conda install`` 无法获得的软件包可以通过 Anaconda.org 获取。Anaconda.org 是一个支持公共和私有软件包仓库的软件包管理服务。它与 Anaconda 和 Miniconda 一样，是 Anaconda 的产品之一。

   要从 Anaconda.org 安装软件包：

   #. 打开浏览器，访问 http://anaconda.org。

   #. 在左上角的“Search Packages”搜索框中输入 ``bottleneck``。

   #. 找到你需要的软件包并点击进入其详情页。

      详情页会显示该软件包所属的渠道名，例如本例中为 "pandas" 渠道。

   #. 现在你已知道渠道名，可以使用 ``conda install`` 命令安装该软件包。在终端中运行：

      .. code::

         conda install -c pandas bottleneck

      此命令指示 conda 从 Anaconda.org 上的 pandas 渠道安装 bottleneck 软件包。

   #. 要确认该软件包已被安装，在终端中运行：

      .. code::

         conda list

      会显示一个软件包列表，其中应包含 bottleneck。

   .. note::
      有关从多个渠道安装软件包的信息，请参阅 :doc:`manage-channels`。

.. tab:: 英文

   Packages that are not available using ``conda install`` can be
   obtained from Anaconda.org, a package management service for
   both public and private package repositories. Anaconda.org
   is an Anaconda product, just like Anaconda and Miniconda.
   
   To install a package from Anaconda.org:
   
   #. In a browser, go to http://anaconda.org.
   
   #. To find the package named bottleneck, type ``bottleneck``
      in the top-left box named Search Packages.
   
   #. Find the package that you want and click it to go to the
      detail page.
   
      The detail page displays the name of the channel. In this
      example it is the "pandas" channel.
   
   #. Now that you know the channel name, use the ``conda install``
      command to install the package. In your terminal window, run:
   
      .. code::
   
         conda install -c pandas bottleneck
   
      This command tells conda to install the bottleneck package
      from the pandas channel on Anaconda.org.
   
   #. To check that the package is installed, in your terminal window, run:
   
      .. code::
   
         conda list
   
      A list of packages appears, including bottleneck.
   
   .. note::
      For information on installing packages from multiple
      channels, see :doc:`manage-channels`.


安装非 conda 软件包
=============================

Installing non-conda packages

.. tab:: 中文

   如果某个软件包无法通过 conda 或 Anaconda.org 获取，可以尝试通过 conda-forge 或其它包管理器（如 pip）安装。
   
   pip 安装的软件包不具备 conda 软件包的全部功能，因此我们建议首先尝试使用 conda 安装。如无法通过 conda 获取该软件包，可尝试从
   `conda-forge <https://conda-forge.org/search.html>`_ 寻找并安装。
   
   若仍无法安装该软件包，可尝试使用 pip 进行安装。由于 pip 与 conda 软件包的差异，可能存在某些兼容性限制，但 conda 已尽可能实现与 pip 的兼容。
   
   .. note::
      Anaconda 和 Miniconda 都已内置 pip 和 conda，因此无需单独安装它们。
   
      Conda 环境可替代 virtualenv，因此在使用 pip 之前无需激活 virtualenv。
   
   pip 可以安装在 conda 环境之外，也可以安装在 conda 环境之内。
   
   为获得 conda 的集成优势，确保在当前激活的 conda 环境中安装 pip，并使用该环境中的 pip 安装软件包。使用 ``conda list`` 命令可查看此方式安装的软件包，并显示它们是通过 pip 安装的标识。
   
   你可以使用以下命令在当前 conda 环境中安装 pip，如 :ref:`pip-in-env` 所述：
   
   ``conda install pip``
   
   如果当前 conda 环境中既安装了 pip，同时环境之外也存在 pip 实例，系统将使用当前环境中安装的 pip。
   
   要安装一个非 conda 的软件包：
   
   #. 激活目标环境：
   
      * 在终端中运行 ``conda activate myenv``。
   
   #. 使用 pip 安装程序（如 See）：
   
      .. code-block:: bash
   
         pip install see
   
   #. 验证软件包是否已安装：
   
      .. code::
   
         conda list
   
      如果未显示该软件包，先按 :ref:`pip-in-env` 中说明安装 pip，然后再尝试上述命令。

.. tab:: 英文

   If a package is not available from conda or Anaconda.org, you may be able to
   find and install the package via conda-forge or with another package manager
   like pip.
   
   Pip packages do not have all the features of conda packages and we recommend
   first trying to install any package with conda. If the package is unavailable
   through conda, try finding and installing it with
   `conda-forge <https://conda-forge.org/search.html>`_.
   
   If you still cannot install the package, you can try
   installing it with pip. The differences between pip and
   conda packages cause certain unavoidable limits in compatibility but conda
   works hard to be as compatible with pip as possible.
   
   .. note::
      Both pip and conda are included in Anaconda and Miniconda, so you do not
      need to install them separately.
   
      Conda environments replace virtualenv, so there is no need to activate a
      virtualenv before using pip.
   
   It is possible to have pip installed outside a conda environment or inside a
   conda environment.
   
   To gain the benefits of conda integration, be sure to install pip inside the
   currently active conda environment and then install packages with that
   instance of pip. The command ``conda list`` shows packages installed this way,
   with a label showing that they were installed with pip.
   
   You can install pip in the current conda environment with the command
   ``conda install pip``, as discussed in :ref:`pip-in-env`.
   
   If there are instances of pip installed both inside and outside the current
   conda environment, the instance of pip installed inside the current conda
   environment is used.
   
   To install a non-conda package:
   
   #. Activate the environment where you want to put the program:
   
      * In your terminal window, run ``conda activate myenv``.
   
   #. To use pip to install a program such as See, in your terminal window, run::
   
        pip install see
   
   #. To verify the package was installed, in your terminal window, run:
   
      .. code::
   
         conda list
   
      If the package is not shown, install pip as described in :ref:`pip-in-env`
      and try these commands again.


安装商业软件包
==============================

Installing commercial packages

.. tab:: 中文

   安装商业软件包（如 IOPro）与安装其他软件包相同。在终端中运行：

   .. code-block:: bash

      conda install --name myenv iopro

   此命令会安装 Anaconda 的一款商业软件包 `IOPro
   <https://docs.continuum.io/iopro/>`_ 的免费试用版，
   该软件包可加速 Python 的数据处理。除学术用途外，该免费试用将在 30 天后到期。

.. tab:: 英文

   Installing a commercial package such as IOPro is the same as
   installing any other package. In your terminal window, run:

   .. code-block:: bash

      conda install --name myenv iopro

   This command installs a free trial of one of Anaconda's
   commercial packages called `IOPro
   <https://docs.continuum.io/iopro/>`_, which can speed up your
   Python processing. Except for academic use, this free trial
   expires after 30 days.


查看已安装软件包列表
====================================

Viewing a list of installed packages

.. tab:: 中文

   使用终端完成以下步骤。

   要列出当前活动环境中的所有软件包：

   .. code::

      conda list

   要列出某个未激活环境（如 myenv）中的所有软件包：

   .. code::

      conda list -n myenv

.. tab:: 英文

   Use the terminal for the following steps.

   To list all of the packages in the active environment:

   .. code::

      conda list

   To list all of the packages in a deactivated environment:

   .. code::

      conda list -n myenv

列出软件包依赖项
============================

Listing package dependencies

.. tab:: 中文

   要查找某个环境中依赖特定软件包的其他软件包，conda 并没有提供单一命令，而是需要执行一系列步骤：

   #. 查看某个特定软件包所依赖的运行时依赖项：

      ``conda search package_name --info``

   #. 找到你当前安装的包缓存目录：

      ``conda info``

   #. 查找软件包依赖项。默认情况下，Anaconda / Miniconda 将软件包存储在 ``~/anaconda/pkgs/`` 目录中（在 macOS Catalina 上为 ``~/opt/pkgs/``）。
      每个软件包目录中包含一个 ``index.json`` 文件，列出了该软件包的依赖项。
      该文件位于 ``~anaconda/pkgs/package_name/info/index.json``。

   #. 现在，你可以使用 grep 搜索所有 ``index.json`` 文件，以找出哪些软件包依赖某个特定软件包：

      ``grep package_name ~/anaconda/pkgs/*/info/index.json``

   该命令的输出将显示包含 `<package_name>` 的所有软件包的完整路径及其版本号。

   示例：

   ``grep numpy ~/anaconda3/pkgs/*/info/index.json``

   上述命令的输出示例::

     /Users/testuser/anaconda3/pkgs/anaconda-4.3.0-np111py36_0/info/index.json: numpy 1.11.3 py36_0  
     /Users/testuser/anaconda3/pkgs/anaconda-4.3.0-np111py36_0/info/index.json: numpydoc 0.6.0 py36_0  
     /Users/testuser/anaconda3/pkgs/anaconda-4.3.0-np111py36_0/info/index.json: numpy 1.11.3 py36_0  

   注意，这里也返回了 “numpydoc”，因为它包含字符串 “numpy”。若要获得更精确的匹配结果，可使用 ``\<`` 和 ``\>`` 进行边界限定。

.. tab:: 英文

   To find what packages are depending on a specific package in
   your environment, there is not one specific conda command.
   It requires a series of steps:
   
   #. List the dependencies that a specific package requires to run:
      ``conda search package_name --info``
   
   #. Find your installation’s package cache directory:
      ``conda info``
   
   #. Find package dependencies. By default, Anaconda/Miniconda stores packages in ~/anaconda/pkgs/ (or ~/opt/pkgs/ on macOS Catalina).
      Each package has an index.json file which lists the package’s dependencies.
      This file resides in ~anaconda/pkgs/package_name/info/index.json.
   
   #. Now you can find what packages depend on a specific package. Use grep to search all index.json files
      as follows: ``grep package_name ~/anaconda/pkgs/*/info/index.json``
   
   The result will be the full package path and version of anything containing the <package_name>.
   
   Example:
   ``grep numpy ~/anaconda3/pkgs/*/info/index.json``
   
   Output from the above command::
   
     /Users/testuser/anaconda3/pkgs/anaconda-4.3.0-np111py36_0/info/index.json: numpy 1.11.3 py36_0
     /Users/testuser/anaconda3/pkgs/anaconda-4.3.0-np111py36_0/info/index.json: numpydoc 0.6.0 py36_0
     /Users/testuser/anaconda3/pkgs/anaconda-4.3.0-np111py36_0/info/index.json: numpy 1.11.3 py36_0
   
   Note this also returned “numpydoc” as it contains the string “numpy”. To get a more specific result
   set you can add \< and \>.

更新软件包
=================

Updating packages

.. tab:: 中文

   使用 ``conda update`` 命令可以检查是否有可用的更新。如果 conda 显示有可用更新，你可以选择是否进行安装。

   使用终端完成以下步骤。

   * 更新特定软件包，例如 biopython：

     .. code::

       conda update biopython

   * 更新 Python：

     .. code::

       conda update python

   * 更新 conda 本身：

     .. code::

       conda update conda

   .. note::
      conda 会将 Python 更新至其主版本系列中可用的最高版本，
      例如 Python 3.9 会更新到 3.x 系列中的最新版本。

   要更新 Anaconda 元包：

   .. code-block:: bash

      conda update conda
      conda update anaconda

   无论你更新的是哪个软件包，conda 都会比较版本信息并报告可用的更新内容。如果没有可用更新，conda 会提示：

   ``All requested packages are already installed.``

   如果有可用的新版本，你希望更新该软件包，输入 ``y`` 确认更新：

   .. code::

      Proceed ([y]/n)? y

.. tab:: 英文

   Use ``conda update`` command to check to see if a new update is
   available. If conda tells you an update is available, you can
   then choose whether or not to install it.
   
   Use the terminal for the following steps.
   
   * To update a specific package:
   
     .. code::
   
       conda update biopython
   
   * To update Python:
   
     .. code::
   
       conda update python
   
   * To update conda itself:
   
     .. code::
   
       conda update conda
   
   .. note::
      Conda updates to the highest version in its series, so
      Python 3.9 updates to the highest available in the 3.x series.
   
   To update the Anaconda metapackage:
   
   .. code-block:: bash
   
      conda update conda
      conda update anaconda
   
   Regardless of what package you are updating, conda compares
   versions and then reports what is available to install. If no
   updates are available, conda reports "All requested packages are
   already installed."
   
   If a newer version of your package is available and you wish to
   update it, type ``y`` to update:
   
   .. code::
   
      Proceed ([y]/n)? y


.. _pinning-packages:

阻止软件包更新（固定）
===========================================

Preventing packages from updating (pinning)

.. tab:: 中文

   在环境中固定（pin）某些软件包的版本可以防止它们被更新。这可以通过在环境的 ``conda-meta`` 目录中添加一个名为 ``pinned`` 的文件来实现，
   文件中列出不希望被更新的软件包。

   示例：以下文件将 NumPy 固定在 1.7 系列（即所有以 1.7 开头的版本），同时强制 SciPy 固定在精确版本 0.14.2::

     numpy 1.7.*
     scipy ==0.14.2

   在该 ``pinned`` 文件存在的情况下，``conda update numpy`` 将保持 NumPy 在 1.7.1，
   而尝试 ``conda install scipy=0.15.0`` 将导致错误。

   若想忽略 pinned 文件对某个软件包更新的限制，可以使用 ``--no-pin`` 标志。在终端中执行：

   .. code-block:: bash

      conda update numpy --no-pin

   由于 pinned 规范会包含在每次 conda 安装操作中，因此在未使用 ``--no-pin`` 的情况下执行的后续 ``conda update`` 命令仍会将 NumPy 恢复为 1.7 系列。

.. tab:: 英文

   Pinning a package specification in an environment prevents
   packages listed in the ``pinned`` file from being updated.

   In the environment's ``conda-meta`` directory, add a file
   named ``pinned`` that includes a list of the packages that you
   do not want updated.

   EXAMPLE: The file below forces NumPy to stay on the 1.7 series,
   which is any version that starts with 1.7. This also forces SciPy to
   stay at exactly version 0.14.2::

     numpy 1.7.*
     scipy ==0.14.2

   With this ``pinned`` file, ``conda update numpy`` keeps NumPy at
   1.7.1, and ``conda install scipy=0.15.0`` causes an error.

   Use the ``--no-pin`` flag to override the update restriction on
   a package. In the terminal, run:

   .. code-block:: bash

      conda update numpy --no-pin

   Because the ``pinned`` specs are included with each conda
   install, subsequent ``conda update`` commands without
   ``--no-pin`` will revert NumPy back to the 1.7 series.


自动将默认软件包添加到新环境
=========================================================

Adding default packages to new environments automatically

.. tab:: 中文

   若想在每次新建环境时自动添加默认软件包：

   #. 打开终端并执行：

      ``conda config --add create_default_packages PACKAGENAME1 PACKAGENAME2``

   #. 此后创建的所有新环境中，都会自动安装这些默认软件包。

   你也可以 :ref:`编辑 .condarc 文件 <config-add-default-pkgs>`，为默认创建环境配置软件包列表。

   此外，也可以通过在命令行中添加 ``--no-default-packages`` 标志来临时禁用默认软件包。

.. tab:: 英文

   To automatically add default packages to each new environment that you create:

   #. Open a terminal window and run:
      ``conda config --add create_default_packages PACKAGENAME1 PACKAGENAME2``

   #. Now, you can create new environments and the default packages will be installed in all of them.

   You can also :ref:`edit the .condarc file <config-add-default-pkgs>` with a list of packages to create
   by default.

   You can override this option at the command prompt with the ``--no-default-packages`` flag.

删除软件包
=================

Removing packages

.. tab:: 中文

   使用终端完成以下步骤。

   * 从某个环境（例如 myenv）中移除某个软件包（如 SciPy）：

     .. code-block:: bash

       conda remove -n myenv scipy

   * 从当前环境中移除某个软件包（如 SciPy）：

     .. code-block:: bash

       conda remove scipy

   * 一次移除多个软件包，例如 SciPy 和 cURL：

     .. code-block:: bash

       conda remove scipy curl

   * 确认软件包已被移除：

     .. code::

       conda list

.. tab:: 英文

   Use the terminal for the following steps.

   * To remove a package such as SciPy in an environment such as
     myenv:

     .. code-block:: bash

       conda remove -n myenv scipy

   * To remove a package such as SciPy in the current environment:

     .. code-block:: bash

       conda remove scipy

   * To remove multiple packages at once, such as SciPy and cURL:

     .. code-block:: bash

       conda remove scipy curl

   * To confirm that a package has been removed:

     .. code::

       conda list
