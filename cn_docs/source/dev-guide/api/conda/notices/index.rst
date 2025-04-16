:py:mod:`notices`
=================

.. py:module:: conda.notices


.. toctree::
   :hidden:
   :titlesonly:
   :maxdepth: 3

   cache/index.rst
   core/index.rst
   fetch/index.rst
   types/index.rst
   views/index.rst



Functions
---------

.. autoapisummary::

   conda.notices.notices



.. py:function:: notices(func)

   Wrapper for "execute" entry points for subcommands.

   If channel notices need to be fetched, we do that first and then
   run the command normally. We then display these notices at the very
   end of the command output so that the user is more likely to see them.

   This ordering was specifically done to address the following bug report:
       - https://github.com/conda/conda/issues/11847

   :param func: Function to be decorated


