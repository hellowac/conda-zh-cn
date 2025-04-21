========================
创建自定义渠道
========================

Creating custom channels

.. tab:: 中文

   在本教程中，我们将逐步演示如何创建自己的通道（channel），该通道可以通过本地文件系统、网络文件系统访问，或通过 Web 服务器进行提供。

   要创建一个自定义通道：

   #. 你需要安装 conda-build 才能完成本教程。如果尚未安装，可以使用以下命令进行安装：

      .. code::

         conda install conda-build

   #. 按照你希望提供支持的平台，将所有软件包组织到子目录中。以下是一个示例结构：

      .. code::

         channel
         ├── linux-64
         │   └── package-1.0-0.tar.bz2
         ├── osx-64
         │   └── package-1.0-0.tar.bz2
         └── win-64
            └── package-1.0-0.tar.bz2

   #. 在通道的根目录上运行 ``conda index``：

      .. code::

         conda index channel/

      ``conda index`` 命令会在每个平台子目录中生成一个名为 ``repodata.json`` 的文件，
      conda 会使用该文件中的元数据来识别通道中的软件包。

      .. note::
         每当你向通道添加或修改软件包时，必须重新运行 ``conda index``，
         否则 conda 无法识别这些更新。

   #. 要测试自定义通道，可以使用 Web 服务器进行托管，或使用 ``file://`` URL 访问通道目录。
      通过向该通道发送搜索命令进行测试。

      **示例**：如果你想从自定义通道位置 ``/opt/channel/linux-64/`` 搜索软件包，可以运行：

      .. code::

         conda search -c file:///opt/channel/ --override-channels

      .. note::
         * 通道 URL 中不包含平台信息，因为 conda 会自动检测并添加对应的平台路径。
         * 使用 ``--override-channels`` 参数可以确保 conda 只搜索你指定的通道，
         而不会搜索默认通道或 ``.condarc`` 文件中配置的其他通道。

      如果你正确配置了私有仓库，你将会看到类似如下的输出：

      .. code::

         Fetching package metadata: . . . .

      接下来将列出搜索到的 conda 软件包。
      这表明你已经成功设置并索引了你的私有通道。


.. tab:: 英文

   In this tutorial, we walk through how to create your own channel
   that can either be accessed via the local or network file system or served
   from a webserver.

   To create a custom channel:

   #. You will need to install conda-build to complete this tutorial. If you do not already have it,
      you can install it with the following command:

      .. code::

         conda install conda-build

   #. Organize all the packages in subdirectories for the platforms you wish to serve. Below
      is an example of what this may look like:

      .. code::

         channel
         ├── linux-64
         │   └── package-1.0-0.tar.bz2
         ├── osx-64
         │   └── package-1.0-0.tar.bz2
         └── win-64
            └── package-1.0-0.tar.bz2

   #. Run ``conda index`` on the channel root directory:

      .. code::

         conda index channel/

      The conda index command generates a file ``repodata.json``,
      saved to each repository directory, which conda uses to get
      the metadata for the packages in the channel.

      .. note::
         Each time you add or modify a package in the channel,
         you must rerun ``conda index`` for conda to see the update.

   #. To test custom channels, serve the custom channel using a web
      server or using a ``file://`` URL to the channel directory.
      Test by sending a search command to the custom channel.

      **Example**: if you want a file in the custom channel location
      ``/opt/channel/linux-64/``, search for files in that location:

      .. code::

         conda search -c file:///opt/channel/ --override-channels

      .. note::
         * The channel URL does not include the platform, as conda
         automatically detects and adds the platform.
         * The option ``--override-channels`` ensures that conda
         searches only your specified channel and no other channels,
         such as default channels or any other channels you may have
         listed in your ``.condarc`` file.

      If you have set up your private repository correctly, you
      get the following output:

      .. code::

         Fetching package metadata: . . . .

      This is followed by a list of the conda packages found. This
      verifies that you have set up and indexed your private
      repository successfully.
