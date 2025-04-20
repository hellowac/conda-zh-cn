=============================================
管理多用户 conda 安装
=============================================

Administering a multi-user conda installation

.. tab:: 中文

   默认情况下，conda 及其安装的所有软件包都会以用户专属配置的形式安装在本地。此过程无需管理员权限，且不会影响上游文件或其他用户。
   
   你可以使 conda 及若干指定软件包可供一个或多个用户使用，同时阻止这些用户通过 conda 安装未经授权的软件包：
   
   #. 在管理员控制之下并对用户可访问的位置安装 conda 及所有允许的软件包（如有）。
   
   #. 在该安装位置的根目录下创建一个
      :doc:`.condarc 系统配置文件 <use-condarc>`。该系统级配置文件将覆盖用户所安装的任何用户级配置文件。
   
   每个用户都会访问中央 conda 安装，并从其主目录下的用户级 ``.condarc`` 配置文件读取设置。该用户配置文件的路径与 ``conda info`` 显示的根环境前缀一致，如下方 :ref:`admin-inst-user` 所示。系统级 ``.condarc`` 文件可以限制用户级 ``.condarc`` 文件的权限。
   
   系统配置设置通常写入系统级 ``.condarc`` 文件中，但也可以用于用户级 ``.condarc`` 文件。所有用户配置设置同样也可以用于系统级 ``.condarc`` 文件中。
   
   有关 ``.condarc`` 文件中各项设置的详细说明，请参阅 :doc:`use-condarc`。

.. tab:: 英文

   By default, conda and all of the packages it installs are installed locally with a
   user-specific configuration. Administrative privileges are not required, and
   no upstream files or other users are affected by the installation.
   
   You can make conda and any number of packages available to a
   group of one or more users, while preventing these users
   from installing unwanted packages with conda:
   
   #. Install conda and the allowed packages, if any, in a
      location that is under administrator control and
      accessible to users.
   
   #. Create a
      :doc:`.condarc system configuration file <use-condarc>` in
      the root directory of the installation. This system-level
      configuration file will override any user-level configuration
      files installed by the user.
   
   Each user accesses the central conda installation, which reads
   settings from the user ``.condarc`` configuration file located
   in their home directory. The path to the user file is the same
   as the root environment prefix displayed by ``conda info``,
   as shown in :ref:`admin-inst-user` below. The user
   ``.condarc`` file is limited by the system ``.condarc`` file.
   
   System configuration settings are commonly used in a
   system ``.condarc`` file but may also be used in a
   user ``.condarc`` file. All user configuration settings may
   also be used in a system ``.condarc`` file.
   
   For information about settings in the ``.condarc`` file,
   see :doc:`use-condarc`.

.. _admin-inst:

管理员控制安装示例
=============================================

Example administrator-controlled installation

.. tab:: 中文

   以下示例介绍如何查看系统配置文件、审查其设置、将其与用户的配置文件进行比较，并判断当用户尝试访问一个被阻止的频道时会发生什么。随后将说明用户如何修改其配置文件以访问管理员允许的频道。

.. tab:: 英文

   The following example describes how to view the system
   configuration file, review the settings, compare it to a user's
   configuration file, and determine what happens when the user
   attempts to access a file from a blocked channel. It then
   describes how the user must modify their configuration file to
   access the channels allowed by the administrator.

系统配置文件
-------------------------

System configuration file

.. tab:: 中文

   #. 系统配置文件必须位于 conda 安装目录的顶层。检查 ``conda`` 所在路径，例如在 miniconda 安装中：
   
      .. code-block:: bash
   
         $ which conda
         /tmp/miniconda/bin/conda
   
   #. 查看管理员目录中 ``.condarc`` 文件的内容：
   
      .. code-block:: bash
   
         cat /tmp/miniconda/.condarc
   
      下列管理员 ``.condarc`` 文件使用 ``#!final`` 标志指定了可供用户使用的频道、默认频道以及 `channel_alias`：
   
      .. code-block:: bash
   
        $ cat /tmp/miniconda/.condarc
   
        channels:                                   #!final
          - admin
   
        channel_alias: https://conda.anaconda.org/  #!final
   
   ``#!final`` 标志类似于 CSS 中的 ``!important`` 规则；在 ``.condarc`` 文件中，任何带有 ``#!final`` 后缀的参数都不能被其他来源的 ``.condarc`` 文件覆盖。有关该标志的更多信息，请参阅 `Anaconda 博客 <https://www.anaconda.com/blog/conda-configuration-engine-power-users>`_。
   
   由于使用了 ``#!final`` 标志，且未显式指定默认频道，因此用户无法从默认频道下载软件包。可以在下一步中验证这一点。

.. tab:: 英文

   #. The system configuration file must be in the top-level conda
      installation directory. Check the path where ``conda`` is located, e.g.
      in a miniconda installation
   
      .. code-block:: bash
   
         $ which conda
         /tmp/miniconda/bin/conda
   
   #. View the contents of the ``.condarc`` file in the
      administrator's directory:
   
      .. code-block:: bash
   
         cat /tmp/miniconda/.condarc
   
      The following administrative ``.condarc`` file
      uses the ``#!final`` flag to specify the channels,
      default channels, and channel_alias available to the user.
   
      .. code-block:: bash
   
        $ cat /tmp/miniconda/.condarc
   
        channels:                                   #!final
          - admin
   
        channel_alias: https://conda.anaconda.org/  #!final
   
   The ``#!final`` flag is very similar to the ``!important``
   rule in CSS; any parameter within the ``.condarc`` that is
   trailed by the ``#!final`` cannot be overwritten by any other
   ``.condarc`` source. For more information on this flag, see the
   `Anaconda Blog <https://www.anaconda.com/blog/conda-configuration-engine-power-users>`_
   on the subject.
   
   Because the ``#!final`` flag has been used and the channel
   defaults are not explicitly specified, users are disallowed
   from downloading packages from the default channels. You can
   check this in the next procedure.

.. _admin-inst-user:

用户配置文件
-----------------------

User configuration file

.. tab:: 中文

   #. 检查用户 conda 安装的位置：
   
      .. code-block:: bash
   
         $ conda info
         Current conda install:
         . . .
                  channel URLs : https://repo.anaconda.com/pkgs/free/osx-64/
                                 https://repo.anaconda.com/pkgs/pro/osx-64/
                  config file : /Users/username/.condarc
   
      ``conda info`` 命令显示 conda 正在使用用户的 ``.condarc`` 文件，路径为 ``/Users/username/.condarc``，并列出了 ``repo.anaconda.com`` 等默认频道作为频道 URL。
   
   #. 查看第 1 步中找到的目录下的管理员 ``.condarc`` 文件内容：
   
      .. code-block:: bash
   
        $ cat ~/.condarc
        channels:
          - defaults
   
      此用户的 ``.condarc`` 文件只指定了默认频道，但管理员配置文件通过限制只允许使用 ``admin`` 频道，已封锁默认频道。如果该用户尝试在默认频道中搜索软件包，将会收到提示告知哪些频道是被允许的：
   
      .. code-block:: bash
   
         $ conda search flask
         Fetching package metadata:
         Error: URL 'http://repo.anaconda.com/pkgs/pro/osx-64/' not
         in allowed channels.
         Allowed channels are:
          - https://conda.anaconda.org/admin/osx-64/
   
      此错误信息提示用户应将 ``admin`` 频道添加到其配置文件中。
   
   #. 用户必须编辑其本地 ``.condarc`` 配置文件，以通过 admin 频道访问软件包：
   
      .. code-block:: yaml
   
        channels:
          - admin
   
      用户现在可以在被允许的 ``admin`` 频道中搜索软件包。

.. tab:: 英文

   #. Check the location of the user's conda installation:
   
      .. code-block:: bash
   
        $ conda info
        Current conda install:
        . . .
               channel URLs : https://repo.anaconda.com/pkgs/free/osx-64/
                              https://repo.anaconda.com/pkgs/pro/osx-64/
               config file : /Users/username/.condarc
   
      The ``conda info`` command shows that conda is using the
      user's ``.condarc`` file, located at
      ``/Users/username/.condarc`` and that the default channels
      such as ``repo.anaconda.com`` are listed as channel URLs.
   
   #. View the contents of the administrative ``.condarc`` file in
      the directory that was located in step 1:
   
      .. code-block:: bash
   
        $ cat ~/.condarc
        channels:
          - defaults
   
      This user's ``.condarc`` file specifies only the default
      channels, but the administrator config file has blocked
      default channels by specifying that only ``admin`` is
      allowed. If this user attempts to search for a package in the
      default channels, they get a message telling them what
      channels are allowed:
   
      .. code-block:: bash
   
         $ conda search flask
         Fetching package metadata:
         Error: URL 'http://repo.anaconda.com/pkgs/pro/osx-64/' not
         in allowed channels.
         Allowed channels are:
          - https://conda.anaconda.org/admin/osx-64/
   
      This error message tells the user to add the ``admin`` channel
      to their configuration file.
   
   #. The user must edit their local ``.condarc`` configuration file
      to access the package through the admin channel:
   
      .. code-block:: yaml
   
        channels:
          - admin
   
      The user can now search for packages in the allowed
      ``admin`` channel.
