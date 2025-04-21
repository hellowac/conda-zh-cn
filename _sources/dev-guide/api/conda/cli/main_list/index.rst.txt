:py:mod:`main_list`
===================

.. py:module:: conda.cli.main_list

.. autoapi-nested-parse::

   CLI implementation for `conda list`.

   Lists all packages installed into an environment.




Functions
---------

.. autoapisummary::

   conda.cli.main_list.configure_parser
   conda.cli.main_list.print_export_header
   conda.cli.main_list.get_packages
   conda.cli.main_list.list_packages
   conda.cli.main_list.print_packages
   conda.cli.main_list.print_explicit
   conda.cli.main_list.execute



.. py:function:: configure_parser(sub_parsers: argparse._SubParsersAction, **kwargs) -> argparse.ArgumentParser


.. py:function:: print_export_header(subdir)


.. py:function:: get_packages(installed, regex)


.. py:function:: list_packages(prefix, regex=None, format='human', reverse=False, show_channel_urls=None)


.. py:function:: print_packages(prefix, regex=None, format='human', reverse=False, piplist=False, json=False, show_channel_urls=None)


.. py:function:: print_explicit(prefix, add_md5=False, remove_auth=True, add_sha256=False)


.. py:function:: execute(args: argparse.Namespace, parser: argparse.ArgumentParser) -> int


