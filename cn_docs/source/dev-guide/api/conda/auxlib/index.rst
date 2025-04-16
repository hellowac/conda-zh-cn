:py:mod:`auxlib`
================

.. py:module:: conda.auxlib

.. autoapi-nested-parse::

   Auxlib is an auxiliary library to the python standard library.

   The aim is to provide core generic features for app development in python. Auxlib fills in some
   python stdlib gaps much like `pytoolz <https://github.com/pytoolz/>`_ has for functional
   programming, `pyrsistent <https://github.com/tobgu/pyrsistent/>`_ has for data structures, or
   `boltons <https://github.com/mahmoud/boltons/>`_ has generally.

   Major areas addressed include:
     - :ref:`packaging`: package versioning, with a clean and less invasive alternative to
       versioneer
     - :ref:`entity`: robust base class for type-enforced data models and transfer objects
     - :ref:`type_coercion`: intelligent type coercion utilities
     - :ref:`configuration`: a map implementation designed specifically to hold application
       configuration and context information
     - :ref:`factory`: factory pattern implementation
     - :ref:`path`: file path utilities especially helpful when working with various python
       package formats
     - :ref:`logz`: logging initialization routines to simplify python logging setup
     - :ref:`crypt`: simple, but correct, pycrypto wrapper

   [2021-11-09] Our version of auxlib has deviated from the upstream project by a significant amount
   (especially compared with the other vendored packages). Further, the upstream project has low
   popularity and is no longer actively maintained. Consequently it was decided to absorb, refactor,
   and replace auxlib. As a first step of this process we moved conda._vendor.auxlib to conda.auxlib.



.. toctree::
   :hidden:
   :titlesonly:
   :maxdepth: 3

   collection/index.rst
   compat/index.rst
   decorators/index.rst
   entity/index.rst
   exceptions/index.rst
   ish/index.rst
   logz/index.rst
   type_coercion/index.rst


.. py:data:: __version__
   :value: '0.0.43'

   

.. py:data:: __author__
   :value: 'Kale Franz'

   

.. py:data:: __email__
   :value: 'kale@franz.io'

   

.. py:data:: __url__
   :value: 'https://github.com/kalefranz/auxlib'

   

.. py:data:: __license__
   :value: 'ISC'

   

.. py:data:: __copyright__
   :value: '(c) 2015 Kale Franz. All rights reserved.'

   

.. py:data:: __summary__
   :value: 'auxiliary library to the python standard library'

   

