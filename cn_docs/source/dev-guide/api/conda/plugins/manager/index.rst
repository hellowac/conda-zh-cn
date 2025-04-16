:py:mod:`manager`
=================

.. py:module:: conda.plugins.manager

.. autoapi-nested-parse::

   This module contains a subclass implementation of pluggy's
   `PluginManager <https://pluggy.readthedocs.io/en/stable/api_reference.html#pluggy.PluginManager>`_.

   Additionally, it contains a function we use to construct the ``PluginManager`` object and
   register all plugins during conda's startup process.



Classes
-------

.. autoapisummary::

   conda.plugins.manager.CondaPluginManager



Functions
---------

.. autoapisummary::

   conda.plugins.manager.get_plugin_manager



.. py:class:: CondaPluginManager(project_name: str | None = None, *args, **kwargs)


   Bases: :py:obj:`pluggy.PluginManager`

   The conda plugin manager to implement behavior additional to pluggy's default plugin manager.

   .. py:attribute:: get_cached_solver_backend

      

   .. py:method:: get_canonical_name(plugin: object) -> str

      Return a canonical name for a plugin object.

      Note that a plugin may be registered under a different name
      specified by the caller of :meth:`register(plugin, name) <register>`.
      To obtain the name of a registered plugin use :meth:`get_name(plugin)
      <get_name>` instead.


   .. py:method:: register(plugin, name: str | None = None) -> str | None

      Call :meth:`pluggy.PluginManager.register` and return the result or
      ignore errors raised, except ``ValueError``, which means the plugin
      had already been registered.


   .. py:method:: load_plugins(*plugins) -> int

      Load the provided list of plugins and fail gracefully on error.
      The provided list of plugins can either be classes or modules with
      :attr:`~conda.plugins.hookimpl`.


   .. py:method:: load_entrypoints(group: str, name: str | None = None) -> int

      Load modules from querying the specified setuptools ``group``.

      :param str group: Entry point group to load plugins.
      :param str name: If given, loads only plugins with the given ``name``.
      :rtype: int
      :return: The number of plugins loaded by this call.


   .. py:method:: get_hook_results(name: Literal[conda.plugins.subcommands]) -> list[conda.plugins.types.CondaSubcommand]
                  get_hook_results(name: Literal[conda.plugins.virtual_packages]) -> list[conda.plugins.types.CondaVirtualPackage]
                  get_hook_results(name: Literal[conda.plugins.solvers]) -> list[conda.plugins.types.CondaSolver]
                  get_hook_results(name: Literal[pre_commands]) -> list[conda.plugins.types.CondaPreCommand]
                  get_hook_results(name: Literal[post_commands]) -> list[conda.plugins.types.CondaPostCommand]
                  get_hook_results(name: Literal[auth_handlers]) -> list[conda.plugins.types.CondaAuthHandler]
                  get_hook_results(name: Literal[conda.plugins.subcommands.doctor.health_checks]) -> list[conda.plugins.types.CondaHealthCheck]
                  get_hook_results(name: Literal[pre_solves]) -> list[conda.plugins.types.CondaPreSolve]
                  get_hook_results(name: Literal[conda.plugins.post_solves]) -> list[conda.plugins.types.CondaPostSolve]
                  get_hook_results(name: Literal[session_headers], *, host: str) -> list[conda.plugins.types.CondaRequestHeader]
                  get_hook_results(name: Literal[request_headers], *, host: str, path: str) -> list[conda.plugins.types.CondaRequestHeader]
                  get_hook_results(name: Literal[settings]) -> list[conda.plugins.types.CondaSetting]
                  get_hook_results(name: Literal[conda.plugins.reporter_backends]) -> list[conda.plugins.types.CondaReporterBackend]

      Return results of the plugin hooks with the given name and
      raise an error if there is a conflict.


   .. py:method:: get_solvers() -> dict[str, conda.plugins.types.CondaSolver]

      Return a mapping from solver name to solver class.


   .. py:method:: get_solver_backend(name: str | None = None) -> type[conda.core.solve.Solver]

      Get the solver backend with the given name (or fall back to the
      name provided in the context).

      See ``context.solver`` for more details.

      Please use the cached version of this method called
      :meth:`get_cached_solver_backend` for high-throughput code paths
      which is set up as a instance-specific LRU cache.


   .. py:method:: get_auth_handler(name: str) -> type[requests.auth.AuthBase] | None

      Get the auth handler with the given name or None


   .. py:method:: get_settings() -> dict[str, conda.common.configuration.ParameterLoader]

      Return a mapping of plugin setting name to ParameterLoader class

      This method intentionally overwrites any duplicates that may be present


   .. py:method:: invoke_pre_commands(command: str) -> None

      Invokes ``CondaPreCommand.action`` functions registered with ``conda_pre_commands``.

      :param command: name of the command that is currently being invoked


   .. py:method:: invoke_post_commands(command: str) -> None

      Invokes ``CondaPostCommand.action`` functions registered with ``conda_post_commands``.

      :param command: name of the command that is currently being invoked


   .. py:method:: disable_external_plugins() -> None

      Disables all currently registered plugins except built-in conda plugins


   .. py:method:: get_subcommands() -> dict[str, conda.plugins.types.CondaSubcommand]


   .. py:method:: get_virtual_packages() -> tuple[conda.plugins.types.CondaVirtualPackage, Ellipsis]


   .. py:method:: get_reporter_backends() -> tuple[conda.plugins.types.CondaReporterBackend, Ellipsis]


   .. py:method:: get_reporter_backend(name: str) -> conda.plugins.types.CondaReporterBackend

      Attempts to find a reporter backend while providing a fallback option if it is
      not found.

      This method must return a valid ``CondaReporterBackend`` object or else it will
      raise an exception.


   .. py:method:: get_virtual_package_records() -> tuple[conda.models.records.PackageRecord, Ellipsis]


   .. py:method:: get_session_headers(host: str) -> dict[str, str]


   .. py:method:: get_request_headers(host: str, path: str) -> dict[str, str]


   .. py:method:: invoke_health_checks(prefix: str, verbose: bool) -> None


   .. py:method:: invoke_pre_solves(specs_to_add: frozenset[conda.models.match_spec.MatchSpec], specs_to_remove: frozenset[conda.models.match_spec.MatchSpec]) -> None

      Invokes ``CondaPreSolve.action`` functions registered with ``conda_pre_solves``.

      :param specs_to_add:
      :param specs_to_remove:


   .. py:method:: invoke_post_solves(repodata_fn: str, unlink_precs: tuple[conda.models.records.PackageRecord, Ellipsis], link_precs: tuple[conda.models.records.PackageRecord, Ellipsis]) -> None

      Invokes ``CondaPostSolve.action`` functions registered with ``conda_post_solves``.

      :param repodata_fn:
      :param unlink_precs:
      :param link_precs:


   .. py:method:: load_settings() -> None

      Iterates through all registered settings and adds them to the
      :class:`conda.common.configuration.PluginConfig` class.



.. py:function:: get_plugin_manager() -> CondaPluginManager

   Get a cached version of the :class:`~conda.plugins.manager.CondaPluginManager` instance,
   with the built-in and entrypoints provided by the plugins loaded.


