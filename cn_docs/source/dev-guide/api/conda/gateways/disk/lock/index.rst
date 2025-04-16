:py:mod:`lock`
==============

.. py:module:: conda.gateways.disk.lock

.. autoapi-nested-parse::

   Record locking to manage potential repodata / repodata metadata file contention
   between conda processes. Try to acquire a lock on a single byte in the metadat
   file; modify both files; then release the lock.




Functions
---------

.. autoapisummary::

   conda.gateways.disk.lock._lock_noop
   conda.gateways.disk.lock._lock_impl
   conda.gateways.disk.lock.lock



Attributes
----------

.. autoapisummary::

   conda.gateways.disk.lock.LOCK_BYTE
   conda.gateways.disk.lock.LOCK_ATTEMPTS
   conda.gateways.disk.lock.LOCK_SLEEP


.. py:data:: LOCK_BYTE
   :value: 21

   

.. py:data:: LOCK_ATTEMPTS
   :value: 10

   

.. py:data:: LOCK_SLEEP
   :value: 1

   

.. py:function:: _lock_noop(fd)

   When locking is not available.


.. py:function:: _lock_impl(fd)


.. py:function:: lock(fd)


