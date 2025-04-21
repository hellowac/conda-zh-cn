=========================
管理虚拟软件包
=========================

Managing virtual packages

.. tab:: 中文
    
    “虚拟”软件包会被注入到 conda 求解器中，以使真实软件包可以依赖于系统中存在但 conda 无法直接管理的某些功能，例如系统驱动版本或 CPU 特性。虚拟软件包并不是真正存在的软件包，因此不会出现在 ``conda list`` 的输出中。conda 会运行一小段代码，用于检测系统功能是否存在，并据此决定是否“提供”该虚拟软件包。目前支持的虚拟软件包列表包括：
    
      * ``__cuda``：显示驱动支持的最高 CUDA 版本。
      * ``__osx``：适用时，表示 OSX 的版本。
      * ``__glibc``：操作系统支持的 glibc 版本。
      * ``__linux``：在 Linux 系统中可用。
      * ``__unix``：在 OSX 或 Linux 系统中可用。
      * ``__win``：在 Windows 系统中可用。
      * ``__conda``：用于求解的 conda 版本。
    
    在未来的 conda 版本中还会添加其他虚拟软件包。这类虚拟包的名称以双下划线开头作为标识。
    
    .. note::
    
       注意，从 ``22.11.0`` 版本开始，
       :doc:`虚拟软件包 <../../dev-guide/plugins/virtual_packages>` 已作为
       :doc:`conda 插件 <../../user-guide/concepts/conda-plugins>` 实现。


.. tab:: 英文

    "Virtual" packages are injected into the conda solver to allow real packages
    to depend on features present on the system that cannot be managed directly by
    conda, like system driver versions or CPU features. Virtual packages are not
    real packages and not displayed by ``conda list``. Instead ``conda`` runs a
    small bit of code to detect the presence or absence of the system feature that
    corresponds to the package. The currently supported list of virtual packages includes:
    
      * ``__cuda``: Maximum version of CUDA supported by the display driver.
      * ``__osx``: OSX version if applicable.
      * ``__glibc``: Version of glibc supported by the OS.
      * ``__linux``: Available when running on Linux.
      * ``__unix``: Available when running on OSX or Linux.
      * ``__win``: Available when running on Win.
      * ``__conda``: Version of conda that is being used for solving.
    
    Other virtual packages will be added in future conda releases. These are denoted
    by a leading double-underscore in the package name.
    
    .. note::
    
       Note that as of version ``22.11.0``,
       :doc:`virtual packages <../../dev-guide/plugins/virtual_packages>` are
       implemented as :doc:`conda plugins <../../user-guide/concepts/conda-plugins>`.

列出检测到的虚拟软件包
=================================

Listing detected virtual packages

.. tab:: 中文

    请使用终端执行以下操作步骤。
    
    要查看检测到的虚拟软件包列表，请运行：
    
    .. code-block:: bash
    
       conda info
    
    如果检测到了某个软件包，你将在 ``virtual packages``（虚拟软件包）部分看到其列出，如下示例所示::
    
             active environment : base
            active env location : /Users/demo/dev/conda/devenv
                    shell level : 1
               user config file : /Users/demo/.condarc
         populated config files : /Users/demo/.condarc
                  conda version : 4.6.3.post8+8f640d35a
            conda-build version : 3.17.8
                 python version : 3.7.2.final.0
               virtual packages : __cuda=10.0
               base environment : /Users/demo/dev/conda/devenv (writable)
                   channel URLs : https://repo.anaconda.com/pkgs/main/osx-64
                                  https://repo.anaconda.com/pkgs/main/noarch
                                  https://repo.anaconda.com/pkgs/free/osx-64
                                  https://repo.anaconda.com/pkgs/free/noarch
                                  https://repo.anaconda.com/pkgs/r/osx-64
                                  https://repo.anaconda.com/pkgs/r/noarch
                  package cache : /Users/demo/dev/conda/devenv/pkgs
                                  /Users/demo/.conda/pkgs
               envs directories : /Users/demo/dev/conda/devenv/envs
                                  /Users/demo/.conda/envs
                       platform : osx-64
                     user-agent : conda/4.6.3.post8+8f640d35a requests/2.21.0 CPython/3.7.2 Darwin/17.7.0 OSX/10.13.6
                        UID:GID : 502:20
                     netrc file : None
                   offline mode : False

.. tab:: 英文

    Use the terminal for the following steps.
    
    To see the list of detected virtual packages, run:
    
    .. code-block:: bash
    
       conda info
    
    If a package is detected, you will see it listed in the ``virtual packages``
    section, as shown in this example::
    
             active environment : base
            active env location : /Users/demo/dev/conda/devenv
                    shell level : 1
               user config file : /Users/demo/.condarc
         populated config files : /Users/demo/.condarc
                  conda version : 4.6.3.post8+8f640d35a
            conda-build version : 3.17.8
                 python version : 3.7.2.final.0
               virtual packages : __cuda=10.0
               base environment : /Users/demo/dev/conda/devenv (writable)
                   channel URLs : https://repo.anaconda.com/pkgs/main/osx-64
                                  https://repo.anaconda.com/pkgs/main/noarch
                                  https://repo.anaconda.com/pkgs/free/osx-64
                                  https://repo.anaconda.com/pkgs/free/noarch
                                  https://repo.anaconda.com/pkgs/r/osx-64
                                  https://repo.anaconda.com/pkgs/r/noarch
                  package cache : /Users/demo/dev/conda/devenv/pkgs
                                  /Users/demo/.conda/pkgs
               envs directories : /Users/demo/dev/conda/devenv/envs
                                  /Users/demo/.conda/envs
                       platform : osx-64
                     user-agent : conda/4.6.3.post8+8f640d35a requests/2.21.0 CPython/3.7.2 Darwin/17.7.0 OSX/10.13.6
                        UID:GID : 502:20
                     netrc file : None
                   offline mode : False


覆盖检测到的软件包
============================

Overriding detected packages

.. tab:: 中文

    在进行故障排查时，可以通过环境变量覆盖虚拟软件包的自动检测机制。支持的变量包括：
    
    * ``CONDA_OVERRIDE_CUDA`` —— CUDA 版本号，或设置为 ``""`` 表示不检测 CUDA。
    * ``CONDA_OVERRIDE_OSX`` —— OSX 版本号，或设置为 ``""`` 表示不检测 OSX。
    * ``CONDA_OVERRIDE_GLIBC`` —— GLIBC 版本号，或设置为 ``""`` 表示不检测 GLIBC。此项仅适用于 Linux 系统。


.. tab:: 英文

    For troubleshooting, it is possible to override virtual package detection
    using an environment variable. Supported variables include:
    
    * ``CONDA_OVERRIDE_CUDA`` - CUDA version number or set to ``""`` for no CUDA
      detected.
    * ``CONDA_OVERRIDE_OSX`` - OSX version number or set to ``""`` for no OSX
      detected.
    * ``CONDA_OVERRIDE_GLIBC`` - GLIBC version number or set to ``""`` for no GLIBC.
      This only applies on Linux.
