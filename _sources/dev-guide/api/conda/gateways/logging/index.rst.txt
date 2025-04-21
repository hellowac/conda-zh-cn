:py:mod:`logging`
=================

.. py:module:: conda.gateways.logging

.. autoapi-nested-parse::

   Configure logging for conda.



Classes
-------

.. autoapisummary::

   conda.gateways.logging.TokenURLFilter
   conda.gateways.logging.StdStreamHandler



Functions
---------

.. autoapisummary::

   conda.gateways.logging.initialize_logging
   conda.gateways.logging.initialize_std_loggers
   conda.gateways.logging.initialize_root_logger
   conda.gateways.logging.set_conda_log_level
   conda.gateways.logging.set_all_logger_level
   conda.gateways.logging.set_file_logging
   conda.gateways.logging.set_log_level



Attributes
----------

.. autoapisummary::

   conda.gateways.logging._VERBOSITY_LEVELS


.. py:data:: _VERBOSITY_LEVELS

   

.. py:class:: TokenURLFilter(name='')


   Bases: :py:obj:`logging.Filter`

   Filter instances are used to perform arbitrary filtering of LogRecords.

   Loggers and Handlers can optionally use Filter instances to filter
   records as desired. The base filter class only allows events which are
   below a certain point in the logger hierarchy. For example, a filter
   initialized with "A.B" will allow events logged by loggers "A.B",
   "A.B.C", "A.B.C.D", "A.B.D" etc. but not "A.BB", "B.A.B" etc. If
   initialized with the empty string, all events are passed.

   Initialize a filter.

   Initialize with the name of the logger which, together with its
   children, will have its events allowed through the filter. If no
   name is specified, allow every event.

   .. py:attribute:: TOKEN_URL_PATTERN

      

   .. py:attribute:: TOKEN_REPLACE

      

   .. py:method:: filter(record)

      Since Python 2's getMessage() is incapable of handling any
      strings that are not unicode when it interpolates the message
      with the arguments, we fix that here by doing it ourselves.

      At the same time we replace tokens in the arguments which was
      not happening until now.



.. py:class:: StdStreamHandler(sys_stream)


   Bases: :py:obj:`logging.StreamHandler`

   Log StreamHandler that always writes to the current sys stream.

   :param sys_stream: stream name, either "stdout" or "stderr" (attribute of module sys)

   .. py:attribute:: terminator
      :value: '\n'

      

   .. py:method:: __getattr__(attr)


   .. py:method:: emit(record)

      Emit a record.

      If a formatter is specified, it is used to format the record.
      The record is then written to the stream with a trailing newline.  If
      exception information is present, it is formatted using
      traceback.print_exception and appended to the stream.  If the stream
      has an 'encoding' attribute, it is used to determine how to do the
      output to the stream.



.. py:function:: initialize_logging()


.. py:function:: initialize_std_loggers()


.. py:function:: initialize_root_logger(level=ERROR)


.. py:function:: set_conda_log_level(level=WARN)


.. py:function:: set_all_logger_level(level=DEBUG)


.. py:function:: set_file_logging(logger_name=None, level=DEBUG, path=None)


.. py:function:: set_log_level(log_level: int)


