:py:mod:`delete`
================

.. py:module:: conda.gateways.disk.delete

.. autoapi-nested-parse::

   Disk utility functions for deleting files and folders.




Functions
---------

.. autoapisummary::

   conda.gateways.disk.delete.rmtree
   conda.gateways.disk.delete.unlink_or_rename_to_trash
   conda.gateways.disk.delete.remove_empty_parent_paths
   conda.gateways.disk.delete.rm_rf
   conda.gateways.disk.delete.delete_trash
   conda.gateways.disk.delete.backoff_rmdir
   conda.gateways.disk.delete.path_is_clean



.. py:function:: rmtree(path)


.. py:function:: unlink_or_rename_to_trash(path)

   If files are in use, especially on windows, we can't remove them.
   The fallback path is to rename them (but keep their folder the same),
   which maintains the file handle validity.  See comments at:
   https://serverfault.com/a/503769


.. py:function:: remove_empty_parent_paths(path)


.. py:function:: rm_rf(path: str | os.PathLike, clean_empty_parents: bool = False) -> bool

   Completely delete path
   max_retries is the number of times to retry on failure. The default is 5. This only applies
   to deleting a directory.
   If removing path fails and trash is True, files will be moved to the trash directory.


.. py:function:: delete_trash(prefix)


.. py:function:: backoff_rmdir(dirpath, max_tries=MAX_TRIES)


.. py:function:: path_is_clean(path)

   Sometimes we can't completely remove a path because files are considered in use
   by python (hardlinking confusion).  For our tests, it is sufficient that either the
   folder doesn't exist, or nothing but temporary file copies are left.


