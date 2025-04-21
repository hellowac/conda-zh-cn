:py:mod:`main_env_config`
=========================

.. py:module:: conda.cli.main_env_config

.. autoapi-nested-parse::

   CLI implementation for `conda-env config`.

   Allows for programmatically interacting with conda-env's configuration files (e.g., `~/.condarc`).




Functions
---------

.. autoapisummary::

   conda.cli.main_env_config.configure_parser
   conda.cli.main_env_config.execute



.. py:function:: configure_parser(sub_parsers: argparse._SubParsersAction, **kwargs) -> argparse.ArgumentParser


.. py:function:: execute(args: argparse.Namespace, parser: argparse.ArgumentParser) -> int


