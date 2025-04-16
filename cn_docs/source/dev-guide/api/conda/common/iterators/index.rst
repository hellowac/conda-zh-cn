:py:mod:`iterators`
===================

.. py:module:: conda.common.iterators

.. autoapi-nested-parse::

   Replacements for parts of the toolz library.




Functions
---------

.. autoapisummary::

   conda.common.iterators.groupby_to_dict
   conda.common.iterators.unique



.. py:function:: groupby_to_dict(keyfunc, sequence)

   A `toolz`-style groupby implementation.

   Returns a dictionary of { key: [group] } instead of iterators.


.. py:function:: unique(sequence: collections.abc.Sequence[Any]) -> collections.abc.Generator[Any, None, None]

   A `toolz` inspired `unique` implementation.

   Returns a generator of unique elements in the sequence


