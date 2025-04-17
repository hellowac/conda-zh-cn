=======
插件
=======

Plugins

.. tab:: 中文

.. tab:: 英文

.. _concept-plugins:


In order to enable customization and extra features that are compatible with and discoverable by conda
(but do not necessarily ship as a default part of the conda codebase), an official conda plugin mechanism
has been implemented as of version ``22.11.0``.

实现
==============

Implementation

.. tab:: 中文

.. tab:: 英文

Plugins in conda integrate the "hook + entry point" structure by utilizing the Pluggy_ Python framework.
This implementation can be broken down via the following two steps:

* Define the hook(s) to be registered
* Register the plugin under the conda entrypoint namespace

钩子
----

Hook

.. tab:: 中文

.. tab:: 英文

Below is an example of a very basic plugin "hook":

.. code-block:: python
   :caption: my_plugin.py

   import conda.plugins


   @conda.plugins.hookimpl
   def conda_subcommands(): ...


使用 pyproject.toml 文件打包
-------------------------------------

Packaging using a pyproject.toml file

.. tab:: 中文

.. tab:: 英文

Below is an example that configures ``setuptools`` using a ``pyproject.toml`` file (note that the
``setup.py`` file is optional if a ``pyproject.toml`` file is defined, and thus will not be discussed here):

.. code-block:: toml
   :caption: pyproject.toml

   [build-system]
   requires = ["setuptools", "setuptools-scm"]
   build-backend = "setuptools.build_meta"

   [project]
   name = "my-conda-plugin"
   version = "1.0.0"
   description = "My conda plugin"
   requires-python = ">=3.7"
   dependencies = ["conda"]

   [project.entry-points."conda"]
   my-conda-plugin = "my_plugin"


Conda 插件用例
=======================

Conda plugins use cases

.. tab:: 中文

.. tab:: 英文

The new conda plugin API ecosystem brings about many possibilities, including but not limited to:

* :doc:`Custom subcommands <../../dev-guide/plugins/subcommands>`
* Support for packaging-related topics (*e.g.*, :doc:`virtual packages <../../dev-guide/plugins/virtual_packages>`)
* Development environment integrations (*e.g.*, shells)
* Alternative dependency solver backends
* Network adapters
* Build system integrations
* Non-Python language support (*e.g.*, C, Rust)
* Experimental features that are not currently covered by conda


Conda 插件的优势
=========================

Benefits of conda plugins

.. tab:: 中文

.. tab:: 英文

A conda plugin ecosystem enables contributors across the conda community to develop and share new features,
thus bringing about more functionality and focus on the user experience. Though the list below is by no means
exhaustive, some of the benefits of conda plugins include:

* Support for a better distribution of maintenance in the conda community
* Enabling third party contributors to use official APIs instead of having to divert to workarounds and wrappers
* The ability to extend conda internals via official APIs
* Lowering the barrier for contributions from other stakeholders in the conda ecosystem
* ... and much more!

.. _Pluggy: https://pluggy.readthedocs.io/en/stable/
