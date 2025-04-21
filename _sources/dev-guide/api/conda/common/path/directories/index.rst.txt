:py:mod:`directories`
=====================

.. py:module:: conda.common.path.directories

.. autoapi-nested-parse::

   Common directory utilities.




Functions
---------

.. autoapisummary::

   conda.common.path.directories.tokenized_startswith
   conda.common.path.directories.get_all_directories
   conda.common.path.directories.get_leaf_directories
   conda.common.path.directories.explode_directories



.. py:function:: tokenized_startswith(test_iterable, startswith_iterable)


.. py:function:: get_all_directories(files: collections.abc.Iterable[str]) -> list[tuple[str, Ellipsis]]


.. py:function:: get_leaf_directories(files: collections.abc.Iterable[str]) -> collections.abc.Sequence[str]


.. py:function:: explode_directories(child_directories: collections.abc.Iterable[tuple[str, Ellipsis]]) -> set[str]


