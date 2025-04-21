:py:mod:`instructions`
======================

.. py:module:: conda.instructions

.. autoapi-nested-parse::

   Define the instruction set (constants) for conda operations.




Functions
---------

.. autoapisummary::

   conda.instructions.PRINT_CMD
   conda.instructions.FETCH_CMD
   conda.instructions.EXTRACT_CMD
   conda.instructions.PROGRESSIVEFETCHEXTRACT_CMD
   conda.instructions.UNLINKLINKTRANSACTION_CMD
   conda.instructions.check_files_in_package



Attributes
----------

.. autoapisummary::

   conda.instructions.CHECK_FETCH
   conda.instructions.FETCH
   conda.instructions.CHECK_EXTRACT
   conda.instructions.EXTRACT
   conda.instructions.RM_EXTRACTED
   conda.instructions.RM_FETCHED
   conda.instructions.PRINT
   conda.instructions.PROGRESS
   conda.instructions.SYMLINK_CONDA
   conda.instructions.UNLINK
   conda.instructions.LINK
   conda.instructions.UNLINKLINKTRANSACTION
   conda.instructions.PROGRESSIVEFETCHEXTRACT
   conda.instructions.PROGRESS_COMMANDS
   conda.instructions.ACTION_CODES
   conda.instructions.commands
   conda.instructions.OP_ORDER


.. py:data:: CHECK_FETCH
   :value: 'CHECK_FETCH'

   

.. py:data:: FETCH
   :value: 'FETCH'

   

.. py:data:: CHECK_EXTRACT
   :value: 'CHECK_EXTRACT'

   

.. py:data:: EXTRACT
   :value: 'EXTRACT'

   

.. py:data:: RM_EXTRACTED
   :value: 'RM_EXTRACTED'

   

.. py:data:: RM_FETCHED
   :value: 'RM_FETCHED'

   

.. py:data:: PRINT
   :value: 'PRINT'

   

.. py:data:: PROGRESS
   :value: 'PROGRESS'

   

.. py:data:: SYMLINK_CONDA
   :value: 'SYMLINK_CONDA'

   

.. py:data:: UNLINK
   :value: 'UNLINK'

   

.. py:data:: LINK
   :value: 'LINK'

   

.. py:data:: UNLINKLINKTRANSACTION
   :value: 'UNLINKLINKTRANSACTION'

   

.. py:data:: PROGRESSIVEFETCHEXTRACT
   :value: 'PROGRESSIVEFETCHEXTRACT'

   

.. py:data:: PROGRESS_COMMANDS

   

.. py:data:: ACTION_CODES
   :value: ()

   

.. py:function:: PRINT_CMD(state, arg)


.. py:function:: FETCH_CMD(state, package_cache_entry)


.. py:function:: EXTRACT_CMD(state, arg)


.. py:function:: PROGRESSIVEFETCHEXTRACT_CMD(state, progressive_fetch_extract)


.. py:function:: UNLINKLINKTRANSACTION_CMD(state, arg)


.. py:function:: check_files_in_package(source_dir, files)


.. py:data:: commands

   

.. py:data:: OP_ORDER
   :value: ()

   

