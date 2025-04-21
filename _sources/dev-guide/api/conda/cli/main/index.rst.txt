:py:mod:`main`
==============

.. py:module:: conda.cli.main

.. autoapi-nested-parse::

   Entry point for all conda subcommands.




Functions
---------

.. autoapisummary::

   conda.cli.main.init_loggers
   conda.cli.main.main_subshell
   conda.cli.main.main_sourced
   conda.cli.main.main



.. py:function:: init_loggers()


.. py:function:: main_subshell(*args, post_parse_hook=None, **kwargs)

   Entrypoint for the "subshell" invocation of CLI interface. E.g. `conda create`.


.. py:function:: main_sourced(shell, *args, **kwargs)

   Entrypoint for the "sourced" invocation of CLI interface. E.g. `conda activate`.


.. py:function:: main(*args, **kwargs)


