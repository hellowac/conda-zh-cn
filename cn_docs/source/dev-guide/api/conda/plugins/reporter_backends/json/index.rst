:py:mod:`json`
==============

.. py:module:: conda.plugins.reporter_backends.json

.. autoapi-nested-parse::

   Defines a JSON reporter backend

   This reporter backend is used to provide JSON strings for output rendering. It is
   essentially just a wrapper around ``conda.common.serialize.json_dump``.



Classes
-------

.. autoapisummary::

   conda.plugins.reporter_backends.json.JSONProgressBar
   conda.plugins.reporter_backends.json.JSONReporterRenderer
   conda.plugins.reporter_backends.json.JSONSpinner



Functions
---------

.. autoapisummary::

   conda.plugins.reporter_backends.json.conda_reporter_backends



.. py:class:: JSONProgressBar(description: str, enabled: bool = True, **kwargs)


   Bases: :py:obj:`conda.plugins.types.ProgressBarBase`

   Progress bar that outputs JSON to stdout

   .. py:method:: update_to(fraction) -> None


   .. py:method:: refresh()


   .. py:method:: close()


   .. py:method:: get_lock()
      :classmethod:

      Used for our own sys.stdout.write/flush calls



.. py:class:: JSONReporterRenderer


   Bases: :py:obj:`conda.plugins.types.ReporterRendererBase`

   Default implementation for JSON reporting in conda

   .. py:method:: render(data: Any, **kwargs) -> str


   .. py:method:: detail_view(data: dict[str, str | int | bool], **kwargs) -> str

      Render the output in a "tabular" format.


   .. py:method:: envs_list(data, **kwargs) -> str

      Render a list of environments


   .. py:method:: progress_bar(description: str, **kwargs) -> conda.plugins.types.ProgressBarBase

      Return a :class:`~conda.plugins.types.ProgressBarBase~` object to use as a progress bar


   .. py:method:: spinner(message: str, fail_message: str = 'failed\n') -> conda.plugins.types.SpinnerBase

      Return a :class:`~conda.plugins.types.SpinnerBase~` object to use as a spinner (i.e.
      loading dialog)


   .. py:method:: prompt(message: str = 'Proceed', choices=('yes', 'no'), default: str = 'yes') -> str

      For this class, we want this method to do nothing



.. py:class:: JSONSpinner(message: str, fail_message: str = 'failed\n')


   Bases: :py:obj:`conda.plugins.types.SpinnerBase`

   This class for a JSONSpinner does nothing because we do not want to include this output.

   .. py:method:: __enter__()


   .. py:method:: __exit__(exc_type, exc_val, exc_tb)



.. py:function:: conda_reporter_backends()

   Reporter backend for JSON

   This is the default reporter backend that returns objects as JSON strings.


