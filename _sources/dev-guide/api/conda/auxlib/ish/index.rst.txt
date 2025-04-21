:py:mod:`ish`
=============

.. py:module:: conda.auxlib.ish



Functions
---------

.. autoapisummary::

   conda.auxlib.ish.dals
   conda.auxlib.ish._get_attr
   conda.auxlib.ish.find_or_none
   conda.auxlib.ish.find_or_raise



.. py:function:: dals(string)

   dedent and left-strip


.. py:function:: _get_attr(obj, attr_name, aliases=())


.. py:function:: find_or_none(key, search_maps, aliases=(), _map_index=0)

   Return the value of the first key found in the list of search_maps,
   otherwise return None.

   .. rubric:: 示例

   >>> from .collection import AttrDict
   >>> d1 = AttrDict({'a': 1, 'b': 2, 'c': 3, 'e': None})
   >>> d2 = AttrDict({'b': 5, 'e': 6, 'f': 7})
   >>> find_or_none('c', (d1, d2))
   3
   >>> find_or_none('f', (d1, d2))
   7
   >>> find_or_none('b', (d1, d2))
   2
   >>> print(find_or_none('g', (d1, d2)))
   None
   >>> find_or_none('e', (d1, d2))
   6


.. py:function:: find_or_raise(key, search_maps, aliases=(), _map_index=0)


