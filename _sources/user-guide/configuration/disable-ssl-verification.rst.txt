==========================
禁用 SSL 验证
==========================

Disabling SSL verification

.. tab:: 中文

    虽然强烈推荐使用启用 SSL 的 conda，但在某些特定场景中也可以禁用 SSL，这在某些情况下是必要的。

    一些公司网络环境中使用的代理服务可能会采用中间人攻击（MITM）来嗅探加密流量。这些服务可能会干扰 conda 和 pip 在通过 SSL 下载 PyPI 等仓库中的软件包时的连接。

    如果你遇到这类干扰，应该配置代理服务的证书，使 conda 所使用的 ``requests`` 包能够识别并使用这些证书。

    若无法做到这一点，从 conda-build 3.0.31 版本起提供了一个选项，可以禁用 SSL 证书验证，从而允许该类流量继续传输。

    当使用 ``conda skeleton pypi`` 从 PyPI 服务器通过 HTTPS 获取软件包时，可以禁用 SSL 验证。

    .. warning::
    此选项会使你的计算机通过一个无法验证安全性的连接下载并执行任意代码。这种做法并不推荐，仅应在确有必要时使用。使用此选项需自行承担风险。

    若要在使用 ``conda skeleton pypi`` 时禁用 SSL 验证，请将环境变量 ``SSL_NO_VERIFY`` 设置为 ``1`` 或 ``True``（大小写不敏感）。

    在类 Unix 系统上：

    .. code-block:: bash

        SSL_NO_VERIFY=1 conda skeleton pypi a_package

    在 Windows 系统上：

    .. code-block:: batch

        set SSL_NO_VERIFY=1
        conda skeleton pypi a_package
        set SSL_NO_VERIFY=

    建议在使用完毕后立即取消设置该环境变量。如果不取消设置，某些其他工具可能会识别该变量，并错误地使用不安全的 SSL 连接。

    使用此选项时， ``requests`` 将向标准错误输出（STDERR）发出有关不安全设置的警告信息。如果你清楚自己在做什么，或已经得到 IT 部门的确认，则可以忽略这些警告。

.. tab:: 英文

    Using conda with SSL is strongly recommended, but it is possible to disable SSL
    and it may be necessary to disable SSL in certain cases.

    Some corporate environments use proxy services that use Man-In-The-Middle
    (MITM) attacks to sniff encrypted traffic. These services can interfere with
    SSL connections such as those used by conda and pip to download packages from
    repositories such as PyPI.

    If you encounter this interference, you should set up the proxy service's
    certificates so that the ``requests`` package used by conda can recognize and
    use the certificates.

    For cases where this is not possible, conda-build versions 3.0.31 and higher
    have an option that disables SSL certificate verification and allows this
    traffic to continue.

    ``conda skeleton pypi`` can disable SSL verification when pulling packages
    from a PyPI server over HTTPS.

    .. warning::
    This option causes your computer to download and execute arbitrary
    code over a connection that it cannot verify as secure. This is not
    recommended and should only be used if necessary. Use this option at your own
    risk.

    To disable SSL verification when using ``conda skeleton pypi``, set the
    ``SSL_NO_VERIFY`` environment variable to either ``1`` or ``True`` (case
    insensitive).

    On \*nix systems:

    .. code-block:: bash

        SSL_NO_VERIFY=1 conda skeleton pypi a_package

    And on Windows systems:

    .. code-block:: batch

        set SSL_NO_VERIFY=1
        conda skeleton pypi a_package
        set SSL_NO_VERIFY=

    We recommend that you unset this environment variable immediately after use.
    If it is not unset, some other tools may recognize it and incorrectly use
    unverified SSL connections.

    Using this option will cause ``requests`` to emit warnings to STDERR about
    insecure settings. If you know that what you're doing is safe, or have been
    advised by your IT department that what you're doing is safe, you may ignore
    these warnings.

=============================================
通过 conda 设置禁用 SSL 验证
=============================================

Disabling SSL verification via conda settings

.. tab:: 中文

    除了通过环境变量禁用 SSL 外，还可以通过将配置文件中的 `ssl_verify` 设置为 `false` 来禁用 SSL。可以通过以下命令来关闭或启用 SSL：

    .. code-block:: bash

        conda config --set ssl_verify False
        # 在禁用 SSL 的情况下运行 conda 命令
        conda config --set ssl_verify True

.. tab:: 英文

    In addition to disabling SSL via environment variables, you can disable it by setting `ssl_verify` to `false` in your config files. To do so, run the following commands to disable and enable it:

    .. code-block:: bash

        conda config --set ssl_verify False
        # Run conda commands with SSL disabled
        conda config --set ssl_verify True
