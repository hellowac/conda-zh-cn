===================================
提高与 pip 的互操作性
===================================

Improving interoperability with pip

.. tab:: 中文

   conda 4.6.0 版本引入了对 conda 与 pip 之间互操作性的改进。  
   该功能目前仍处于实验性阶段，默认未启用。
   
   启用该功能后：
   
   - conda 可以使用由 pip 安装的软件包来满足依赖；
   - conda 能够干净地移除由 pip 安装的软件包；
   - 在适当的情况下，conda 可用自身的软件包替换掉 pip 安装的版本。
   
   如果你希望试用该功能，可使用以下 ``.condarc`` 设置启用：
   
   .. code-block:: bash
   
      conda config --set pip_interop_enabled True
   
   .. note::
   
      将 ``pip_interop_enabled`` 设置为 ``True`` 可能会导致 conda 执行速度变慢。
   
   即使未启用该功能，conda 现在也能更智能地识别 pip 的元数据。  
   例如，假设我们使用 conda 创建一个环境：
   
   .. code-block:: bash
   
      conda create -y -n some_pip_test python=3.7 imagesize=1.0
   
   然后使用 pip 更新 `imagesize`：
   
   .. code-block:: bash
   
      conda activate some_pip_test
      pip install -U imagesize
   
   在 conda 4.6.0 之前，运行 ``conda list`` 会返回重复的结果：
   
   .. code-block::
   
      imagesize                 1.1.0
   
      imagesize                 1.0.0 py37_0
   
   而从 conda 4.6.0 开始，只会显示 pip 安装的新版本：
   
   .. code-block::
   
      imagesize                 1.1.0 pypi_0    pypi

.. tab:: 英文

   The conda 4.6.0 release added improved support for interoperability between conda and pip.
   This feature is still experimental and is therefore off by default.

   With this interoperability,
   conda can use pip-installed packages to satisfy dependencies,
   cleanly remove pip-installed software, and replace them with
   conda packages when appropriate.

   If you’d like to try the feature, you can set this ``.condarc`` setting::

      conda config --set pip_interop_enabled True

   .. note::

      Setting ``pip_interop_enabled`` to ``True`` may slow down conda.

   Even without activating this feature, conda now understands pip metadata
   more intelligently. For example, if we create an environment with conda::

      conda create -y -n some_pip_test python=3.7 imagesize=1.0

   Then we update imagesize in that environment using pip::

      conda activate some_pip_test
      pip install -U imagesize

   Prior to conda 4.6.0, the ``conda list`` command returned ambiguous results::

      imagesize                 1.1.0

      imagesize                 1.0.0 py37_0

   Conda 4.6.0 now shows only one entry for imagesize (the newer pip entry)::

      imagesize                 1.1.0 pypi_0    pypi
