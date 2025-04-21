================
安装 conda
================

Installing conda

.. tab:: 中文

    若要安装 conda，首先需要选择适合你的安装程序。以下是当前最常用的一些安装程序：

.. tab:: 英文

    To install conda, you must first pick the right installer for you.
    The following are the most popular installers currently available:

.. glossary::

    `Miniconda <https://docs.anaconda.com/miniconda/>`__
        .. tab:: 中文
            
            Miniconda 是由 Anaconda 提供的一个精简版安装器。如果你希望自己手动安装大部分软件包，推荐使用此安装器。

        .. tab:: 英文
            
            Miniconda is a minimal installer provided by Anaconda. Use this installer
            if you want to install most packages yourself.


    `Anaconda Distribution <https://www.anaconda.com/download>`_
        .. tab:: 中文
            
            Anaconda Distribution 是一个功能完整的安装器，附带了一整套用于数据科学的软件包，以及 Anaconda Navigator（一个用于管理 conda 环境的图形界面应用）。

        .. tab:: 英文
            
            Anaconda Distribution is a full featured installer that comes with a suite
            of packages for data science, as well as Anaconda Navigator, a GUI application
            for working with conda environments.

    `Miniforge <https://conda-forge.org/download>`_
        .. tab:: 中文
            
            Miniforge 是由 conda-forge 社区维护的安装器，预配置为使用 conda-forge 通道。如需了解更多信息，请访问 `conda-forge 官方网站 <https://conda-forge.org>`_。

        .. tab:: 英文

            Miniforge is an installer maintained by the conda-forge community that comes
            preconfigured for use with the conda-forge channel. To learn more about conda-forge,
            visit `their website <https://conda-forge.org>`_.
            

.. _anaconda-tos_notes:

.. tab:: 中文

    .. note::

        Miniconda 和 Anaconda Distribution 默认配置为使用 `Anaconda
        软件源 <https://repo.anaconda.com/>`__，并且从该源安装/使用软件包受 `Anaconda 服务条款
        <https://www.anaconda.com/terms-of-service>`__ 的约束，这意味着 *可能* 需要商业付费许可。根据 2024 年 9 月的政策，对于个人用户、高校、以及少于 200 名员工的公司，存在例外情况。

        请查阅最新的 `服务条款 <https://www.anaconda.com/terms-of-service>`__ 、Anaconda 关于学术和科研使用条款的更新说明： `Anaconda 的服务条款更新说明（适用于学术和研究用途） <https://www.anaconda.com/blog/update-on-anacondas-terms-of-service-for-academia-and-research>`__ ，以及 `Anaconda 服务条款常见问答
        <https://www.anaconda.com/pricing/terms-of-service-faqs>`__ 以获取详细解答。

.. tab:: 英文        

    .. note::

        Miniconda and Anaconda Distribution come preconfigured to use the `Anaconda
        Repository <https://repo.anaconda.com/>`__ and installing/using packages
        from that repository is governed by the `Anaconda Terms of Service
        <https://www.anaconda.com/terms-of-service>`__, which means that it *might*
        require a commercial fee license. There are exceptions for individuals,
        universities, and companies with fewer than 200 employees (as of September
        2024).

        Please review the `terms of service <https://www.anaconda.com/terms-of-service>`__, Anaconda's most recent `Update on Anaconda’s Terms of Service for Academia
        and Research <https://www.anaconda.com/blog/update-on-anacondas-terms-of-service-for-academia-and-research>`__,
        and the `Anaconda Terms of Service FAQ
        <https://www.anaconda.com/pricing/terms-of-service-faqs>`__ to answer your questions.


.. _system-reqs:

系统要求
===================

System requirements

.. tab:: 中文

    * 支持的操作系统：Windows、macOS 或 Linux

    * 对于 Miniconda 或 Miniforge：需要 400 MB 的磁盘空间

    * 对于 Anaconda：下载和安装所需至少 3 GB 的磁盘空间

    * Windows 系统：Python 3.9 需要 Windows 8.1 或更新版本

    .. admonition:: 小贴士

        如果你选择安装在用户可写的位置（例如 ``/Users/my-username/conda`` 或 ``C:\Users\my-username\conda``），则无需管理员权限或 root 权限即可安装 conda。

.. tab:: 英文

    * A supported operating systems: Windows, macOS, or Linux

    * For Miniconda or Miniforge: 400 MB disk space

    * For Anaconda: Minimum 3 GB disk space to download and install

    * For Windows: Windows 8.1 or newer for Python 3.9

    .. admonition:: Tip

        You do not need administrative or root permissions to install conda if you select a
        user-writable install location (e.g. ``/Users/my-username/conda`` or ``C:\Users\my-username\conda``).

常规安装
====================

Regular installation

.. tab:: 中文

    按照您的操作系统的说明进行操作:

    * :doc:`Windows <windows>`
    * :doc:`macOS <macos>`
    * :doc:`Linux <linux>`

.. tab:: 英文

    Follow the instructions for your operating system:

    * :doc:`Windows <windows>`
    * :doc:`macOS <macos>`
    * :doc:`Linux <linux>`


静默安装
=========================

Installing in silent mode

.. tab:: 中文

    你可以使用 :ref:`静默安装 <silent-mode-glossary>` 方式部署或测试 Miniconda、Anaconda 或 Miniforge，或用于构建服务（如 GitHub Actions）。

    请根据操作系统查阅对应的静默模式安装指南：

.. tab:: 英文

    You can use :ref:`silent installation <silent-mode-glossary>` of
    Miniconda, Anaconda, or Miniforge for deployment or testing or building
    services, such as GitHub Actions.

    Follow the silent-mode instructions for your operating system:

* :ref:`Windows <install-win-silent>`
* :ref:`macOS <install-macos-silent>`
* :ref:`Linux <install-linux-silent>`


.. _hash-verification:

加密哈希验证
===============================

Cryptographic hash verification

.. tab:: 中文

    `Miniconda <https://docs.anaconda.com/miniconda/>`__ 和 `Anaconda Distribution <https://docs.anaconda.com/anaconda/hashes/>`__ 提供 SHA-256 校验和。我们不推荐使用 MD5 校验方式，因为 SHA-256 更安全。
    
    下载安装文件后，在安装前请使用如下方法进行校验：
    
    * Windows：
    
      * 如果你安装了 PowerShell V4 或更高版本：
    
        打开 PowerShell 控制台并运行以下命令进行校验::
    
          Get-FileHash filename -Algorithm SHA256
    
      * 如果未安装 PowerShell V4 或更高版本：
    
        可使用 Microsoft 网站提供的免费 `在线校验工具
        <https://gallery.technet.microsoft.com/PowerShell-File-Checksum-e57dcd67>`_。
    
        #. 下载该工具并解压。
    
        #. 打开命令提示符窗口。
    
        #. 切换到包含目标文件的目录。
    
        #. 运行以下命令::
    
            Start-PsFCIV -Path C:\path\to\file.ext -HashAlgorithm SHA256 -Online
    
    * macOS：在 iTerm 或终端中输入 ``shasum -a 256 filename``。
    
    * Linux：在终端中输入 ``sha256sum filename``。

.. tab:: 英文

    SHA-256 checksums are available for
    `Miniconda <https://docs.anaconda.com/miniconda/>`__ and
    `Anaconda Distribution <https://docs.anaconda.com/anaconda/hashes/>`__.
    We do not recommend using MD5 verification as SHA-256 is more secure.
    
    Download the installer file and, before installing, verify it as follows:
    
    * Windows:
    
      * If you have PowerShell V4 or later:
    
        Open a PowerShell console and verify the file as follows::
    
          Get-FileHash filename -Algorithm SHA256
    
      * If you don't have PowerShell V4 or later:
    
        Use the free `online verifier tool
        <https://gallery.technet.microsoft.com/PowerShell-File-Checksum-e57dcd67>`_
        on the Microsoft website.
    
        #. Download the file and extract it.
    
        #. Open a Command Prompt window.
    
        #. Navigate to the file.
    
        #. Run the following command::
    
            Start-PsFCIV -Path C:\path\to\file.ext -HashAlgorithm SHA256 -Online
    
    * macOS: In iTerm or a terminal window enter ``shasum -a 256 filename``.
    
    * Linux: In a terminal window enter ``sha256sum filename``.

.. toctree::
   :maxdepth: 1
   :hidden:

   windows
   macos
   linux
   rpm-debian
