:py:mod:`main_env_vars`
=======================

.. py:module:: conda.cli.main_env_vars

.. autoapi-nested-parse::

   CLI implementation for `conda-env config vars`.

   Allows for configuring conda-env's vars.




Functions
---------

.. autoapisummary::

   conda.cli.main_env_vars.configure_parser
   conda.cli.main_env_vars.execute_list
   conda.cli.main_env_vars.execute_set
   conda.cli.main_env_vars.execute_unset



.. py:function:: configure_parser(sub_parsers: argparse._SubParsersAction, **kwargs) -> argparse.ArgumentParser


.. py:function:: execute_list(args: argparse.Namespace, parser: argparse.ArgumentParser) -> int


.. py:function:: execute_set(args: argparse.Namespace, parser: argparse.ArgumentParser) -> int


.. py:function:: execute_unset(args: argparse.Namespace, parser: argparse.ArgumentParser) -> int


