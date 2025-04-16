:py:mod:`update`
================

.. py:module:: conda.gateways.disk.update

.. autoapi-nested-parse::

   Disk utility functions for modifying existing files or directories.




Functions
---------

.. autoapisummary::

   conda.gateways.disk.update.update_file_in_place_as_binary
   conda.gateways.disk.update.rename
   conda.gateways.disk.update.rename_context
   conda.gateways.disk.update.backoff_rename
   conda.gateways.disk.update.touch



Attributes
----------

.. autoapisummary::

   conda.gateways.disk.update.SHEBANG_REGEX


.. py:data:: SHEBANG_REGEX

   

.. py:exception:: CancelOperation


   Bases: :py:obj:`Exception`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:function:: update_file_in_place_as_binary(file_full_path, callback)


.. py:function:: rename(source_path, destination_path, force=False)


.. py:function:: rename_context(source: str, destination: str | None = None, dry_run: bool = False)

   Used for removing a directory when there are dependent actions (i.e. you need to ensure
   other actions succeed before removing it).

   .. rubric:: Example

   with rename_context(directory):
       # Do dependent actions here


.. py:function:: backoff_rename(source_path, destination_path, force=False)


.. py:function:: touch(path, mkdir=False, sudo_safe=False)


