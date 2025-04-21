=====================
软件包规范
=====================

Package specification

.. _package_metadata:

软件包元数据
================

Package metadata

.. tab:: 中文

``info/`` 目录包含了有关软件包的所有元数据。  
该位置的文件不会被安装到安装前缀下。尽管你可以自由添加任何文件到该目录中，但 conda 仅检查下文所述文件的内容。

.. tab:: 英文

    The ``info/`` directory contains all metadata about a package.
    Files in this location are not installed under the install
    prefix. Although you are free to add any file to this directory,
    conda only inspects the content of the files discussed below.

信息
----

Info

.. tab:: 中文

    * files
    
      * 软件包中的所有文件的列表（不包括 ``info/`` 中的文件）
    
    * ``index.json``
    
      * 有关软件包的元数据，包括平台、版本、依赖关系和构建信息
    
    .. code-block:: bash
    
      {
        "arch": "x86_64",
        "build": "py37hfa4b5c9_1",
        "build_number": 1,
        "depends": [
          "depend > 1.1.1"
        ],
        "license": "BSD 3-Clause",
        "name": "fun-packge",
        "platform": "linux",
        "subdir": "linux-64",
        "timestamp": 1535416612069,
        "version": "0.0.0"
      }
    
    * ``paths.json``
    
      * 软件包中所有文件的列表，以及其关联的 SHA-256、字节大小和路径类型（例如 hardlink 或 softlink）
    
    .. code-block:: bash
    
      {
        "paths": [
          {
            "_path": "lib/python3.7/site-packages/fun-packge/__init__.py",
            "path_type": "hardlink",
            "sha256": "76f3b6e34feeb651aff33ca59e0279c4eadce5a50c6ad93b961c846f7ba717e9",
            "size_in_bytes": 2067
          },
          {
            "_path": "lib/python3.7/site-packages/fun-packge/__config__.py",
            "path_type": "hardlink",
            "sha256": "348e3602616c1fe4c84502b1d8cf97c740d886002c78edab176759610d287f06",
            "size_in_bytes": 87519
          },
          ...
      }

.. tab:: 英文

    * files
    
      * a list of all the files in the package (not included in ``info/``)
    
    * ``index.json``
    
      * metadata about the package including platform, version,
        dependencies, and build info
    
    .. code-block:: bash
    
      {
        "arch": "x86_64",
        "build": "py37hfa4b5c9_1",
        "build_number": 1,
        "depends": [
          "depend > 1.1.1"
        ],
        "license": "BSD 3-Clause",
        "name": "fun-packge",
        "platform": "linux",
        "subdir": "linux-64",
        "timestamp": 1535416612069,
        "version": "0.0.0"
      }
    
    * ``paths.json``
    
      * a list of files in the package, along with their associated SHA-256, size in bytes,
        and the type of path (eg. hardlink vs. softlink)
    
    .. code-block:: bash
    
      {
        "paths": [
          {
            "_path": "lib/python3.7/site-packages/fun-packge/__init__.py",
            "path_type": "hardlink",
            "sha256": "76f3b6e34feeb651aff33ca59e0279c4eadce5a50c6ad93b961c846f7ba717e9",
            "size_in_bytes": 2067
          },
          {
            "_path": "lib/python3.7/site-packages/fun-packge/__config__.py",
            "path_type": "hardlink",
            "sha256": "348e3602616c1fe4c84502b1d8cf97c740d886002c78edab176759610d287f06",
            "size_in_bytes": 87519
          },
          ...
      }


info/index.json
---------------

info/index.json

.. tab:: 中文
    
    该文件包含有关软件包的基本信息，如名称、版本、构建字符串和依赖项。其内容会被存储到 ``repodata.json`` 中，该文件是仓库索引文件，因此命名为 ``index.json``。该 JSON 对象是一个字典，包含如下键。conda 包的文件名由前三个值组成，如：  
    ``<name>-<version>-<build>.tar.bz2``
    
    .. list-table::
       :widths: 15 15 50
    
       * - **键**
         - **类型**
         - **说明**
    
       * - name
         - string
         - 软件包名称的小写形式。可以包含字符 ``-``。
    
       * - version
         - string
         - 软件包版本。不能包含 ``-``。  
           Conda 遵循 `PEP 440 <https://www.python.org/dev/peps/pep-0440/>`_。
    
       * - build
         - string
         - 构建字符串。不能包含 ``-``。用于区分名称和版本相同的不同构建，例如：
    
           * 不同的依赖项，例如 Python 3.4 与 Python 2.7。
           * 构建过程中的修复。
           * 不同的可选依赖项，例如 MKL 与 ATLAS 链接。  
             conda 实际上并不会检查构建字符串的内容，诸如 ``np18py34_1`` 的字符串仅供人类阅读，conda 不会解析这些字符串。
    
       * - build_number
         - integer
         - 软件包构建编号，为非负整数。
    
           与构建字符串不同，conda 会检查 build_number。  
           conda 使用它来对名称和版本相同的软件包进行排序，以确定最新版本。  
           这很重要，因为带有 bug 修复的新构建可能会被添加到仓库中。
    
       * - depends
         - string 列表
         - 依赖项规范的列表，每个元素是一个字符串，详见 :ref:`build-version-spec`。
    
       * - arch
         - string
         - （可选）软件包构建所针对的架构。
    
           示例： ``x86_64``  
           conda 当前不会使用该键。
    
       * - platform
         - string
         - （可选）软件包构建所针对的操作系统。
    
           示例： ``osx``  
           conda 当前不会使用该键。特定架构与平台的软件包通常通过仓库子目录区分——参见 :ref:`repo-si`。

.. tab:: 英文

    This file contains basic information about the package, such as
    name, version, build string, and dependencies. The content of this
    file is stored in ``repodata.json``, which is the repository
    index file, hence the name ``index.json``. The JSON object is a
    dictionary containing the keys shown below. The filename of the
    conda package is composed of the first 3 values, as in:
    ``<name>-<version>-<build>.tar.bz2``.
    
    .. list-table::
       :widths: 15 15 50
    
       * - **Key**
         - **Type**
         - **Description**
    
       * - name
         - string
         - The lowercase name of the package. May contain the "-"
           character.
    
       * - version
         - string
         - The package version. May not contain "-". Conda
           acknowledges `PEP 440
           <https://www.python.org/dev/peps/pep-0440/>`_.
    
       * - build
         - string
         - The build string. May not contain "-". Differentiates
           builds of packages with otherwise identical names and
           versions, such as:
    
           * A build with other dependencies, such as Python 3.4
             instead of Python 2.7.
           * A bug fix in the build process.
           * Some different optional dependencies, such as MKL versus
             ATLAS linkage. Nothing in conda actually inspects the
             build string. Strings such as ``np18py34_1`` are
             designed only for human readability and conda never
             parses them.
    
       * - build_number
         - integer
         - A non-negative integer representing the build number of
           the package.
    
           Unlike the build string, the build_number is inspected by
           conda. Conda uses it to sort packages that have otherwise
           identical names and versions to determine the latest one.
           This is important because new builds that contain bug
           fixes for the way a package is built may be added to a
           repository.
    
       * - depends
         - list of strings
         - A list of dependency specifications, where each element
           is a string, as outlined in :ref:`build-version-spec`.
    
       * - arch
         - string
         - Optional. The architecture the package is built for.
    
           EXAMPLE: ``x86_64``
    
           Conda currently does not use this key.
    
       * - platform
         - string
         - Optional. The OS that the package is built for.
    
           EXAMPLE: ``osx``
    
           Conda currently does not use this key. Packages for a
           specific architecture and platform are usually
           distinguished by the repository subdirectory that contains
           them---see :ref:`repo-si`.

info/files
----------

info/files

.. tab:: 中文

    此文件列出软件包中自身包含的所有文件，每行一个。这些文件都需要链接到环境中。任何未列在该文件中的包内文件在安装时不会被链接。  
    ``info/files`` 中的文件路径分隔符必须始终为 ``/``，即使在 Windows 上也如此，以匹配压缩包中的目录格式。

.. tab:: 英文

    Lists all files that are part of the package itself, 1 per line.
    All of these files need to get linked into the environment. Any
    files in the package that are not listed in this file are not
    linked when the package is installed. The directory delimiter for
    the files in ``info/files`` should always be "/", even on
    Windows. This matches the directory delimiter used in the
    tarball.


info/has_prefix
---------------

info/has_prefix

.. tab:: 中文
    
    （可选）文件。列出所有包含硬编码构建前缀或占位符前缀的文件，这些前缀在安装时需要替换为实际的安装前缀。
    
    .. note::
       由于二进制替换的方式，占位符前缀必须长于安装前缀。
    
    该文件的每一行应为一个路径，此时其被视为文本文件，使用默认占位符 ``/opt/anaconda1anaconda2anaconda3``；或为空格分隔的 占位符、模式、路径 三项：
    
    * 占位符：构建时的前缀或占位符前缀。
    * 模式：为 ``text`` 或 ``binary``。
    * 路径：需更新文件的相对路径。
    
    示例：Windows 上::
    
      "Scripts/script1.py"
      "C:\Users\username\anaconda\envs\_build" text "Scripts/script2.bat"
      "C:/Users/username/anaconda/envs/_build" binary "Scripts/binary"
    
    示例：macOS 或 Linux 上::
    
      bin/script.sh
      /Users/username/anaconda/envs/_build binary bin/binary
      /Users/username/anaconda/envs/_build text share/text
    
    .. note::
       相对路径中的目录分隔符必须始终为 ``/``，即使在 Windows 上也是如此。  
       占位符在 Windows 上可使用 ``\\`` 或 ``/``，但替换前缀将匹配占位符中使用的分隔符。  
       默认占位符 ``/opt/anaconda1anaconda2anaconda3`` 是一个例外，替换为安装前缀时使用本地路径分隔符。  
       在 Windows 上，占位符与路径总是以引号括起，以支持带空格的路径。

.. tab:: 英文

    Optional file. Lists all files that contain a hard-coded build
    prefix or placeholder prefix, which needs to be replaced by the
    install prefix at installation time.
    
    .. note::
       Due to the way the binary replacement works, the
       placeholder prefix must be longer than the install prefix.
    
    Each line of this file should be either a path, in which case it
    is considered a text file with the default placeholder
    ``/opt/anaconda1anaconda2anaconda3``, or a space-separated list
    of placeholder, mode, and path, where:
    
    * Placeholder is the build or placeholder prefix.
    * Mode is either ``text`` or ``binary``.
    * Path is the relative path of the file to be updated.
    
    EXAMPLE: On Windows::
    
      "Scripts/script1.py"
      "C:\Users\username\anaconda\envs\_build" text "Scripts/script2.bat"
      "C:/Users/username/anaconda/envs/_build" binary "Scripts/binary"
    
    EXAMPLE: On macOS or Linux::
    
      bin/script.sh
      /Users/username/anaconda/envs/_build binary bin/binary
      /Users/username/anaconda/envs/_build text share/text
    
    .. note::
       The directory delimiter for the relative path must always
       be "/", even on Windows. The placeholder may contain either "\\"
       or "/" on Windows, but the replacement prefix will match the
       delimiter used in the placeholder. The default placeholder
       ``/opt/anaconda1anaconda2anaconda3`` is an exception, being
       replaced with the install prefix using the native path
       delimiter. On Windows, the placeholder and path always appear
       in quotes to support paths with spaces.

info/license.txt
----------------

info/license.txt

.. tab:: 中文

    （可选）文件。软件包的软件许可证。

.. tab:: 英文

    Optional file. The software license for the package.

info/no_link
------------

info/no_link

.. tab:: 中文

    （可选）文件。列出无法被链接（软链接或硬链接）到环境中的所有文件，这些文件将被复制而非链接。

.. tab:: 英文

    Optional file. Lists all files that cannot be linked - either
    soft-linked or hard-linked - into environments and are copied
    instead.

info/about.json
---------------

info/about.json

.. tab:: 中文

    （可选）文件。包含 ``meta.yaml`` 文件中 `about 段 <https://docs.conda.io/projects/conda-build/en/latest/resources/define-metadata.html#about-section>`_ 中的条目。  
    若构建配方中提供了以下键，则它们会被添加到 ``info/about.json`` 中：

    * home
    * dev_url
    * doc_url
    * license_url
    * license
    * summary
    * description
    * license_family

.. tab:: 英文

    Optional file. Contains the entries in the `about section <https://docs.conda.io/projects/conda-build/en/latest/resources/define-metadata.html#about-section>`_
    of the ``meta.yaml`` file. The following keys are
    added to ``info/about.json`` if present in the build recipe:

    * home
    * dev_url
    * doc_url
    * license_url
    * license
    * summary
    * description
    * license_family

info/recipe
-----------

info/recipe

.. tab:: 中文

    包含构建配方全部内容的目录。

.. tab:: 英文

    A directory containing the full contents of the build recipe.

meta.yaml.rendered
------------------

meta.yaml.rendered

.. tab:: 中文

    完整渲染的构建配方。参见
    `conda render <https://docs.conda.io/projects/conda-build/en/latest/resources/commands/conda-render.html>`_。

    仅当 `build 部分 <https://docs.conda.io/projects/conda-build/en/latest/resources/define-metadata.html#build-section>`_ 中的 include_recipe 标志
    设置为 ``True`` 时，该目录才会存在。

.. tab:: 英文

    The fully rendered build recipe. See
    `conda render <https://docs.conda.io/projects/conda-build/en/latest/resources/commands/conda-render.html>`_.

    This directory is present only when the the include_recipe flag
    is ``True`` in the `build section <https://docs.conda.io/projects/conda-build/en/latest/resources/define-metadata.html#build-section>`_.


.. _repo-si:

代码库结构和索引
==============================

Repository structure and index

.. tab:: 中文

    一个 conda 仓库（或称频道）是一个目录树，通常通过 HTTPS 提供服务，
    它包含若干平台子目录，每个子目录中包含 conda 软件包以及一个仓库索引。
    索引文件 ``repodata.json`` 列出了该平台子目录中的所有 conda 软件包。
    可使用 ``conda index`` 从某一目录中的 conda 软件包生成这样的索引。
    它是将完整的 conda 软件包文件名映射为 ``info/index.json`` 中所述字典对象的简单方式，
    参见 `链接脚本 <https://docs.conda.io/projects/conda-build/en/latest/resources/link-scripts.html>`_。

    以下示例展示了一个仓库在 64 位 Linux 与 32 位 Windows 上提供软件包
    ``misc-1.0-np17py27_0.tar.bz2`` 的情况::

      <some path>/linux-64/repodata.json
                          repodata.json.bz2
                          misc-1.0-np17py27_0.tar.bz2
                /win-32/repodata.json
                        repodata.json.bz2
                        misc-1.0-np17py27_0.tar.bz2

    .. note::
      这两个 conda 软件包具有相同的文件名，
      它们仅通过所在的仓库子目录进行区分。

.. tab:: 英文
    
    A conda repository - or channel - is a directory tree, usually
    served over HTTPS, which has platform subdirectories, each of
    which contain conda packages and a repository index. The index
    file ``repodata.json`` lists all conda packages in the platform
    subdirectory. Use ``conda index`` to create such an index from
    the conda packages within a directory. It is simple mapping of
    the full conda package filename to the dictionary object in
    ``info/index.json`` described in `link scripts <https://docs.conda.io/projects/conda-build/en/latest/resources/link-scripts.html>`_.
    
    In the following example, a repository provides the conda package
    ``misc-1.0-np17py27_0.tar.bz2`` on 64-bit Linux and 32-bit
    Windows::
    
      <some path>/linux-64/repodata.json
                           repodata.json.bz2
                           misc-1.0-np17py27_0.tar.bz2
                 /win-32/repodata.json
                         repodata.json.bz2
                         misc-1.0-np17py27_0.tar.bz2
    
    .. note::
       Both conda packages have identical filenames and are
       distinguished only by the repository subdirectory that contains
       them.


.. _build-version-spec:

软件包匹配规范
============================

Package match specifications

.. tab:: 中文

    匹配规范（match specification）并不等同于命令行中 ``conda install`` 的语法，
    例如 ``conda install python=3.9``。
    在内部，conda 会将命令行语法转换为本节中定义的规范。

    示例：python=3.9 会被转换为 python 3.9*。

    软件包依赖通过匹配规范进行指定。
    匹配规范是由 1 至 3 个部分组成的以空格分隔的字符串：

    * 第一部分始终是软件包的精确名称。

    * 第二部分指定版本，可能包含特殊字符：

      * \| 表示“或”。

        示例：``1.0|1.2`` 匹配版本 1.0 或 1.2

      * \* 匹配版本字符串中的 0 个或多个字符。
        相当于正则表达式中的 ``.*``。

        示例：1.0|1.4* 匹配 1.0、1.4 和 1.4.1b2，但不匹配 1.2。

      * <、>、<=、>=、== 和 != 是版本的关系运算符，
        其比较方式遵循 `PEP-440 <https://www.python.org/dev/peps/pep-0440/>`_。
        例如，``<=1.0`` 匹配 ``0.9``、``0.9.1`` 和 ``1.0``，但不匹配 ``1.0.1``。
        ``==`` 和 ``!=`` 表示精确相等。

        预发布版本也受到支持，例如 ``>1.0b4`` 将匹配 ``1.0b5`` 和 ``1.0rc1``，
        但不匹配 ``1.0b4`` 或 ``1.0a5``。

        示例：<=1.0 匹配 0.9、0.9.1 和 1.0，但不匹配 1.0.1。

      * , 表示“与”。

        示例：>=2,<3 匹配所有 2.x 系列版本，如 2.0、2.1 和 2.9，
        但不匹配 3.0 或 1.0。

      * , 的优先级高于 \|，因此 >=1,<2|>3 的含义是：
        大于等于 1 且小于 2，或大于 3，匹配 1、1.3 和 3.0，但不匹配 2.2。

      Conda 会以 \| 为分隔符解析版本。如果某部分以 <、>、= 或 ! 开头，
      则按关系运算符解析，否则按可能包含 "*" 的版本解析。

    * 第三部分始终是精确的构建字符串。当匹配规范包含三部分时，
      第二部分必须是精确版本。

    请注意，版本规范中不能包含空格，
    因为空格用于分隔整个匹配规范中的包名、版本和构建字符串。
    ``python >= 2.7`` 是无效的匹配规范。
    此外，``python>=2.7`` 会被解释为名为 ``python>=2.7`` 的包的任意版本。

    在命令行中使用时，若版本规范包含空格，或使用了 <、>、\*、\| 等字符，
    应使用双引号括起整个字符串。

    示例::
    
      conda install numpy=1.11
      conda install numpy==1.11
      conda install "numpy>1.11"
      conda install "numpy=1.11.1|1.11.3"
      conda install "numpy>=1.8,<2"


.. tab:: 英文

    This match specification is not the same as the syntax used at
    the command line with ``conda install``, such as
    ``conda install python=3.9``. Internally, conda translates the
    command line syntax to the spec defined in this section.
    
    EXAMPLE: python=3.9 is translated to python 3.9*.
    
    Package dependencies are specified using a match specification.
    A match specification is a space-separated string of 1, 2, or 3
    parts:
    
    * The first part is always the exact name of the package.
    
    * The second part refers to the version and may contain special
      characters:
    
      * \| means OR.
    
        EXAMPLE: ``1.0|1.2`` matches version 1.0 or 1.2
    
      * \* matches 0 or more characters in the version string. In
        terms of regular expressions, it is the same as ``r``.*````.
    
        EXAMPLE: 1.0|1.4* matches 1.0, 1.4 and 1.4.1b2, but not 1.2.
    
      * <, >, <=, >=, == and != are relational operators on versions,
        which are compared using
        `PEP-440 <https://www.python.org/dev/peps/pep-0440/>`_.  For example,
        ``<=1.0`` matches ``0.9``, ``0.9.1``, and ``1.0``, but not ``1.0.1``.
        ``==`` and ``!=`` are exact equality.
    
        Pre-release versioning is also supported such that ``>1.0b4`` will match
        ``1.0b5`` and ``1.0rc1`` but not ``1.0b4`` or ``1.0a5``.
    
        EXAMPLE: <=1.0 matches 0.9, 0.9.1, and 1.0, but not 1.0.1.
    
      * , means AND.
    
        EXAMPLE: >=2,<3 matches all packages in the 2 series. 2.0,
        2.1 and 2.9 all match, but 3.0 and 1.0 do not.
    
      * , has higher precedence than \|, so >=1,<2|>3 means greater
        than or equal to 1 AND less than 2 or greater than 3, which
        matches 1, 1.3 and 3.0, but not 2.2.
    
      Conda parses the version by splitting it into parts separated
      by \|. If the part begins with <, >, =, or !, it is parsed as a
      relational operator. Otherwise, it is parsed as a version,
      possibly containing the "*" operator.
    
    * The third part is always the exact build string. When there are
      3 parts, the second part must be the exact version.
    
    Remember that the version specification cannot contain spaces,
    as spaces are used to delimit the package, version, and build
    string in the whole match specification. ``python >= 2.7`` is an
    invalid match specification. Furthermore, ``python>=2.7`` is
    matched as any version of a package named ``python>=2.7``.
    
    When using the command line, put double quotes around any package
    version specification that contains the space character or any of
    the following characters: <, >, \*, or \|.
    
    EXAMPLE::
    
      conda install numpy=1.11
      conda install numpy==1.11
      conda install "numpy>1.11"
      conda install "numpy=1.11.1|1.11.3"
      conda install "numpy>=1.8,<2"


示例
--------

Examples

.. tab:: 中文

    OR 条件 "numpy=1.11.1|1.11.3" 匹配 1.11.1 或 1.11.3。
    
    AND 条件 "numpy>=1.8,<2" 匹配 1.8 和 1.9，但不匹配 2.0。
    
    模糊约束 numpy=1.11 匹配 1.11、1.11.0、1.11.1、1.11.2、1.11.18 等。
    
    精确约束 numpy==1.11 匹配 1.11、1.11.0、1.11.0.0 等。
    
    构建字符串约束 "numpy=1.11.2=*nomkl*" 匹配不包含 MKL 的 NumPy 1.11.2 包，
    而不匹配正常的 MKL NumPy 1.11.2 包。
    
    构建字符串约束 "numpy=1.11.1|1.11.3=py36_0" 匹配构建于 Python 3.6 的 NumPy 1.11.1 或 1.11.3，
    但不匹配构建于 Python 3.5 或 Python 2.7 的版本。
    
    以下是所有适用于 numpy-1.8.1-py27_0 的有效匹配规范：
    
    * numpy
    * numpy 1.8*
    * numpy 1.8.1
    * numpy >=1.8
    * numpy ==1.8.1
    * numpy 1.8|1.8*
    * numpy >=1.8,<2
    * numpy >=1.8,<2|1.9
    * numpy 1.8.1 py27_0
    * numpy=1.8.1=py27_0

.. tab:: 英文

    The OR constraint "numpy=1.11.1|1.11.3" matches with 1.11.1 or
    1.11.3.
    
    The AND constraint "numpy>=1.8,<2" matches with 1.8 and 1.9 but
    not 2.0.
    
    The fuzzy constraint numpy=1.11 matches 1.11, 1.11.0, 1.11.1,
    1.11.2, 1.11.18, and so on.
    
    The exact constraint numpy==1.11 matches 1.11, 1.11.0, 1.11.0.0,
    and so on.
    
    The build string constraint "numpy=1.11.2=*nomkl*" matches the
    NumPy 1.11.2 packages without MKL but not the normal MKL NumPy
    1.11.2 packages.
    
    The build string constraint "numpy=1.11.1|1.11.3=py36_0" matches
    NumPy 1.11.1 or 1.11.3 built for Python 3.6 but not any versions
    of NumPy built for Python 3.5 or Python 2.7.
    
    The following are all valid match specifications for
    numpy-1.8.1-py27_0:
    
    * numpy
    * numpy 1.8*
    * numpy 1.8.1
    * numpy >=1.8
    * numpy ==1.8.1
    * numpy 1.8|1.8*
    * numpy >=1.8,<2
    * numpy >=1.8,<2|1.9
    * numpy 1.8.1 py27_0
    * numpy=1.8.1=py27_0

版本排序
================

Version ordering

.. tab:: 中文

    ``class VersionOrder(object)`` 实现了版本字符串之间的排序关系。

    版本字符串可包含通常的字母数字字符（A-Za-z0-9），
    通过点或下划线分隔各个组成部分。禁止出现空段（例如连续两个点、前/后导下划线）。
    版本字符串前可以有一个可选的 epoch 编号（即一个整数后跟 ``!``），
    用于表示版本规则发生变化。版本比较不区分大小写。

.. tab:: 英文

    The ``class VersionOrder(object)`` implements an order relation
    between version strings.
    
    Version strings can contain the usual alphanumeric characters
    (A-Za-z0-9), separated into components by dots and underscores. Empty
    segments (i.e. two consecutive dots, a leading/trailing underscore)
    are not permitted. An optional epoch number - an integer
    followed by ``!`` - can precede the actual version string
    (this is useful to indicate a change in the versioning
    scheme itself). Version comparison is case-insensitive.

支持的版本字符串
-------------------------

Supported version strings

.. tab:: 中文

    Conda 支持六种类型的版本字符串：
    
    * 发布版本（release）仅包含整数，如 ``1.0``、``2.3.5``。
    * 预发布版本（pre-release）使用如 ``a`` 或 ``rc`` 的后缀，
      例如 ``1.0a1``、``1.2.beta3``、``2.3.5rc3``。
    * 开发版本（development）以 ``dev`` 标识，例如 ``1.0dev42``、``2.3.5.dev12``。
    * 后发布版本（post-release）以 ``post`` 标识，例如 ``1.0post1``、``2.3.5.post2``。
    * 标记版本（tagged）带有指定属性的后缀，如 ``1.1.parallel``。
      标签可用于前述四种类型，排序时视为预发布版本中的字符串。
    * 本地版本（local version）是通过 ``+`` 分隔附加的可选字符串。
      仅在主版本相等时参与比较，其处理方式与主版本一致。

.. tab:: 英文

    Conda supports six types of version strings:
    
       * Release versions contain only integers, e.g. ``1.0``, ``2.3.5``.
       * Pre-release versions use additional letters such as ``a`` or ``rc``,
         for example ``1.0a1``, ``1.2.beta3``, ``2.3.5rc3``.
       * Development versions are indicated by the string ``dev``,
         for example ``1.0dev42``, ``2.3.5.dev12``.
       * Post-release versions are indicated by the string ``post``,
         for example ``1.0post1``, ``2.3.5.post2``.
       * Tagged versions have a suffix that specifies a particular
         property of interest, e.g. ``1.1.parallel``. Tags can be added
         to any of the preceding 4 types. As far as sorting is concerned,
         tags are treated like strings in pre-release versions.
       * An optional local version string separated by ``+`` can be appended
         to the main (upstream) version string. It is only considered
         in comparisons when the main versions are equal, but otherwise
         handled in exactly the same manner.


可预测的版本排序
----------------------------

Predictable version ordering

.. tab:: 中文

    为了获得可预测的版本排序，必须保持软件包的版本号方案随时间一致。
    Conda 认为预发布版本低于正式版本。
    
    * 版本字符串应始终具有相同数量的组件（可选 tag 或 local 版本除外）。
    * 标识非发布版本的字母/字符串应位于一致位置。
    
    比较前，版本字符串会按以下方式解析：
    
    * 首先以 ``!`` 和 ``+`` 分别分隔 epoch、主版本号和本地版本号。
      若无 ``!``，epoch 设为 0；若无 ``+``，local version 为空。
    * 主版本再按 ``.`` 和 ``_`` 分隔成组件。
    * 每个组件再次划分为数字和非数字的序列。
    * 全数字子组件转为整数。
    * 字符串转为小写，``dev`` 和 ``post`` 有特殊处理。
    * 若组件以字母开头，则插入填充值 0，以保持数字与字符串对齐：
      ``1.1.a1 == 1.1.0a1``。
    * 本地版本部分亦重复该处理。
    
    示例：
    
    ``1.2g.beta15.rc  =>  [[0], [1], [2, 'g'], [0, 'beta', 15], [0, 'rc']]``
    
    ``1!2.15.1_ALPHA  =>  [[1], [2], [15], [1, '_alpha']]``
    
    解析结果为列表后，按字典序逐对比较各子组件，规则如下：
    
    * 整数按数值比较。
    * 字符串按不区分大小写的字典序比较。
    * 字符串小于整数，例外如下：
    
      * ``dev`` 版本小于所有其它对应类型版本。
      * ``post`` 版本大于所有其它对应类型版本。
    
    * 若某一子组件无对应项，则补充为整数 0，
      确保 ``'1.1' == 1.1.0'``。
    
    最终排序如下所示::
    
       0.4
     < 0.4.0
     < 0.4.1.rc
     == 0.4.1.RC   # 不区分大小写
     < 0.4.1
     < 0.5a1
     < 0.5b3
     < 0.5C1       # 不区分大小写
     < 0.5
     < 0.9.6
     < 0.960923
     < 1.0
     < 1.1dev1     # 特殊处理 ``dev``
     < 1.1a1
     < 1.1.0dev1   # 特殊处理 ``dev``
     == 1.1.dev1   # 数字 0 插入前缀
     < 1.1.a1
     < 1.1.0rc1
     < 1.1.0
     == 1.1
     < 1.1.0post1  # 特殊处理 ``post``
     == 1.1.post1  # 数字 0 插入前缀
     < 1.1post1    # 特殊处理 ``post``
     < 1996.07.12
     < 1!0.4.1     # epoch 增长
     < 1!3.1.1.6
     < 2!0.4.1     # epoch 再次增长
    
    某些软件包（尤其是 OpenSSL）使用不兼容的版本方案。
    尤其是 OpenSSL 中字母被解释为版本计数器而非预发布标识。
    例如，OpenSSL 中 ``1.0.1 < 1.0.1a`` 为真，而 conda 软件包中排序相反。
    可通过在普通版本号后添加 dash 来规避该问题：
    
    ``1.0.1a  =>  1.0.1post.a      # 确保 OpenSSL 顺序正确``

.. tab:: 英文

    To obtain a predictable version ordering, it is crucial to keep the
    version number scheme of a given package consistent over time.
    Conda considers prerelease versions as less than release versions.
    
    * Version strings should always have the same number of components
      (except for an optional tag suffix or local version string).
    
    * Letters/Strings indicating non-release versions should always
      occur at the same position.
    
    Before comparison, version strings are parsed as follows:
    
      * They are first split into epoch, version number, and local version
        number at ``!`` and ``+`` respectively. If there is no ``!``,
        the epoch is set to 0. If there is no ``+``, the local version is
        empty.
      * The version part is then split into components at ``.`` and ``_``.
      * Each component is split again into runs of numerals and non-numerals
      * Subcomponents containing only numerals are converted to integers.
      * Strings are converted to lowercase, with special treatment for ``dev``
        and ``post``.
      * When a component starts with a letter, the fillvalue 0 is inserted
        to keep numbers and strings in phase, resulting in ``1.1.a1' == 1.1.0a1'``.
      * The same is repeated for the local version part.
    
    Examples:
    
      ``1.2g.beta15.rc  =>  [[0], [1], [2, 'g'], [0, 'beta', 15], [0, 'rc']]``
    
      ``1!2.15.1_ALPHA  =>  [[1], [2], [15], [1, '_alpha']]``
    
    The resulting lists are compared lexicographically, where the following
    rules are applied to each pair of corresponding subcomponents:
    
      * Integers are compared numerically.
      * Strings are compared lexicographically, case-insensitive.
      * Strings are smaller than integers, except
    
          * ``dev`` versions are smaller than all corresponding versions of other types.
    
          * ``post`` versions are greater than all corresponding versions of other types.
      * If a subcomponent has no correspondent, the missing correspondent is
        treated as integer 0 to ensure ``'1.1' == 1.1.0'``.
    
    The resulting order is::
    
       0.4
     < 0.4.0
     < 0.4.1.rc
     == 0.4.1.RC   # case-insensitive comparison
     < 0.4.1
     < 0.5a1
     < 0.5b3
     < 0.5C1      # case-insensitive comparison
     < 0.5
     < 0.9.6
     < 0.960923
     < 1.0
     < 1.1dev1    # special case ``dev``
     < 1.1a1
     < 1.1.0dev1  # special case ``dev``
     == 1.1.dev1   # 0 is inserted before string
     < 1.1.a1
     < 1.1.0rc1
     < 1.1.0
     == 1.1
     < 1.1.0post1 # special case ``post``
     == 1.1.post1  # 0 is inserted before string
     < 1.1post1   # special case ``post``
     < 1996.07.12
     < 1!0.4.1    # epoch increased
     < 1!3.1.1.6
     < 2!0.4.1    # epoch increased again
    
    Some packages (most notably OpenSSL) have incompatible version conventions.
    In particular, OpenSSL interprets letters as version counters rather than
    pre-release identifiers. For OpenSSL, the relation ``1.0.1 < 1.0.1a   =>   True   # for OpenSSL``
    holds, whereas conda packages use the opposite ordering.
    You can work around this problem by appending a dash to plain
    version numbers:
    
    ``1.0.1a  =>  1.0.1post.a      # ensure correct ordering for OpenSSL``
