:py:mod:`core`
==============

.. py:module:: conda.core

.. autoapi-nested-parse::

   Code in ``conda.core`` is the core logic.  It is strictly forbidden from having side effects.
   No printing to stdout or stderr, no disk manipulation, no http requests.
   All side effects should be implemented through ``conda.gateways``.  Objects defined in
   ``conda.models`` should be heavily preferred for ``conda.core`` function/method arguments
   and return values.

   Conda modules importable from ``conda.core`` are

   - ``conda.common``
   - ``conda.core``
   - ``conda.models``
   - ``conda.gateways``

   Conda modules strictly off limits for import within ``conda.core`` are

   - ``conda.api``
   - ``conda.cli``
   - ``conda.client``



.. toctree::
   :hidden:
   :titlesonly:
   :maxdepth: 3

   envs_manager/index.rst
   index/index.rst
   initialize/index.rst
   link/index.rst
   package_cache_data/index.rst
   path_actions/index.rst
   portability/index.rst
   prefix_data/index.rst
   solve/index.rst
   subdir_data/index.rst


