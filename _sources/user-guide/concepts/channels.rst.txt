========
频道
========

Channels

.. tab:: 中文

.. tab:: 英文

.. _concepts-channels:

什么是“频道”？
====================

What is a "channel"?

.. tab:: 中文

    “渠道（channel）”是软件包的存储位置，是托管和管理软件包的基础。Conda :doc:`软件包 <../concepts/packages>` 从远程渠道下载，这些渠道对应包含 conda 软件包的目录 URL。 ``conda`` 命令会搜索一组渠道。默认情况下，软件包将从默认渠道（ `default channel`_ ）自动下载和更新，该渠道可能需要付费许可，详见其 `软件仓库服务条款 <https://www.anaconda.com/terms-of-service>`_。

    而 ``conda-forge`` 渠道则是完全免费的。你可以自定义 conda 搜索的软件包渠道列表。这一特性在维护私有或内部渠道时非常有用。详细信息请参阅 :ref:`修改你的渠道列表 <config-channels>`。

.. tab:: 英文

    Channels are the locations where packages are stored.
    They serve as the base for hosting and managing packages.
    Conda :doc:`packages <../concepts/packages>` are downloaded
    from remote channels, which are URLs to directories
    containing conda packages.
    The ``conda`` command searches a set of channels. By default,
    packages are automatically downloaded and updated from
    the `default channel`_, which may require a
    paid license, as described in the `repository terms of service`_.
    The ``conda-forge`` channel is free for all to use.
    You can modify which remote channels are automatically searched;
    this feature is beneficial when maintaining a private or internal channel.
    For details, see how to :ref:`modify your channel lists <config-channels>`.
    
    We use conda-forge as an example channel.
    `Conda-forge <https://conda-forge.org/>`_ is a community channel
    made up of thousands of contributors. Conda-forge itself is
    analogous to PyPI but with a unified,
    automated build infrastructure and more peer review of
    recipes.

.. _`repository terms of service`: https://www.anaconda.com/terms-of-service

.. _specifying-channels:

安装软件包时指定频道
============================================

Specifying channels when installing packages

.. tab:: 中文

    我们以下以 conda-forge 为例说明：
    
    `Conda-forge <https://conda-forge.org/>`_ 是一个由数千名贡献者组成的社区渠道。它类似于 PyPI，但拥有统一的自动化构建体系以及更严格的配方审核流程。
    
    * 使用 `--channel` 从命令行指定渠道：
    
    .. code-block:: bash
    
       $ conda install scipy --channel conda-forge
    
    你可以通过多次传入该参数来指定多个渠道：
    
    .. code-block:: bash
    
       $ conda install scipy --channel conda-forge --channel bioconda
    
    优先级按从左到右递减 —— 第一个渠道的优先级高于第二个。
    
    * 使用 `--override-channels` 强制仅搜索指定的渠道，而忽略 ``.condarc`` 中的配置和默认渠道：
    
    .. code-block:: bash
    
       $ conda search scipy --channel file:/<path to>/local-channel --override-channels
    
    * 在 ``.condarc`` 文件中，可使用 ``channels`` 键指定 conda 搜索软件包时使用的渠道列表。
    
    参阅 :doc:`管理渠道 <../tasks/manage-channels>` 获取更多信息。

.. tab:: 英文

    * From the command line use `--channel`
    
    .. code-block:: bash
    
      $ conda install scipy --channel conda-forge
    
    You may specify multiple channels by passing the argument multiple times:
    
    .. code-block:: bash
    
      $ conda install scipy --channel conda-forge --channel bioconda
    
    Priority decreases from left to right - the first argument is higher priority than the second.
    
    * From the command line use `--override-channels` to only search the specified channel(s), rather than any channels configured in .condarc. This also ignores conda's default channels.
    
    .. code-block:: bash
    
      $ conda search scipy --channel file:/<path to>/local-channel --override-channels
    
    * In .condarc, use the key ``channels`` to see a list of channels for conda to search for packages.
    
    Learn more about :doc:`managing channels <../tasks/manage-channels>`.

.. _rss-feed:

Conda 克隆频道 RSS 订阅
============================

Conda clone channel RSS feed

.. tab:: 中文

    Conda 提供了一个 RSS 订阅源，用于展示通过渠道克隆的所有内容，以及当前 CDN（内容分发网络）中可用的内容。这个 RSS 源以滚动的两周为窗口，展示了渠道中发生的变更（如同步、添加或删除软件包），适合用来跟踪包的状态或确认是否已同步。
    
    以下是 `conda-forge 渠道的 RSS 订阅源 <https://conda-static.anaconda.org/conda-forge/rss.xml>`_ 示例。
    
    RSS 中每次同步操作都会显示一条记录。其他条目则显示被添加或移除的软件包。每条记录包含所属子目录、操作类型（添加或删除）、软件包名称，并附有标准 RSS 规范的发布时间戳。

.. tab:: 英文

    We offer a RSS feed that represents all the things
    that have been cloned by the channel clone and are
    now available behind the CDN (content delivery network).
    The RSS feed shows what has happened on a rolling,
    two-week time frame and is useful for seeing where
    packages are or if a sync has been run.

    Let's look at the `conda-forge channel RSS feed <https://conda-static.anaconda.org/conda-forge/rss.xml>`_
    as an example.

    In that feed, it will tell you every time that it runs a sync.
    The feed includes other entries for packages that were added or
    removed. Each entry is formatted to show the subdirectory
    the package is from, the action that was taken (addition or removal),
    and the name of the package. Everything has a publishing date,
    per standard RSS practice.

.. code-block:: xml

  <rss version="0.91">
    <channel>
      <title>conda-forge updates</title>
      <link>https://anaconda.org</link>
      <description>Updates in the last two weeks</description>
      <language>en</language>
      <copyright>Copyright 2019, Anaconda, Inc.</copyright>
      <pubDate>30 Jul 2019 19:45:47 UTC</pubDate>
        <item>
          <title>running sync</title>
          <pubDate>26 Jul 2019 19:26:36 UTC</pubDate>
        </item>
        <item>
          <title>linux-64:add:jupyterlab-1.0.4-py36_0.tar.bz2</title>
          <pubDate>26 Jul 2019 19:26:36 UTC</pubDate>
        </item>
        <item>
          <title>linux-64:add:jupyterlab-1.0.4-py37_0.tar.bz2</title>
          <pubDate>26 Jul 2019 19:26:36 UTC</pubDate>
        </item>

.. _`default channel`: https://repo.anaconda.com/pkgs/
