:py:mod:`exceptions`
====================

.. py:module:: conda.auxlib.exceptions


Classes
-------

.. autoapisummary::

   conda.auxlib.exceptions.AuxlibError



Functions
---------

.. autoapisummary::

   conda.auxlib.exceptions.Raise



.. py:function:: Raise(exception)


.. py:class:: AuxlibError


   Mixin to identify exceptions associated with the auxlib package.


.. py:exception:: ValidationError(key, value=None, valid_types=None, msg=None)


   Bases: :py:obj:`AuxlibError`, :py:obj:`TypeError`

   Mixin to identify exceptions associated with the auxlib package.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: ThisShouldNeverHappenError


   Bases: :py:obj:`AuxlibError`, :py:obj:`AttributeError`

   Mixin to identify exceptions associated with the auxlib package.

   Initialize self.  See help(type(self)) for accurate signature.


