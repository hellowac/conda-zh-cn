===========
性能
===========

Performance

.. tab:: 中文

    Conda 的性能可能受到多种因素的影响。与许多软件包管理器不同，Anaconda 的仓库通常不会过滤或移除旧版本的软件包，以便于用户可以轻松地重建旧环境。但这也意味着索引元数据会不断增长，随着软件包数量的增加，conda 的速度可能会变慢。

.. tab:: 英文

    Conda's performance can be affected by a variety of things.
    Unlike many package managers, Anaconda’s repositories generally
    don’t filter or remove old packages from the index. This allows old
    environments to be easily recreated. However, it does mean that the
    index metadata is always growing, and thus conda becomes slower as the
    number of packages increases.

软件包的安装方式
==========================

How a package is installed

.. tab:: 中文

    在安装软件包的过程中，conda 实际上正在执行一系列复杂的操作，在这些步骤的任何一个阶段都可能出现性能瓶颈。

    Conda 在安装软件包时遵循以下步骤：

    1. 下载并处理索引元数据；
    2. 缩减索引范围；
    3. 将软件包数据与约束表达为 SAT 问题；
    4. 运行求解器；
    5. 下载并解压软件包；
    6. 验证软件包内容；
    7. 将软件包从缓存链接到环境中。

    因此，当你遇到性能变慢时，可以从以下几个方面排查潜在原因：

    * 是在创建新环境还是在已有环境中安装？
    * 环境中是否包含通过 pip 安装的依赖？
    * 使用了哪些渠道？
    * 正在安装哪些软件包？
    * 渠道元数据是否正常？
    * 渠道之间是否存在不良交互？

.. tab:: 英文

    While you are waiting, conda is doing a lot of work installing the
    packages. At any point along these steps, performance issues may arise.

    Conda follows these steps when installing a package:

    #. Downloading and processing index metadata.
    #. Reducing the index.
    #. Expressing the package data and constraints as a SAT problem.
    #. Running the solver.
    #. Downloading and extracting packages.
    #. Verifying package contents.
    #. Linking packages from package cache into environments.

    Therefore, if you're experiencing a slowdown, evaluate the following questions
    to identify potential causes:

    * Are you creating a new environment or installing into an existing one?
    * Does your environment have pip-installed dependencies in it?
    * What channels are you using?
    * What packages are you installing?
    * Is the channel metadata sane?
    * Are channels interacting in bad ways?


提升 conda 性能
===========================

Improving conda performance

.. tab:: 中文

    为应对这些挑战，你可以将部分包转移至归档渠道，并采用以下方法，将 condа 需要处理的包视图尽可能简化：
    
    以下是我们提升 conda 性能的一些建议：
    
    你是否：
      * 正在使用 conda-forge？
        * 使用 `conda-metachannel` 工具缩小 condа 的问题规模。
      * 正在使用 bioconda？
        * 同样建议使用 `conda-metachannel`。
        * 可阅读此内容了解更多：`docker 镜像说明 <https://github.com/bioconda/bioconda-recipes/issues/13774>`_。
      * 使用了过于宽泛的包规格？
        * 建议更具体一些。指定更明确的版本号可减少候选项，使求解更快。
          例如，不要只写 ``numpy``，而应使用 ``numpy=1.15``，甚至 ``numpy=1.15.4``。
        * 使用 R 时，不要只写 ``r-essentials``，而应写成 ``r-base=3.5 r-essentials``。
      * 对 “verifying transaction” 步骤感到卡顿，并想冒点风险？
        * 可执行： ``conda config --set safety_checks disabled``。
      * 遇到默认渠道与 conda-forge 混用导致的问题？
        * 执行： ``conda config --set channel_priority strict``。
        * 这不仅能避免混用，还能提升求解速度。
      * 发现 Anaconda 或 Miniconda 安装随时间推移变慢？
        * 建议新建环境。随着环境的膨胀，求解过程也会变得更加复杂。使用小型、专用环境往往更加高效。

    阅读更多关于《 `我们如何让 conda 更快（4.7 版本） <https://www.anaconda.com/how-we-made-conda-faster-4-7/>`_ 》。

.. tab:: 英文

    To address these challenges, you can move packages to archive
    channels and follow the methods below to present conda with a smaller, simpler view than
    all available packages.

    To speed up conda, we offer the following recommendations.

    Are you:
        * Using conda-forge?
            * Use conda-metachannel to reduce conda’s problem size.
        * Using bioconda?
            * Use conda-metachannel to reduce conda’s problem size.
            * `Read more about docker images <https://github.com/bioconda/bioconda-recipes/issues/13774>`_.
        * Specifying very broad package specs?
            * Be more specific. Letting conda filter more candidates makes it faster.
            For example, instead of ``numpy``, we recommend ``numpy=1.15`` or, even better, ``numpy=1.15.4``.
            * If you are using R, instead of specifying only ``r-essentials``, specify ``r-base=3.5 r-essentials``.
        * Feeling frustrated with “verifying transaction” and also feeling lucky?
            * Run ``conda config --set safety_checks disabled``.
        * Getting strange mixtures of defaults and conda-forge?
            * Run ``conda config --set channel_priority strict``.
            * This also makes things go faster by eliminating possible mixed solutions.
        * Observing that an Anaconda or Miniconda installation is getting slower over time?
            * Create a fresh environment. As environments grow, they become harder
            and harder to solve. Working with small, dedicated environments can
            be much faster.

    Read more about `how we made conda faster <https://www.anaconda.com/how-we-made-conda-faster-4-7/>`_.

.. _concepts-performance-channel-priority:

设置严格的通道优先级
---------------------------

Set strict channel priority

.. tab:: 中文

    设置 strict channel priority（严格渠道优先级）后，如果某个软件包在高优先级渠道中已存在，conda 会忽略所有低优先级渠道中同名的软件包。

    .. figure:: ../../img/strict-disabled.png
       :width: 50%
    .. figure:: ../../img/strict-enabled.png
       :width: 50%

    这种做法可以显著缩小软件包搜索空间，并减少使用约束不足的软件包。

    但也需要注意：设置严格优先级可能会导致某些环境无法解析。详见 :ref:`strict`。

.. tab:: 英文

    Setting strict channel priority makes it so that if a package exists on
    a channel, conda will ignore all packages with the same name on lower
    priority channels.
    
    .. figure:: ../../img/strict-disabled.png
        :width: 50%
    .. figure:: ../../img/strict-enabled.png
        :width: 50%
    
    This can dramatically reduce package search space and reduces the use of
    improperly constrained packages.
    
    One thing to consider is that setting strict channel priority may make
    environments unsatisfiable. Learn more about :ref:`strict`.


缩减索引
----------------

Reduce the index

.. tab:: 中文

    加快 conda 的另一种方法是缩减索引范围。conda 会根据用户的输入规格（spec）来裁剪索引，但通常 repodata 中包含了许多并不会实际参与求解的数据。提前过滤掉这些无关数据可以节省时间。

    使你的输入规格更具体，会提升索引裁剪的效果，从而加快整体流程。为每个包指定具体的版本与构建号可以显著减少参与求解的包数，从而降低 SAT 问题的复杂度。

    缩减索引的好处包括：

    * 减少用于生成求解子句的冗余输入；
    * 降低求解的复杂度；
    * 偏向选择符合约束的新版本软件包。

    阅读更多内容请参见《`理解并提升 Conda 的性能 <https://www.anaconda.com/understanding-and-improving-condas-performance/>`_》。
    
.. tab:: 英文
    
    One option for speeding up conda is to reduce the index. The index is
    reduced by conda based upon the user's input specs. It's likely that
    your repodata contains package data that is not used in the solving stage.
    Filtering out these unnecessary packages before solving can save time.
    
    Making your input specifications more specific improves
    the effectiveness of the index reduction and, thus, speeds up the
    process. Listing a version and build string for each of your specs can
    dramatically reduce the number of packages that are considered when solving
    so that the SAT doesn’t have as much work to do.
    
    Reducing the index:
      * Reduces unnecessary input into generating solver clauses.
      * Reduces solve complexity.
      * Prefers newer packages that apply constraints.
    
    Read more on `Understanding and Improving Conda's Performance
    <https://www.anaconda.com/understanding-and-improving-condas-performance/>`_.
