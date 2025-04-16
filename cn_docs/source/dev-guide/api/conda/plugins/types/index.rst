:py:mod:`types`
===============

.. py:module:: conda.plugins.types

.. autoapi-nested-parse::

   Definition of specific return types for use when defining a conda plugin hook.

   Each type corresponds to the plugin hook for which it is used.



Classes
-------

.. autoapisummary::

   conda.plugins.types.CondaSubcommand
   conda.plugins.types.CondaVirtualPackage
   conda.plugins.types.CondaSolver
   conda.plugins.types.CondaPreCommand
   conda.plugins.types.CondaPostCommand
   conda.plugins.types.ChannelNameMixin
   conda.plugins.types.ChannelAuthBase
   conda.plugins.types.CondaAuthHandler
   conda.plugins.types.CondaHealthCheck
   conda.plugins.types.CondaPreSolve
   conda.plugins.types.CondaPostSolve
   conda.plugins.types.CondaSetting
   conda.plugins.types.ProgressBarBase
   conda.plugins.types.SpinnerBase
   conda.plugins.types.ReporterRendererBase
   conda.plugins.types.CondaReporterBackend
   conda.plugins.types.CondaRequestHeader




.. py:class:: CondaSubcommand


   Return type to use when defining a conda subcommand plugin hook.

   For details on how this is used, see
   :meth:`~conda.plugins.hookspec.CondaSpecs.conda_subcommands`.

   :param name: Subcommand name (e.g., ``conda my-subcommand-name``).
   :param summary: Subcommand summary, will be shown in ``conda --help``.
   :param action: Callable that will be run when the subcommand is invoked.
   :param configure_parser: Callable that will be run when the subcommand parser is initialized.

   .. py:attribute:: name
      :type: str

      

   .. py:attribute:: summary
      :type: str

      

   .. py:attribute:: action
      :type: Callable[[argparse.Namespace | tuple[str]], int | None]

      

   .. py:attribute:: configure_parser
      :type: Callable[[argparse.ArgumentParser], None] | None

      


.. py:class:: CondaVirtualPackage


   Bases: :py:obj:`NamedTuple`

   Return type to use when defining a conda virtual package plugin hook.

   For details on how this is used, see
   :meth:`~conda.plugins.hookspec.CondaSpecs.conda_virtual_packages`.

   :param name: Virtual package name (e.g., ``my_custom_os``).
   :param version: Virtual package version (e.g., ``1.2.3``).
   :param build: Virtual package build string (e.g., ``x86_64``).

   .. py:attribute:: name
      :type: str

      

   .. py:attribute:: version
      :type: str | None

      

   .. py:attribute:: build
      :type: str | None

      

   .. py:method:: to_virtual_package() -> conda.models.records.PackageRecord



.. py:class:: CondaSolver


   Bases: :py:obj:`NamedTuple`

   Return type to use when defining a conda solver plugin hook.

   For details on how this is used, see
   :meth:`~conda.plugins.hookspec.CondaSpecs.conda_solvers`.

   :param name: Solver name (e.g., ``custom-solver``).
   :param backend: Type that will be instantiated as the solver backend.

   .. py:attribute:: name
      :type: str

      

   .. py:attribute:: backend
      :type: type[conda.core.solve.Solver]

      


.. py:class:: CondaPreCommand


   Bases: :py:obj:`NamedTuple`

   Return type to use when defining a conda pre-command plugin hook.

   For details on how this is used, see
   :meth:`~conda.plugins.hookspec.CondaSpecs.conda_pre_commands`.

   :param name: Pre-command name (e.g., ``custom_plugin_pre_commands``).
   :param action: Callable which contains the code to be run.
   :param run_for: Represents the command(s) this will be run on (e.g. ``install`` or ``create``).

   .. py:attribute:: name
      :type: str

      

   .. py:attribute:: action
      :type: Callable[[str], None]

      

   .. py:attribute:: run_for
      :type: set[str]

      


.. py:class:: CondaPostCommand


   Bases: :py:obj:`NamedTuple`

   Return type to use when defining a conda post-command plugin hook.

   For details on how this is used, see
   :meth:`~conda.plugins.hookspec.CondaSpecs.conda_post_commands`.

   :param name: Post-command name (e.g., ``custom_plugin_post_commands``).
   :param action: Callable which contains the code to be run.
   :param run_for: Represents the command(s) this will be run on (e.g. ``install`` or ``create``).

   .. py:attribute:: name
      :type: str

      

   .. py:attribute:: action
      :type: Callable[[str], None]

      

   .. py:attribute:: run_for
      :type: set[str]

      


.. py:class:: ChannelNameMixin(channel_name: str, *args, **kwargs)


   Class mixin to make all plugin implementations compatible, e.g. when they
   use an existing (e.g. 3rd party) requests authentication handler.

   Please use the concrete :class:`~conda.plugins.types.ChannelAuthBase`
   in case you're creating an own implementation.


.. py:class:: ChannelAuthBase(channel_name: str, *args, **kwargs)


   Bases: :py:obj:`ChannelNameMixin`, :py:obj:`requests.auth.AuthBase`

   Base class that we require all plugin implementations to use to be compatible.

   Authentication is tightly coupled with individual channels. Therefore, an additional
   ``channel_name`` property must be set on the ``requests.auth.AuthBase`` based class.


.. py:class:: CondaAuthHandler


   Bases: :py:obj:`NamedTuple`

   Return type to use when the defining the conda auth handlers hook.

   :param name: Name (e.g., ``basic-auth``). This name should be unique
                and only one may be registered at a time.
   :param handler: Type that will be used as the authentication handler
                   during network requests.

   .. py:attribute:: name
      :type: str

      

   .. py:attribute:: handler
      :type: type[ChannelAuthBase]

      


.. py:class:: CondaHealthCheck


   Bases: :py:obj:`NamedTuple`

   Return type to use when defining conda health checks plugin hook.

   .. py:attribute:: name
      :type: str

      

   .. py:attribute:: action
      :type: Callable[[str, bool], None]

      


.. py:class:: CondaPreSolve


   Return type to use when defining a conda pre-solve plugin hook.

   For details on how this is used, see
   :meth:`~conda.plugins.hookspec.CondaSpecs.conda_pre_solves`.

   :param name: Pre-solve name (e.g., ``custom_plugin_pre_solve``).
   :param action: Callable which contains the code to be run.

   .. py:attribute:: name
      :type: str

      

   .. py:attribute:: action
      :type: Callable[[frozenset[conda.models.match_spec.MatchSpec], frozenset[conda.models.match_spec.MatchSpec]], None]

      


.. py:class:: CondaPostSolve


   Return type to use when defining a conda post-solve plugin hook.

   For details on how this is used, see
   :meth:`~conda.plugins.hookspec.CondaSpecs.conda_post_solves`.

   :param name: Post-solve name (e.g., ``custom_plugin_post_solve``).
   :param action: Callable which contains the code to be run.

   .. py:attribute:: name
      :type: str

      

   .. py:attribute:: action
      :type: Callable[[str, tuple[conda.models.records.PackageRecord, Ellipsis], tuple[conda.models.records.PackageRecord, Ellipsis]], None]

      


.. py:class:: CondaSetting


   Return type to use when defining a conda setting plugin hook.

   For details on how this is used, see
   :meth:`~conda.plugins.hookspec.CondaSpecs.conda_settings`.

   :param name: name of the setting (e.g., ``config_param``)
   :param description: description of the setting that should be targeted
                       towards users of the plugin
   :param parameter: Parameter instance containing the setting definition
   :param aliases: alternative names of the setting

   .. py:attribute:: name
      :type: str

      

   .. py:attribute:: description
      :type: str

      

   .. py:attribute:: parameter
      :type: conda.common.configuration.Parameter

      

   .. py:attribute:: aliases
      :type: tuple[str, Ellipsis]

      


.. py:class:: ProgressBarBase(description: str, **kwargs)


   Bases: :py:obj:`abc.ABC`

   Helper class that provides a standard way to create an ABC using
   inheritance.

   .. py:method:: update_to(fraction) -> None
      :abstractmethod:


   .. py:method:: refresh() -> None
      :abstractmethod:


   .. py:method:: close() -> None
      :abstractmethod:


   .. py:method:: finish()


   .. py:method:: get_lock()
      :classmethod:



.. py:class:: SpinnerBase(message: str, fail_message: str = 'failed\n')


   Bases: :py:obj:`abc.ABC`

   Helper class that provides a standard way to create an ABC using
   inheritance.

   .. py:method:: __enter__()
      :abstractmethod:


   .. py:method:: __exit__(exc_type, exc_val, exc_tb)
      :abstractmethod:



.. py:class:: ReporterRendererBase


   Bases: :py:obj:`abc.ABC`

   Base class for all reporter renderers.

   .. py:method:: render(data: Any, **kwargs) -> str


   .. py:method:: detail_view(data: dict[str, str | int | bool], **kwargs) -> str
      :abstractmethod:

      Render the output in a "tabular" format.


   .. py:method:: envs_list(data, **kwargs) -> str
      :abstractmethod:

      Render a list of environments


   .. py:method:: progress_bar(description: str, **kwargs) -> ProgressBarBase
      :abstractmethod:

      Return a :class:`~conda.plugins.types.ProgressBarBase~` object to use as a progress bar


   .. py:method:: progress_bar_context_manager() -> contextlib.AbstractContextManager
      :classmethod:

      Returns a null context by default but allows plugins to define their own if necessary


   .. py:method:: spinner(message, failed_message) -> SpinnerBase
      :abstractmethod:

      Return a :class:`~conda.plugins.types.SpinnerBase~` object to use as a spinner (i.e.
      loading dialog)


   .. py:method:: prompt(message: str = 'Proceed', choices=('yes', 'no'), default: str = 'yes') -> str
      :abstractmethod:

      Allows for defining an implementation of a "yes/no" confirmation function



.. py:class:: CondaReporterBackend


   Return type to use when defining a conda reporter backend plugin hook.

   For details on how this is used, see:
   :meth:`~conda.plugins.hookspec.CondaSpecs.conda_reporter_backends`.

   :param name: name of the reporter backend (e.g., ``email_reporter``)
                This is how the reporter backend with be references in configuration files.
   :param description: short description of what the reporter handler does
   :param renderer: implementation of ``ReporterRendererBase`` that will be used as the
                    reporter renderer

   .. py:attribute:: name
      :type: str

      

   .. py:attribute:: description
      :type: str

      

   .. py:attribute:: renderer
      :type: type[ReporterRendererBase]

      


.. py:class:: CondaRequestHeader


   Define vendor specific headers to include HTTP requests

   For details on how this is used, see
   :meth:`~conda.plugins.hookspec.CondaSpecs.conda_request_headers` and
   :meth:`~conda.plugins.hookspec.CondaSpecs.conda_session_headers`.

   :param name: name of the header used in the HTTP request
   :param value: value of the header used in the HTTP request

   .. py:attribute:: name
      :type: str

      

   .. py:attribute:: value
      :type: str

      


