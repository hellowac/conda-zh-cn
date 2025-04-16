:py:mod:`main_rename`
=====================

.. py:module:: conda.cli.main_rename

.. autoapi-nested-parse::

   CLI implementation for `conda rename`.

   Renames an existing environment by cloning it and then removing the original environment.




Functions
---------

.. autoapisummary::

   conda.cli.main_rename.configure_parser
   conda.cli.main_rename.check_protected_dirs
   conda.cli.main_rename.validate_src
   conda.cli.main_rename.validate_destination
   conda.cli.main_rename.execute



.. py:function:: configure_parser(sub_parsers: argparse._SubParsersAction, **kwargs) -> argparse.ArgumentParser


.. py:function:: check_protected_dirs(prefix: str | pathlib.Path, json: bool = False) -> None

   Ensure that the new prefix does not contain protected directories.


.. py:function:: validate_src() -> str

   Ensure that we are receiving at least one valid value for the environment
   to be renamed and that the "base" environment is not being renamed


.. py:function:: validate_destination(dest: str, force: bool = False) -> str

   Ensure that our destination does not exist


.. py:function:: execute(args: argparse.Namespace, parser: argparse.ArgumentParser) -> int

   Executes the command for renaming an existing environment.


