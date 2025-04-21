-----------------------------------------
Miniconda 的 RPM 和 Debian 存储库
-----------------------------------------

RPM and Debian Repositories for Miniconda

.. tab:: 中文
  
  Conda 可作为 RedHat RPM 包或 Debian 软件包获取。这些软件包等价于 Miniconda 安装器，仅包含 conda 及其依赖项。你可以使用 `yum` 或 `apt` 来安装、卸载并管理系统中的 conda。要安装 conda，请按照对应 Linux 发行版的说明进行操作。
  
  要在 RedHat、CentOS、Fedora 以及其他基于 RPM 的发行版（如 openSUSE）上安装 RPM 包，请先下载 GPG 密钥并添加 conda 的软件源配置文件：
  
  .. code-block:: bash
  
     # 导入我们的 GPG 公钥
     rpm --import https://repo.anaconda.com/pkgs/misc/gpgkeys/anaconda.asc
  
     # 添加 Anaconda 软件源
     cat <<EOF > /etc/yum.repos.d/conda.repo
     [conda]
     name=Conda
     baseurl=https://repo.anaconda.com/pkgs/misc/rpmrepo/conda
     enabled=1
     gpgcheck=1
     gpgkey=https://repo.anaconda.com/pkgs/misc/gpgkeys/anaconda.asc
     EOF
  
  至此，Conda 已可在你的 RPM 系统上安装：
  
  .. code-block:: bash
  
     # 安装 conda！
     yum install conda
     Loaded plugins: fastestmirror, ovl
     Setting up Install Process
     Loading mirror speeds from cached hostfile
      * base: repo1.dal.innoscale.net
      * extras: mirrordenver.fdcservers.net
      * updates: mirror.tzulo.com
     Resolving Dependencies
     --> Running transaction check
     ---> Package conda.x86_64 0:4.5.11-0 will be installed
     --> Finished Dependency Resolution
  
     Dependencies Resolved
  
  
   ===============================================================================
     Package         Arch        Version             Repository            Size
  
   ===============================================================================
     Installing:
     conda           x86_64      4.5.11-0            conda                 73 M
  
     Transaction Summary
  
   ===============================================================================
     Install   	1 Package(s)
  
     Total download size: 73 M
     Installed size: 210 M
     Is this ok [y/N]:
  
  要在基于 Debian 的发行版（如 Ubuntu）上安装 conda，请下载 GPG 公钥并将 conda 仓库添加到 sources 列表中：
  
  .. code-block:: bash
  
     # 将我们的 GPG 公钥安装到受信任密钥存储中
     curl https://repo.anaconda.com/pkgs/misc/gpgkeys/anaconda.asc | gpg --dearmor > conda.gpg
     install -o root -g root -m 644 conda.gpg /usr/share/keyrings/conda-archive-keyring.gpg
  
     # 验证指纹是否正确（否则将输出错误信息）
     gpg --keyring /usr/share/keyrings/conda-archive-keyring.gpg --no-default-keyring --fingerprint 34161F5BF5EB1D4BFBBB8F0A8AEB4F8B29D82806
  
     # 添加我们的 Debian 仓库
     echo "deb [arch=amd64 signed-by=/usr/share/keyrings/conda-archive-keyring.gpg] https://repo.anaconda.com/pkgs/misc/debrepo/conda stable main" > /etc/apt/sources.list.d/conda.list
  
     **注意：** 如果运行上述命令时出现 “Permission denied” 错误（因为 `/etc/apt/sources.list.d/conda.list` 为写保护），可以尝试使用以下命令代替：
     echo "deb [arch=amd64 signed-by=/usr/share/keyrings/conda-archive-keyring.gpg] https://repo.anaconda.com/pkgs/misc/debrepo/conda stable main" | sudo tee -a /etc/apt/sources.list.d/conda.list
  
  至此，Conda 已可在你的 Debian 系统上安装：
  
  .. code-block:: bash
  
     # 安装 conda！
     apt update
     apt install conda
     Reading package lists... Done
     Building dependency tree
     Reading state information... Done
     The following NEW packages will be installed:
     conda
     0 upgraded, 1 newly installed, 0 to remove and 3 not upgraded.
     Need to get 76.3 MB of archives.
     After this operation, 221 MB of additional disk space will be used.
     Get:1 https://repo.anaconda.com/pkgs/misc/debrepo/conda stable/main amd64
     conda amd64 4.5.11-0 [76.3 MB]
     Fetched 76.3 MB in 10s (7733 kB/s)
     debconf: delaying package configuration, since apt-utils is not installed
     Selecting previously unselected package conda.
     (Reading database ... 4799 files and directories currently installed.)
     Preparing to unpack .../conda_4.5.11-0_amd64.deb ...
     Unpacking conda (4.5.11-0) ...
     Setting up conda (4.5.11-0) …
  
  通过输入以下命令检查是否安装成功：
  
  .. code-block:: bash
  
     source /opt/conda/etc/profile.d/conda.sh
     conda -V
     conda 4.5.11
  
  通过系统软件包管理器安装 conda，可方便地将其部署到多个运行 Linux 的集群节点上，而无需担心非特权用户修改 conda 安装内容。  
  非特权用户只需运行 ``source /opt/conda/etc/profile.d/conda.sh`` 即可使用 conda。
  
  管理员也可以在 `/opt/conda/.condarc` 分发 `.condarc` 文件，从而为整个组织预配置通道（channel）、包缓存目录和环境位置。例如，配置文件可如下所示：
  
  .. code-block:: yaml
  
     channels:
       - defaults
     pkg_dirs:
       - /shared/conda/pkgs
       - $HOME/.conda/pkgs
     envs_dirs:
       - /shared/conda/envs
       - $HOME/.conda/envs
  
  这些 RPM 与 Debian 软件包也可用于在 Docker 容器中部署 conda。
  
  .. admonition:: 提示
  
      推荐以只读方式使用该安装方法，并仅通过相应的包管理器升级 conda。

.. tab:: 英文

  Conda is available as either a RedHat RPM or as a Debian package. The packages are the
  equivalent to the Miniconda installer, which only contains conda and its dependencies.
  You can use yum or apt to install, uninstall, and manage conda on your system. To
  install conda, follow the instructions for your Linux distribution.
  
  To install the RPM on RedHat, CentOS, Fedora distributions, and other RPM-based distributions,
  such as openSUSE, download the GPG key and add a repository configuration file for conda.
  
  .. code-block:: bash
  
     # Import our GPG public key
     rpm --import https://repo.anaconda.com/pkgs/misc/gpgkeys/anaconda.asc
  
     # Add the Anaconda repository
     cat <<EOF > /etc/yum.repos.d/conda.repo
     [conda]
     name=Conda
     baseurl=https://repo.anaconda.com/pkgs/misc/rpmrepo/conda
     enabled=1
     gpgcheck=1
     gpgkey=https://repo.anaconda.com/pkgs/misc/gpgkeys/anaconda.asc
     EOF
  
  Conda is ready to install on your RPM-based distribution.
  
  .. code-block:: bash
  
     # Install it!
     yum install conda
     Loaded plugins: fastestmirror, ovl
     Setting up Install Process
     Loading mirror speeds from cached hostfile
      * base: repo1.dal.innoscale.net
      * extras: mirrordenver.fdcservers.net
      * updates: mirror.tzulo.com
     Resolving Dependencies
     --> Running transaction check
     ---> Package conda.x86_64 0:4.5.11-0 will be installed
     --> Finished Dependency Resolution
  
     Dependencies Resolved
  
  
   ===============================================================================
     Package         Arch        Version             Repository            Size
  
   ===============================================================================
     Installing:
     conda           x86_64      4.5.11-0            conda                 73 M
  
     Transaction Summary
  
   ===============================================================================
     Install   	1 Package(s)
  
     Total download size: 73 M
     Installed size: 210 M
     Is this ok [y/N]:
  
  To install on Debian-based Linux distributions, such as Ubuntu, download the public GPG
  key and add the conda repository to the sources list.
  
  .. code-block:: bash
  
     # Install our public GPG key to trusted store
     curl https://repo.anaconda.com/pkgs/misc/gpgkeys/anaconda.asc | gpg --dearmor > conda.gpg
     install -o root -g root -m 644 conda.gpg /usr/share/keyrings/conda-archive-keyring.gpg
  
     # Check whether fingerprint is correct (will output an error message otherwise)
     gpg --keyring /usr/share/keyrings/conda-archive-keyring.gpg --no-default-keyring --fingerprint 34161F5BF5EB1D4BFBBB8F0A8AEB4F8B29D82806
  
     # Add our Debian repo
     echo "deb [arch=amd64 signed-by=/usr/share/keyrings/conda-archive-keyring.gpg] https://repo.anaconda.com/pkgs/misc/debrepo/conda stable main" > /etc/apt/sources.list.d/conda.list
  
     **NB:** If you receive a Permission denied error when trying to run the above command (because `/etc/apt/sources.list.d/conda.list` is write protected), try using the following command instead:
     echo "deb [arch=amd64 signed-by=/usr/share/keyrings/conda-archive-keyring.gpg] https://repo.anaconda.com/pkgs/misc/debrepo/conda stable main" | sudo tee -a /etc/apt/sources.list.d/conda.list
  
  Conda is ready to install on your Debian-based distribution.
  
  .. code-block:: bash
  
     # Install it!
     apt update
     apt install conda
     Reading package lists... Done
     Building dependency tree
     Reading state information... Done
     The following NEW packages will be installed:
     conda
     0 upgraded, 1 newly installed, 0 to remove and 3 not upgraded.
     Need to get 76.3 MB of archives.
     After this operation, 221 MB of additional disk space will be used.
     Get:1 https://repo.anaconda.com/pkgs/misc/debrepo/conda stable/main amd64
     conda amd64 4.5.11-0 [76.3 MB]
     Fetched 76.3 MB in 10s (7733 kB/s)
     debconf: delaying package configuration, since apt-utils is not installed
     Selecting previously unselected package conda.
     (Reading database ... 4799 files and directories currently installed.)
     Preparing to unpack .../conda_4.5.11-0_amd64.deb ...
     Unpacking conda (4.5.11-0) ...
     Setting up conda (4.5.11-0) …
  
  Check to see if the installation is successful by typing:
  
  .. code-block:: bash
  
     source /opt/conda/etc/profile.d/conda.sh
     conda -V
     conda 4.5.11
  
  
  Installing conda packages with the system package manager makes it very easy
  to distribute conda across a cluster of machines running Linux without having
  to worry about any non-privileged user modifying the installation.
  Any non-privileged user simply needs to run ``source /opt/conda/etc/profile.d/conda.sh`` to use conda.
  
  Administrators can also distribute a .condarc file at /opt/conda/.condarc so that a
  predefined configuration for channels, package cache directory, and environment locations
  is pre-seeded to all users in a large organization. A sample configuration could look like:
  
  .. code-block:: yaml
  
     channels:
       - defaults
     pkg_dirs:
       - /shared/conda/pkgs
       - $HOME/.conda/pkgs
     envs_dirs:
       - /shared/conda/envs
       - $HOME/.conda/envs
  
  These RPM and Debian packages also provide another way to set up conda inside a Docker container.
  
  .. admonition:: Tip
  
      It is recommended to use this installation method in a read-only manner and upgrade conda using
      the respective package manager only.
  