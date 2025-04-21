===================
在 Linux 上安装
===================

Installing on Linux

.. tab:: 中文
   
   #. 下载安装程序：
   
      * `适用于 Linux 的 Miniconda 安装程序 <https://docs.anaconda.com/miniconda/>`__。
   
      * `适用于 Linux 的 Anaconda Distribution 安装程序 <https://www.anaconda.com/download/>`__。
   
      * `适用于 Linux 的 Miniforge 安装程序 <https://conda-forge.org/download/>`_。
   
   #. :ref:`校验安装程序哈希值 <hash-verification>`。
   
   #. 在终端窗口中运行以下命令：
   
      .. code::
   
         bash <conda-installer-name>-latest-Linux-x86_64.sh
   
      ``conda-installer-name`` 可能是 "Miniconda3"、"Anaconda" 或 "Miniforge3" 中的一个。
   
   #. 按照安装程序界面中的提示操作。如果对某项设置不确定，可直接接受默认值。之后也可以进行更改。
   
   #. 为使更改生效，请关闭并重新打开你的终端窗口。
   
   #. 测试 conda 是否安装成功。在终端中运行命令 ``conda list``。  
      如果安装正确，将会列出已安装的软件包。

.. tab:: 英文

   #. Download the installer:
   
      * `Miniconda installer for Linux <https://docs.anaconda.com/miniconda/>`__.
   
      * `Anaconda Distribution installer for Linux <https://www.anaconda.com/download/>`__.
   
      * `Miniforge installer for Linux <https://conda-forge.org/download/>`_.
   
   #. :ref:`Verify your installer hashes <hash-verification>`.
   
   #. In your terminal window, run:
   
      .. code::
   
         bash <conda-installer-name>-latest-Linux-x86_64.sh
   
      ``conda-installer-name`` will be one of "Miniconda3", "Anaconda", or "Miniforge3".
   
   #. Follow the prompts on the installer screens. If you are unsure about any setting, accept the defaults. You
      can change them later.
   
   #. To make the changes take effect, close and then re-open your
      terminal window.
   
   #.  Test your installation. In your terminal window, run the command ``conda list``.
       A list of installed packages appears if it has been installed correctly.


.. _install-linux-silent:

使用 fish shell
=====================

Using with fish shell

.. tab:: 中文

   要在 fish shell 中使用 conda，请在终端中执行以下命令：

   将 conda 可执行路径添加至 $PATH （如果尚未添加）::

         fish_add_path <conda-install-location>/condabin

   配置 fish shell 支持::

         conda init fish

.. tab:: 英文

   To use conda with fish shell, run the following in your terminal:

   Add conda binary to $PATH, if not yet added::

         fish_add_path <conda-install-location>/condabin


   Configure fish-shell::

         conda init fish

静默安装
=========================

Installing in silent mode

.. tab:: 中文

   请参阅 :ref:`在 macOS 上以静默模式安装 <install-macos-silent>` 的说明。

.. tab:: 英文

   See the instructions for :ref:`installing in silent mode on macOS <install-macos-silent>`.


更新 conda
==============

Updating conda

.. tab:: 中文

   #. 打开1个终端创窗口.

   #. 运行 ``conda update conda``.

.. tab:: 英文

   #. Open a terminal window.

   #. Run ``conda update conda``.


卸载 conda
==================

Uninstalling conda

.. tab:: 中文

   #. 打开一个终端窗口。
   
   #. 删除整个 conda 安装目录（*路径可能根据你的安装位置有所不同*）::
   
        rm -rf ~/conda
   
   #. *可选项*：运行 ``conda init --reverse --all``，以撤销对 shell 初始化脚本所做的更改。
   
   #. *可选项*：删除可能已创建在主目录中的以下隐藏文件和文件夹：
   
      * ``.condarc`` 文件  
      * ``.conda`` 目录  
      * ``.continuum`` 目录
   
      可通过以下命令统一删除::
   
        rm -rf ~/.condarc ~/.conda ~/.continuum

.. tab:: 英文

   #. Open a terminal window.
   
   #. Remove the entire conda install directory with (*this may differ*
      *depending on your installation location*) ::
   
        rm -rf ~/conda
   
   #. *Optional*: run ``conda init --reverse --all`` to undo changes to shell initialization scripts
   
   #. *Optional*: remove the following hidden file and folders that
      may have been created in the home directory:
   
      * ``.condarc`` file
      * ``.conda`` directory
      * ``.continuum`` directory
   
      By running::
   
        rm -rf ~/.condarc ~/.conda ~/.continuum
