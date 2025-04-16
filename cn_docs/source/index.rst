===================
Conda 文档
===================

Conda Documentation

.. tab:: 中文

    欢迎使用 conda 文档！Conda 为所有语言提供包、依赖项和环境管理功能。在这里，您可以找到在自己的项目中使用 conda 所需的一切。

.. tab:: 英文

    Welcome to conda's documentation! Conda provides package, dependency, and environment management for any language. Here, you will find everything you need to get started using conda in your own projects.

安装  :octicon:`download;1em;sd-text-primary`
................................................

Install  :octicon:`download;1em;sd-text-primary`

.. tab:: 中文

    我们建议使用以下 conda 发行版来安装 conda：
    
    .. grid:: 2
    
        .. grid-item-card:: Miniconda
    
            `Miniconda <https://docs.anaconda.com/miniconda>`__ 是由 `Anaconda <https://anaconda.com/>`__ 开发的安装程序，已预先配置好与 Anaconda 仓库配合使用。请参阅 Anaconda 的 :ref:`服务条款 <anaconda-tos_notes>` 的说明。
    
            .. button-link:: https://repo.anaconda.com/miniconda/Miniconda3-latest-Windows-x86_64.exe
                :color: primary
    
                :fab:`windows` Windows :bdg-light-line:`x86_64` :octicon:`download`
    
            .. button-link:: https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.pkg
                :color: primary
    
                :fab:`apple` macOS :bdg-light-line:`arm64 (Apple Silicon)` :octicon:`download`
    
            .. button-link:: https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.pkg
                :color: primary
    
                :fab:`apple` macOS :bdg-light-line:`x86_64 (Intel)` :octicon:`download`
    
            .. button-link:: https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
                :color: primary
    
                :fab:`linux` Linux :bdg-light-line:`x86_64 (amd64)` :octicon:`download`
    
            .. button-link:: https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-aarch64.sh
                :color: primary
    
                :fab:`linux` Linux :bdg-light-line:`aarch64 (arm64)` :octicon:`download`
    
            ++++
    
            或者 :fa:`beer-mug-empty` `Homebrew <https://brew.sh/>`__:
    
            .. code-block:: bash
    
                brew install miniconda
    
        .. grid-item-card:: Miniforge
    
            Miniforge 是由 `conda-forge 社区 <https://conda-forge.org>`__ 维护的安装程序，已预先配置为与 conda-forge 频道一起使用。
    
            .. button-link:: https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Windows-x86_64.exe
                :color: primary
    
                :fab:`windows` Windows :bdg-light-line:`x86_64` :octicon:`download`
    
            .. button-link:: https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-MacOSX-arm64.sh
                :color: primary
    
                :fab:`apple` macOS :bdg-light-line:`arm64 (Apple Silicon)` :octicon:`download`
    
            .. button-link:: https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-MacOSX-x86_64.sh
                :color: primary
    
                :fab:`apple` macOS :bdg-light-line:`x86_64 (Intel)` :octicon:`download`
    
            .. button-link:: https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh
                :color: primary
    
                :fab:`linux` Linux :bdg-light-line:`x86_64 (amd64)` :octicon:`download`
    
            .. button-link:: https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-aarch64.sh
                :color: primary
    
                :fab:`linux` Linux :bdg-light-line:`aarch64 (arm64)` :octicon:`download`
    
            +++
    
            或者 :fa:`beer-mug-empty` `Homebrew <https://brew.sh/>`__:
    
            .. code-block:: bash
    
                brew install miniforge


    .. raw:: html

        <p class="text-small">如需更详细的信息, 见 <a href="https://docs.anaconda.com/miniconda/" target="_blank">Miniconda的安装指南</a> 和
        <a href="https://conda-forge.org/download/" target="_blank">conda-forge的下载页</a></p>.

.. tab:: 英文

    We recommend the following conda distribtions to install conda:
    
    .. grid:: 2
    
        .. grid-item-card:: Miniconda
    
            `Miniconda <https://docs.anaconda.com/miniconda>`__ is an installer
            by `Anaconda <https://anaconda.com/>`__ that comes
            preconfigured for use with the Anaconda Repository. See the
            notes about Anaconda's :ref:`Terms of Service <anaconda-tos_notes>`.
    
            .. button-link:: https://repo.anaconda.com/miniconda/Miniconda3-latest-Windows-x86_64.exe
                :color: primary
    
                :fab:`windows` Windows :bdg-light-line:`x86_64` :octicon:`download`
    
            .. button-link:: https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.pkg
                :color: primary
    
                :fab:`apple` macOS :bdg-light-line:`arm64 (Apple Silicon)` :octicon:`download`
    
            .. button-link:: https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.pkg
                :color: primary
    
                :fab:`apple` macOS :bdg-light-line:`x86_64 (Intel)` :octicon:`download`
    
            .. button-link:: https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
                :color: primary
    
                :fab:`linux` Linux :bdg-light-line:`x86_64 (amd64)` :octicon:`download`
    
            .. button-link:: https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-aarch64.sh
                :color: primary
    
                :fab:`linux` Linux :bdg-light-line:`aarch64 (arm64)` :octicon:`download`
    
            ++++
    
            Or with :fa:`beer-mug-empty` `Homebrew <https://brew.sh/>`__:
    
            .. code-block:: bash
    
                brew install miniconda
    
        .. grid-item-card:: Miniforge
    
            Miniforge is an installer maintained by the `conda-forge community <https://
            conda-forge.org>`__ that comes preconfigured for use with the conda-forge
            channel.
    
            .. button-link:: https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Windows-x86_64.exe
                :color: primary
    
                :fab:`windows` Windows :bdg-light-line:`x86_64` :octicon:`download`
    
            .. button-link:: https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-MacOSX-arm64.sh
                :color: primary
    
                :fab:`apple` macOS :bdg-light-line:`arm64 (Apple Silicon)` :octicon:`download`
    
            .. button-link:: https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-MacOSX-x86_64.sh
                :color: primary
    
                :fab:`apple` macOS :bdg-light-line:`x86_64 (Intel)` :octicon:`download`
    
            .. button-link:: https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh
                :color: primary
    
                :fab:`linux` Linux :bdg-light-line:`x86_64 (amd64)` :octicon:`download`
    
            .. button-link:: https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-aarch64.sh
                :color: primary
    
                :fab:`linux` Linux :bdg-light-line:`aarch64 (arm64)` :octicon:`download`
    
            +++
    
            Or with :fa:`beer-mug-empty` `Homebrew <https://brew.sh/>`__:
    
            .. code-block:: bash
    
                brew install miniforge


    .. raw:: html

        <p class="text-small">For more detailed instructions, see <a href="https://docs.anaconda.com/miniconda/" target="_blank">Miniconda's installation guide</a> and
        <a href="https://conda-forge.org/download/" target="_blank">conda-forge's download site</a></p>.

刚接触 conda？:octicon:`rocket;1em;sd-text-primary`
...................................................

New to conda? :octicon:`rocket;1em;sd-text-primary`

.. tab:: 中文

    如果你是刚接触conda，我们首先推荐以下文章：
    
    .. grid:: 1 2 2 2
        :gutter: 2
    
        .. grid-item-card:: 入门指南 :octicon:`rocket;1em;sd-text-primary`
            :link: /user-guide/getting-started/
            :link-type: doc
    
            学习使用 conda 的基础知识，例如创建包并将其添加到环境中
    
        .. grid-item-card:: 管理环境 :octicon:`file-submodule;1em;sd-text-primary`
            :link: /user-guide/tasks/manage-environments/
            :link-type: doc
    
            了解有关环境以及在项目中使用它们的最佳实践的更多信息
    
    .. seealso::
    
        想要免费获得更深入的 conda 使用培训吗？查看 Anaconda 的 `conda 基础免费课程 <https://learning.anaconda.cloud/conda-basics>`_ 。

.. tab:: 英文

    If you are new to conda, we first recommend the following articles:
    
    .. grid:: 1 2 2 2
        :gutter: 2
    
        .. grid-item-card:: Getting started guide :octicon:`rocket;1em;sd-text-primary`
            :link: /user-guide/getting-started/
            :link-type: doc
    
            Learn the basics of using conda such as creating and adding packages to environments
    
        .. grid-item-card:: Managing environments :octicon:`file-submodule;1em;sd-text-primary`
            :link: /user-guide/tasks/manage-environments/
            :link-type: doc
    
            Learn more about environments and best practices for using them in your projects
    
    .. seealso::
    
        Want to get even more in-depth training on how to use conda for free? Check out Anaconda's
        `free course on conda basics <https://learning.anaconda.cloud/conda-basics>`_.
    
其他有用资源 :octicon:`light-bulb;1em;sd-text-primary`
......................................................................

Other useful resources :octicon:`light-bulb;1em;sd-text-primary`

.. tab:: 中文

    .. grid:: 1 2 2 2
        :gutter: 2

        .. grid-item-card:: 命令参考 :octicon:`terminal;1em;sd-text-primary`
            :link: /commands/index/
            :link-type: doc

            所有标准命令和选项的完整参考

        .. grid-item-card:: 备忘录 :octicon:`note;1em;sd-text-primary`
            :link: /user-guide/cheatsheet/
            :link-type: doc

            获取常用命令的最新速查表

        .. grid-item-card:: 配置 conda :octicon:`gear;1em;sd-text-primary`
            :link: /user-guide/configuration/use-condarc/
            :link-type: doc

            了解配置 conda 行为的各种方式

        .. grid-item-card:: 术语 :octicon:`book;1em;sd-text-primary`
            :link: /glossary/
            :link-type: doc

            使用 conda 时需要了解的重要词汇

.. tab:: 英文

    .. grid:: 1 2 2 2
        :gutter: 2

        .. grid-item-card:: Command reference :octicon:`terminal;1em;sd-text-primary`
            :link: /commands/index/
            :link-type: doc

            Full reference for all standard commands and options

        .. grid-item-card:: Cheatsheets :octicon:`note;1em;sd-text-primary`
            :link: /user-guide/cheatsheet/
            :link-type: doc

            Get the latest cheatsheet for commonly used commands

        .. grid-item-card:: Configuring conda :octicon:`gear;1em;sd-text-primary`
            :link: /user-guide/configuration/use-condarc/
            :link-type: doc

            Learn about the various ways conda's behavior can be configured

        .. grid-item-card:: Glossary :octicon:`book;1em;sd-text-primary`
            :link: /glossary/
            :link-type: doc

            Important vocabulary to know when working with conda


欢迎贡献者 :octicon:`git-pull-request;1em;sd-text-primary`
....................................................................

Contributors welcome :octicon:`git-pull-request;1em;sd-text-primary`

.. tab:: 中文

    Conda 是一个开源项目，始终欢迎新的贡献。请阅读以下指南，开始开发 conda 并做出您自己的贡献。

    .. grid:: 1 2 2 2
        :gutter: 2

        .. grid-item-card:: Contributing 101 :octicon:`people;1em;sd-text-primary`
            :link: /dev-guide/contributing/
            :link-type: doc

            详细了解 conda 项目的管理方式和贡献方式

        .. grid-item-card:: Development environment :octicon:`file-code;1em;sd-text-primary`
            :link: /dev-guide/development-environment/
            :link-type: doc

            按照本指南设置您自己的开发环境

.. tab:: 英文

    Conda is an open source project and always welcomes new contributions.
    Please read the following guides to get started developing conda and
    making your own contributions.

    .. grid:: 1 2 2 2
        :gutter: 2

        .. grid-item-card:: Contributing 101 :octicon:`people;1em;sd-text-primary`
            :link: /dev-guide/contributing/
            :link-type: doc

            Learn more about how the conda project is managed and how to contribute

        .. grid-item-card:: Development environment :octicon:`file-code;1em;sd-text-primary`
            :link: /dev-guide/development-environment/
            :link-type: doc

            Follow this guide to get your own development environment set up



.. toctree::
   :hidden:
   :maxdepth: 1
   :titlesonly:

   user-guide/index
   configuration
   commands/index
   release-notes
   glossary
   dev-guide/index
   api/index

.. |reg|    unicode:: U+000AE .. REGISTERED SIGN
