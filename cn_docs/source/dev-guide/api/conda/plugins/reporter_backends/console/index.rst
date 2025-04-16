:py:mod:`console`
=================

.. py:module:: conda.plugins.reporter_backends.console

.. autoapi-nested-parse::

   Defines a "console" reporter backend.

   This reporter backend provides the default output for conda.



Classes
-------

.. autoapisummary::

   conda.plugins.reporter_backends.console.QuietProgressBar
   conda.plugins.reporter_backends.console.TQDMProgressBar
   conda.plugins.reporter_backends.console.Spinner
   conda.plugins.reporter_backends.console.QuietSpinner
   conda.plugins.reporter_backends.console.ConsoleReporterRenderer



Functions
---------

.. autoapisummary::

   conda.plugins.reporter_backends.console.conda_reporter_backends



.. py:class:: QuietProgressBar(description: str, **kwargs)


   Bases: :py:obj:`conda.plugins.types.ProgressBarBase`

   Progress bar class used when no output should be printed

   .. py:method:: update_to(fraction) -> None


   .. py:method:: refresh() -> None


   .. py:method:: close() -> None



.. py:class:: TQDMProgressBar(description: str, position=None, leave=True, **kwargs)


   Bases: :py:obj:`conda.plugins.types.ProgressBarBase`

   Progress bar class used for tqdm progress bars

   .. py:method:: update_to(fraction) -> None


   .. py:method:: close() -> None


   .. py:method:: refresh() -> None


   .. py:method:: _tqdm(*args, **kwargs)
      :staticmethod:

      Deferred import so it doesn't hit the `conda activate` paths.



.. py:class:: Spinner(message, fail_message='failed\n')


   Bases: :py:obj:`conda.plugins.types.SpinnerBase`

   Helper class that provides a standard way to create an ABC using
   inheritance.

   .. py:attribute:: spinner_cycle

      

   .. py:method:: start()


   .. py:method:: stop()


   .. py:method:: _start_spinning()


   .. py:method:: __enter__()


   .. py:method:: __exit__(exc_type, exc_val, exc_tb)



.. py:class:: QuietSpinner(message: str, fail_message: str = 'failed\n')


   Bases: :py:obj:`conda.plugins.types.SpinnerBase`

   Helper class that provides a standard way to create an ABC using
   inheritance.

   .. py:method:: __enter__()


   .. py:method:: __exit__(exc_type, exc_val, exc_tb)



.. py:class:: ConsoleReporterRenderer


   Bases: :py:obj:`conda.plugins.types.ReporterRendererBase`

   Default implementation for console reporting in conda

   .. py:method:: detail_view(data: dict[str, str | int | bool], **kwargs) -> str

      Render the output in a "tabular" format.


   .. py:method:: envs_list(prefixes, output=True, **kwargs) -> str

      Render a list of environments


   .. py:method:: progress_bar(description: str, **kwargs) -> conda.plugins.types.ProgressBarBase

      Determines whether to return a TQDMProgressBar or QuietProgressBar


   .. py:method:: spinner(message: str, fail_message: str = 'failed\n') -> conda.plugins.types.SpinnerBase

      Determines whether to return a Spinner or QuietSpinner


   .. py:method:: prompt(message='Proceed', choices=('yes', 'no'), default='yes') -> str

      Implementation of a prompt dialog



.. py:function:: conda_reporter_backends()

   Reporter backend for console


