:py:mod:`pip_util`
==================

.. py:module:: conda.env.pip_util

.. autoapi-nested-parse::

   Functions related to core conda functionality that relates to pip

   NOTE: This modules used to in conda, as conda/pip.py




Functions
---------

.. autoapisummary::

   conda.env.pip_util.pip_subprocess
   conda.env.pip_util.get_pip_installed_packages



.. py:function:: pip_subprocess(args, prefix, cwd)

   Run pip in a subprocess


.. py:function:: get_pip_installed_packages(stdout)

   Return the list of pip packages installed based on the command output


