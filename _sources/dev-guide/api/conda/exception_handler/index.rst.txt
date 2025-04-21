:py:mod:`exception_handler`
===========================

.. py:module:: conda.exception_handler

.. autoapi-nested-parse::

   Error handling and error reporting.



Classes
-------

.. autoapisummary::

   conda.exception_handler.ExceptionHandler



Functions
---------

.. autoapisummary::

   conda.exception_handler.conda_exception_handler



.. py:class:: ExceptionHandler


   .. py:property:: http_timeout


   .. py:property:: user_agent


   .. py:property:: error_upload_url


   .. py:method:: __call__(func, *args, **kwargs)


   .. py:method:: write_out(*content)


   .. py:method:: handle_exception(exc_val, exc_tb)


   .. py:method:: handle_application_exception(exc_val, exc_tb)


   .. py:method:: _print_conda_exception(exc_val, exc_tb)


   .. py:method:: handle_unexpected_exception(exc_val, exc_tb)


   .. py:method:: handle_reportable_application_exception(exc_val, exc_tb)


   .. py:method:: get_error_report(exc_val, exc_tb)


   .. py:method:: print_unexpected_error_report(error_report)


   .. py:method:: print_expected_error_report(error_report)


   .. py:method:: _isatty()


   .. py:method:: _upload(error_report) -> None

      Determine whether or not to upload the error report.


   .. py:method:: _ask_upload()


   .. py:method:: _execute_upload(error_report)


   .. py:method:: _post_upload(do_upload)



.. py:function:: conda_exception_handler(func, *args, **kwargs)


