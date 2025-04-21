:py:mod:`plugins`
=================

.. py:module:: conda.plugins

.. autoapi-nested-parse::

   In this module, you will find everything relevant to conda's plugin system.
   It contains all of the code that plugin authors will use to write plugins,
   as well as conda's internal implementations of plugins.

   **Modules relevant for plugin authors**

   - :mod:`conda.plugins.hookspec`: all available hook specifications are listed here, including
     examples of how to use them
   - :mod:`conda.plugins.types`: important types to use when defining plugin hooks

   **Modules relevant for internal development**

   - :mod:`conda.plugins.manager`: includes our custom subclass of pluggy's
     `PluginManager <https://pluggy.readthedocs.io/en/stable/api_reference.html#pluggy.PluginManager>`_ class

   **Modules with internal plugin implementations**

   - :mod:`conda.plugins.solvers`: implementation of the "classic" solver
   - :mod:`conda.plugins.subcommands.doctor`: ``conda doctor`` subcommand
   - :mod:`conda.plugins.virtual_packages`: registers virtual packages in conda



.. toctree::
   :hidden:
   :titlesonly:
   :maxdepth: 3

   hookspec/index.rst
   manager/index.rst
   post_solves/index.rst
   reporter_backends/index.rst
   solvers/index.rst
   subcommands/index.rst
   types/index.rst
   virtual_packages/index.rst


Classes
-------

.. autoapisummary::

   conda.plugins.CondaAuthHandler
   conda.plugins.CondaHealthCheck
   conda.plugins.CondaPostCommand
   conda.plugins.CondaPostSolve
   conda.plugins.CondaPreCommand
   conda.plugins.CondaPreSolve
   conda.plugins.CondaReporterBackend
   conda.plugins.CondaRequestHeader
   conda.plugins.CondaSetting
   conda.plugins.CondaSolver
   conda.plugins.CondaSubcommand
   conda.plugins.CondaVirtualPackage




Attributes
----------

.. autoapisummary::

   conda.plugins.hookimpl


.. py:data:: hookimpl

   Decorator used to mark plugin hook implementations

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



