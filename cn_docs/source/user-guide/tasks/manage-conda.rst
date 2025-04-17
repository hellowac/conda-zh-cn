==============
管理 conda
==============

Managing conda

.. tab:: 中文

.. tab:: 英文

验证 conda 是否已安装
=================================

Verifying that conda is installed

.. tab:: 中文

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
