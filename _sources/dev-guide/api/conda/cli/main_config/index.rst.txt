:py:mod:`main_config`
=====================

.. py:module:: conda.cli.main_config

.. autoapi-nested-parse::

   CLI implementation for `conda config`.

   Allows for programmatically interacting with conda's configuration files (e.g., `~/.condarc`).




Functions
---------

.. autoapisummary::

   conda.cli.main_config.configure_parser
   conda.cli.main_config.execute
   conda.cli.main_config.format_dict
   conda.cli.main_config.parameter_description_builder
   conda.cli.main_config.describe_all_parameters
   conda.cli.main_config.print_config_item
   conda.cli.main_config._get_key
   conda.cli.main_config._set_key
   conda.cli.main_config._remove_item
   conda.cli.main_config._remove_key
   conda.cli.main_config._read_rc
   conda.cli.main_config._write_rc
   conda.cli.main_config.set_keys
   conda.cli.main_config.execute_config



.. py:function:: configure_parser(sub_parsers: argparse._SubParsersAction, **kwargs) -> argparse.ArgumentParser


.. py:function:: execute(args: argparse.Namespace, parser: argparse.ArgumentParser) -> int


.. py:function:: format_dict(d)


.. py:function:: parameter_description_builder(name)


.. py:function:: describe_all_parameters()


.. py:function:: print_config_item(key, value)


.. py:function:: _get_key(key: str, config: dict, *, json: dict[str, Any] = {}, warnings: list[str] = []) -> None


.. py:function:: _set_key(key: str, item: Any, config: dict) -> None


.. py:function:: _remove_item(key: str, item: Any, config: dict) -> None


.. py:function:: _remove_key(key: str, config: dict) -> None


.. py:function:: _read_rc(path: str | os.PathLike | pathlib.Path) -> dict


.. py:function:: _write_rc(path: str | os.PathLike | pathlib.Path, config: dict) -> None


.. py:function:: set_keys(*args: tuple[str, Any], path: str | os.PathLike | pathlib.Path) -> None


.. py:function:: execute_config(args, parser)


