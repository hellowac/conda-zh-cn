:py:mod:`context`
=================

.. py:module:: conda.base.context

.. autoapi-nested-parse::

   Conda's global configuration object.

   The context aggregates all configuration files, environment variables, and command line arguments
   into one global stateful object to be used across all of conda.



Classes
-------

.. autoapisummary::

   conda.base.context.Context
   conda.base.context.ContextStackObject
   conda.base.context.ContextStack
   conda.base.context.PluginConfig



Functions
---------

.. autoapisummary::

   conda.base.context.user_data_dir
   conda.base.context.mockable_context_envs_dirs
   conda.base.context.channel_alias_validation
   conda.base.context.default_python_default
   conda.base.context.default_python_validation
   conda.base.context.ssl_verify_validation
   conda.base.context._warn_defaults_deprecation
   conda.base.context.reset_context
   conda.base.context.fresh_context
   conda.base.context.stack_context
   conda.base.context.stack_context_default
   conda.base.context.replace_context
   conda.base.context.replace_context_default
   conda.base.context.env_name
   conda.base.context.locate_prefix_by_name
   conda.base.context.validate_channels
   conda.base.context.validate_prefix_name
   conda.base.context.determine_target_prefix
   conda.base.context._first_writable_envs_dir
   conda.base.context.get_plugin_config_data
   conda.base.context.add_plugin_setting
   conda.base.context.remove_all_plugin_settings



Attributes
----------

.. autoapisummary::

   conda.base.context._platform_map
   conda.base.context.non_x86_machines
   conda.base.context._arch_names
   conda.base.context.user_rc_path
   conda.base.context.sys_rc_path
   conda.base.context.context_stack
   conda.base.context.conda_tests_ctxt_mgmt_def_pol
   conda.base.context.context


.. py:data:: _platform_map

   

.. py:data:: non_x86_machines

   

.. py:data:: _arch_names

   

.. py:data:: user_rc_path

   

.. py:data:: sys_rc_path

   

.. py:function:: user_data_dir(appname: str | None = None, appauthor: str | None | Literal[False] = None, version: str | None = None, roaming: bool = False)


.. py:function:: mockable_context_envs_dirs(root_writable, root_prefix, _envs_dirs)


.. py:function:: channel_alias_validation(value)


.. py:function:: default_python_default()


.. py:function:: default_python_validation(value)


.. py:function:: ssl_verify_validation(value)


.. py:function:: _warn_defaults_deprecation()


.. py:class:: Context(search_path=None, argparse_args=None, **kwargs)


   Bases: :py:obj:`conda.common.configuration.Configuration`

   .. py:property:: plugin_manager
      :type: conda.plugins.manager.CondaPluginManager

      This is the preferred way of accessing the ``PluginManager`` object for this application
      and is located here to avoid problems with cyclical imports elsewhere in the code.

   .. py:property:: conda_build_local_paths


   .. py:property:: conda_build_local_urls


   .. py:property:: croot

      This is where source caches and work folders live

   .. py:property:: local_build_root


   .. py:property:: conda_build


   .. py:property:: arch_name


   .. py:property:: platform


   .. py:property:: default_threads
      :type: int | None


   .. py:property:: repodata_threads
      :type: int | None


   .. py:property:: fetch_threads
      :type: int | None

      If both are not overriden (0), return experimentally-determined value of 5

   .. py:property:: verify_threads
      :type: int | None


   .. py:property:: execute_threads


   .. py:property:: subdir


   .. py:property:: subdirs


   .. py:property:: bits


   .. py:property:: root_writable


   .. py:property:: envs_dirs


   .. py:property:: pkgs_dirs


   .. py:property:: default_prefix


   .. py:property:: active_prefix


   .. py:property:: shlvl


   .. py:property:: aggressive_update_packages


   .. py:property:: target_prefix


   .. py:property:: conda_prefix


   .. py:property:: conda_exe


   .. py:property:: av_data_dir

      Where critical artifact verification data (e.g., various public keys) can be found.

   .. py:property:: signing_metadata_url_base

      Base URL for artifact verification signing metadata (*.root.json, key_mgr.json).

   .. py:property:: conda_exe_vars_dict

      The vars can refer to each other if necessary since the dict is ordered.
      None means unset it.

   .. py:property:: migrated_channel_aliases


   .. py:property:: prefix_specified


   .. py:property:: restore_free_channel
      :type: bool


   .. py:property:: channels


   .. py:property:: config_files


   .. py:property:: use_only_tar_bz2


   .. py:property:: binstar_upload


   .. py:property:: trace
      :type: bool

      Alias for context.verbosity >=4.

   .. py:property:: debug
      :type: bool

      Alias for context.verbosity >=3.

   .. py:property:: info
      :type: bool

      Alias for context.verbosity >=2.

   .. py:property:: verbose
      :type: bool

      Alias for context.verbosity >=1.

   .. py:property:: verbosity
      :type: int

      Verbosity level.

      For cleaner and readable code it is preferable to use the following alias properties:
          context.trace
          context.debug
          context.info
          context.verbose
          context.log_level

   .. py:property:: log_level
      :type: int

      Map context.verbosity to logging level.

   .. py:property:: console
      :type: str


   .. py:property:: auto_activate_base
      :type: bool


   .. py:property:: default_activation_env
      :type: str


   .. py:property:: category_map


   .. py:attribute:: add_pip_as_python_dependency

      

   .. py:attribute:: allow_conda_downgrades

      

   .. py:attribute:: allow_cycles

      

   .. py:attribute:: allow_softlinks

      

   .. py:attribute:: auto_update_conda

      

   .. py:attribute:: auto_activate

      

   .. py:attribute:: _default_activation_env

      

   .. py:attribute:: auto_stack

      

   .. py:attribute:: notify_outdated_conda

      

   .. py:attribute:: clobber

      

   .. py:attribute:: changeps1

      

   .. py:attribute:: env_prompt

      

   .. py:attribute:: create_default_packages

      

   .. py:attribute:: register_envs

      

   .. py:attribute:: default_python

      

   .. py:attribute:: download_only

      

   .. py:attribute:: enable_private_envs

      

   .. py:attribute:: force_32bit

      

   .. py:attribute:: non_admin_enabled

      

   .. py:attribute:: pip_interop_enabled

      

   .. py:attribute:: _default_threads

      

   .. py:attribute:: _repodata_threads

      

   .. py:attribute:: _fetch_threads

      

   .. py:attribute:: _verify_threads

      

   .. py:attribute:: _execute_threads

      

   .. py:attribute:: _aggressive_update_packages

      

   .. py:attribute:: safety_checks

      

   .. py:attribute:: extra_safety_checks

      

   .. py:attribute:: _signing_metadata_url_base

      

   .. py:attribute:: path_conflict

      

   .. py:attribute:: pinned_packages

      

   .. py:attribute:: disallowed_packages

      

   .. py:attribute:: rollback_enabled

      

   .. py:attribute:: track_features

      

   .. py:attribute:: use_index_cache

      

   .. py:attribute:: separate_format_cache

      

   .. py:attribute:: _root_prefix

      

   .. py:attribute:: _envs_dirs

      

   .. py:attribute:: _pkgs_dirs

      

   .. py:attribute:: _subdir

      

   .. py:attribute:: _subdirs

      

   .. py:attribute:: local_repodata_ttl

      

   .. py:attribute:: ssl_verify

      

   .. py:attribute:: client_ssl_cert

      

   .. py:attribute:: client_ssl_cert_key

      

   .. py:attribute:: proxy_servers

      

   .. py:attribute:: remote_connect_timeout_secs

      

   .. py:attribute:: remote_read_timeout_secs

      

   .. py:attribute:: remote_max_retries

      

   .. py:attribute:: remote_backoff_factor

      

   .. py:attribute:: add_anaconda_token

      

   .. py:attribute:: allow_non_channel_urls

      

   .. py:attribute:: _channel_alias

      

   .. py:attribute:: channel_priority

      

   .. py:attribute:: _channels

      

   .. py:attribute:: channel_settings

      

   .. py:attribute:: _custom_channels

      

   .. py:attribute:: _custom_multichannels

      

   .. py:attribute:: _default_channels

      

   .. py:attribute:: _migrated_channel_aliases

      

   .. py:attribute:: migrated_custom_channels

      

   .. py:attribute:: override_channels_enabled

      

   .. py:attribute:: show_channel_urls

      

   .. py:attribute:: use_local

      

   .. py:attribute:: allowlist_channels

      

   .. py:attribute:: denylist_channels

      

   .. py:attribute:: _restore_free_channel

      

   .. py:attribute:: repodata_fns

      

   .. py:attribute:: _use_only_tar_bz2

      

   .. py:attribute:: always_softlink

      

   .. py:attribute:: always_copy

      

   .. py:attribute:: always_yes

      

   .. py:attribute:: _debug

      

   .. py:attribute:: _trace

      

   .. py:attribute:: dev

      

   .. py:attribute:: dry_run

      

   .. py:attribute:: error_upload_url

      

   .. py:attribute:: force

      

   .. py:attribute:: json

      

   .. py:attribute:: _console

      

   .. py:attribute:: offline

      

   .. py:attribute:: quiet

      

   .. py:attribute:: ignore_pinned

      

   .. py:attribute:: report_errors

      

   .. py:attribute:: shortcuts

      

   .. py:attribute:: number_channel_notices

      

   .. py:attribute:: shortcuts

      

   .. py:attribute:: shortcuts_only

      

   .. py:attribute:: _verbosity

      

   .. py:attribute:: experimental

      

   .. py:attribute:: no_lock

      

   .. py:attribute:: repodata_use_zst

      

   .. py:attribute:: envvars_force_uppercase

      

   .. py:attribute:: deps_modifier

      

   .. py:attribute:: update_modifier

      

   .. py:attribute:: sat_solver

      

   .. py:attribute:: solver_ignore_timestamps

      

   .. py:attribute:: solver

      

   .. py:attribute:: force_remove

      

   .. py:attribute:: force_reinstall

      

   .. py:attribute:: target_prefix_override

      

   .. py:attribute:: unsatisfiable_hints

      

   .. py:attribute:: unsatisfiable_hints_check_depth

      

   .. py:attribute:: bld_path

      

   .. py:attribute:: anaconda_upload

      

   .. py:attribute:: _croot

      

   .. py:attribute:: _conda_build

      

   .. py:attribute:: no_plugins

      

   .. py:method:: post_build_validation()


   .. py:method:: plugins() -> PluginConfig

      Preferred way of accessing settings introduced by the settings plugin hook


   .. py:method:: _native_subdir()


   .. py:method:: known_subdirs()


   .. py:method:: trash_dir()


   .. py:method:: root_prefix()


   .. py:method:: channel_alias()


   .. py:method:: default_channels()


   .. py:method:: custom_multichannels()


   .. py:method:: custom_channels()


   .. py:method:: solver_user_agent()


   .. py:method:: user_agent()


   .. py:method:: _override(key, value)

      TODO: This might be broken in some ways. Unsure what happens if the `old`
      value is a property and gets set to a new value. Or if the new value
      overrides the validation logic on the underlying ParameterLoader instance.

      Investigate and implement in a safer way.


   .. py:method:: requests_version()


   .. py:method:: python_implementation_name_version()


   .. py:method:: platform_system_release()


   .. py:method:: os_distribution_name_version()


   .. py:method:: libc_family_version()


   .. py:method:: get_descriptions()


   .. py:method:: description_map()



.. py:function:: reset_context(search_path=SEARCH_PATH, argparse_args=None)


.. py:function:: fresh_context(env=None, search_path=SEARCH_PATH, argparse_args=None, **kwargs)


.. py:class:: ContextStackObject(search_path=SEARCH_PATH, argparse_args=None)


   .. py:method:: set_value(search_path=SEARCH_PATH, argparse_args=None)


   .. py:method:: apply()



.. py:class:: ContextStack


   .. py:method:: push(search_path, argparse_args)


   .. py:method:: apply()


   .. py:method:: pop()


   .. py:method:: replace(search_path, argparse_args)



.. py:data:: context_stack

   

.. py:function:: stack_context(pushing, search_path=SEARCH_PATH, argparse_args=None)


.. py:function:: stack_context_default(pushing, argparse_args=None)


.. py:function:: replace_context(pushing=None, search_path=SEARCH_PATH, argparse_args=None)


.. py:function:: replace_context_default(pushing=None, argparse_args=None)


.. py:data:: conda_tests_ctxt_mgmt_def_pol

   

.. py:function:: env_name(prefix)


.. py:function:: locate_prefix_by_name(name, envs_dirs=None)

   Find the location of a prefix given a conda env name.  If the location does not exist, an
   error is raised.


.. py:function:: validate_channels(channels: collections.abc.Iterator[str]) -> tuple[str, Ellipsis]

   Validate if the given channel URLs are allowed based on the context's allowlist
   and denylist configurations.

   :param channels: A list of channels (either URLs or names) to validate.
   :raises ChannelNotAllowed: If any URL is not in the allowlist.
   :raises ChannelDenied: If any URL is in the denylist.


.. py:function:: validate_prefix_name(prefix_name: str, ctx: Context, allow_base=True) -> str

   Run various validations to make sure prefix_name is valid


.. py:function:: determine_target_prefix(ctx, args=None)

   Get the prefix to operate in.  The prefix may not yet exist.

   :param ctx: the context of conda
   :param args: the argparse args from the command line

   Returns: the prefix
   Raises: CondaEnvironmentNotFoundError if the prefix is invalid


.. py:function:: _first_writable_envs_dir()


.. py:function:: get_plugin_config_data(data: dict[pathlib.Path, dict[str, conda.common.configuration.RawParameter]]) -> dict[pathlib.Path, dict[str, conda.common.configuration.RawParameter]]

   This is used to move everything under the key "plugins" from the provided dictionary
   to the top level of the returned dictionary. The returned dictionary is then passed
   to :class:`PluginConfig`.


.. py:class:: PluginConfig(data)


   Class used to hold settings for conda plugins.

   The object created by this class should only be accessed via
   :class:`conda.base.context.Context.plugins`.

   When this class is updated via the :func:`add_plugin_setting` function it adds new setting
   properties which can be accessed later via the context object.

   We currently call that function in
   :meth:`conda.plugins.manager.CondaPluginManager.load_settings`.
   because ``CondaPluginManager`` has access to all registered plugin settings via the settings
   plugin hook.


.. py:function:: add_plugin_setting(name: str, parameter: conda.common.configuration.Parameter, aliases: tuple[str, Ellipsis] = ())

   Adds a setting to the :class:`PluginConfig` class


.. py:function:: remove_all_plugin_settings() -> None

   Removes all attached settings from the :class:`PluginConfig` class


.. py:data:: context

   

