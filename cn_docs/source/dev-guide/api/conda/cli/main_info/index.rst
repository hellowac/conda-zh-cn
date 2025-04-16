:py:mod:`main_info`
===================

.. py:module:: conda.cli.main_info

.. autoapi-nested-parse::

   CLI implementation for `conda info`.

   Display information about current conda installation.



Classes
-------

.. autoapisummary::

   conda.cli.main_info.InfoRenderer



Functions
---------

.. autoapisummary::

   conda.cli.main_info.configure_parser
   conda.cli.main_info.get_user_site
   conda.cli.main_info.dump_record
   conda.cli.main_info.pretty_package
   conda.cli.main_info.get_info_dict
   conda.cli.main_info.get_env_vars_str
   conda.cli.main_info.get_main_info_display
   conda.cli.main_info.get_main_info_str
   conda.cli.main_info.get_info_components
   conda.cli.main_info.execute



Attributes
----------

.. autoapisummary::

   conda.cli.main_info.IGNORE_FIELDS
   conda.cli.main_info.SKIP_FIELDS
   conda.cli.main_info.InfoComponents


.. py:function:: configure_parser(sub_parsers: argparse._SubParsersAction, **kwargs) -> argparse.ArgumentParser


.. py:function:: get_user_site() -> list[str]

   Method used to populate ``site_dirs`` in ``conda info``.

   :returns: List of directories.


.. py:data:: IGNORE_FIELDS
   :type: set[str]

   

.. py:data:: SKIP_FIELDS
   :type: set[str]

   

.. py:function:: dump_record(prec: conda.models.records.PackageRecord) -> dict[str, Any]

   Returns a dictionary of key/value pairs from ``prec``.  Keys included in ``IGNORE_FIELDS`` are not returned.

   :param prec: A ``PackageRecord`` object.
   :returns: A dictionary of elements dumped from ``prec``


.. py:function:: pretty_package(prec: conda.models.records.PackageRecord) -> None

   Pretty prints contents of a ``PackageRecord``

   :param prec: A ``PackageRecord``


.. py:function:: get_info_dict() -> dict[str, Any]

   Returns a dictionary of contextual information.

   :returns:  Dictionary of conda information to be sent to stdout.


.. py:function:: get_env_vars_str(info_dict: dict[str, Any]) -> str

   Returns a printable string representing environment variables from the dictionary returned by ``get_info_dict``.

   :param info_dict:  The returned dictionary from ``get_info_dict()``.
   :returns:  String to print.


.. py:function:: get_main_info_display(info_dict: dict[str, Any]) -> dict[str, str]

   Returns the data that can be used to display information for conda info


.. py:function:: get_main_info_str(info_dict: dict[str, Any]) -> str

   Returns a printable string of the contents of ``info_dict``.

   :param info_dict:  The output of ``get_info_dict()``.
   :returns:  String to print.


.. py:data:: InfoComponents

   

.. py:class:: InfoRenderer(context)


   Provides a ``render`` method for rendering ``InfoComponents``

   .. py:method:: render(components: collections.abc.Iterable[InfoComponents])

      Iterates through the registered components, obtains the data to render via a
      ``_<component>_component`` method and then renders it.


   .. py:method:: _base_component() -> str | dict


   .. py:method:: _channels_component() -> str | dict


   .. py:method:: _detail_component() -> dict[str, str]


   .. py:method:: _envs_component()


   .. py:method:: _system_component() -> str


   .. py:method:: _json_all_component() -> dict[str, Any]



.. py:function:: get_info_components(args: argparse.Namespace, context: conda.base.context.Context) -> set[InfoComponents]

   Based on values in ``args`` and ``context`` determine which components need to be displayed
   and return them as a ``set``


.. py:function:: execute(args: argparse.Namespace, parser: argparse.ArgumentParser) -> int

   Implements ``conda info`` command.

    * ``conda info``
    * ``conda info --base``
    * ``conda info <package_spec> ...``
    * ``conda info --unsafe-channels``
    * ``conda info --envs``
    * ``conda info --system``


