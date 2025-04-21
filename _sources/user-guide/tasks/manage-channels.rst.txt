=================
管理渠道
=================

Managing channels

.. tab:: 中文
    
    Conda 渠道（channels）是存放软件包的位置，它们是托管和管理 Conda 软件包的基础。  
    Conda 软件包会从远程渠道下载，这些远程渠道本质上是包含 Conda 包的目录的 URL。  
    `conda` 命令会搜索一组默认渠道，并自动从 `default channel`_ 下载和更新软件包。  
    关于 :doc:`conda 渠道 <../concepts/channels>` 及其使用条款的更多信息请参考相关文档。
    
    不同渠道可能包含同名的软件包，因此 Conda 必须处理所谓的 **渠道冲突** （channel collisions）。
    
    如果你只使用默认渠道（defaults），就不会发生渠道冲突。  
    如果你使用的所有渠道中的包互不重叠（即没有重复的包名），也不会有冲突。  
    当多个渠道列表中包含同名软件包时，Conda 的冲突解决机制才会生效。
    
    默认情况下，Conda 会 **优先选择高优先级渠道** 中的软件包，而不是低优先级渠道中的版本。  
    这意味着你可以安心地将非默认渠道放在渠道列表的后面，从中获取默认渠道中没有的额外软件包，  
    同时又不担心这些渠道会覆盖核心软件包。
    
    Conda 会从所有列出的渠道中收集同名软件包，并按以下顺序处理：
    
    #. 按照 **渠道优先级从高到低** 对包进行排序。
    #. 对于渠道优先级相同的包，按 **版本号从高到低** 排序。例如，如果 channelA 提供 NumPy 1.12.0 和 1.13.1，后者优先。
    #. 如果版本号也相同，则按 **构建号从高到低** 排序。例如，如果 channelA 提供 NumPy 1.12.0 build 1 和 build 2，则 build 2 优先。channelB 的所有 NumPy 包将排在 channelA 的之后。
    #. 安装排序列表中第一个满足安装条件的包。
    
    简而言之，排序优先级如下：
    
    ``channelA::numpy-1.13_1 > channelA::numpy-1.12.1_1 > channelA::numpy-1.12.1_0 > channelB::numpy-1.13_1``
    
    .. note::
       如果开启了 strict 模式的渠道优先级，则不会考虑 channelB::numpy-1.13_1。
    
    若希望 Conda 安装所列渠道中**最新版本**的软件包：
    
    - 可将以下内容添加至你的 ``.condarc`` 文件：
    
      ``channel_priority: disabled``
    
    - 或运行以下等效命令::
    
        conda config --set channel_priority disabled
    
    此时 Conda 的排序机制如下：
    
    #. 按 **版本号从高到低** 排序。
    #. 对版本相同的包，按 **渠道优先级从高到低** 排序。
    #. 若渠道优先级和版本都相同，按 **构建号从高到低** 排序。
    
    注意：不同渠道间的构建号不可比较，因此构建号始终排在渠道优先级之后。
    
    以下命令会将 ``new_channel`` 添加到渠道列表顶部，使其成为最高优先级渠道::
    
      conda config --add channels new_channel
    
    等效命令是::
    
      conda config --prepend channels new_channel
    
    而如果你想将其添加到列表底部（最低优先级），可使用::
    
      conda config --append channels new_channel

.. tab:: 英文
    
    Conda channels are the locations where packages are stored.
    They serve as the base for hosting and managing packages.
    Conda packages are downloaded from remote channels, which are URLs to
    directories containing conda packages. The conda command searches a default
    set of channels and packages are automatically downloaded and updated
    from the `default channel`_. Read more about
    :doc:`conda channels <../concepts/channels>` and the various terms of service
    for their use.
    
    Different channels can have the same package, so conda must handle these
    channel collisions.
    
    There will be no channel collisions if you use only the defaults channel.
    There will also be no channel collisions if all of the channels you use only
    contain packages that do not exist in any of the other channels in your list.
    The way conda resolves these collisions matters only when you have multiple
    channels in your channel list that host the same package.
    
    By default, conda prefers packages from a higher priority
    channel over any version from a lower priority channel.
    Therefore, you can now safely put channels at the bottom of your
    channel list to provide additional packages that are not in the
    default channels and still be confident that these channels will
    not override the core package set.
    
    Conda collects all of the packages with the same name across all
    listed channels and processes them as follows:
    
    #. Sorts packages from highest to lowest channel priority.
    
    #. Sorts tied packages---packages with the same channel priority---from highest to
       lowest version number. For example, if channelA contains NumPy 1.12.0
       and 1.13.1, NumPy 1.13.1 will be sorted higher.
    
    #. Sorts still-tied packages---packages with the same channel priority and same
       version---from highest to lowest build number. For example, if channelA contains
       both NumPy 1.12.0 build 1 and build 2, build 2 is sorted first. Any packages
       in channelB would be sorted below those in channelA.
    
    #. Installs the first package on the sorted list that satisfies
       the installation specifications.
    
    Essentially, the order goes:
    channelA::numpy-1.13_1 > channelA::numpy-1.12.1_1 > channelA::numpy-1.12.1_0 > channelB::numpy-1.13_1
    
    .. note::
       If strict channel priority is turned on then channelB::numpy-1.13_1 isn't
       included in the list at all.
    
    
    To make conda install the newest version
    of a package in any listed channel:
    
    * Add ``channel_priority: disabled`` to your ``.condarc`` file.
    
      OR
    
    * Run the equivalent command::
    
        conda config --set channel_priority disabled
    
    Conda then sorts as follows:
    
    #. Sorts the package list from highest to lowest version number.
    
    #. Sorts tied packages from highest to lowest channel priority.
    
    #. Sorts tied packages from highest to lowest build number.
    
    Because build numbers from different channels are not
    comparable, build number still comes after channel priority.
    
    The following command adds the channel "new_channel" to the top
    of the channel list, making it the highest priority::
    
      conda config --add channels new_channel
    
    Conda has an equivalent command::
    
      conda config --prepend channels new_channel
    
    Conda also has a command that adds the new channel to the
    bottom of the channel list, making it the lowest priority::
    
      conda config --append channels new_channel

.. _strict:

严格的渠道优先级
=======================

Strict channel priority

.. tab:: 中文

  从 Conda 4.6.0 起，Conda 引入了 **严格渠道优先级（strict channel priority）** 功能。  
  该功能可以显著加快 Conda 的操作速度，并减少软件包不兼容问题。我们建议在可能情况下启用 strict 模式。

  你可以运行以下命令查看相关说明：

  ``conda config --describe channel_priority``

  输出内容如下：

  .. code-block:: none

      channel_priority (ChannelPriority)
      可选值：'strict'、'flexible' 和 'disabled'。默认值为 'flexible'。
      
      - 若设置为 'strict'，则当某包在高优先级渠道中出现时，低优先级渠道中的该包将被完全忽略。
      
      - 若设置为 'flexible'，则解析器可访问低优先级渠道以满足依赖关系，而不是直接报错。
      
      - 若设置为 'disabled'，则以软件包版本优先，渠道优先级仅用于打破平分。
      
      旧版本 Conda 中，该参数为布尔值（True / False），现在 True 相当于 'flexible'。

      channel_priority: flexible

.. tab:: 英文

    As of version 4.6.0, Conda has a strict channel priority feature.
    Strict channel priority can dramatically speed up conda operations and
    also reduce package incompatibility problems. We recommend setting channel
    priority to "strict" when possible.

    Details about it can be seen by typing ``conda config --describe channel_priority``.

    .. code-block:: none

        channel_priority (ChannelPriority)
        Accepts values of 'strict', 'flexible', and 'disabled'. The default
        value is 'flexible'. With strict channel priority, packages in lower
        priority channels are not considered if a package with the same name
        appears in a higher priority channel. With flexible channel priority,
        the solver may reach into lower priority channels to fulfill
        dependencies, rather than raising an unsatisfiable error. With channel
        priority disabled, package version takes precedence, and the
        configured priority of channels is used only to break ties. In
        previous versions of conda, this parameter was configured as either
        True or False. True is now an alias to 'flexible'.

        channel_priority: flexible

.. _`default channel`: https://repo.anaconda.com/pkgs/
