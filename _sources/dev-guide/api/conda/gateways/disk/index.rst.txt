:py:mod:`disk`
==============

.. py:module:: conda.gateways.disk


.. toctree::
   :hidden:
   :titlesonly:
   :maxdepth: 3

   create/index.rst
   delete/index.rst
   link/index.rst
   lock/index.rst
   permissions/index.rst
   read/index.rst
   test/index.rst
   update/index.rst



Functions
---------

.. autoapisummary::

   conda.gateways.disk.exp_backoff_fn
   conda.gateways.disk.mkdir_p
   conda.gateways.disk.mkdir_p_sudo_safe



Attributes
----------

.. autoapisummary::

   conda.gateways.disk.on_win
   conda.gateways.disk.TRACE
   conda.gateways.disk.MAX_TRIES


.. py:data:: on_win

   

.. py:data:: TRACE
   :value: 5

   

.. py:data:: MAX_TRIES
   :value: 7

   

.. py:function:: exp_backoff_fn(fn, *args, **kwargs)

   Mostly for retrying file operations that fail on Windows due to virus scanners


.. py:function:: mkdir_p(path)


.. py:function:: mkdir_p_sudo_safe(path)


