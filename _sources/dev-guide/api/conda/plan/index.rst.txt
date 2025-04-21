:py:mod:`plan`
==============

.. py:module:: conda.plan

.. autoapi-nested-parse::

   Handle the planning of installs and their execution.

   .. note::

      conda.install uses canonical package names in its interface functions,
      whereas conda.resolve uses package filenames, as those are used as index
      keys.  We try to keep fixes to this "impedance mismatch" local to this
      module.



