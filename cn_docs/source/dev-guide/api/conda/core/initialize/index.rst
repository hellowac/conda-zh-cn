:py:mod:`initialize`
====================

.. py:module:: conda.core.initialize

.. autoapi-nested-parse::

   Backend logic for `conda init`.

   Sections in this module are

     1. top-level functions
     2. plan creators
     3. plan runners
     4. individual operations
     5. helper functions

   The top-level functions compose and execute full plans.

   A plan is created by composing various individual operations.  The plan data structure is a
   list of dicts, where each dict represents an individual operation.  The dict contains two
   keys--`function` and `kwargs`--where function is the name of the individual operation function
   within this module.

   Each individual operation must

     a) return a `Result` (i.e. NEEDS_SUDO, MODIFIED, or NO_CHANGE)
     b) have no side effects if context.dry_run is True
     c) be verbose and descriptive about the changes being made or proposed is context.verbose

   The plan runner functions take the plan (list of dicts) as an argument, and then coordinate the
   execution of each individual operation.  The docstring for `run_plan_elevated()` has details on
   how that strategy is implemented.



Classes
-------

.. autoapisummary::

   conda.core.initialize.Result



Functions
---------

.. autoapisummary::

   conda.core.initialize.install
   conda.core.initialize.initialize
   conda.core.initialize.initialize_dev
   conda.core.initialize._initialize_dev_bash
   conda.core.initialize._initialize_dev_cmdexe
   conda.core.initialize.make_install_plan
   conda.core.initialize.make_initialize_plan
   conda.core.initialize.run_plan
   conda.core.initialize.run_plan_elevated
   conda.core.initialize.run_plan_from_stdin
   conda.core.initialize.run_plan_from_temp_file
   conda.core.initialize.print_plan_results
   conda.core.initialize.make_entry_point
   conda.core.initialize.make_entry_point_exe
   conda.core.initialize.install_anaconda_prompt
   conda.core.initialize._install_file
   conda.core.initialize.install_conda_sh
   conda.core.initialize.install_Scripts_activate_bat
   conda.core.initialize.install_activate_bat
   conda.core.initialize.install_deactivate_bat
   conda.core.initialize.install_activate
   conda.core.initialize.install_deactivate
   conda.core.initialize.install_condabin_conda_bat
   conda.core.initialize.install_library_bin_conda_bat
   conda.core.initialize.install_condabin_conda_activate_bat
   conda.core.initialize.install_condabin_rename_tmp_bat
   conda.core.initialize.install_condabin_conda_auto_activate_bat
   conda.core.initialize.install_condabin_hook_bat
   conda.core.initialize.install_conda_fish
   conda.core.initialize.install_conda_psm1
   conda.core.initialize.install_conda_hook_ps1
   conda.core.initialize.install_conda_xsh
   conda.core.initialize.install_conda_csh
   conda.core.initialize._config_fish_content
   conda.core.initialize.init_fish_user
   conda.core.initialize._config_xonsh_content
   conda.core.initialize.init_xonsh_user
   conda.core.initialize._bashrc_content
   conda.core.initialize.init_sh_user
   conda.core.initialize.init_sh_system
   conda.core.initialize._read_windows_registry
   conda.core.initialize._write_windows_registry
   conda.core.initialize.init_cmd_exe_registry
   conda.core.initialize.init_long_path
   conda.core.initialize._powershell_profile_content
   conda.core.initialize.init_powershell_user
   conda.core.initialize.remove_conda_in_sp_dir
   conda.core.initialize.make_conda_egg_link
   conda.core.initialize.modify_easy_install_pth
   conda.core.initialize.make_dev_egg_info_file
   conda.core.initialize.make_diff
   conda.core.initialize._get_python_info



Attributes
----------

.. autoapisummary::

   conda.core.initialize.CONDA_INITIALIZE_RE_BLOCK
   conda.core.initialize.CONDA_INITIALIZE_PS_RE_BLOCK
   conda.core.initialize.temp_path


.. py:data:: CONDA_INITIALIZE_RE_BLOCK
   :value: '^# >>> conda initialize >>>(?:\\n|\\r\\n)([\\s\\S]*?)# <<< conda initialize <<<(?:\\n|\\r\\n)?'

   

.. py:data:: CONDA_INITIALIZE_PS_RE_BLOCK
   :value: '^#region conda initialize(?:\\n|\\r\\n)([\\s\\S]*?)#endregion(?:\\n|\\r\\n)?'

   

.. py:class:: Result


   .. py:attribute:: NEEDS_SUDO
      :value: 'needs sudo'

      

   .. py:attribute:: MODIFIED
      :value: 'modified'

      

   .. py:attribute:: NO_CHANGE
      :value: 'no change'

      


.. py:function:: install(conda_prefix)


.. py:function:: initialize(conda_prefix, shells, for_user, for_system, anaconda_prompt, reverse=False)


.. py:function:: initialize_dev(shell, dev_env_prefix=None, conda_source_root=None)


.. py:function:: _initialize_dev_bash(prefix, env_vars, unset_env_vars)


.. py:function:: _initialize_dev_cmdexe(prefix, env_vars, unset_env_vars)


.. py:function:: make_install_plan(conda_prefix)


.. py:function:: make_initialize_plan(conda_prefix, shells, for_user, for_system, anaconda_prompt, reverse=False)

   Creates a plan for initializing conda in shells.

   Bash:
   On Linux, when opening the terminal, .bashrc is sourced (because it is an interactive shell).
   On macOS on the other hand, the .bash_profile gets sourced by default when executing it in
   Terminal.app. Some other programs do the same on macOS so that's why we're initializing conda
   in .bash_profile.
   On Windows, there are multiple ways to open bash depending on how it was installed. Git Bash,
   Cygwin, and MSYS2 all use .bash_profile by default.

   PowerShell:
   There's several places PowerShell can store its path, depending on if it's Windows PowerShell,
   PowerShell Core on Windows, or PowerShell Core on macOS/Linux. The easiest way to resolve it
   is to just ask different possible installations of PowerShell where their profiles are.


.. py:function:: run_plan(plan)


.. py:function:: run_plan_elevated(plan)

   The strategy of this function differs between unix and Windows.  Both strategies use a
   subprocess call, where the subprocess is run with elevated privileges.  The executable
   invoked with the subprocess is `python -m conda.core.initialize`, so see the
   `if __name__ == "__main__"` at the bottom of this module.

   For unix platforms, we convert the plan list to json, and then call this module with
   `sudo python -m conda.core.initialize` while piping the plan json to stdin.  We collect json
   from stdout for the results of the plan execution with elevated privileges.

   For Windows, we create a temporary file that holds the json content of the plan.  The
   subprocess reads the content of the file, modifies the content of the file with updated
   execution status, and then closes the file.  This process then reads the content of that file
   for the individual operation execution results, and then deletes the file.


.. py:function:: run_plan_from_stdin()


.. py:function:: run_plan_from_temp_file(temp_path)


.. py:function:: print_plan_results(plan, stream=None)


.. py:function:: make_entry_point(target_path, conda_prefix, module, func)


.. py:function:: make_entry_point_exe(target_path, conda_prefix)


.. py:function:: install_anaconda_prompt(target_path, conda_prefix, reverse)


.. py:function:: _install_file(target_path, file_content)


.. py:function:: install_conda_sh(target_path, conda_prefix)


.. py:function:: install_Scripts_activate_bat(target_path, conda_prefix)


.. py:function:: install_activate_bat(target_path, conda_prefix)


.. py:function:: install_deactivate_bat(target_path, conda_prefix)


.. py:function:: install_activate(target_path, conda_prefix)


.. py:function:: install_deactivate(target_path, conda_prefix)


.. py:function:: install_condabin_conda_bat(target_path, conda_prefix)


.. py:function:: install_library_bin_conda_bat(target_path, conda_prefix)


.. py:function:: install_condabin_conda_activate_bat(target_path, conda_prefix)


.. py:function:: install_condabin_rename_tmp_bat(target_path, conda_prefix)


.. py:function:: install_condabin_conda_auto_activate_bat(target_path, conda_prefix)


.. py:function:: install_condabin_hook_bat(target_path, conda_prefix)


.. py:function:: install_conda_fish(target_path, conda_prefix)


.. py:function:: install_conda_psm1(target_path, conda_prefix)


.. py:function:: install_conda_hook_ps1(target_path, conda_prefix)


.. py:function:: install_conda_xsh(target_path, conda_prefix)


.. py:function:: install_conda_csh(target_path, conda_prefix)


.. py:function:: _config_fish_content(conda_prefix)


.. py:function:: init_fish_user(target_path, conda_prefix, reverse)


.. py:function:: _config_xonsh_content(conda_prefix)


.. py:function:: init_xonsh_user(target_path, conda_prefix, reverse)


.. py:function:: _bashrc_content(conda_prefix, shell)


.. py:function:: init_sh_user(target_path, conda_prefix, shell, reverse=False)


.. py:function:: init_sh_system(target_path, conda_prefix, reverse=False)


.. py:function:: _read_windows_registry(target_path)


.. py:function:: _write_windows_registry(target_path, value_value, value_type)


.. py:function:: init_cmd_exe_registry(target_path, conda_prefix, reverse=False)


.. py:function:: init_long_path(target_path)


.. py:function:: _powershell_profile_content(conda_prefix)


.. py:function:: init_powershell_user(target_path, conda_prefix, reverse)


.. py:function:: remove_conda_in_sp_dir(target_path)


.. py:function:: make_conda_egg_link(target_path, conda_source_root)


.. py:function:: modify_easy_install_pth(target_path, conda_source_root)


.. py:function:: make_dev_egg_info_file(target_path)


.. py:function:: make_diff(old, new)


.. py:function:: _get_python_info(prefix)


.. py:data:: temp_path

   

