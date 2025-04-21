=======
插件
=======

Plugins

.. _concept-plugins:

.. tab:: 中文

   为了实现与 Conda 兼容且可被 Conda 发现的自定义功能和扩展特性（这些功能不一定作为 Conda 代码库的默认组成部分发布），从 Conda 版本 ``22.11.0`` 开始，官方引入了一套插件机制。

.. tab:: 英文


   In order to enable customization and extra features that are compatible with and discoverable by conda
   (but do not necessarily ship as a default part of the conda codebase), an official conda plugin mechanism
   has been implemented as of version ``22.11.0``.

实现
==============

Implementation

.. tab:: 中文

   Conda 插件采用了由 Pluggy_ Python 框架实现的 “钩子（hook）+ 入口点（entry point）” 结构。其实现大致可分为以下两个步骤：

   * 定义要注册的钩子函数；
   * 在 Conda 的入口点命名空间下注册插件。

.. tab:: 英文

   Plugins in conda integrate the "hook + entry point" structure by utilizing the Pluggy_ Python framework.
   This implementation can be broken down via the following two steps:

   * Define the hook(s) to be registered
   * Register the plugin under the conda entrypoint namespace

钩子
----

Hook

.. tab:: 中文

   下面是一个非常基础的插件钩子示例：

   .. code-block:: python
      :caption: my_plugin.py

      import conda.plugins

      @conda.plugins.hookimpl
      def conda_subcommands(): ...

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

   以下是使用 ``pyproject.toml`` 配置 ``setuptools`` 的示例（如果已定义 ``pyproject.toml``，则 ``setup.py`` 文件是可选的，因此此处不再赘述）：

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

   全新的 Conda 插件 API 生态为扩展 Conda 功能带来了广阔的可能性，包括但不限于：

   * :doc:`自定义子命令 <../../dev-guide/plugins/subcommands>`
   * 支持与打包相关的功能（例如 :doc:`虚拟包 <../../dev-guide/plugins/virtual_packages>`）
   * 开发环境集成（例如与 shell 集成）
   * 替代性依赖求解器后端
   * 网络适配器
   * 构建系统集成
   * 非 Python 语言支持（如 C、Rust 等）
   * 当前 Conda 尚未涵盖的实验性功能

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

   Conda 插件生态系统使整个 Conda 社区的贡献者能够开发并共享新功能，从而实现更丰富的功能并提升用户体验。虽然以下列表并不全面，但 Conda 插件带来的主要优势包括：

   * 有助于在 Conda 社区内实现更合理的维护职责分配；
   * 使第三方贡献者能够使用官方 API，而不必依赖 hack 或包装器；
   * 通过官方 API 扩展 Conda 内部功能；
   * 降低 Conda 生态中其他参与者的贡献门槛；
   * ……以及更多可能！

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
