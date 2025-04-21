:py:mod:`main_search`
=====================

.. py:module:: conda.cli.main_search

.. autoapi-nested-parse::

   CLI implementation for `conda search`.

   Query channels for packages matching the provided package spec.




Functions
---------

.. autoapisummary::

   conda.cli.main_search.configure_parser
   conda.cli.main_search.execute
   conda.cli.main_search._pretty_record_format
   conda.cli.main_search.pretty_record



.. py:function:: configure_parser(sub_parsers: argparse._SubParsersAction, **kwargs) -> argparse.ArgumentParser


.. py:function:: execute(args: argparse.Namespace, parser: argparse.ArgumentParser) -> int

   Implements `conda search` commands.

   `conda search <spec>` searches channels for packages.
   `conda search <spec> --envs` searches environments for packages.



.. py:function:: _pretty_record_format(record: conda.models.records.PackageRecord) -> str

   Format a `PackageRecord` for `pretty_record()`


.. py:function:: pretty_record(record: conda.models.records.PackageRecord, print=print) -> None

   Pretty prints a `PackageRecord`.

   :param record:  The `PackageRecord` object to print.


