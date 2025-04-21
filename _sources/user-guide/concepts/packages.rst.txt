========
软件包
========

Packages

.. tab:: 中文

.. tab:: 英文

.. _concept-conda-package:

什么是软件包？
==================

What is a package?

.. tab:: 中文

    软件包是压缩的 tarball 文件（``.tar.bz2``）或 ``.conda`` 文件，包含以下内容：

    * 系统级库。
    * Python 或其他模块。
    * 可执行程序及其他组件。
    * 位于 ``info/`` 目录下的元数据。
    * 一组直接安装到 ``install`` 前缀目录中的文件。

    Conda 会跟踪软件包之间以及软件包与平台之间的依赖关系。Conda 的软件包格式在所有平台和操作系统上完全相同。

    Conda 软件包只包含文件（包括符号链接），不包含目录。目录会在需要时创建或删除，但无法通过 tar 压缩包直接创建空目录。

.. tab:: 英文

    A package is a compressed tarball file (``.tar.bz2``) or
    ``.conda`` file that contains:

    * system-level libraries.
    * Python or other modules.---
    * executable programs and other components.
    * metadata under the ``info/`` directory.
    * a collection of files that are installed directly into an ``install`` prefix.

    Conda keeps track of the dependencies between packages and platforms.
    The conda package format is identical across platforms and
    operating systems.

    Only files, including symbolic links, are part of a conda
    package. Directories are not included. Directories are created
    and removed as needed, but you cannot create an empty directory
    from the tar archive directly.

.conda 文件格式
==================

.conda file format

.. tab:: 中文

    `.conda` 文件格式在 conda 4.7 中引入，是 `.tar.bz2` 的更紧凑（因此更快速）替代方案。

    `.conda` 文件格式是一个外层未压缩的 ZIP 格式容器，其中包含两个内层的压缩 `.tar` 文件。

    `.conda` 格式最初支持的内部压缩格式是 Zstandard（zstd）。实际使用的压缩格式并不重要，只要 `libarchive` 支持即可。随着更先进压缩算法的发展，压缩格式可能会发生变化，而 `.conda` 文件格式本身无需修改。只需更新 `libarchive` 即可支持新格式。

    这些压缩文件相比 bzip2 格式可以明显减小体积，并且解压速度更快。建议在可用时优先使用 `.conda` 格式，我们仍会同时提供 `.tar.bz2` 格式的软件包。

    更多关于 `.conda` 文件格式的信息见：
    `introduction of the .conda file format <https://www.anaconda.com/understanding-and-improving-condas-performance/>`_。

    .. note::
    
        在 conda 4.7 及以后版本中，不可以使用以 `.conda` 结尾的软件包名称，因为这会与 `.conda` 文件格式冲突。

.. tab:: 英文

    The .conda file format was introduced in conda 4.7 as a more
    compact, and thus faster, alternative to a tarball.
    
    The .conda file format consists of an outer, uncompressed
    ZIP-format container, with 2 inner compressed .tar files.
    
    For the .conda format's initial internal compression format support,
    we chose Zstandard (zstd). The actual compression format used does not
    matter, as long as the format is supported by libarchive. The compression
    format may change in the future as more advanced compression algorithms are
    developed and no change to the .conda format is necessary. Only an updated
    libarchive would be required to add a new compression format to .conda files.
    
    These compressed files can be significantly smaller than their
    bzip2 equivalents. In addition, they decompress much more quickly.
    .conda is the preferred file format to use where available,
    although we continue to provide .tar.bz2 files in tandem.
    
    Read more about the `introduction of the .conda file format <https://www.anaconda.com/understanding-and-improving-condas-performance/>`_.
    
    .. note::
    
        In conda 4.7 and later, you cannot use package names that
        end in “.conda” as they conflict with the .conda file format
        for packages.


使用软件包
==============

Using packages

.. tab:: 中文

    * 搜索软件包：

    .. code-block:: bash
    
      conda search scipy

    * 安装软件包：

    .. code-block:: bash
    
      conda install scipy

    * 构建软件包（需先安装 `conda-build`）：

    .. code-block:: bash
    
      conda build my_fun_package

.. tab:: 英文

    * You may search for packages
    
    .. code-block:: bash
    
      conda search scipy
    
    
    * You may install a package
    
    .. code-block:: bash
    
      conda install scipy
    
    
    * You may build a package after `installing conda-build <https://docs.conda.io/projects/conda-build/en/latest/index.html>`_
    
    .. code-block:: bash
    
      conda build my_fun_package



软件包结构
=================

Package structure

.. tab:: 中文

    .. code-block:: bash
    
      .
      ├── bin
      │   └── pyflakes
      ├── info
      │   ├── LICENSE.txt
      │   ├── files
      │   ├── index.json
      │   ├── paths.json
      │   └── recipe
      └── lib
          └── python3.5
    
    * `bin` 目录包含相关二进制可执行文件。
    * `lib` 目录包含相关库文件（例如 `.py` 文件）。
    * `info` 目录包含软件包的元数据。

.. tab:: 英文

    .. code-block:: bash
    
      .
      ├── bin
      │   └── pyflakes
      ├── info
      │   ├── LICENSE.txt
      │   ├── files
      │   ├── index.json
      │   ├── paths.json
      │   └── recipe
      └── lib
          └── python3.5
    
    * bin contains relevant binaries for the package.
    
    * lib contains the relevant library files (eg. the .py files).
    
    * info contains package metadata.


.. _meta-package:

元软件包
============

Metapackages

.. tab:: 中文

    如果 conda 软件包仅包含元数据而不含文件，则称为 **元包（metapackage）**。元包可以依赖多个核心或底层库，并可以链接到执行时自动下载的软件文件。元包常用于收集元数据，并简化复杂的软件包规范。

    一个典型的元包示例是 `"anaconda"`，它集合了 Anaconda 发行版安装程序中的所有软件包。命令 ``conda create -n envname anaconda`` 会创建一个与 Anaconda 发行版安装器所生成的环境完全一致的环境。可以使用 ``conda metapackage`` 命令创建元包，并在命令中指定名称和版本号。

.. tab:: 英文

    When a conda package is used for metadata alone and does not contain
    any files, it is referred to as a metapackage.
    The metapackage may contain dependencies to several core, low-level libraries
    and can contain links to software files that are
    automatically downloaded when executed.
    Metapackages are used to capture metadata and make complicated package
    specifications simpler.


    An example of a metapackage is "anaconda," which
    collects together all the packages in the Anaconda Distribution
    installer. The command ``conda create -n envname anaconda`` creates an
    environment that exactly matches what would be created from the
    Anaconda Distribution installer. You can create metapackages with the
    ``conda metapackage`` command. Include the name and version
    in the command.

Anaconda 元软件包
--------------------

Anaconda metapackage

.. tab:: 中文

    Anaconda 元包用于构建 `Anaconda Distribution <https://docs.anaconda.com/anaconda/>`_ 安装器，使得每个安装器版本都包含一组具体版本的软件包。该特定版本的软件包集合就封装在 Anaconda 元包中。

    Anaconda 元包包含多个核心底层库，包括压缩、加密、线性代数和一些图形界面库。

    详细内容见：  
    `the Anaconda metapackage and Anaconda Distribution <https://www.anaconda.com/whats-in-a-name-clarifying-the-anaconda-metapackage/>`_

.. tab:: 英文

    The Anaconda metapackage is used in the creation of the
    `Anaconda Distribution <https://docs.anaconda.com/anaconda/>`_
    installers so that they have a set of packages associated with them.
    Each installer release has a version number, which corresponds
    to a particular collection of packages at specific versions.
    That collection of packages at specific versions is encapsulated
    in the Anaconda metapackage.

    The Anaconda metapackage contains several core, low-level
    libraries, including compression, encryption, linear algebra, and
    some GUI libraries.

    `Read more about the Anaconda metapackage and Anaconda Distribution
    <https://www.anaconda.com/whats-in-a-name-clarifying-the-anaconda-metapackage/>`_.

.. _mutex-metapackages:

互斥元软件包
------------------

Mutex metapackages

.. tab:: 中文

    **互斥元包（mutex metapackage）** 是一种非常简单的包，它只有名称，不一定具有依赖项或构建步骤。互斥元包常作为构建另一个软件包变体的“输出”。互斥元包可帮助在具有不同名称的包之间实现互斥安装。

    以下是使用互斥元包将 NumPy 构建为不同 BLAS 实现的示例。

.. tab:: 英文

    A mutex metapackage is a very simple package that has a
    name. It need not have any dependencies or build steps.
    Mutex metapackages are frequently an "output" in a recipe
    that builds some variant of another package.
    Mutex metapackages function as a tool to help achieve mutual
    exclusivity among packages with different names.

    Let's look at some examples for how to use mutex metapackages
    to build NumPy against different BLAS implementations.

使用 BLAS 变体构建 NumPy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Building NumPy with BLAS variants

.. tab:: 中文

    当你使用 MKL 构建 NumPy 时，也需要将 SciPy、scikit-learn 及其他使用 BLAS 的库也一起使用 MKL 构建。重要的是，这些“变体”（使用特定选项构建的软件包）必须一起安装，不能与其他 BLAS 实现混用，以避免崩溃、性能问题或数值误差。这在构建时和安装时都需要注意。下面介绍如何使用元包实现此需求。

    首先看 metapackage ``blas=1.0=mkl``：  
    https://github.com/AnacondaRecipes/intel_repack-feedstock/blob/e699b12/recipe/meta.yaml#L108-L112

    注意 ``mkl`` 是 ``blas`` 的一个构建字符串（build string）。

    该元包通过 ``run_exports`` 机制，在使用 `mkl-devel` 包作为构建依赖时自动加入：  
    https://github.com/AnacondaRecipes/intel_repack-feedstock/blob/e699b12/recipe/meta.yaml#L124

    同样，这里是 OpenBLAS 的元包定义：  
    https://github.com/AnacondaRecipes/openblas-feedstock/blob/ae5af5e/recipe/meta.yaml#L127-L131

    以及 OpenBLAS 的 ``run_exports``，定义在 openblas-devel 中：  
    https://github.com/AnacondaRecipes/openblas-feedstock/blob/ae5af5e/recipe/meta.yaml#L100

    Conda 的互斥模型依赖于软件包名称。OpenBLAS 与 MKL 不是同一个包名，因此 conda 无法原生实现互斥安装。Conda 可以同时安装 NumPy （使用 MKL） 和 SciPy （使用 OpenBLAS）。而元包通过构建字符串将选项统一为同一个包名，从而实现互斥安装。 ``run_exports`` 自动添加元包，确保依赖库的使用者（即依赖这些库的软件包）具备正确的依赖信息，以形成统一的运行时库集。

.. tab:: 英文

    If you build NumPy with MKL, you also need to build
    SciPy, scikit-learn, and anything else using BLAS
    also with MKL. It is important to ensure that these
    “variants” (packages built with a particular set of options)
    are installed together and never with an alternate BLAS
    implementation. This is to avoid crashes, slowness, or numerical problems.
    Lining up these libraries is both a build-time and an install-time concern.
    We’ll show how to use metapackages to achieve this need.

    Let's start with the metapackage ``blas=1.0=mkl``:
    https://github.com/AnacondaRecipes/intel_repack-feedstock/blob/e699b12/recipe/meta.yaml#L108-L112

    Note that ``mkl`` is a string of ``blas``.

    That metapackage is automatically added as a dependency
    using ``run_exports`` when someone uses the mkl-devel
    package as a build-time dependency:
    https://github.com/AnacondaRecipes/intel_repack-feedstock/blob/e699b12/recipe/meta.yaml#L124

    By the same token, here’s the metapackage for OpenBLAS:
    https://github.com/AnacondaRecipes/openblas-feedstock/blob/ae5af5e/recipe/meta.yaml#L127-L131

    And the ``run_exports`` for OpenBLAS, as part of
    openblas-devel:
    https://github.com/AnacondaRecipes/openblas-feedstock/blob/ae5af5e/recipe/meta.yaml#L100

    Fundamentally, conda’s model of mutual exclusivity relies on the package name.
    OpenBLAS and MKL are obviously not the same package name, and thus are not
    mutually exclusive. There’s nothing stopping conda from installing both at
    once. There’s nothing stopping conda from installing NumPy with MKL and SciPy
    with OpenBLAS. The metapackage is what allows us to achieve the mutual
    exclusivity. It unifies the options on a single package name,
    but with a different build string. Automating the addition of the
    metapackage with ``run_exports`` helps ensure the library consumers
    (package builders who depend on libraries) will have correct dependency
    information to achieve the unified runtime library collection.

使用 BLAS 变体安装 NumPy
***********************************

Installing NumPy with BLAS variants

.. tab:: 中文

    要指定你想要的 NumPy 变体，你可以尝试直接指定所需的 BLAS 库，例如::
    
      conda install numpy mkl
    
    然而，这并不能真正排除 OpenBLAS 被选中的可能性。
    MKL 及其依赖项并不是互斥的（也就是说，它们的名称不会相似，只是版本或构建字符串不同），
    这条安装路径可能会引入一定的歧义，甚至导致混合使用多个 BLAS 实现的情形。
    
    因此，推荐使用 metapackage 的方式来指定。
    若希望以 **无歧义** 的方式安装基于 MKL 的 NumPy，可以通过直接或间接指定互斥包（mutex package）来实现::
    
      conda install numpy "blas=*=mkl"
    
    当然，也有更简便的方法。比如你可以选择安装某个依赖了所需互斥包的其他软件包。
    
    OpenBLAS 提供了这样的 “nomkl” 包：
    https://github.com/AnacondaRecipes/openblas-feedstock/blob/ae5af5e/recipe/meta.yaml#L133-L147
    
    “nomkl” 本身不应作为其他软件包的依赖项。
    它纯粹是为用户提供的一种工具，用于将默认的 MKL 切换为 OpenBLAS。
    
    那 MKL 是如何成为默认选项的呢？解算器（solver）需要一种机制来对某些软件包进行优先排序。
    我们借助一个较早的 Conda 特性来实现这一点： ``track_features``。
    它最初是为其他目的设计的，但在此场景中被用于优先级管理。


.. tab:: 英文

    To specify which variant of NumPy that you want, you could potentially
    specify the BLAS library you want::

      conda install numpy mkl

    However, that doesn’t actually preclude OpenBLAS from being chosen.
    Neither MKL nor its dependencies are mutually exclusive (meaning they
    do not have similar names and different version/build-string).

    This pathway may lead to some ambiguity and solutions with mixed BLAS,
    so using the metapackage is recommended. To specify MKL-powered NumPy
    in a non-ambiguous way, you can specify the mutex package (either directly
    or indirectly)::

      conda install numpy “blas=*=mkl”

    There is a simpler way to address this, however. For example, you may want to
    try another package that has the desired mutex package as a dependency.

    OpenBLAS has this with its “nomkl” package:
    https://github.com/AnacondaRecipes/openblas-feedstock/blob/ae5af5e/recipe/meta.yaml#L133-L147

    Nothing should use “nomkl” as a dependency. It is strictly a utility for users
    to facilitate switching from MKL (which is the default) to OpenBLAS.

    How did MKL become the default? The solver needs a way to prioritize some packages
    over others. We achieve that with an older conda feature called track_features that originally
    served a different purpose.

Track_features
**************

Track_features

.. tab:: 中文

    Conda 的一个优化目标是尽可能减少为指定期望规格所需的 ``track_features`` 数量。
    通过为一个或多个候选项添加 ``track_features``，Conda 会降低其优先级，或可理解为“加重其权重”。
    在多个候选包中， **优先级最低** 的是指那些在环境中会激活最多 ``track_features`` 的那个；
    而默认包是那个在环境中会激活最少 ``track_features`` 的。

    不过，这里有一个限制： **每个** ``track_feature`` 必须是唯一的。
    不能有两个包提供相同的 ``track_feature``。
    因此，我们的标准做法是将 ``track_features`` 附加到希望设为“非默认”的 metapackage 上。

    再看看 OpenBLAS 的构建配方：
    https://github.com/AnacondaRecipes/openblas-feedstock/blob/ae5af5e/recipe/meta.yaml#L127-L137

    该配方中的 ``track_features`` 条目正是 Conda 在 OpenBLAS 与 MKL 之间选择 MKL 的原因。
    MKL 不附带任何 ``track_features``。
    假如存在三个可选项，你可以这样分配：

    - 默认选项：不附加任何 ``track_feature``；
    - 次优选项：附加 1 个 ``track_feature``；
    - 最低优选项：附加 2 个 ``track_features``。

    不过，由于通常我们只关心默认选项， **因此实际操作中只需为所有非默认选项各添加一个** ``track_feature`` 即可。


.. tab:: 英文

    One of conda’s optimization goals is to minimize the number of track_features needed
    to specify the desired specs. By adding track_features to one or more of the options,
    conda will de-prioritize it or “weigh it down.” The lowest priority package is the one
    that would cause the most track_features to be activated in the environment. The default
    package among many variants is the one that would cause the least track_features to be activated.

    There is a catch, though: any track_features must be unique. No two packages can provide the
    same track_feature. For this reason, our standard practice is to attach track_features to
    the metapackage associated with what we want to be non-default.

    Take another look at the OpenBLAS recipe: https://github.com/AnacondaRecipes/openblas-feedstock/blob/ae5af5e/recipe/meta.yaml#L127-L137

    This attached track_features entry is why MKL is chosen over OpenBLAS.
    MKL does not have any track_features associated with it. If there are 3 options,
    you would attach 0 track_features to the default, then 1 track_features for the next preferred
    option, and finally 2 for the least preferred option. However, since you generally only care
    about the one default, it is usually sufficient to add 1 track_feature to all options other
    than the default option.

更多信息
*********

More info

.. tab:: 中文

    作为参考，Windows 上的 Visual Studio 版本对齐也使用互斥元包 https://github.com/AnacondaRecipes/aggregate/blob/9635228/vs2017/meta.yaml#L24

.. tab:: 英文

    For reference, the Visual Studio version alignment on Windows also uses mutex metapackages.
    https://github.com/AnacondaRecipes/aggregate/blob/9635228/vs2017/meta.yaml#L24


.. _noarch:

Noarch 软件包
===============

Noarch packages

.. tab:: 中文

    **Noarch（跨平台）软件包** 是指与体系结构无关的软件包，因此只需构建一次即可在所有平台使用。这类软件包可以是 generic 或 Python 类型：

    * `noarch: generic` 允许分发文档、数据集和源代码；
    * `noarch: python` 专指纯 Python 包，如下所述。

    在构建配置（ `meta.yaml` ）的 `build` 部分声明 `noarch` 可以减少 CI 资源占用。因此，符合条件的软件包应尽可能标记为 noarch。

.. tab:: 英文

    Noarch packages are packages that are not architecture specific
    and therefore only have to be built once. Noarch packages are
    either generic or Python. Noarch generic packages allow users to
    distribute docs, datasets, and source code in conda packages.
    Noarch Python packages are described below.

    Declaring these packages as ``noarch`` in the ``build`` section of
    the ``meta.yaml`` reduces shared CI resources. Therefore, all packages
    that qualify to be noarch packages should be declared as such.

Noarch Python
-------------

Noarch Python

.. tab:: 中文

    设置 `noarch: python` 的好处在于，只需构建一次，即可支持多个平台和 Python 版本，平台差异和版本差异在安装时解决。

    满足以下所有条件的软件包可被声明为 noarch Python 包：

    * 不包含编译扩展。
    * 无 post-link、pre-link 或 pre-unlink 脚本。
    * 无操作系统特定构建脚本。
    * 无 Python 版本特定要求。
    * 除了 Python 版本外无跳过（skip）声明。若为 py3-only，请移除 skip 语句，并在 host 和 run 中添加版本约束。
    * 不使用 2to3。
    * 不使用 setup.py 中的 scripts 参数。
    * 若 setup.py 中有 ``console_script`` 类型的入口点，需在 ``meta.yaml`` 中列出。
    * 无 activate 脚本。
    * 不是 conda 的依赖项。

    .. note::
        ``noarch: python`` 不支持使用 selector（如 `# [win]` ），但支持版本约束。某些场景下可将 ``skip: True  # [py2k]`` 替换为版本约束，如： ``python >=3``。

    .. note::
        仅 ``console_script`` 类型的入口点必须列在 `meta.yaml` 中。其他入口点不影响 noarch，因此无需额外处理。

    更多信息见：  
    `conda's noarch packages <https://www.anaconda.com/condas-new-noarch-packages/>`_

.. tab:: 英文

    The ``noarch: python`` directive in the build section
    makes pure-Python packages that only need to be built once.

    Noarch Python packages cut down on the overhead of building multiple
    different pure Python packages on different architectures and Python
    versions by sorting out platform and Python version-specific differences
    at install time.

    In order to qualify as a noarch Python package, all of the following
    criteria must be fulfilled:

    * No compiled extensions.

    * No post-link, pre-link, or pre-unlink scripts.

    * No OS-specific build scripts.

    * No Python version-specific requirements.

    * No skips except for Python version. If the recipe is py3 only,
      remove skip statement and add version constraint on Python in host
      and run section.

    * 2to3 is not used.

    * Scripts argument in setup.py is not used.

    * If ``console_script`` entrypoints are in setup.py,
      they are listed in ``meta.yaml``.

    * No activate scripts.

    * Not a dependency of conda.

    .. note::
      While ``noarch: python`` does not work with selectors, it does
      work with version constraints. ``skip: True  # [py2k]`` can sometimes
      be replaced with a constrained Python version in the host and run
      subsections, for example: ``python >=3`` instead of just ``python``.

    .. note::
      Only ``console_script`` entry points have to be listed in ``meta.yaml``.
      Other entry points do not conflict with ``noarch`` and therefore do
      not require extra treatment.

    Read more about `conda's noarch packages <https://www.anaconda.com/condas-new-noarch-packages/>`_.

.. _link_unlink:

链接和取消链接脚本
=======================

Link and unlink scripts

.. tab:: 中文

    您可以选择在链接和取消链接步骤之前和之后执行脚本。更多信息，请参阅 `添加预链接、后链接和取消链接前脚本 <https://docs.conda.io/projects/conda-build/en/latest/resources/link-scripts.html>`_。

.. tab:: 英文

    You may optionally execute scripts before and after the link and unlink steps. For more information, see `Adding pre-link, post-link, and pre-unlink scripts <https://docs.conda.io/projects/conda-build/en/latest/resources/link-scripts.html>`_.

.. _package_specs:

更多信息
================

More information

.. tab:: 中文

    如需了解更多信息，请深入了解我们的 :doc:`管理软件包指南 <../tasks/manage-pkgs>`。如需了解更多关于软件包元数据、仓库结构和索引以及软件包匹配规范的信息，请参阅 :doc:`软件包规范 <../concepts/pkg-specs>`。

.. tab:: 英文

    For more information, go for a deeper dive in our :doc:`managing packages guide <../tasks/manage-pkgs>`. Learn more about package metadata, repository structure and index, and package match specifications at :doc:`Package specifications <../concepts/pkg-specs>`.
