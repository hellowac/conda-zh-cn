:py:mod:`toposort`
==================

.. py:module:: conda.common.toposort

.. autoapi-nested-parse::

   Topological sorting implementation.




Functions
---------

.. autoapisummary::

   conda.common.toposort._toposort
   conda.common.toposort.pop_key
   conda.common.toposort._safe_toposort
   conda.common.toposort.toposort



.. py:function:: _toposort(data)

   Dependencies are expressed as a dictionary whose keys are items
   and whose values are a set of dependent items. Output is a list of
   sets in topological order. The first set consists of items with no
   dependences, each subsequent set consists of items that depend upon
   items in the preceding sets.


.. py:function:: pop_key(data)

   Pop an item from the graph that has the fewest dependencies in the case of a tie
   The winners will be sorted alphabetically


.. py:function:: _safe_toposort(data)

   Dependencies are expressed as a dictionary whose keys are items
   and whose values are a set of dependent items. Output is a list of
   sets in topological order. The first set consists of items with no
   dependencies, each subsequent set consists of items that depend upon
   items in the preceding sets.


.. py:function:: toposort(data, safe=True)


