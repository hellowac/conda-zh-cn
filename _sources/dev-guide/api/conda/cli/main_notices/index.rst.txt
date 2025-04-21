:py:mod:`main_notices`
======================

.. py:module:: conda.cli.main_notices

.. autoapi-nested-parse::

   CLI implementation for `conda notices`.

   Manually retrieves channel notifications, caches them and displays them.




Functions
---------

.. autoapisummary::

   conda.cli.main_notices.configure_parser
   conda.cli.main_notices.execute



.. py:function:: configure_parser(sub_parsers: argparse._SubParsersAction, **kwargs) -> argparse.ArgumentParser


.. py:function:: execute(args: argparse.Namespace, parser: argparse.ArgumentParser) -> int

   Command that retrieves channel notifications, caches them and displays them.


