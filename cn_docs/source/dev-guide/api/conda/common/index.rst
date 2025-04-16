:py:mod:`common`
================

.. py:module:: conda.common

.. autoapi-nested-parse::

   Code in ``conda.common`` is not conda-specific.  Technically, it sits *aside* the application
   stack and not *within* the stack.  It is able to stand independently on its own.
   The *only* allowed imports of conda code in ``conda.common`` modules are imports of other
   ``conda.common`` modules.

   If objects are needed from other parts of conda, they should be passed directly as arguments to
   functions and methods.



.. toctree::
   :hidden:
   :titlesonly:
   :maxdepth: 3

   _logic/index.rst
   _os/index.rst
   compat/index.rst
   configuration/index.rst
   constants/index.rst
   disk/index.rst
   io/index.rst
   iterators/index.rst
   logic/index.rst
   path/index.rst
   pkg_formats/index.rst
   serialize/index.rst
   signals/index.rst
   toposort/index.rst
   url/index.rst


