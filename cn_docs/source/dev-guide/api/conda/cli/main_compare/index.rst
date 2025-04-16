:py:mod:`main_compare`
======================

.. py:module:: conda.cli.main_compare

.. autoapi-nested-parse::

   CLI implementation for `conda compare`.

   Compare the packages in an environment with the packages listed in an environment file.




Functions
---------

.. autoapisummary::

   conda.cli.main_compare.configure_parser
   conda.cli.main_compare.get_packages
   conda.cli.main_compare.compare_packages
   conda.cli.main_compare.execute



.. py:function:: configure_parser(sub_parsers: argparse._SubParsersAction, **kwargs) -> argparse.ArgumentParser


.. py:function:: get_packages(prefix)


.. py:function:: compare_packages(active_pkgs, specification_pkgs) -> tuple[int, list[str]]


.. py:function:: execute(args: argparse.Namespace, parser: argparse.ArgumentParser) -> int


