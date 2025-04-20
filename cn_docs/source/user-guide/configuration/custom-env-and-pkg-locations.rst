========================================================
使用环境和包缓存的自定义位置
========================================================

Using Custom Locations for Environment and Package Cache

.. tab:: 中文

  对于任意一次 conda 安装来说，占用磁盘空间最大的两个文件夹通常是用于存储已创建环境的 ``envs`` 文件夹和用于存储已下载软件包的 ``pkgs`` 文件夹。  
  如果 conda 安装的位置磁盘空间有限，而同一台计算机上的其他位置拥有更多可用磁盘空间，可以通过设置 ``envs_dirs`` 和 ``pkgs_dirs`` 来分别更改 conda 存储环境和软件包的位置。

  假设 conda 安装在用户的主目录下，而 ``/nfs/volume/user`` 目录具有更多可用空间且可写，最佳的配置方式是在用户主目录下的 ``.condarc`` 文件中添加以下内容：

    .. code-block:: yaml

        envs_dirs:
          - /nfs/volume/user/conda_envs
        pkgs_dirs:
          - /nfs/volume/user/conda_pkgs

  在上面的示例中，我们指示 conda 使用 ``/nfs/volume/user/conda_envs`` 目录来存储所有我们创建的环境，使用 ``/nfs/volume/user/conda_pkgs`` 目录来存储所有我们下载的软件包。

  为了进一步节省空间，在可能的情况下，``/nfs/volume/user/conda_pkgs`` 中的内容将通过硬链接（hard link）的方式链接至 ``/nfs/volume/user/conda_envs`` 中的环境。这意味着，在一次 conda 安装中，``pkgs_dirs`` 通常会占用最多的磁盘空间。但是，在无法使用硬链接的情况下，文件将被复制到环境目录中，这意味着每个新环境都会增加磁盘空间占用。为了确保硬链接可以正常工作，推荐始终将 ``envs_dirs`` 与 ``pkgs_dirs`` 存储在同一挂载卷中。

.. tab:: 英文

    For any given conda installation, the two largest folders in terms of
    disk space are often the ``envs`` and ``pkgs`` folders
    that store created environments and downloaded packages, respectively.
    If the location where conda is installed has limited disk
    space and another location with more disk space is available on the
    same computer, we can change where conda saves its environments and
    packages with the settings ``envs_dirs`` and ``pkgs_dirs``, respectively.

    Assuming conda is installed in the user's home directory and the
    the folder ``/nfs/volume/user`` with more disk space is writable,
    the best way to configure this is by adding the following entries to the
    ``.condarc`` file in the user's home directory:

      .. code-block:: yaml

          envs_dirs:
            - /nfs/volume/user/conda_envs
          pkgs_dirs:
            - /nfs/volume/user/conda_pkgs

    In the example above, we tell conda to use the folder ``/nfs/volume/user/conda_envs``
    to store all of the environments we create, and we tell conda to use
    ``/nfs/volume/user/conda_pkgs`` to store all of the packages that we download.

    To save even more space, the contents of ``/nfs/volume/user/conda_pkgs`` will be
    hard linked to the environments in ``/nfs/volume/user/conda_envs`` when possible.
    This means that ``pkgs_dirs`` will normally take up the most space for a conda
    installation. But, when hard linking is not possible, the files will be copied
    over to the environment which means each new environment increases the amount
    of disk space taken. To ensure this hard linking works properly, we recommend
    to always store the ``envs_dirs`` and ``pkgs_dirs`` on the same mounted volume.
