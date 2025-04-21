:py:mod:`reporters`
===================

.. py:module:: conda.reporters

.. autoapi-nested-parse::

   Holds functions for output rendering in conda




Functions
---------

.. autoapisummary::

   conda.reporters._get_render_func
   conda.reporters.render
   conda.reporters.get_progress_bar
   conda.reporters.get_progress_bar_context_manager
   conda.reporters.get_spinner
   conda.reporters.confirm_yn



Attributes
----------

.. autoapisummary::

   conda.reporters.logger


.. py:data:: logger

   

.. py:function:: _get_render_func(style: str | None = None) -> Callable

   Retrieves the render function to use


.. py:function:: render(data, style: str | None = None, **kwargs) -> None

   Used to render output in conda

   The output will either be rendered as "json" or normal "console" output to stdout.
   This function allows us to configure different reporter backends for these two types
   of output.


.. py:function:: get_progress_bar(description: str, **kwargs) -> conda.plugins.types.ProgressBarBase

   Retrieve the progress bar for the currently configured reporter backend


.. py:function:: get_progress_bar_context_manager() -> contextlib.AbstractContextManager

   Retrieve progress bar context manager to use with registered reporter


.. py:function:: get_spinner(message: str, fail_message: str = 'failed\n') -> conda.plugins.types.SpinnerBase

   Retrieve spinner to use with registered reporter


.. py:function:: confirm_yn(message: str = 'Proceed', default='yes', dry_run=None) -> bool

   Display a "yes/no" confirmation input


