:py:mod:`doctor`
================

.. py:module:: conda.plugins.subcommands.doctor

.. autoapi-nested-parse::

   Implementation for `conda doctor` subcommand.
   Adds various environment and package checks to detect issues or possible environment
   corruption.



.. toctree::
   :hidden:
   :titlesonly:
   :maxdepth: 3

   health_checks/index.rst


Classes
-------

.. autoapisummary::

   conda.plugins.subcommands.doctor.CondaSubcommand



Functions
---------

.. autoapisummary::

   conda.plugins.subcommands.doctor.add_parser_help
   conda.plugins.subcommands.doctor.add_parser_prefix
   conda.plugins.subcommands.doctor.add_parser_verbose
   conda.plugins.subcommands.doctor.is_conda_environment
   conda.plugins.subcommands.doctor.configure_parser
   conda.plugins.subcommands.doctor.execute
   conda.plugins.subcommands.doctor.conda_subcommands



Attributes
----------

.. autoapisummary::

   conda.plugins.subcommands.doctor.context
   conda.plugins.subcommands.doctor.hookimpl


.. py:data:: context

   

.. py:function:: add_parser_help(p: argparse.ArgumentParser) -> None

   So we can use consistent capitalization and periods in the help. You must
   use the add_help=False argument to ArgumentParser or add_parser to use
   this. Add this first to be consistent with the default argparse output.



.. py:function:: add_parser_prefix(p: argparse.ArgumentParser, prefix_required: bool = False) -> argparse._MutuallyExclusiveGroup


.. py:function:: add_parser_verbose(parser: argparse.ArgumentParser | argparse._ArgumentGroup) -> None


.. py:exception:: EnvironmentLocationNotFound(location)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:function:: is_conda_environment(prefix)


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

      


.. py:data:: hookimpl

   Decorator used to mark plugin hook implementations

.. py:function:: configure_parser(parser: argparse.ArgumentParser)


.. py:function:: execute(args: argparse.Namespace) -> None

   Run registered health_check plugins.


.. py:function:: conda_subcommands()


