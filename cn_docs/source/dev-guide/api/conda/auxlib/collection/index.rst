:py:mod:`collection`
====================

.. py:module:: conda.auxlib.collection

.. autoapi-nested-parse::

   Common collection classes.



Classes
-------

.. autoapisummary::

   conda.auxlib.collection.AttrDict



Functions
---------

.. autoapisummary::

   conda.auxlib.collection.first
   conda.auxlib.collection.last



.. py:class:: AttrDict(*args, **kwargs)


   Bases: :py:obj:`dict`

   Sub-classes dict, and further allows attribute-like access to dictionary items.

   .. rubric:: Examples

   >>> d = AttrDict({'a': 1})
   >>> d.a, d['a'], d.get('a')
   (1, 1, 1)
   >>> d.b = 2
   >>> d.b, d['b']
   (2, 2)

   Initialize self.  See help(type(self)) for accurate signature.


.. py:function:: first(seq, key=bool, default=None, apply=lambda x: x)

   Give the first value that satisfies the key test.

   :param seq:
   :type seq: iterable
   :param key: test for each element of iterable
   :type key: callable
   :param default: returned when all elements fail test
   :param apply: applied to element before return, but not to default value
   :type apply: callable

   Returns: first element in seq that passes key, mutated with optional apply

   .. rubric:: Examples

   >>> first([0, False, None, [], (), 42])
   42
   >>> first([0, False, None, [], ()]) is None
   True
   >>> first([0, False, None, [], ()], default='ohai')
   'ohai'
   >>> import re
   >>> m = first(re.match(regex, 'abc') for regex in ['b.*', 'a(.*)'])
   >>> m.group(1)
   'bc'

   The optional `key` argument specifies a one-argument predicate function
   like that used for `filter()`.  The `key` argument, if supplied, must be
   in keyword form.  For example:
   >>> first([1, 1, 3, 4, 5], key=lambda x: x % 2 == 0)
   4


.. py:function:: last(seq, key=bool, default=None, apply=lambda x: x)


