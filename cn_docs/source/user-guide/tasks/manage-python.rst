===============
管理 Python
===============

Managing Python

.. tab:: 中文

.. tab:: 英文

Conda treats Python the same as any other package, so it is easy
to manage and update multiple installations.

Conda supports Python 3.9, 3.10, 3.11 and 3.12.

查看可用的 Python 版本列表
===========================================

Viewing a list of available Python versions

.. tab:: 中文

.. tab:: 英文

To list the versions of Python that are available to install,
in your terminal window, run::

    conda search python

This lists all packages whose names contain the text ``python``.

To list only the packages whose full name is exactly ``python``,
add the ``--full-name`` option. In your terminal window, run::

    conda search --full-name python


安装其他版本的 Python
=========================================

Installing a different version of Python

.. tab:: 中文

.. tab:: 英文

To install a different version of Python without overwriting the
current version, create a new environment and install the second
Python version into it:

#. Create the new environment:

   * To create the new environment for Python 3.9, in your terminal
     window run:

     .. code-block:: bash

        conda create -n py39 python=3.9

     .. note::
        Replace ``py39`` with the name of the environment you
        want to create. ``python=3.9`` is the package and version you
        want to install in this new environment. This could be any
        package, such as ``numpy=1.19``, or :ref:`multiple packages
        <installing multiple packages>`.

#. :ref:`Activate the new environment <activate-env>`.

#. Verify that the new environment is your :ref:`current
   environment <determine-current-env>`.

#. To verify that the current environment uses the new Python
   version, in your terminal window, run:

   .. code::

      python --version

安装 PyPy
===============

Installing PyPy

.. tab:: 中文

.. tab:: 英文

To use the PyPy builds you can do the following::

    conda config --add channels conda-forge
    conda config --set channel_priority strict
    conda create -n pypy pypy
    conda activate pypy


使用其他版本的 Python
====================================

Using a different version of Python

.. tab:: 中文

.. tab:: 英文

To switch to an environment that has different version of Python,
:ref:`activate the environment <activate-env>`.


更新 Python
===============

Updating Python

.. tab:: 中文

.. tab:: 英文

To update Python to the latest version in your environment, run::

    conda update python

This command will update you to the latest major release (e.g. from ``python=3.10`` to ``python=3.12``).

If you would like to remain on a minor release, use the ``conda install`` command instead::

    conda install python=3.10
