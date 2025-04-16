:py:mod:`activate`
==================

.. py:module:: conda.activate

.. autoapi-nested-parse::

   Conda activate and deactivate logic.

   Implementation for all shell interface logic exposed via
   `conda shell.* [activate|deactivate|reactivate|hook|commands]`. This includes a custom argument
   parser, an abstract shell class, and special path handling for Windows.

   See conda.cli.main.main_sourced for the entry point into this module.



Classes
-------

.. autoapisummary::

   conda.activate._Activator
   conda.activate.PosixActivator
   conda.activate.CshActivator
   conda.activate.XonshActivator
   conda.activate.CmdExeActivator
   conda.activate.FishActivator
   conda.activate.PowerShellActivator
   conda.activate.JSONFormatMixin



Functions
---------

.. autoapisummary::

   conda.activate.expand
   conda.activate.ensure_binary
   conda.activate.ensure_fs_path_encoding
   conda.activate.backslash_to_forwardslash
   conda.activate._build_activator_cls



Attributes
----------

.. autoapisummary::

   conda.activate.BUILTIN_COMMANDS
   conda.activate.activator_map
   conda.activate.formatter_map


.. py:data:: BUILTIN_COMMANDS

   

.. py:class:: _Activator(arguments=None)


   .. py:attribute:: pathsep_join
      :type: str

      

   .. py:attribute:: sep
      :type: str

      

   .. py:attribute:: path_conversion
      :type: collections.abc.Callable[[str | collections.abc.Iterable[str] | None], str | tuple[str, Ellipsis] | None]

      

   .. py:attribute:: script_extension
      :type: str

      

   .. py:attribute:: tempfile_extension
      :type: str | None

      

   .. py:attribute:: command_join
      :type: str

      

   .. py:attribute:: unset_var_tmpl
      :type: str

      

   .. py:attribute:: export_var_tmpl
      :type: str

      

   .. py:attribute:: set_var_tmpl
      :type: str

      

   .. py:attribute:: run_script_tmpl
      :type: str

      

   .. py:attribute:: hook_source_path
      :type: pathlib.Path | None

      

   .. py:method:: get_export_unset_vars(export_metavars=True, **kwargs)

      :param export_metavars: whether to export `conda_exe_vars` meta variables.
      :param kwargs: environment variables to export.
          .. if you pass and set any other variable to None, then it
          emits it to the dict with a value of None.

      :return: A dict of env vars to export ordered the same way as kwargs.
          And a list of env vars to unset.


   .. py:method:: _finalize(commands, ext)


   .. py:method:: activate()


   .. py:method:: deactivate()


   .. py:method:: reactivate()


   .. py:method:: hook(auto_activate: bool | None = None) -> str


   .. py:method:: execute()


   .. py:method:: commands()

      Returns a list of possible subcommands that are valid
      immediately following `conda` at the command line.
      This method is generally only used by tab-completion.


   .. py:method:: _hook_preamble() -> str | None
      :abstractmethod:


   .. py:method:: _hook_postamble() -> str | None


   .. py:method:: _parse_and_set_args() -> None


   .. py:method:: _yield_commands(cmds_dict)


   .. py:method:: build_activate(env_name_or_prefix)


   .. py:method:: build_stack(env_name_or_prefix)


   .. py:method:: _build_activate_stack(env_name_or_prefix, stack)


   .. py:method:: build_deactivate()


   .. py:method:: build_reactivate()


   .. py:method:: _get_starting_path_list()


   .. py:method:: _get_path_dirs(prefix)


   .. py:method:: _add_prefix_to_path(prefix, starting_path_dirs=None)


   .. py:method:: _remove_prefix_from_path(prefix, starting_path_dirs=None)


   .. py:method:: _replace_prefix_in_path(old_prefix, new_prefix, starting_path_dirs=None)


   .. py:method:: _update_prompt(set_vars, conda_prompt_modifier)


   .. py:method:: _default_env(prefix)


   .. py:method:: _prompt_modifier(prefix, conda_default_env)


   .. py:method:: _get_activate_scripts(prefix)


   .. py:method:: _get_deactivate_scripts(prefix)


   .. py:method:: _get_environment_env_vars(prefix)



.. py:function:: expand(path)


.. py:function:: ensure_binary(value)


.. py:function:: ensure_fs_path_encoding(value)


.. py:function:: backslash_to_forwardslash(paths: str | collections.abc.Iterable[str] | None) -> str | tuple[str, Ellipsis] | None


.. py:class:: PosixActivator(arguments=None)


   Bases: :py:obj:`_Activator`

   .. py:attribute:: pathsep_join

      

   .. py:attribute:: sep
      :value: '/'

      

   .. py:attribute:: path_conversion

      

   .. py:attribute:: script_extension
      :value: '.sh'

      

   .. py:attribute:: tempfile_extension

      

   .. py:attribute:: command_join
      :value: '\n'

      

   .. py:attribute:: unset_var_tmpl
      :value: 'unset %s'

      

   .. py:attribute:: export_var_tmpl
      :value: "export %s='%s'"

      

   .. py:attribute:: set_var_tmpl
      :value: "%s='%s'"

      

   .. py:attribute:: run_script_tmpl
      :value: '. "%s"'

      

   .. py:attribute:: hook_source_path

      

   .. py:method:: _update_prompt(set_vars, conda_prompt_modifier)


   .. py:method:: _hook_preamble() -> str



.. py:class:: CshActivator(arguments=None)


   Bases: :py:obj:`_Activator`

   .. py:attribute:: pathsep_join

      

   .. py:attribute:: sep
      :value: '/'

      

   .. py:attribute:: path_conversion

      

   .. py:attribute:: script_extension
      :value: '.csh'

      

   .. py:attribute:: tempfile_extension

      

   .. py:attribute:: command_join
      :value: ';\n'

      

   .. py:attribute:: unset_var_tmpl
      :value: 'unsetenv %s'

      

   .. py:attribute:: export_var_tmpl
      :value: 'setenv %s "%s"'

      

   .. py:attribute:: set_var_tmpl
      :value: "set %s='%s'"

      

   .. py:attribute:: run_script_tmpl
      :value: 'source "%s"'

      

   .. py:attribute:: hook_source_path

      

   .. py:method:: _update_prompt(set_vars, conda_prompt_modifier)


   .. py:method:: _hook_preamble() -> str



.. py:class:: XonshActivator(arguments=None)


   Bases: :py:obj:`_Activator`

   .. py:attribute:: pathsep_join

      

   .. py:attribute:: sep
      :value: '/'

      

   .. py:attribute:: path_conversion

      

   .. py:attribute:: script_extension

      

   .. py:attribute:: tempfile_extension

      

   .. py:attribute:: command_join
      :value: '\n'

      

   .. py:attribute:: unset_var_tmpl
      :value: Multiline-String

       .. raw:: html

           <details><summary>Show Value</summary>

       .. code-block:: python

           """try:
               del $%s
           except KeyError:
               pass"""

       .. raw:: html

           </details>

      

   .. py:attribute:: export_var_tmpl
      :value: "$%s = '%s'"

      

   .. py:attribute:: set_var_tmpl
      :value: "$%s = '%s'"

      

   .. py:attribute:: run_script_tmpl

      

   .. py:attribute:: hook_source_path

      

   .. py:method:: _hook_preamble() -> str



.. py:class:: CmdExeActivator(arguments=None)


   Bases: :py:obj:`_Activator`

   .. py:attribute:: pathsep_join

      

   .. py:attribute:: sep
      :value: '\\'

      

   .. py:attribute:: path_conversion

      

   .. py:attribute:: script_extension
      :value: '.bat'

      

   .. py:attribute:: tempfile_extension
      :value: '.env'

      

   .. py:attribute:: command_join
      :value: '\n'

      

   .. py:attribute:: unset_var_tmpl
      :value: '%s='

      

   .. py:attribute:: run_script_tmpl
      :value: '_CONDA_SCRIPT=%s'

      

   .. py:attribute:: hook_source_path

      

   .. py:method:: _update_prompt(set_vars, conda_prompt_modifier)


   .. py:method:: _hook_preamble() -> None



.. py:class:: FishActivator(arguments=None)


   Bases: :py:obj:`_Activator`

   .. py:attribute:: pathsep_join

      

   .. py:attribute:: sep
      :value: '/'

      

   .. py:attribute:: path_conversion

      

   .. py:attribute:: script_extension
      :value: '.fish'

      

   .. py:attribute:: tempfile_extension

      

   .. py:attribute:: command_join
      :value: ';\n'

      

   .. py:attribute:: unset_var_tmpl
      :value: 'set -e %s'

      

   .. py:attribute:: export_var_tmpl
      :value: 'set -gx %s "%s"'

      

   .. py:attribute:: set_var_tmpl
      :value: 'set -g %s "%s"'

      

   .. py:attribute:: run_script_tmpl
      :value: 'source "%s"'

      

   .. py:attribute:: hook_source_path

      

   .. py:method:: _hook_preamble() -> str



.. py:class:: PowerShellActivator(arguments=None)


   Bases: :py:obj:`_Activator`

   .. py:attribute:: pathsep_join

      

   .. py:attribute:: sep

      

   .. py:attribute:: path_conversion

      

   .. py:attribute:: script_extension
      :value: '.ps1'

      

   .. py:attribute:: tempfile_extension

      

   .. py:attribute:: command_join
      :value: '\n'

      

   .. py:attribute:: unset_var_tmpl
      :value: '$Env:%s = $null'

      

   .. py:attribute:: export_var_tmpl
      :value: '$Env:%s = "%s"'

      

   .. py:attribute:: set_var_tmpl
      :value: '$Env:%s = "%s"'

      

   .. py:attribute:: run_script_tmpl
      :value: '. "%s"'

      

   .. py:attribute:: hook_source_path

      

   .. py:method:: _hook_preamble() -> str


   .. py:method:: _hook_postamble() -> str



.. py:class:: JSONFormatMixin(arguments=None)


   Bases: :py:obj:`_Activator`

   Returns the necessary values for activation as JSON, so that tools can use them.

   .. py:attribute:: pathsep_join

      

   .. py:attribute:: tempfile_extension

      

   .. py:attribute:: command_join

      

   .. py:method:: _hook_preamble()


   .. py:method:: _finalize(commands, ext)


   .. py:method:: _yield_commands(cmds_dict)



.. py:data:: activator_map
   :type: dict[str, type[_Activator]]

   

.. py:data:: formatter_map

   

.. py:function:: _build_activator_cls(shell)

   Dynamically construct the activator class.

   Detect the base activator and any number of formatters (appended using '+' to the base name).
   For example, `posix+json` (as in `conda shell.posix+json activate`) would use the
   `PosixActivator` base class and add the `JSONFormatMixin`.


