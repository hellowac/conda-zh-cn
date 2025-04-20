========
设置
========

Settings

.. tab:: 中文

  本页概述了 conda 中许多重要的设置，并尽可能提供了示例。

.. tab:: 英文

  This page contains an overview of many important settings available in conda with examples where possible.

常规配置
=====================

General configuration

.. _config-channels:

``channels``: 渠道位置
-------------------------------

``channels``: Channel locations

.. tab:: 中文

    在 ``.condarc`` 文件中列出 channel 位置将覆盖 conda 的默认设置，  
    使 conda 只按指定顺序搜索这些列出的频道。
    
    使用 ``defaults`` 可以自动包含所有默认频道。  
    非 URL 类型的频道将被解释为 Anaconda.org 的用户名或组织名。  
    你可以通过修改 ``channel_alias``（详见 :ref:`set-ch-alias`）来更改这一行为。默认值为 ``defaults``。
    
    **示例：**
    
    .. code-block:: yaml
    
      channels:
        - <anaconda_dot_org_username>
        - http://some.custom/channel
        - file:///some/local/directory
        - defaults
    
    如需为单个环境选择频道，可以在该环境根目录下放置一个 ``.condarc`` 文件，  
    或者在使用 ``conda config`` 时使用 ``--env`` 选项。
    
    **示例：** 若你在主目录下使用 Python 3 安装了 Miniconda，  
    且环境名称为 "flowers"，其路径可能为：
    
    .. code-block::
    
      ~/miniconda3/envs/flowers/.condarc

.. tab:: 英文

    Listing channel locations in the ``.condarc`` file overrides
    conda defaults, causing conda to search only the channels listed there
    in the order given.
    
    Use ``defaults`` to automatically include all default channels.
    Non-URL channels are interpreted as Anaconda.org user or organization
    names. You can change this by modifying the ``channel_alias`` as described
    in :ref:`set-ch-alias`. The default is just ``defaults``.
    
    **Example:**
    
    .. code-block:: yaml
    
      channels:
        - <anaconda_dot_org_username>
        - http://some.custom/channel
        - file:///some/local/directory
        - defaults
    
    To select channels for a single environment, put a ``.condarc``
    file in the root directory of that environment (or use the
    ``--env`` option when using ``conda config``).
    
    **Example:** If you have installed Miniconda with Python 3 in your
    home directory and the environment is named "flowers", the
    path may be::
    
      ~/miniconda3/envs/flowers/.condarc

.. _default-channels:

``default_channels``：默认频道
--------------------------------------

``default_channels``: Default channels

.. tab:: 中文

    通常， ``defaults`` channel 会指向  
    `repo.anaconda.com <https://repo.anaconda.com/>`_ 上的若干频道，  
    但如果定义了 ``default_channels``，则会设置一组新的默认频道。  
    这对于隔离网络（airgapped）或企业内部部署尤为有用。
    
    为确保所有用户仅从本地仓库获取软件包，管理员可以同时设置  
    :ref:`channel alias <channel-alias>` 和 ``default_channels``：
    
    .. code-block:: yaml
    
      default_channels:
        - http://some.custom/channel
        - file:///some/local/directory

.. tab:: 英文

    Normally, the defaults channel points to several channels at the
    `repo.anaconda.com <https://repo.anaconda.com/>`_ repository, but if
    ``default_channels`` is defined, it sets the new list of default channels.
    This is especially useful for airgapped and enterprise installations.
    
    To ensure that all users only pull packages from an on-premises
    repository, an administrator can set both :ref:`channel alias <channel-alias>` and
    ``default_channels``.
    
    .. code-block:: yaml
    
      default_channels:
        - http://some.custom/channel
        - file:///some/local/directory

.. _auto-update-conda:


.. _channel-settings:

``channel_settings``：单个频道的额外设置
------------------------------------------------------------

``channel_settings``: Extra settings for individual channels

.. versionadded:: 23.3.0

.. tab:: 中文
    
    通过 ``channel_settings``，你可以为每个频道设置额外的配置选项。  
    目前主要用于通过 :doc:`/dev-guide/plugins/auth_handlers` 插件钩子  
    注册额外的认证处理器，但将来也可能支持更多用途。
    
    以下是一个示例，假设已经通过上述插件钩子注册了一个名为  
    "test-auth-handler" 的认证处理器：
    
    .. code-block:: yaml
    
      channel_settings:
         - channel: https://some.custom/channel
           auth: test-auth-handler
           user: my-user-account
         - channel: https://some.base-url-prefix/*
           auth: another-auth-handler
    
    .. note::
    
       ``channel_settings`` 中的每一项必须定义 ``channel`` 属性，  
       以便配置知道这些设置对应的是哪个频道。  
       ``channel`` 属性可以使用类似 glob 的 URL 模式进行匹配。  
       注意：此处必须精确匹配 HTTP 模式（schema），例如 ``*`` 并不是合法的模式。

.. tab:: 英文

    With ``channel_settings``, it is possible to add extra configuration options
    for individual channels. This is currently used to register additional authentication
    handlers for conda via the :doc:`/dev-guide/plugins/auth_handlers` plugin hook, but may also
    accommodate more use cases in the future.
    
    Here is an example of how it may be defined provided there was an available authentication
    handler called, "test-auth-handler" registered via the aforementioned plugin hook:
    
    .. code-block:: yaml
    
      channel_settings:
         - channel: https://some.custom/channel
           auth: test-auth-handler
           user: my-user-account
         - channel: https://some.base-url-prefix/*
           auth: another-auth-handler
    
    .. note::
    
       Each entry in ``channel_settings`` needs to define the ``channel`` attribute so that
       the configuration knows which channel these settings are associated with. The ``channel``
       attribute may specify a glob-like URL pattern for matching. Note that in this case, the HTTP
       schema must match exactly to the channel URL, so a pattern like ``*`` is not valid.


``allowlist_channels`` 和 ``denylist_channels``：允许或拒绝特定频道
---------------------------------------------------------------------------------

``allowlist_channels`` and ``denylist_channels``: Allow or deny specific channels

.. tab:: 中文

    .. versionadded:: 24.9.0
    
      ``denylist_channels`` 设置在 conda 24.9.0 中引入，作为对现有 ``allowlist_channels`` 的补充。
    
    使用 ``allowlist_channels`` 和 ``denylist_channels``，你可以允许或禁止特定频道参与 conda 操作。  
    这在企业或多用户环境中限制 conda 访问特定渠道时尤其有用。
    
    denylist 的优先级高于 allowlist。若某频道同时出现在两个列表中，将被拒绝访问。
    
    **示例：**
    
    以下示例使用 ``allowlist_channels`` 仅允许 ``defaults`` 和 ``conda-forge``：
    
    .. code-block:: yaml
    
      allowlist_channels:
        - defaults
        - conda-forge
    
    以下示例使用 ``denylist_channels`` 拒绝 ``conda-forge``：
    
    .. code-block:: yaml
    
      denylist_channels:
        - conda-forge
    
    以下示例同时使用 ``allowlist_channels`` 和 ``denylist_channels``，  
    显式允许 ``defaults``，但拒绝 ``conda-forge``：
    
    .. code-block:: yaml
    
      allowlist_channels:
        - defaults
      denylist_channels:
        - conda-forge
    
    以下示例展示了 conda 会根据频道的基本 URL 自动进行归一化，  
    因此你可以使用完整的 URL 或其基础形式：
    
    .. code-block:: yaml
    
      allowlist_channels:
        - defaults
      denylist_channels:
        - https://conda.anaconda.org/conda-forge/linux-64
    
    以下示例拒绝使用 ``defaults``（其对应 :ref:`default_channels <default-channels>` 设置项）：
    
    .. code-block:: yaml
    
      denylist_channels:
        - defaults
    
    .. note::
    
      :ref:`defaults channel <default-channels>` 默认指向  
      `repo.anaconda.com <https://repo.anaconda.com/>`_ 仓库上的若干频道。
    
    以下示例显式拒绝托管在 ``repo.anaconda.com`` 上的频道：
    
    .. code-block:: yaml
    
      denylist_channels:
        - https://repo.anaconda.com/pkgs/main
        - https://repo.anaconda.com/pkgs/r
        - https://repo.anaconda.com/pkgs/msys2

.. tab:: 英文

    .. versionadded:: 24.9.0
    
      The ``denylist_channels`` setting was introduced in conda 24.9.0 complementing the
      existing ``allowlist_channels`` setting.
    
    With ``allowlist_channels`` and ``denylist_channels``, you can allow or deny specific channels
    from being used in conda operations. This is useful for restricting the channels that conda
    can access, especially in enterprise or multi-user environments.
    
    The denylist takes precedence over the allowlist. If a channel is in both lists, it is denied.
    
    **Examples:**
    
    An example which allows the ``defaults`` and ``conda-forge`` channels with the ``allowlist_channels``
    setting is:
    
    .. code-block:: yaml
    
      allowlist_channels:
        - defaults
        - conda-forge
    
    An example which denies the ``conda-forge`` channel with the ``denylist_channels`` setting is:
    
    .. code-block:: yaml
    
      denylist_channels:
        - conda-forge
    
    An example which explicitly allows the ``defaults`` channel but denies the ``conda-forge`` channel
    by using both the ``allowlist_channels`` and ``denylist_channels`` settings is:
    
    .. code-block:: yaml
    
      allowlist_channels:
        - defaults
      denylist_channels:
        - conda-forge
    
    An example to show that channels are automatically normalized based on their base URLs,
    so you can use either the full channel URL or just the base URL:
    
    .. code-block:: yaml
    
      allowlist_channels:
        - defaults
      denylist_channels:
        - https://conda.anaconda.org/conda-forge/linux-64
    
    An example that denies using ``defaults`` (which maps to the :ref:`default_channels <default-channels>`)
    configuration option:
    
    .. code-block:: yaml
    
      denylist_channels:
        - defaults
    
    .. note::
    
      The :ref:`defaults channel <default-channels>` points to a list of channels at the
      `repo.anaconda.com <https://repo.anaconda.com/>`_ repository by default.
    
    An example to explicitly deny the channels that are hosted on ``repo.anaconda.com``:
    
    .. code-block:: yaml
    
      denylist_channels:
        - https://repo.anaconda.com/pkgs/main
        - https://repo.anaconda.com/pkgs/r
        - https://repo.anaconda.com/pkgs/msys2


``auto_update_conda``：自动更新 conda
-------------------------------------------------

``auto_update_conda``: Update conda automatically

.. tab:: 中文

    当值为 ``True`` 时，conda 会在用户在根环境中更新或安装包时自动更新。当值为 ``False`` 时，conda 仅在用户手动执行 ``conda update`` 命令时自动更新。默认值为 ``True``。

.. tab:: 英文

    When ``True``, conda updates itself any time a user updates or installs a package in the root environment. When ``False``, conda updates itself only if the user manually issues a ``conda update`` command. The default is ``True``.

**Example:**

.. code-block:: yaml

  auto_update_conda: False

.. _always-yes:

``always_yes``：始终启用
--------------------------

``always_yes``: Always yes

.. tab:: 中文

    每当系统提示继续时（例如安装时），请选择 ``yes`` 选项。与在命令行中使用 ``--yes`` 标志相同。默认值为 ``False``。

.. tab:: 英文

    Choose the ``yes`` option whenever asked to proceed, such as when installing. Same as using the ``--yes`` flag at the command line. The default is ``False``.

**Example:**

.. code-block:: yaml

  always_yes: True

.. _show-channel-urls:

``show_channel_urls``：显示频道 URL
----------------------------------------

``show_channel_urls``: Show channel URLs

.. tab:: 中文

    在“conda list”中以及显示要下载的内容时显示渠道 URL。默认值为“False”。

.. tab:: 英文

    Show channel URLs in ``conda list`` and when displaying what is going to be downloaded. The default is ``False``.

**Example:**

.. code-block:: yaml

  show_channel_urls: True

.. _change-command-prompt:

``changeps1``：更改命令提示符
------------------------------------

``changeps1``: Change command prompt

.. tab:: 中文

    使用“conda activate”时，将命令提示符从“$PS1”更改为包含已激活的环境。默认值为“True”。

.. tab:: 英文

    When using ``conda activate``, change the command prompt from ``$PS1`` to include the activated environment. The default is ``True``.

**Example:**

.. code-block:: yaml

  changeps1: False

.. _add-pip-python-dependency:

``add_pip_as_python_dependency``：添加 pip 作为 Python 依赖项
--------------------------------------------------------------

``add_pip_as_python_dependency``: Add pip as Python dependency

.. tab:: 中文

    将 pip、wheel 和 setuptools 添加为 Python 的依赖项。这可确保每次安装 Python 时都会安装 pip、wheel 和 setuptools。默认值为“True”。

.. tab:: 英文

    Add pip, wheel, and setuptools as dependencies of Python. This ensures that pip, wheel, and setuptools are always installed any time Python is installed. The default is ``True``.

**Example:**

.. code-block:: yaml

  add_pip_as_python_dependency: False

.. _use-pip:

``use_pip``：使用 pip
--------------------

``use_pip``: Use pip

.. tab:: 中文

    使用“conda list”列出软件包时，请使用 pip。这不会影响除“conda list”命令输出之外的任何 conda 命令或功能。默认值为“True”。

.. tab:: 英文

    Use pip when listing packages with ``conda list``. This does not affect any conda command or functionality other than the output of the command ``conda list``. The default is ``True``.

**Example:**

.. code-block:: yaml

  use_pip: False

.. _config-proxy:

``proxy_servers``：配置 conda 以在代理服务器后使用
----------------------------------------------------------------

``proxy_servers``: Configure conda for use behind a proxy server

.. tab:: 中文

    默认情况下，代理设置将从环境变量 `HTTP_PROXY` 和 `HTTPS_PROXY` 或系统设置中获取。  
    在此处设置会覆盖默认行为：
    
    .. code-block:: yaml
    
      proxy_servers:
          http: http://user:pass@corp.com:8080
          https: http://user:pass@corp.com:8080
    
    .. admonition:: 混用 HTTPS 与 HTTP
    
      URL 中的协议（即 ``http://`` 或 ``https://``）应与代理服务器的实际协议匹配。  
      上述示例中的键 ``http`` 与 ``https`` 仅表示要路由的流量类型，而非代理服务器本身使用的协议。  
      请确保根据代理服务器的配置为两个键使用正确的协议。
    
    若要为特定的 scheme 与主机配置代理，请使用 ``scheme://hostname`` 形式作为键。  
    该键会匹配所有请求中与给定 scheme 和完整主机名完全一致的情况：
    
    .. code-block:: yaml
    
      proxy_servers:
        'http://10.20.1.128': 'http://10.10.1.10:5323'
    
    如果你未提供用户名与密码，或认证失败，conda 会提示输入用户名和密码。
    
    如果你的密码中包含特殊字符，需要进行转义，方法详见 Wikipedia 上的  
    `百分号编码（Percent-encoding）保留字符说明 <https://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters>`_。
    
    请注意不要将 ``http`` 错误地用于 ``https``，或将 ``https`` 错误地用于 ``http``。

.. tab:: 英文

    By default, proxy settings are pulled from the HTTP_PROXY and HTTPS_PROXY environment variables or the system. Setting them here overrides that default:
    
    .. code-block:: yaml
    
      proxy_servers:
          http: http://user:pass@corp.com:8080
          https: http://user:pass@corp.com:8080
    
    .. admonition:: Mixing HTTPS and HTTP
    
      The protocol in the URL (either ``http://`` or ``https://``) should match
      the actual protocol of your proxy server. The keys ``http`` and ``https`` in
      the above example merely indicate the type of traffic to route, not the
      protocol of the proxy server itself. Ensure that both keys use the correct
      protocol based on your proxy server's configuration.
    
    To give a proxy for a specific scheme and host, use the
    ``scheme://hostname`` form for the key. This matches for any request
    to the given scheme and exact host name:
    
    .. code-block:: yaml
    
      proxy_servers:
        'http://10.20.1.128': 'http://10.10.1.10:5323'
    
    If you do not include the username and password or if
    authentication fails, conda prompts for a username and password.
    
    If your password contains special characters, you need to escape
    them as described in `Percent-encoding reserved characters
    <https://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters>`_
    on Wikipedia.
    
    Be careful not to use ``http`` when you mean ``https`` or
    ``https`` when you mean ``http``.


.. _SSL_verification:

``ssl_verify``：SSL 验证
--------------------------------

``ssl_verify``: SSL verification

.. tab:: 中文

    如果你处在进行 SSL 检查的代理之后，例如 Cisco IronPort Web Security Appliance (WSA)，可能需要通过 ``ssl_verify`` 覆盖默认的 SSL 验证设置。
    
    默认情况下，该变量为 ``True``，这意味着启用 SSL 验证，conda 会验证 SSL 连接的证书。  
    将该变量设置为 ``False`` 会禁用连接的正常安全验证，这种做法**不推荐**：
    
    .. code-block:: yaml
    
      ssl_verify: False
    
    .. versionadded:: 23.9.0  
       ``ssl_verify: truststore`` 设置仅在 conda 23.9.0 或更高版本中可用，且要求使用 Python 3.10 或更高版本。
    
    如果证书颁发机构已被操作系统信任（例如由系统管理员安装），  
    你可以将 ``ssl_verify`` 设置为 ``truststore``，以使用操作系统的证书存储：
    
    .. code-block:: yaml
    
      ssl_verify: truststore
    
    你还可以将 ``ssl_verify`` 设置为某个证书路径的字符串，  
    该证书将用于验证 SSL 连接：
    
    .. code-block:: yaml
    
      ssl_verify: corp.crt

.. tab:: 英文

    If you are behind a proxy that does SSL inspection, such as a
    Cisco IronPort Web Security Appliance (WSA), you may need to use
    ``ssl_verify`` to override the SSL verification settings.
    
    By default, this variable is ``True``, which means that SSL
    verification is used and conda verifies certificates for SSL
    connections. Setting this variable to ``False`` disables the
    connection's normal security and is not recommended:
    
    .. code-block:: yaml
    
      ssl_verify: False
    
    .. versionadded:: 23.9.0
       The ``ssl_verify: truststore`` setting is only available with conda 23.9.0 or later and using Python 3.10 or later.
    
    If the certificate authority is already trusted by the operating
    system, for instance because it was installed by a system
    administrator, you can tell conda to use the operating system
    certificate store by setting ``ssl_verify`` to "truststore":
    
    .. code-block:: yaml
    
      ssl_verify: truststore
    
    You can also set ``ssl_verify`` to a string path to a certificate,
    which can be used to verify SSL connections:
    
    .. code-block:: yaml
    
      ssl_verify: corp.crt

.. _offline-mode-only:

``offline``：仅限离线模式
------------------------------

``offline``: Offline mode only

.. tab:: 中文

    过滤所有不使用 ``file://`` 协议的频道 URL。默认值为 ``False``。

.. tab:: 英文

    Filters out all channel URLs that do not use the ``file://`` protocol. The default is ``False``.

**Example:**

.. code-block:: yaml

  offline: True

高级配置
======================

Advanced configuration

.. tab:: 中文

.. tab:: 英文

.. _disallow-soft-linking:

``allow_softlinks``：禁止软链接
------------------------------------------

``allow_softlinks``: Disallow soft-linking

.. tab:: 中文

    当 ``allow_softlinks`` 为 ``True`` 时，conda 会在可能的情况下使用硬链接，而在无法使用硬链接时（例如，在与包缓存所在文件系统不同的文件系统上安装时）使用软链接（符号链接）。

    当 ``allow_softlinks`` 为 ``False`` 时，conda 仍会在可能的情况下使用硬链接，但如果无法使用硬链接，conda 会复制文件。各个包可以覆盖此选项，指定某些文件永远不应使用软链接。

    默认值为 ``True``.

.. tab:: 英文

    When ``allow_softlinks`` is ``True``, conda uses hard links when possible and soft links (symlinks) when hard links are not possible, such as when installing on a different file system than the one that the package cache is on.

    When ``allow_softlinks`` is ``False``, conda still uses hard links when possible, but when it is not possible, conda copies files. Individual packages can override this option, specifying that certain files should never be soft linked.

    The default is ``True``.

**Example:**

.. code-block:: yaml

  allow_softlinks: False

.. _set-ch-alias:

.. _channel-alias:

``channel_alias``：设置频道别名
--------------------------------------

``channel_alias``: Set a channel alias

.. tab:: 中文

    每当你使用 ``-c`` 或 ``--channel`` 标志向 conda 指定一个 **不是 URL 的** 频道名称时，conda 会将 ``channel_alias`` 添加到该名称前。默认的 ``channel_alias`` 是：
    
    ``https://conda.anaconda.org``
    
    如果你将 ``channel_alias`` 设置为 ``https://my.anaconda.repo:8080/conda/``，那么当用户运行以下命令：
    
    ``conda install -c conda-forge some-package``
    
    实际上会从 ``https://my.anaconda.repo:8080/conda/conda-forge`` 安装名为 `some-package` 的软件包。
    
    例如，以下命令::
    
      conda install --channel asmeurer <package>
    
    等价于::
    
      conda install --channel https://conda.anaconda.org/asmeurer <package>
    
    你可以将 ``channel_alias`` 设置为你自己的软件包仓库。
    
    **示例：**如果你的仓库位于 https://your.repo.com，可以这样设置：
    
    .. code-block:: yaml
    
      channel_alias: https://your.repo/
    
    在 Windows 上，URL **必须**以斜杠（"/"）结尾：
    
    **示例：** ``https://your.repo/conda/``
    
    当 ``channel_alias`` 设置为 ``https://your.repo.com`` 时，以下命令::
    
      conda install --channel jsmith <package>
    
    等价于::
    
      conda install --channel https://your.repo.com/jsmith <package>

.. tab:: 英文

    Whenever you use the ``-c`` or ``--channel`` flag to give conda a
    channel name that is not a URL, conda prepends the ``channel_alias``
    to the name that it was given. The default ``channel_alias`` is
    https://conda.anaconda.org.
    
    If ``channel_alias`` is set
    to ``https://my.anaconda.repo:8080/conda/``, then a user who runs the
    command ``conda install -c conda-forge some-package`` will install the
    package some-package from ``https://my.anaconda.repo:8080/conda/conda-forge``.
    
    For example, the command::
    
      conda install --channel asmeurer <package>
    
    is the same as::
    
      conda install --channel https://conda.anaconda.org/asmeurer <package>
    
    You can set ``channel_alias`` to your own repository.
    
    **Example:** To set ``channel_alias`` to your repository at
    https://your.repo.com:
    
    .. code-block:: yaml
    
      channel_alias: https://your.repo/
    
    On Windows, you must include a slash ("/") at the end of the URL:
    
    **Example:** https://your.repo/conda/
    
    When ``channel_alias`` set to your repository at
    https://your.repo.com::
    
      conda install --channel jsmith <package>
    
    is the same as::
    
      conda install --channel https://your.repo.com/jsmith <package>

.. _config-add-default-pkgs:

``create_default_packages``：始终默认添加软件包
-----------------------------------------------------------

``create_default_packages``: Always add packages by default

.. tab:: 中文

    创建新环境时，默认添加指定的软件包。默认软件包会安装在您创建的每个环境中。您可以在命令提示符下使用“--no-default-packages”标志覆盖此选项。默认设置是不包含任何软件包。

.. tab:: 英文

    When creating new environments, add the specified packages by default. The default packages are installed in every environment you create. You can override this option at the command prompt with the ``--no-default-packages`` flag. The default is to not include any packages.

**Example:**

.. code-block:: yaml

  create_default_packages:
    - pip
    - ipython
    - scipy=0.15.0

.. _track-features:

``track_features``：跟踪功能
----------------------------------

``track_features``: Track features

.. tab:: 中文

    启用默认跟踪某些功能。默认不跟踪任何功能。这类似于将 MKL 添加到“create_default_packages”列表中。

.. tab:: 英文

    Enable certain features to be tracked by default. The default is to not track any features. This is similar to adding MKL to the ``create_default_packages`` list.

**Example:**

.. code-block:: yaml

  track_features:
    - mkl

.. _disable-updating:

``update_dependencies``：禁用依赖项更新
---------------------------------------------------------

``update_dependencies``: Disable updating of dependencies

.. tab:: 中文

    默认情况下，``conda install`` 会将指定的软件包更新到最新版本，并安装该软件包所需的所有依赖项。然而，如果当前环境中已经安装了满足该软件包依赖要求的依赖项，conda **不会**将这些依赖更新到最新版本。
    
    如果你希望 conda **将所有依赖项也更新为与当前环境兼容的最新版本**，可以将 ``update_dependencies`` 设置为 ``True``。
    
    该选项默认值为 ``False``。
    
    **示例：**
    
    .. code-block:: yaml
    
       update_dependencies: True
    
    .. note::
    
       conda 仍会确保满足所有依赖规范。因此，在某些情况下，某些依赖项仍然会被更新；而在另一些情况下，这可能反而会阻止你在命令行中指定的包被更新到最新版本。你始终可以在命令行中通过显式指定版本号来强制 conda 安装某个版本，例如：
    
       ``conda install numpy=1.9.3``
    
    如果你只是希望 **避免更新某些特定软件包** ，更好的做法可能是“锁定”这些包的版本。参见 :ref:`pinning-packages` 获取更多信息。

.. tab:: 英文

    By default, ``conda install`` updates the given package to the latest version and installs any dependencies necessary for that package. However, if dependencies that satisfy the package's requirements are already installed, conda will not update those packages to the latest version.
    
    In this case, if you would prefer that conda update all dependencies to the latest version that is compatible with the environment, set ``update_dependencies`` to ``True``.
    
    The default is ``False``.
    
    **Example:**
    
    .. code-block:: yaml
    
       update_dependencies: True
    
    .. note::
    
       Conda still ensures that dependency specifications are
       satisfied. Thus, some dependencies may still be updated or,
       conversely, this may prevent packages given at the command line
       from being updated to their latest versions. You can always
       specify versions at the command line to force conda to install a
       given version, such as ``conda install numpy=1.9.3``.
    
    To avoid updating only specific packages in an environment, a
    better option may be to pin them. For more information, see
    :ref:`pinning-packages`.

.. _disallow-install:

``disallow``：禁止安装特定软件包
--------------------------------------------------------

``disallow``: Disallow installation of specific packages

.. tab:: 中文

    禁止安装某些软件包。默认允许安装所有软件包。

.. tab:: 英文

    Disallow the installation of certain packages. The default is to allow installation of all packages.

**Example:**

.. code-block:: yaml

  disallow:
    - anaconda

.. _add-anaconda-token:

``add_anaconda_token``：添加 Anaconda.org 令牌以自动查看私有软件包
------------------------------------------------------------------------------------

``add_anaconda_token``: Add Anaconda.org token to automatically see private packages

.. tab:: 中文

    当频道别名为 Anaconda.org 或 Anaconda 服务器 GUI 时，您可以设置系统配置，以便用户自动查看私有软件包。Anaconda.org 以前称为 binstar.org。这将使用 Anaconda 命令行客户端（您可以使用“conda install anaconda-client”安装）自动将令牌添加到频道 URL。

    默认值为“True”。

    **Example:**
    
    .. code-block:: yaml
    
      add_anaconda_token: False

    .. note::

        即使设置为“True”，也只有在安装了 Anaconda 命令行客户端并使用“anaconda login”命令登录后才会启用此设置。

.. tab:: 英文

    When the channel alias is Anaconda.org or an Anaconda Server GUI, you can set the system configuration so that users automatically see private packages. Anaconda.org was formerly known as binstar.org. This uses the Anaconda command-line client, which you can install with ``conda install anaconda-client``, to automatically add the token to the channel URLs.

    The default is ``True``.

    **Example:**
    
    .. code-block:: yaml
    
      add_anaconda_token: False

    .. note::

        Even when set to ``True``, this setting is enabled only if
        the Anaconda command-line client is installed and you are
        logged in with the ``anaconda login`` command.

.. _specify-env-directories:

``envs_dirs``：指定环境目录
----------------------------------------------

``envs_dirs``: Specify environment directories

.. tab:: 中文

    指定环境所在的目录。如果设置了此键，则根目录的 ``envs_dir`` 将不会使用，除非显式包含。此键还决定了软件包缓存的存储位置。

    对于 ``envs_dirs`` 中的每个环境，``envs/pkgs`` 被用作软件包缓存，除了根目录中的标准 ``envs`` 目录，默认使用 ``root_dir/pkgs`` 作为缓存位置。

    **示例：**

    .. code-block:: yaml

      envs_dirs:
        - ~/my-envs
        - /opt/anaconda/envs

    ``CONDA_ENVS_PATH`` 环境变量可以覆盖 ``envs_dirs`` 设置：

    * 对于 macOS 和 Linux：
      ``CONDA_ENVS_PATH=~/my-envs:/opt/anaconda/envs``

    * 对于 Windows：
      ``set CONDA_ENVS_PATH=C:\Users\joe\envs;C:\Anaconda\envs``

.. tab:: 英文

    Specify directories in which environments are located. If this
    key is set, the root prefix ``envs_dir`` is not used unless
    explicitly included. This key also determines where the package
    caches are located.

    For each envs here, ``envs/pkgs`` is used as the pkgs cache,
    except for the standard ``envs`` directory in the root
    directory, for which the normal ``root_dir/pkgs`` is used.

    **Example:**

    .. code-block:: yaml

      envs_dirs:
        - ~/my-envs
        - /opt/anaconda/envs

    The ``CONDA_ENVS_PATH`` environment variable overwrites the ``envs_dirs`` setting:

    * For macOS and Linux:
      ``CONDA_ENVS_PATH=~/my-envs:/opt/anaconda/envs``

    * For Windows:
      ``set CONDA_ENVS_PATH=C:\Users\joe\envs;C:\Anaconda\envs``

.. _specify-pkg-directories:

``pkgs_dirs``：指定软件包目录
------------------------------------------

``pkgs_dirs``: Specify package directories

.. tab:: 中文

    指定软件包所在的目录。如果设置了此键，则根目录的 ``pkgs_dirs`` 将不会使用，除非显式包含。

    如果未设置 ``pkgs_dirs`` 键，则默认使用 ``envs/pkgs`` 作为软件包缓存，除了根目录中的标准 ``envs`` 目录，默认使用 ``root_dir/pkgs`` 作为缓存位置。

    **示例：**

    .. code-block:: yaml

      pkgs_dirs:
        - /opt/anaconda/pkgs

    ``CONDA_PKGS_DIRS`` 环境变量可以覆盖 ``pkgs_dirs`` 设置：

    * 对于 macOS 和 Linux：
      ``CONDA_PKGS_DIRS=/opt/anaconda/pkgs``

    * 对于 Windows：
      ``set CONDA_PKGS_DIRS=C:\Anaconda\pkgs``

.. tab:: 英文

    Specify directories in which packages are located. If this
    key is set, the root prefix ``pkgs_dirs`` is not used unless
    explicitly included.

    If the ``pkgs_dirs`` key is not set, then ``envs/pkgs`` is used
    as the pkgs cache, except for the standard ``envs`` directory in the root
    directory, for which the normal ``root_dir/pkgs`` is used.

    **Example:**

    .. code-block:: yaml

      pkgs_dirs:
        - /opt/anaconda/pkgs

    The ``CONDA_PKGS_DIRS`` environment variable overwrites the
    ``pkgs_dirs`` setting:

    * For macOS and Linux:
      ``CONDA_PKGS_DIRS=/opt/anaconda/pkgs``

    * For Windows:
      ``set CONDA_PKGS_DIRS=C:\Anaconda\pkgs``

.. _use-only-tar-bz2:

``use_only_tar_bz2``：强制 conda 仅下载 .tar.bz2 软件包
--------------------------------------------------------------------

``use_only_tar_bz2``: Force conda to download only .tar.bz2 packages

.. tab:: 中文

    Conda 4.7 引入了新的 ``.conda`` 软件包文件格式。
    ``.conda`` 是一种更紧凑且更快速的替代格式，相较于 ``.tar.bz2`` 软件包更具优势，因此在可用的情况下，建议使用该格式。

    尽管如此，仍然可以通过将 ``use_only_tar_bz2`` 布尔值设置为 ``True`` 强制 conda 仅下载 ``.tar.bz2`` 软件包。

    默认值为 ``False``。

    **示例：**

    .. code-block:: yaml

      use_only_tar_bz2: True

    .. 注意::

      如果安装了 conda-build 且版本低于 3.18.3，则此值会被强制设置为 ``True``，
      因为较旧版本的 conda 在处理新文件格式时会出现问题。

.. tab:: 英文

    Conda 4.7 introduced a new ``.conda`` package file format.
    ``.conda`` is a more compact and faster alternative to ``.tar.bz2`` packages.
    It's thus the preferred file format to use where available.

    Nevertheless, it's possible to force conda to only download ``.tar.bz2`` packages
    by setting the ``use_only_tar_bz2`` boolean to ``True``.

    The default is ``False``.

    **Example:**

    .. code-block:: yaml

      use_only_tar_bz2: True

    .. note::

      This is forced to ``True`` if conda-build is installed and older than 3.18.3,
      because older versions of conda break when conda feeds it the new file format.

.. _console:

``console``：配置显示类型
---------------------------------------

``console``: Configure display type

.. tab:: 中文

    .. versionadded:: 24.11.0
      ``console`` 设置仅在此版本之后可用。

    ``console`` 设置允许你修改 conda 命令输出的呈现方式。
    此设置主要用于选择插件提供的新报告后端。

    例如，某个插件可能会创建一个名为 "colors" 的新报告后端。作为用户，你可以
    在 ``.condarc`` 文件中按如下方式进行配置：

    .. code-block:: yaml

      console: colors

    或者在命令行中使用 ``--console`` 选项指定它：

    .. code-block:: commandline

      conda info --console=colors

.. tab:: 英文


    .. versionadded:: 24.11.0
      the ``console`` setting is only available after this version.

    The ``console`` setting allows you to modify the way output is rendered for conda commands.
    This setting is primarily used as a way to select new reporter backends made available by plugins.

    For example, a plugin may create a new reporter backend called "colors". As a user, you would
    configure it in your ``.condarc`` file as shown below:

    .. code-block:: yaml

      console: colors

    or specify it on the command line with the ``--console`` option

    .. code-block:: commandline

      conda info --console=colors


Conda-build 配置
=========================

Conda-build configuration

.. _specify-root-dir:

``root-dir``：指定 conda-build 输出根目录
-------------------------------------------------------

``root-dir``: Specify conda-build output root directory

.. tab:: 中文

    构建输出根目录。你也可以通过 ``CONDA_BLD_PATH`` 环境变量来设置此项。默认值为 ``<CONDA_PREFIX>/conda-bld/``。如果你没有写入权限到 ``<CONDA_PREFIX>/conda-bld/``，则默认值为 ``~/conda-bld/``。

    **示例：**

    .. code-block:: yaml

      conda-build:
          root-dir: ~/conda-builds

.. tab:: 英文

    Build output root directory. You can also set this with the ``CONDA_BLD_PATH`` environment variable. The default is ``<CONDA_PREFIX>/conda-bld/``. If you do not have write permissions to ``<CONDA_PREFIX>/conda-bld/``, the default is ``~/conda-bld/``.

    **Example:**

    .. code-block:: yaml

      conda-build:
          root-dir: ~/conda-builds

.. _specify-output-folder:

``output_folder``：指定 conda-build 构建文件夹（conda-build 3.16.3+）
-------------------------------------------------------------------------

``output_folder``: Specify conda-build build folder (conda-build 3.16.3+)

.. tab:: 中文

    用于保存输出包的文件夹。如果构建或测试成功，包将被移动到此文件夹。如果未设置，则输出文件夹与 ``root-dir`` 相同：即根构建目录。

    **示例：**

    .. code-block:: yaml

      conda-build:
          output_folder: conda-bld

.. tab:: 英文

    Folder to dump output package to. Packages are moved here if build or test
    succeeds. If unset, the output folder corresponds to the same directory as
    ``root-dir``: the root build directory.
    .. code-block:: yaml

      conda-build:
          output_folder: conda-bld

.. _pkg_format:

``pkg_version``：指定 conda-build 软件包版本
----------------------------------------------------

``pkg_version``: Specify conda-build package version

.. tab:: 中文


    要创建的 Conda 包版本。使用 ``2`` 表示 ``.conda`` 包。如果未设置，conda-build 默认为 ``.tar.bz2``。

    **示例：**

    .. code-block:: yaml

      conda-build:
          pkg_format: 2

.. tab:: 英文

    Conda package version to create. Use ``2`` for ``.conda`` packages. If not set, conda-build defaults to ``.tar.bz2``.

    .. code-block:: yaml

      conda-build:
          pkg_format: 2

.. _auto-upload:

``anaconda_upload``：自动将 conda-build 软件包上传到Anaconda.org
------------------------------------------------------------------------------

``anaconda_upload``: Automatically upload conda-build packages to Anaconda.org

.. tab:: 中文

    自动将通过 conda-build 构建的包上传到 `Anaconda.org <http://anaconda.org>`_。默认值为 ``False``。

    **示例：**

    .. code-block:: yaml

      anaconda_upload: True

.. tab:: 英文

    Automatically upload packages built with conda-build to
    `Anaconda.org <http://anaconda.org>`_. The default is ``False``.

    **Example:**

    .. code-block:: yaml

      anaconda_upload: True

.. _anaconda-token:

``anaconda_token``：用于 Anaconda.org 上传的令牌 (conda-build 3.0+)
--------------------------------------------------------------------------------

``anaconda_token``: Token to be used for Anaconda.org uploads (conda-build 3.0+)

.. tab:: 中文

    令牌是一种通过 Anaconda.org 进行身份验证的方法，而无需登录。你可以通过此 ``.condarc`` 设置或 CLI 参数将令牌传递给 conda-build。默认情况下此项未设置。设置它会隐式启用 ``anaconda_upload``。

    **示例：**

    .. code-block:: yaml

      conda-build:
          anaconda_token: gobbledygook

.. tab:: 英文

    Tokens are a means of authenticating with Anaconda.org without logging in.
    You can pass your token to conda-build with this ``.condarc`` setting, or with a CLI
    argument. This is unset by default. Setting it implicitly enables
    ``anaconda_upload``.

    .. code-block:: yaml

      conda-build:
          anaconda_token: gobbledygook

.. _quiet:

``quiet``：限制构建输出详细程度 (conda-build 3.0+)
----------------------------------------------------------

``quiet``: Limit build output verbosity (conda-build 3.0+)

.. tab:: 中文

    可以通过 ``quiet`` 设置来减少 conda-build 的输出详细信息。要查看更多详细信息，可以使用 CLI 标志 ``--debug``。

    **示例：**

    .. code-block:: yaml

      conda-build:
          quiet: true

.. tab:: 英文

    Conda-build's output verbosity can be reduced with the ``quiet`` setting. For
    more verbosity, use the CLI flag ``--debug``.

    .. code-block:: yaml

      conda-build:
          quiet: true

.. _filename-hashing:

``filename_hashing``：禁用文件名哈希 (conda-build 3.0+)
-----------------------------------------------------------------

``filename_hashing``: Disable filename hashing (conda-build 3.0+)

.. tab:: 中文

    Conda-build 3 为文件名添加哈希值，以允许对依赖版本进行更大的自定义。如果你发现这很干扰，可以通过以下配置条目禁用哈希值。

    **示例：**

    .. code-block:: yaml

      conda-build:
          filename_hashing: false

    .. warning::

      Conda-build 在覆盖包时不进行检查。如果你使用了 conda-build 3 的构建矩阵，并且构建配置没有反映在构建字符串中，包可能会由于覆盖而丢失。

.. tab:: 英文

    Conda-build 3 adds hashes to filenames to allow greater customization of
    dependency versions. If you find this disruptive, you can disable the hashing
    with the following config entry:

    .. code-block:: yaml

      conda-build:
          filename_hashing: false

    .. warning::

      Conda-build does not check when clobbering packages. If you
      utilize conda-build 3's build matrices with a build configuration that is not
      reflected in the build string, packages will be missing due to clobbering.

.. _no-verify:

``no_verify``：禁用配方和包验证 (conda-build 3.0+)
-------------------------------------------------------------------------

``no_verify``: Disable recipe and package verification (conda-build 3.0+)

.. tab:: 中文

    默认情况下，conda-build 使用 conda-verify 确保你的配方和包符合一些最低的校验标准。你可以禁用这些校验：

    **示例：**

    .. code-block:: yaml

      conda-build:
          no_verify: true

.. tab:: 英文

    By default, conda-build uses conda-verify to ensure that your recipe
    and package meet some minimum sanity checks. You can disable these:

    .. code-block:: yaml

      conda-build:
          no_verify: true

.. _set-build-id:

``set_build_id``：禁用每次构建时创建文件夹 (conda-build 3.0+)
----------------------------------------------------------------------

``set_build_id``: Disable per-build folder creation (conda-build 3.0+)

.. tab:: 中文

    默认情况下，conda-build 为每个构建创建一个新文件夹，文件夹名为包名加上时间戳。这允许你同时进行多个构建。如果你在处理长路径时遇到问题，可能需要禁用此行为。你应该首先尝试使用上述的 ``root-dir`` 设置来更改构建输出根目录，但在必要时也可以退而求其次：

    **示例：**

    .. code-block:: yaml

      conda-build:
          set_build_id: false

.. tab:: 英文

    By default, conda-build creates a new folder for each build, named for the
    package name plus a timestamp. This allows you to do multiple builds at once.
    If you have issues with long paths, you may need to disable this behavior.
    You should first try to change the build output root directory with the
    ``root-dir`` setting described above, but fall back to this as necessary:
    
    .. code-block:: yaml
    
       conda-build:
           set_build_id: false
    
.. _skip-existing:

``skip_existing``：跳过构建已存在的包 (conda-build 3.0+)
-------------------------------------------------------------------------------

``skip_existing``: Skip building packages that already exist (conda-build 3.0+)

.. tab:: 中文

    默认情况下，conda-build 会构建你指定的所有配方。你可以选择跳过已构建的配方。如果配方的 *所有* 输出在当前配置的渠道上都已可用，则该配方将被跳过。

    **示例：**

    .. code-block:: yaml

      conda-build:
          skip_existing: true

.. tab:: 英文

    By default, conda-build builds all recipes that you specify. You can instead
    skip recipes that are already built. A recipe is skipped if and only if *all* of
    its outputs are available on your currently configured channels.

    .. code-block:: yaml

      conda-build:
          skip_existing: true

.. _include-recipe:

``include_recipe``：从包中省略配方 (conda-build 3.0+)
---------------------------------------------------------------

``include_recipe``: Omit recipe from package (conda-build 3.0+)

.. tab:: 中文

默认情况下，conda-build 会包含用于构建包的配方。如果此配方包含敏感或专有信息，可以选择省略该配方。

**示例：**

.. code-block:: yaml

   conda-build:
       include_recipe: false

.. note::

   如果不包含配方，则无法在构建完成后使用 conda-build 测试包。这意味着你不能将构建和测试步骤分为两个独立的命令（ ``conda build --notest recipe`` 和 ``conda build -t recipe``）。如果你需要省略配方并分割步骤，唯一的选择是，在测试步骤之后从 tarball 工件中移除配方文件。Conda-build 不提供执行此操作的工具。

.. tab:: 英文

    By default, conda-build includes the recipe that was used to build the package.
    If this contains sensitive or proprietary information, you can omit the recipe.

    .. code-block:: yaml

      conda-build:
          include_recipe: false

    .. note::

      If you do not include the recipe, you cannot use conda-build to test
      the package after the build completes. This means that you cannot split your
      build and test steps across two distinct CLI commands (``conda build --notest
      recipe`` and ``conda build -t recipe``). If you need to omit the recipe and
      split your steps, your only option is to remove the recipe files from the
      tarball artifacts after your test step. Conda-build does not provide tools for
      doing that.

.. _disable-activation:

``activate``：禁用构建/测试期间的环境激活 (conda-build 3.0+)
-------------------------------------------------------------------------------------

``activate``: Disable activation of environments during build/test (conda-build 3.0+)

.. tab:: 中文

    默认情况下，conda-build 在执行构建或测试脚本之前会激活构建和测试环境。这会添加必要的 PATH 条目，并运行你可能有的任何 activate.d 脚本。如果禁用激活，PATH 仍会被修改，但 activate.d 脚本不会运行。虽然这不是推荐的做法，但有些人可能更喜欢这种方式。

    **示例：**

    .. code-block:: yaml

        conda-build:
            activate: false

.. tab:: 英文

    By default, conda-build activates the build and test environments prior to
    executing the build or test scripts. This adds necessary PATH entries, and also
    runs any activate.d scripts you may have. If you disable activation, the PATH
    will still be modified, but the activate.d scripts will not run. This is not
    recommended, but some people prefer this.

    .. code-block:: yaml

      conda-build:
          activate: false

.. _long-test-prefix:

``long_test_prefix``：禁用构建期间的长前缀测试 (conda-build 3.16.3+)
---------------------------------------------------------------------------

``long_test_prefix``: Disable long prefix during test (conda-build 3.16.3+)

.. tab:: 中文

    默认情况下，conda-build 会为测试前缀使用长前缀。如果你有配方在长前缀中失败，但仍希望在短前缀中测试它们，你可以禁用长测试前缀。这不推荐使用。

    **示例：**

    .. code-block:: yaml

      conda-build:
          long_test_prefix: false

    默认值为 ``true``。

.. tab:: 英文

    By default, conda-build uses a long prefix for the test prefix. If you have recipes
    that fail in long prefixes but would still like to test them in short prefixes, you
    can disable the long test prefix. This is not recommended.

    .. code-block:: yaml

      conda-build:
          long_test_prefix: false

    The default is ``true``.

.. _pypi-upload-settings:

``pypirc``：PyPI 上传设置 (conda-build 3.0+)
---------------------------------------------------

``pypirc``: PyPI upload settings (conda-build 3.0+)

.. tab:: 中文

    默认情况下未设置。如果你的配方中包含 wheel 输出，conda-build 会尝试使用 ``pypi_repository`` 设置中指定的 PyPI 仓库上传它们，使用来自该文件路径的凭据。

    **示例：**

    .. code-block:: yaml

      conda-build:
          pypirc: ~/.pypirc

.. tab:: 英文

    Unset by default. If you have wheel outputs in your recipe, conda-build will
    try to upload them to the PyPI repository specified by the ``pypi_repository``
    setting using credentials from this file path.

    .. code-block:: yaml

      conda-build:
          pypirc: ~/.pypirc

.. _pypi-repository:

``pypi_repository``：要上传到的 PyPI 仓库 (conda-build 3.0+)
--------------------------------------------------------------------

``pypi_repository``: PyPI repository to upload to (conda-build 3.0+)

.. tab:: 中文

    默认情况下未设置。如果你的配方中包含 wheel 输出，conda-build 会尝试使用从 ``pypirc`` 设置中指定的文件获取凭据上传这些输出到 PyPI 仓库。

    **示例：**

    .. code-block:: yaml

      conda-build:
          pypi_repository: pypi

.. tab:: 英文

    Unset by default. If you have wheel outputs in your recipe, conda-build will
    try to upload them to this PyPI repository using credentials from the file
    specified by the ``pypirc`` setting.

    .. code-block:: yaml

      conda-build:
          pypi_repository: pypi

环境变量扩展
==================================

Expansion of environment variables

.. tab:: 中文

    Conda 会在某些配置设置中扩展环境变量。这些设置包括：

    - ``channel``
    - ``channel_alias``
    - ``channels``
    - ``client_cert_key``
    - ``client_cert``
    - ``custom_channels``
    - ``custom_multichannels``
    - ``default_channels``
    - ``envs_dirs``
    - ``envs_path``
    - ``migrated_custom_channels``
    - ``pkgs_dirs``
    - ``proxy_servers``
    - ``verify_ssl``
    - ``allowlist_channels``
    - ``denylist_channels``

    这允许你像这样将私有仓库的凭据存储在环境变量中：

    **示例：**

    .. code-block:: yaml

      channels:
        - https://${USERNAME}:${PASSWORD}@my.private.conda.channel

.. tab:: 英文

    Conda expands environment variables in a subset of configuration settings.
    These are:

    - ``channel``
    - ``channel_alias``
    - ``channels``
    - ``client_cert_key``
    - ``client_cert``
    - ``custom_channels``
    - ``custom_multichannels``
    - ``default_channels``
    - ``envs_dirs``
    - ``envs_path``
    - ``migrated_custom_channels``
    - ``pkgs_dirs``
    - ``proxy_servers``
    - ``verify_ssl``
    - ``allowlist_channels``
    - ``denylist_channels``

    This allows you to store the credentials of a private repository in an
    environment variable, like so:

    .. code-block:: yaml

      channels:
        - https://${USERNAME}:${PASSWORD}@my.private.conda.channel
.. _threads:

配置线程数
=============================

Configuring number of threads

.. tab:: 中文

    你可以使用 ``.condarc`` 文件或环境变量来添加配置，以控制线程数。你可能希望这样做，以便 conda 更好地利用你的系统。如果你有非常快速的 SSD，可能希望增加线程数，以缩短创建环境和安装/删除包所需的时间。

.. tab:: 英文

    You can use your ``.condarc`` file or environment variables to
    add configuration to control the number of threads. You may
    want to do this to tweak conda to better utilize your system.
    If you have a very fast SSD, you might increase the number
    of threads to shorten the time it takes for conda to create
    environments and install/remove packages.

``repodata_threads``
--------------------

``repodata_threads``

.. tab:: 中文

    * 默认线程数：None
    * 下载、解析和创建来自 ``repodata.json`` 文件的 repodata 结构时使用的线程数。多个下载可能同时进行。这样可以加速开始解决问题的时间。

.. tab:: 英文

    * Default number of threads: None
    * Threads used when downloading, parsing, and creating repodata
      structures from ``repodata.json`` files. Multiple downloads from
      different channels may occur simultaneously. This speeds up the
      time it takes to start solving.

``verify_threads``
------------------

``verify_threads``

.. tab:: 中文

    * 默认线程数：1
    * 用于验证将安装到环境中的包和文件的完整性。默认值为 1，因为在较慢的硬盘上使用多个线程可能会遇到问题。

.. tab:: 英文

    * Default number of threads: 1
    * Threads used when verifying the integrity of packages and files
      to be installed in your environment. Defaults to 1, as using
      multiple threads here can run into problems with slower hard
      drives.

``execute_threads``
-------------------

``execute_threads``

.. tab:: 中文

    * 默认线程数：1
    * 用于取消链接、删除、链接或复制文件到环境中的线程数。默认值为 1，因为在较慢的硬盘上使用多个线程可能会遇到问题。

.. tab:: 英文

    * Default number of threads: 1
    * Threads used to unlink, remove, link, or copy files into your
      environment. Defaults to 1, as using multiple threads here can
      run into problems with slower hard drives.

``default_threads``
-------------------

``default_threads``

.. tab:: 中文

    * 默认线程数：None
    * 设置后，这个值将用于上述所有线程设置。其默认设置为 (None)，不会影响其他设置。

    可以在 ``.condarc`` 中或使用 conda config 设置以上任何内容：

    在终端中::

      conda config --set repodata_threads 2

    在 ``.condarc`` 中::

      verify_threads: 4

.. tab:: 英文

    * Default number of threads: None
    * When set, this value is used for all of the above thread
      settings. With its default setting (None), it does not affect
      the other settings.

    Setting any of the above can be done in ``.condarc`` or with
    conda config:

    At your terminal::

      conda config --set repodata_threads 2

    In ``.condarc``::

      verify_threads: 4
