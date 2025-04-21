:py:mod:`main_clean`
====================

.. py:module:: conda.cli.main_clean

.. autoapi-nested-parse::

   CLI implementation for `conda clean`.

   Removes cached package tarballs, index files, package metadata, temporary files, and log files.




Functions
---------

.. autoapisummary::

   conda.cli.main_clean.configure_parser
   conda.cli.main_clean._get_size
   conda.cli.main_clean._get_pkgs_dirs
   conda.cli.main_clean._get_total_size
   conda.cli.main_clean._rm_rf
   conda.cli.main_clean.find_tarballs
   conda.cli.main_clean.find_pkgs
   conda.cli.main_clean.rm_pkgs
   conda.cli.main_clean.find_index_cache
   conda.cli.main_clean.find_pkgs_dirs
   conda.cli.main_clean.find_tempfiles
   conda.cli.main_clean.find_logfiles
   conda.cli.main_clean.rm_items
   conda.cli.main_clean._execute
   conda.cli.main_clean.execute



.. py:function:: configure_parser(sub_parsers: argparse._SubParsersAction, **kwargs) -> argparse.ArgumentParser


.. py:function:: _get_size(*parts: str, warnings: list[str] | None) -> int


.. py:function:: _get_pkgs_dirs(pkg_sizes: dict[str, dict[str, int]]) -> dict[str, tuple[str, Ellipsis]]


.. py:function:: _get_total_size(pkg_sizes: dict[str, dict[str, int]]) -> int


.. py:function:: _rm_rf(*parts: str, quiet: bool, verbose: bool) -> None


.. py:function:: find_tarballs() -> dict[str, Any]


.. py:function:: find_pkgs() -> dict[str, Any]


.. py:function:: rm_pkgs(pkgs_dirs: dict[str, tuple[str]], warnings: list[str], total_size: int, pkg_sizes: dict[str, dict[str, int]], *, quiet: bool, verbose: bool, dry_run: bool, name: str) -> None


.. py:function:: find_index_cache() -> list[str]


.. py:function:: find_pkgs_dirs() -> list[str]


.. py:function:: find_tempfiles(paths: collections.abc.Iterable[str]) -> list[str]


.. py:function:: find_logfiles() -> list[str]


.. py:function:: rm_items(items: list[str], *, quiet: bool, verbose: bool, dry_run: bool, name: str) -> None


.. py:function:: _execute(args, parser)


.. py:function:: execute(args: argparse.Namespace, parser: argparse.ArgumentParser) -> int


