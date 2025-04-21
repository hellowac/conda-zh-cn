==============
管理 conda
==============

Managing conda

验证 conda 是否已安装
=================================

Verifying that conda is installed

.. tab:: 中文

   要验证是否已安装 conda，请在终端窗口中运行：

   .. code::

      conda --version

   Conda 将输出已安装的版本号，例如 ``conda 4.12.0``。

   如果你收到错误信息，请确认以下事项：

   * 你已登录到安装 Anaconda 或 Miniconda 时所用的用户账户。

   * 当前所在的目录可以被 Anaconda 或 Miniconda 检测到。

   * 安装 conda 后你已经关闭并重新打开了终端窗口。

.. tab:: 英文

   To verify that conda is installed, in your terminal window, run:
   
   .. code::
   
      conda --version
   
   Conda responds with the version number that you have installed,
   such as ``conda 4.12.0``.
   
   If you get an error message, make sure of the following:
   
   * You are logged into the same user account that you used to
     install Anaconda or Miniconda.
   
   * You are in a directory that Anaconda or Miniconda can find.
   
   * You have closed and re-opened the terminal window after
     installing conda.


确定您的 conda 版本
==============================

Determining your conda version

.. tab:: 中文

   除了上述的 ``conda --version`` 命令，你还可以通过运行以下命令之一来查看已安装的 conda 版本：

   .. code-block:: bash

      conda info

   或

   .. code-block:: bash

      conda -V

.. tab:: 英文

   In addition to the ``conda --version`` command explained above,
   you can determine what conda version is installed by running
   one of the following commands in your terminal window:

   .. code-block:: bash

      conda info

   OR

   .. code-block:: bash

      conda -V


将 conda 更新至当前版本
=====================================

Updating conda to the current version

.. tab:: 中文

   要更新 conda，请在终端窗口中运行：

   .. code::

      conda update conda

   Conda 会比较当前版本与可用版本，并报告有哪些内容可供安装。它还会告知此次更新将自动更新或更改的其他软件包。如果 conda 报告有新版本可用，输入 ``y`` 以进行更新：

   .. code::

      Proceed ([y]/n)? y

.. tab:: 英文

   To update conda, in your terminal window, run:

   .. code::

      conda update conda

   Conda compares versions and reports what is available to install.
   It also tells you about other packages that will be automatically
   updated or changed with the update. If conda reports that a newer
   version is available, type ``y`` to update:

   .. code::

      Proceed ([y]/n)? y


隐藏有关更新 conda 的警告消息
================================================

Suppressing warning message about updating conda

.. tab:: 中文

   当你不希望更新到最新版本时，可以通过以下方式关闭相关的警告信息：

   .. code-block::

      ==> WARNING: A newer version of conda exists. <==
      current version: 4.6.13
      latest version: 4.8.0

   更新 conda 的方式是运行：``conda update -n base conda``

   从终端运行以下命令以关闭该提示：
   ``conda config --set notify_outdated_conda false``

   或在你的 ``.condarc`` 文件中添加以下配置行：
   ``notify_outdated_conda: false``

.. tab:: 英文

   To suppress the following warning message when you do not want
   to update conda to the latest version:

   .. code-block::

      ==> WARNING: A newer version of conda exists. <==
      current version: 4.6.13
      latest version: 4.8.0

   Update conda by running: ``conda update -n base conda``

   Run the following command from your terminal:
   ``conda config --set notify_outdated_conda false``

   Or add the following line in your ``.condarc`` file:
   ``notify_outdated_conda: false``
