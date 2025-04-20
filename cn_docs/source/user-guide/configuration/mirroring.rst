==================
镜像渠道
==================

Mirroring channels

.. tab:: 中文

    conda 配置系统有几个键可用于设置镜像上下文。

.. tab:: 英文

    The conda configuration system has several keys that can be used to set up a mirrored context.

默认设置
=================

The default setup

.. tab:: 中文

    默认情况下， ``conda`` 可以从两个主要位置提供软件包：
    
    - ``repo.anaconda.com``：这是 ``defaults`` 通道默认指向的位置。  
      自 conda 24.9.0 起，此默认值已被标记为即将弃用，  
      但在旧版本中仍为默认设置。该默认值将在 conda 25.3.0 中被移除。
    
      此基础位置被硬编码在 ``default_channels`` 的默认值中：
        - ``https://repo.anaconda.com/pkgs/main``
        - ``https://repo.anaconda.com/pkgs/r``
        - ``https://repo.anaconda.com/pkgs/msys2``
    - ``conda.anaconda.org``：conda 客户端会在此处查找社区通道，例如 ``conda-forge`` 或 ``bioconda``。  
      此基础地址可以通过 ``channel_alias`` 配置。
    
    因此，在镜像这些通道时，需要同时考虑这两个来源地址。

.. tab:: 英文

    By default, ``conda`` can serve packages from two main locations:

    - ``repo.anaconda.com``: this is where ``defaults`` points to by default.
      The default value has been marked for pending deprecation as of conda 24.9.0,
      but it is still the default for older versions. In conda 25.3.0, this default
      will be removed.

      This base location is hardcoded in the default value of ``default_channels``:
        - ``https://repo.anaconda.com/pkgs/main``
        - ``https://repo.anaconda.com/pkgs/r``
        - ``https://repo.anaconda.com/pkgs/msys2``
    - ``conda.anaconda.org``: this is where conda clients look up community channels like ``conda-forge`` or ``bioconda``.
      This base location can be configured via ``channel_alias``.

    So, when it comes to mirroring these channels, you have to account for those two locations.


镜像 ``defaults``
===================

Mirror ``defaults``

.. tab:: 中文

    使用 ``default_channels`` 覆盖 :doc:`默认配置 </configuration>` 。例如：

.. tab:: 英文

    Use ``default_channels`` to overwrite the :doc:`default configuration </configuration>`. For example:

.. code-block:: yaml

    default_channels:
        - https://my-mirror.com/pkgs/main
        - https://my-mirror.com/pkgs/r
        - https://my-mirror.com/pkgs/msys2


镜像所有社区频道
=============================

Mirror all community channels

.. tab:: 中文

    重新定义 ``channel_alias`` 以指向你的镜像。例如：

    .. code-block:: yaml

        channel_alias: https://my-mirror.com

    这将使 ``conda`` 查找 ``https://my-mirror.com/conda-forge`` 、 ``https://my-mirror.com/bioconda`` 等处的所有社区频道。

.. tab:: 英文

    Redefine ``channel_alias`` to point to your mirror. For example:

    .. code-block:: yaml

        channel_alias: https://my-mirror.com

    This will make ``conda`` look for all community channels at ``https://my-mirror.com/conda-forge``, ``https://my-mirror.com/bioconda``, etc.


仅镜像部分社区频道
===================================

Mirror only some community channels

.. tab:: 中文

    如果你只想镜像某些社区通道，必须使用 ``custom_channels``。  
    此设置优先于 ``channel_alias``。例如：

    .. code-block:: yaml

        custom_channels:
            conda-forge: https://my-mirror.com/conda-forge

    上述配置会使 conda 将 conda-forge 通道解析为 ``https://my-mirror.com/conda-forge``。  
    而其他所有社区通道仍将从 ``https://conda.anaconda.org`` 查找。

    .. note::

        欢迎参阅 :doc:`/configuration` 了解所有可用的配置选项。

.. tab:: 英文

    If you want to mirror only some community channels, you must use ``custom_channels``.
    This takes precedence over ``channel_alias``. For example:

    .. code-block:: yaml

        custom_channels:
            conda-forge: https://my-mirror.com/conda-forge

    With this configuration, conda-forge will be looked up at ``https://my-mirror.com/conda-forge``.
    All other community channels will be looked up at ``https://conda.anaconda.org``.


    .. note::

        Feel free to explore all the available options in :doc:`/configuration`.
