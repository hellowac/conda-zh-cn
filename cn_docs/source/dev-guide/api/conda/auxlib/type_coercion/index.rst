:py:mod:`type_coercion`
=======================

.. py:module:: conda.auxlib.type_coercion

.. autoapi-nested-parse::

   Collection of functions to coerce conversion of types with an intelligent guess.




Functions
---------

.. autoapisummary::

   conda.auxlib.type_coercion.numberify
   conda.auxlib.type_coercion.boolify
   conda.auxlib.type_coercion.typify
   conda.auxlib.type_coercion.maybecall



.. py:function:: numberify(value)

   .. rubric:: 示例

   >>> [numberify(x) for x in ('1234', 1234, '0755', 0o0755, False, 0, '0', True, 1, '1')]
     [1234, 1234, 755, 493, 0, 0, 0, 1, 1, 1]
   >>> [numberify(x) for x in ('12.34', 12.34, 1.2+3.5j, '1.2+3.5j')]
   [12.34, 12.34, (1.2+3.5j), (1.2+3.5j)]


.. py:function:: boolify(value, nullable=False, return_string=False)

   Convert a number, string, or sequence type into a pure boolean.

   :param value: pretty much anything
   :type value: number, string, sequence

   :returns: boolean representation of the given value
   :rtype: bool

   .. rubric:: 示例

   >>> [boolify(x) for x in ('yes', 'no')]
   [True, False]
   >>> [boolify(x) for x in (0.1, 0+0j, True, '0', '0.0', '0.1', '2')]
   [True, False, True, False, False, True, True]
   >>> [boolify(x) for x in ("true", "yes", "on", "y")]
   [True, True, True, True]
   >>> [boolify(x) for x in ("no", "non", "none", "off", "")]
   [False, False, False, False, False]
   >>> [boolify(x) for x in ([], set(), dict(), tuple())]
   [False, False, False, False]
   >>> [boolify(x) for x in ([1], set([False]), dict({'a': 1}), tuple([2]))]
   [True, True, True, True]


.. py:function:: typify(value, type_hint=None)

   Take a primitive value, usually a string, and try to make a more relevant type out of it.
   An optional type_hint will try to coerce the value to that type.

   :param value: Usually a string, not a sequence
   :type value: Any
   :param type_hint:
   :type type_hint: type or tuple[type]

   .. rubric:: 示例

   >>> typify('32')
   32
   >>> typify('32', float)
   32.0
   >>> typify('32.0')
   32.0
   >>> typify('32.0.0')
   '32.0.0'
   >>> [typify(x) for x in ('true', 'yes', 'on')]
   [True, True, True]
   >>> [typify(x) for x in ('no', 'FALSe', 'off')]
   [False, False, False]
   >>> [typify(x) for x in ('none', 'None', None)]
   [None, None, None]


.. py:function:: maybecall(value)


