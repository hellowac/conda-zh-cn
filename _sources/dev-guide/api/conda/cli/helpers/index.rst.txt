:py:mod:`helpers`
=================

.. py:module:: conda.cli.helpers

.. autoapi-nested-parse::

   Collection of helper functions to standardize reused CLI arguments.



Classes
-------

.. autoapisummary::

   conda.cli.helpers._ValidatePackages



Functions
---------

.. autoapisummary::

   conda.cli.helpers.add_parser_create_install_update
   conda.cli.helpers.add_parser_pscheck
   conda.cli.helpers.add_parser_show_channel_urls
   conda.cli.helpers.add_parser_help
   conda.cli.helpers.add_parser_prefix
   conda.cli.helpers.add_parser_prefix_to_group
   conda.cli.helpers.add_parser_json
   conda.cli.helpers.add_output_and_prompt_options
   conda.cli.helpers.add_parser_channels
   conda.cli.helpers.add_parser_solver_mode
   conda.cli.helpers.add_parser_update_modifiers
   conda.cli.helpers.add_parser_prune
   conda.cli.helpers.add_parser_solver
   conda.cli.helpers.add_parser_networking
   conda.cli.helpers.add_parser_package_install_options
   conda.cli.helpers.add_parser_known
   conda.cli.helpers.add_parser_default_packages
   conda.cli.helpers.add_parser_platform
   conda.cli.helpers.add_parser_verbose



.. py:class:: _ValidatePackages(option_strings, dest, nargs=None, const=None, default=None, type=None, choices=None, required=False, help=None, metavar=None)


   Bases: :py:obj:`argparse._StoreAction`

   Used to validate match specs of packages

   .. py:method:: _validate_no_denylist_channels(packages_specs)
      :staticmethod:

      Ensure the packages do not contain denylist_channels


   .. py:method:: __call__(parser, namespace, values, option_string=None)



.. py:function:: add_parser_create_install_update(p, prefix_required=False)


.. py:function:: add_parser_pscheck(p: argparse.ArgumentParser) -> None


.. py:function:: add_parser_show_channel_urls(p: argparse.ArgumentParser | argparse._ArgumentGroup) -> None


.. py:function:: add_parser_help(p: argparse.ArgumentParser) -> None

   So we can use consistent capitalization and periods in the help. You must
   use the add_help=False argument to ArgumentParser or add_parser to use
   this. Add this first to be consistent with the default argparse output.



.. py:function:: add_parser_prefix(p: argparse.ArgumentParser, prefix_required: bool = False) -> argparse._MutuallyExclusiveGroup


.. py:function:: add_parser_prefix_to_group(m: argparse._MutuallyExclusiveGroup) -> None


.. py:function:: add_parser_json(p: argparse.ArgumentParser) -> argparse._ArgumentGroup


.. py:function:: add_output_and_prompt_options(p: argparse.ArgumentParser) -> argparse._ArgumentGroup


.. py:function:: add_parser_channels(p: argparse.ArgumentParser) -> argparse._ArgumentGroup


.. py:function:: add_parser_solver_mode(p: argparse.ArgumentParser) -> argparse._ArgumentGroup


.. py:function:: add_parser_update_modifiers(solver_mode_options: argparse.ArgumentParser)


.. py:function:: add_parser_prune(p: argparse.ArgumentParser) -> None


.. py:function:: add_parser_solver(p: argparse.ArgumentParser) -> None

   Add a command-line flag for alternative solver backends.

   See ``context.solver`` for more info.


.. py:function:: add_parser_networking(p: argparse.ArgumentParser) -> argparse._ArgumentGroup


.. py:function:: add_parser_package_install_options(p: argparse.ArgumentParser) -> argparse._ArgumentGroup


.. py:function:: add_parser_known(p: argparse.ArgumentParser) -> None


.. py:function:: add_parser_default_packages(p: argparse.ArgumentParser) -> None


.. py:function:: add_parser_platform(parser)


.. py:function:: add_parser_verbose(parser: argparse.ArgumentParser | argparse._ArgumentGroup) -> None


