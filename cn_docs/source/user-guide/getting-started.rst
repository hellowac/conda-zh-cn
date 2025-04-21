==========================
conda 入门
==========================

Getting started with conda

.. tab:: 中文

   Conda 是一款功能强大的命令行工具，用于管理软件包和环境，可在 Windows、macOS 和 Linux 上运行。

   本 conda 入门指南介绍了启动和使用 conda 创建环境及安装软件包的基础知识。
    
   .. tip::
   
      Anaconda Navigator 是一个图形桌面应用程序，使您无需在命令行运行命令即可使用 conda。
   
      请参阅 `开始使用 Anaconda Navigator <https://docs.anaconda.com/navigator/getting-started/>`_ 以了解更多信息。

.. tab:: 英文

   Conda is a powerful command line tool for package and environment management that runs on Windows, macOS, and Linux.
   
   This guide to getting started with conda goes over the basics of starting up and using conda to create environments and install packages.
   
   .. tip::
   
      Anaconda Navigator is a graphical desktop application that enables you to use conda without having to run commands at the command line.
   
      See `Getting started with Anaconda Navigator <https://docs.anaconda.com/navigator/getting-started/>`__ to learn more.

开始之前
================

Before you start

.. tab:: 中文

   要启动一个 ``conda`` 安装环境，可以使用精简安装器，例如 `Miniconda <https://docs.anaconda.com/miniconda/>`__ 或 `Miniforge <https://conda-forge.org/download>`__。

   Conda 也包含在 `Anaconda Distribution <https://docs.anaconda.com/anaconda/install/>`_ 中。

   .. note::

      Miniconda 和 Anaconda Distribution 默认配置为使用 `Anaconda 仓库 <https://repo.anaconda.com/>`__，并且从该仓库安装或使用软件包受到 `Anaconda 服务条款 <https://www.anaconda.com/terms-of-service>`__ 的约束，这意味着 *可能* 需要商业付费许可。对于个人用户、大学以及员工数量少于 200 的公司（截至 2024 年 9 月）存在豁免情况。

      请查阅 `服务条款 <https://www.anaconda.com/terms-of-service>`__、Anaconda 最新发布的关于学术和研究用途的 `服务条款更新 <https://www.anaconda.com/blog/update-on-anacondas-terms-of-service-for-academia-and-research>`__，以及 `Anaconda 服务条款常见问题 <https://www.anaconda.com/pricing/terms-of-service-faqs>`__ 来解答您的疑问。

.. tab:: 英文

   To bootstrap a ``conda`` installation, use a minimal installer such as `Miniconda <https://docs.anaconda.com/miniconda/>`__ or `Miniforge <https://conda-forge.org/download>`__.

   Conda is also included in the `Anaconda Distribution <https://docs.anaconda.com/anaconda/install/>`_.

   .. note::

      Miniconda and Anaconda Distribution come preconfigured to use the `Anaconda
      Repository <https://repo.anaconda.com/>`__ and installing/using packages
      from that repository is governed by the `Anaconda Terms of Service
      <https://www.anaconda.com/terms-of-service>`__, which means that it *might*
      require a commercial fee license. There are exceptions for individuals,
      universities and companies with fewer than 200 employees (as of September
      2024).

      Please review the `terms of service <https://www.anaconda.com/terms-of-service>`__, Anaconda's most recent `Update on Anaconda’s Terms of Service for Academia
      and Research <https://www.anaconda.com/blog/update-on-anacondas-terms-of-service-for-academia-and-research>`__,
      and the `Anaconda Terms of Service FAQ
      <https://www.anaconda.com/pricing/terms-of-service-faqs>`__ to answer your questions.

启动 conda
==============

Starting conda

.. tab:: 中文

   Conda 可在 Windows、macOS 和 Linux 上使用，并可配合任意终端程序（或 shell）使用。

   .. tab-set::

      .. tab-item:: Windows

         #. 打开 Anaconda 或 Miniforge 命令提示符（cmd.exe）。使用 Anaconda Distribution 或 Miniconda 时也可选择 PowerShell 提示符。

      .. tab-item:: macOS

         #. 打开 Launchpad。
         #. 打开“其他”应用程序文件夹。
         #. 打开“终端”应用程序。

      .. tab-item:: Linux

         打开终端窗口。

.. tab:: 英文

   Conda is available on Windows, macOS, or Linux and can be used with any terminal application (or shell).

   .. tab-set::

      .. tab-item:: Windows

         #. Open either the Anaconda or Miniforge Command Prompt (cmd.exe). A PowerShell prompt is also available with Anaconda Distribution or Miniconda.

      .. tab-item:: macOS

         #. Open Launchpad.
         #. Open the Other application folder.
         #. Open the Terminal application.

      .. tab-item:: Linux

         Open a terminal window.

创建环境
=====================

Creating environments

.. tab:: 中文

   Conda 允许你创建独立的环境，每个环境都包含其自身的文件、软件包和软件包依赖。每个环境的内容彼此之间互不干扰。

   创建新环境的最基本命令如下::

      conda create -n <env-name>

   若要在创建环境时添加软件包，可在环境名称之后指定软件包::

      conda create -n myenvironment python numpy pandas

   关于环境管理的更多信息，请参见 :doc:`管理环境 <tasks/manage-environments>`。

.. tab:: 英文

   Conda allows you to create separate environments, each containing their own files, packages, and package dependencies. The contents of each environment do not interact with each other.

   The most basic way to create a new environment is with the following command::

      conda create -n <env-name>

   To add packages while creating an environment, specify them after the environment name::

      conda create -n myenvironment python numpy pandas

   For more information on working with environments, see :doc:`Managing environments <tasks/manage-environments>`.

列出环境
====================

Listing environments

.. tab:: 中文

   查看所有环境的列表::

      conda info --envs

   输出将类似如下所示::

      conda environments:

         base           /home/username/Anaconda3
         myenvironment   * /home/username/Anaconda3/envs/myenvironment

   .. tip::

      当前活动环境是带有星号（*）的那个。

   若要将当前环境切换回默认环境::

      conda activate

   .. tip::

      当环境被取消激活后，其名称将不再显示在提示符中，星号（*）也将返回到默认环境。可通过重复执行 ``conda info --envs`` 命令进行验证。

.. tab:: 英文

   To see a list of all your environments::

      conda info --envs

   A list of environments appears, similar to the following::

      conda environments:

         base           /home/username/Anaconda3
         myenvironment   * /home/username/Anaconda3/envs/myenvironment

   .. tip::
      The active environment is the one with an asterisk (*).

   To change your current environment back to the default one::

      conda activate

   .. tip::
      When the environment is deactivated, its name is no longer shown in your prompt,
      and the asterisk (*) returns to the default env. To verify, you can repeat the
      ``conda info --envs`` command.

安装软件包
===================

Installing packages

.. tab:: 中文

   你也可以向已有环境中安装软件包。为此，你可以激活想要修改的环境，或者在命令行中直接指定环境名称::

      # 通过激活环境的方式
      conda activate myenvironment
      conda install matplotlib

      # 通过命令行选项的方式
      conda install --name myenvironment matplotlib

   关于搜索和安装软件包的更多信息，请参见 :doc:`管理软件包 <tasks/manage-pkgs>` 。

.. tab:: 英文

   You can also install packages into a previously created environment. To do this, you can either activate the environment you want to modify or specify the environment name on the command line::

      # via environment activation
      conda activate myenvironment
      conda install matplotlib

      # via command line option
      conda install --name myenvironment matplotlib

   For more information on searching for and installing packages, see :doc:`Managing packages <tasks/manage-pkgs>`.

指定渠道
===================

Specifying channels

.. tab:: 中文

   **通道（channel）** 是存储软件包的位置，可以是你自己的计算机，也可以是互联网上的其他位置。默认情况下，conda 会在其 :ref:`默认通道 <default-channels>` 中查找软件包。

   如果你需要的软件包在其他通道（如 conda-forge）中，你可以在安装时手动指定通道::

      conda install conda-forge::numpy

   你也可以在 `.condarc` 文件中覆盖默认通道设置。具体示例请参见 :ref:`通道位置（channels） <config-channels>`，或阅读完整文档 :doc:`使用 .condarc 进行 Conda 配置 <configuration/use-condarc>`。

   .. tip::

      搜索 `Anaconda.org <https://www.anaconda.org>`_ 查找更多套餐和渠道.

.. tab:: 英文

   Channels are locations (on your own computer or elsewhere on the Internet) where packages are stored. By default, conda searches for packages in its :ref:`default channels <default-channels>`.

   If a package you want is located in another channel, such as conda-forge, you can manually specify the channel when installing the package::

      conda install conda-forge::numpy

   You can also override the default channels in your `.condarc` file. For a direct example, see :ref:`Channel locations (channels) <config-channels>` or read the entire :doc:`Using the .condarc conda configuration file <configuration/use-condarc>`.

   .. tip::

      Find more packages and channels by searching `Anaconda.org <https://www.anaconda.org>`_.

更新 conda
==============

Updating conda

.. tab:: 中文

   若要查看 conda 的版本，请运行以下命令::

      conda --version

   无论在哪个环境中运行该命令，conda 都会显示其当前版本：

   .. parsed-literal::

      conda |version|

   .. note::

      如果你看到错误信息 ``command not found: conda``，请关闭并重新打开终端窗口，并确认你当前登录的用户账户与安装 conda 时使用的是同一个。

   若要更新 conda 到最新版本::

      conda update conda

   Conda 会将你当前的版本与可用的最新版本进行比较，并显示可更新的内容。

   .. tip::
      
      我们建议你始终将 conda 保持为最新版本。有关 conda 的官方版本支持策略，请参见 `CEP 10 <https://github.com/conda-incubator/ceps/blob/main/cep-10.md>`_。

.. tab:: 英文

   To see your conda version, use the following command::

      conda --version

   No matter which environment you run this command in, conda displays its current version:

   .. parsed-literal::

      conda |version|

   .. note::
      If you get an error message ``command not found: conda``, close and reopen
      your terminal window and verify that you are logged
      into the same user account that you used to install conda.

   To update conda to the latest version::

      conda update conda

   Conda compares your version to the latest available version and then displays what is available to install.

   .. tip::
      We recommend that you always keep conda updated to the latest version.
      For conda's official version support policy, see `CEP 10 <https://github.com/conda-incubator/ceps/blob/main/cep-10.md>`_.

更多信息
================

More information

.. tab:: 中文

   * :doc:`Conda 备忘单 <cheatsheet>`
   * `全部文档 <https://conda.io/docs/>`_
   * `免费社区支持 <https://groups.google.com/a/anaconda.com/forum/#!forum/anaconda>`_

.. tab:: 英文

   * :doc:`Conda cheat sheet <cheatsheet>`
   * `Full documentation <https://conda.io/docs/>`_
   * `Free community support <https://groups.google.com/a/anaconda.com/forum/#!forum/anaconda>`_
