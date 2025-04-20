======================
使用免费通道
======================

Using the free channel

.. tab:: 中文
    
    ``free`` 通道包含了 2017 年 9 月 26 日之前创建的软件包。在 conda 4.7 之前，``free`` 通道是 ``defaults`` 通道的一部分。  
    详见 :ref:`defaults channel <default-channels>`。
    
    移除 ``free`` 通道可以减少 conda 的搜索范围，并隐藏旧软件。这些旧软件可能包含不兼容的依赖约束信息。  
    阅读更多内容请见：`我们为何在 conda 4.7 中移除了 free 通道 <https://www.anaconda.com/why-we-removed-the-free-channel-in-conda-4-7/>`_。
    
    如果你仍然需要 ``free`` 通道中的内容来重建旧环境，可以按照下方说明重新添加该通道。
    
    .. versionchanged:: 24.9.0
    
      ``restore_free_channel`` 选项已被标记为即将弃用，将在 conda 25.9.0 中移除。
    
      要达到相同效果，你可以通过常规 ``condarc`` 配置将 ``free`` 通道添加至  
      :ref:`defaults channel <default-channels>`。
    
      在类 UNIX 系统上：
    
      .. code-block:: yaml
    
         default_channels:
             - https://repo.anaconda.com/pkgs/main
             - https://repo.anaconda.com/pkgs/free
             - https://repo.anaconda.com/pkgs/r
    
      在 Windows 系统上：
    
      .. code-block:: yaml
    
         default_channels:
             - https://repo.anaconda.com/pkgs/main
             - https://repo.anaconda.com/pkgs/free
             - https://repo.anaconda.com/pkgs/r
             - https://repo.anaconda.com/pkgs/msys2
    
      注意：free 通道应列在 main 通道之后。

.. tab:: 英文

    The free channel contains packages created prior to
    September 26, 2017. Prior to conda 4.7, the free
    channel was part of the ``defaults`` channel.
    Read more about the :ref:`defaults channel <default-channels>`.
    
    Removing the ``free`` channel reduced conda's search space
    and hid old software. That old software could have incompatible
    constraint information. Read more about `why we made this change
    <https://www.anaconda.com/why-we-removed-the-free-channel-in-conda-4-7/>`_.
    
    
    If you still need the content from the ``free`` channel to reproduce
    old environments, you can re-add the channel following the directions below.
    
    .. versionchanged:: 24.9.0
    
      The ``restore_free_channel`` option has been marked for pending deprecation
      with removal in conda 25.9.0.
    
      To achieve the same effect, you may add the ``free`` channel to your
      the :ref:`defaults channel <default-channels>` using the regular ``condarc``
      configuration.
    
      On UNIX-style systems:
    
      .. code-block:: yaml
    
         default_channels:
             - https://repo.anaconda.com/pkgs/main
             - https://repo.anaconda.com/pkgs/free
             - https://repo.anaconda.com/pkgs/r
    
      On Windows:
    
      .. code-block:: yaml
    
         default_channels:
             - https://repo.anaconda.com/pkgs/main
             - https://repo.anaconda.com/pkgs/free
             - https://repo.anaconda.com/pkgs/r
             - https://repo.anaconda.com/pkgs/msys2
    
      Note that the free channel is listed after the main channel.

.. _free-channel-default:

将免费通道添加到默认设置
===================================

Adding the free channel to defaults

.. tab:: 中文

    如果你希望将 ``free`` 通道重新添加到默认通道列表中，可以运行以下命令：
    
    ::
    
       conda config --set restore_free_channel true
    
    通道的顺序很重要。使用上述命令可以确保按正确顺序恢复 ``free`` 通道。

.. tab:: 英文

    If you want to add the ``free`` channel back into your default list,
    use the command::
    
       conda config --set restore_free_channel true
    
    The order of the channels is important. Using the above
    command will restore the ``free`` channel in the correct order.

更改 .condarc
=================

Changing .condarc

.. tab:: 中文

    你也可以通过修改 ``.condarc`` 文件，手动将 ``free`` 通道添加回默认通道。
    
    在 ``.condarc`` 文件中的 conda 部分添加如下内容::
    
       restore_free_channel: true
    
    详见 :doc:`use-condarc`。

.. tab:: 英文

    You can also add the ``free`` channel back into your defaults by
    changing the ``.condarc`` file itself.
    
    Add the following to the conda section of your ``.condarc`` file::
    
       restore_free_channel: true
    
    Read more about :doc:`use-condarc`.

包名称变更
====================

Package name changes

.. tab:: 中文

    在 ``free`` 通道中提供的某些软件包在 ``main`` 通道中使用了不同的名称。
    
    .. list-table::
       :widths: 25 75
       :header-rows: 1
    
       * - ``free`` 中的软件包名
         - ``main`` 中的软件包名
       * - dateutil
         - python-dateutil
       * - gcc
         - gcc_linux-64 或类似名称
       * - pil
         - pillow
       * - ipython-notebook
         - 现可通过 notebook 安装；也可以创建元包
       * - Ipython-qtconsole
         - 现可通过 qtconsole 安装；也可以创建元包
       * - beautiful-soup
         - beautifulsoup4
       * - pydot-ng
         - pydot

.. tab:: 英文
    
    Some packages that are available in the ``free`` channel
    have different names in the ``main`` channel.
    
    .. list-table::
       :widths: 25 75
       :header-rows: 1
    
       * - Package name in ``free``
         - Package name in ``main``
       * - dateutil
         - python-dateutil
       * - gcc
         - gcc_linux-64 and similar
       * - pil
         - pillow
       * - ipython-notebook
         - now installable via notebook, a metapackage could be created
       * - Ipython-qtconsole
         - now installable via qtconsole, a metapackage could be created
       * - beautiful-soup
         - beautifulsoup4
       * - pydot-ng
         - pydot


故障排除
===============

Troubleshooting

.. tab:: 中文

    你可能会遇到一些错误，例如 UnsatisfiableError 或 PackagesNotFoundError。
    
    以下是一个示例：
    
    ::
    
       $ conda create -n test -c file:///Users/jsmith/anaconda/conda-bld bad_pkg
       Collecting package metadata: done
       Solving environment: failed
    
       UnsatisfiableError: The following specifications were found to be in conflict:
         - cryptography=2.6.1 -> openssl[version='>=1.1.1b,<1.1.2a']
         - python=3.7.0 -> openssl[version='>=1.0.2o,<1.0.3a']
       Use "conda search <package> --info" to see the dependencies for each package.
    
    此类错误可能出现于以下情况：
    
    - 你尝试安装的软件包仅存在于 ``free`` 通道，而不在 ``main`` 通道中。
    - 你希望重建的环境基于较旧的环境文件，其中引用了 ``free`` 通道中的包，但这些包无法找到。
    - 某些软件包依赖于 ``free`` 通道中才能找到的文件。如果这些依赖无法安装，conda 会阻止你安装该软件包。
    
    遇到这些错误时，可以考虑使用在 ``main`` 通道中可用的较新版本包。如果确实需要旧版本，可以  
    :ref:`将 free 通道添加回默认设置 <free-channel-default>`。

.. tab:: 英文

    You may encounter some errors, such as UnsatisfiableError
    or a PackagesNotFoundError.
    
    An example of this error is::
    
       $ conda create -n test -c file:///Users/jsmith/anaconda/conda-bld bad_pkg
       Collecting package metadata: done
       Solving environment: failed
    
       UnsatisfiableError: The following specifications were found to be in conflict:
         - cryptography=2.6.1 -> openssl[version='>=1.1.1b,<1.1.2a']
         - python=3.7.0 -> openssl[version='>=1.0.2o,<1.0.3a']
       Use "conda search <package> --info" to see the dependencies for each package.
    
    This can occur if:
    
    - you’re trying to install a package that is only available in
      ``free`` and not in ``main``.
    - you have older environments in files you want to recreate.
      If those spec files reference packages that are in ``free``,
      they will not show up.
    - a package is dependent upon files found only in the free
      channel. Conda will not let you install the package if it cannot
      install the dependency, which the package requires to work.
    
    If you encounter these errors, consider using a newer package than
    the one in ``free``. If you want those older versions, you can
    :ref:`add the free channel back into your defaults
    <free-channel-default>`.
