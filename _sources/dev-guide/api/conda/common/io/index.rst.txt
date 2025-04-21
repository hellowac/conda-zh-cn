:py:mod:`io`
============

.. py:module:: conda.common.io

.. autoapi-nested-parse::

   Common I/O utilities.



Classes
-------

.. autoapisummary::

   conda.common.io.DeltaSecondsFormatter
   conda.common.io.ContextDecorator
   conda.common.io.SwallowBrokenPipe
   conda.common.io.CaptureTarget
   conda.common.io.Spinner
   conda.common.io.ProgressBar
   conda.common.io.DummyExecutor
   conda.common.io.ThreadLimitedThreadPoolExecutor
   conda.common.io.time_recorder



Functions
---------

.. autoapisummary::

   conda.common.io.dashlist
   conda.common.io.env_vars
   conda.common.io.env_var
   conda.common.io.env_unmodified
   conda.common.io.captured
   conda.common.io.argv
   conda.common.io._logger_lock
   conda.common.io.disable_logger
   conda.common.io.stderr_log_level
   conda.common.io.attach_stderr_handler
   conda.common.io.timeout
   conda.common.io.get_instrumentation_record_file
   conda.common.io.print_instrumentation_data



Attributes
----------

.. autoapisummary::

   conda.common.io.IS_INTERACTIVE
   conda.common.io._FORMATTER
   conda.common.io.swallow_broken_pipe
   conda.common.io.as_completed


.. py:data:: IS_INTERACTIVE

   

.. py:class:: DeltaSecondsFormatter(fmt=None, datefmt=None)


   Bases: :py:obj:`logging.Formatter`

   Logging formatter with additional attributes for run time logging.

   .. attribute:: `delta_secs`

      Elapsed seconds since last log/format call (or creation of logger).

   .. attribute:: `relative_created_secs`

      Like `relativeCreated`, time relative to the initialization of the
      `logging` module but conveniently scaled to seconds as a `float` value.

   Initialize the formatter with specified format strings.

   Initialize the formatter either with the specified format string, or a
   default as described above. Allow for specialized date formatting with
   the optional datefmt argument. If datefmt is omitted, you get an
   ISO8601-like (or RFC 3339-like) format.

   Use a style parameter of '%', '{' or '$' to specify that you want to
   use one of %-formatting, :meth:`str.format` (``{}``) formatting or
   :class:`string.Template` formatting in your format string.

   .. versionchanged:: 3.2
      Added the ``style`` parameter.

   .. py:method:: format(record)

      Format the specified record as text.

      The record's attribute dictionary is used as the operand to a
      string formatting operation which yields the returned string.
      Before formatting the dictionary, a couple of preparatory steps
      are carried out. The message attribute of the record is computed
      using LogRecord.getMessage(). If the formatting string uses the
      time (as determined by a call to usesTime(), formatTime() is
      called to format the event time. If there is exception information,
      it is formatted using formatException() and appended to the message.



.. py:data:: _FORMATTER

   

.. py:function:: dashlist(iterable, indent=2)


.. py:class:: ContextDecorator


   Base class for a context manager class (implementing __enter__() and __exit__()) that also
   makes it a decorator.

   .. py:method:: __call__(f)



.. py:class:: SwallowBrokenPipe


   Bases: :py:obj:`ContextDecorator`

   Base class for a context manager class (implementing __enter__() and __exit__()) that also
   makes it a decorator.

   .. py:method:: __enter__()


   .. py:method:: __exit__(exc_type, exc_val, exc_tb)



.. py:data:: swallow_broken_pipe

   

.. py:class:: CaptureTarget(*args, **kwds)


   Bases: :py:obj:`enum.Enum`

   Constants used for contextmanager captured.

   Used similarly like the constants PIPE, STDOUT for stdlib's subprocess.Popen.

   .. py:attribute:: STRING

      

   .. py:attribute:: STDOUT

      


.. py:function:: env_vars(var_map=None, callback=None, stack_callback=None)


.. py:function:: env_var(name, value, callback=None, stack_callback=None)


.. py:function:: env_unmodified(callback=None)


.. py:function:: captured(stdout=CaptureTarget.STRING, stderr=CaptureTarget.STRING)

   Capture outputs of sys.stdout and sys.stderr.

   If stdout is STRING, capture sys.stdout as a string,
   if stdout is None, do not capture sys.stdout, leaving it untouched,
   otherwise redirect sys.stdout to the file-like object given by stdout.

   Behave correspondingly for stderr with the exception that if stderr is STDOUT,
   redirect sys.stderr to stdout target and set stderr attribute of yielded object to None.

   .. code-block:: pycon

      >>> from conda.common.io import captured
      >>> with captured() as c:
      ...     print("hello world!")
      ...
      >>> c.stdout
      'hello world!\n'

   :param stdout: capture target for sys.stdout, one of STRING, None, or file-like object
   :param stderr: capture target for sys.stderr, one of STRING, STDOUT, None, or file-like object

   :生成器: *CapturedText* --

         has attributes stdout, stderr which are either strings, None or the
             corresponding file-like function argument.


.. py:function:: argv(args_list)


.. py:function:: _logger_lock()


.. py:function:: disable_logger(logger_name)


.. py:function:: stderr_log_level(level, logger_name=None)


.. py:function:: attach_stderr_handler(level=WARN, logger_name=None, propagate=False, formatter=None, filters=None)

   Attach a new `stderr` handler to the given logger and configure both.

   This function creates a new StreamHandler that writes to `stderr` and attaches it
   to the logger given by `logger_name` (which maybe `None`, in which case the root
   logger is used). If the logger already has a handler by the name of `stderr`, it is
   removed first.

   The given `level` is set **for the handler**, not for the logger; however, this
   function also sets the level of the given logger to the minimum of its current
   effective level and the new handler level, ensuring that the handler will receive the
   required log records, while minimizing the number of unnecessary log events. It also
   sets the loggers `propagate` property according to the `propagate` argument.
   The `formatter` argument can be used to set the formatter of the handler.


.. py:function:: timeout(timeout_secs, func, *args, default_return=None, **kwargs)

   Enforce a maximum time for a callable to complete.
   Not yet implemented on Windows.


.. py:class:: Spinner(message, enabled=True, json=False, fail_message='failed\n')


   :param message: A message to prefix the spinner with. The string ': ' is automatically appended.
   :type message: str
   :param enabled: If False, usage is a no-op.
   :type enabled: bool
   :param json: If True, will not output non-json to stdout.
   :type json: bool

   .. py:attribute:: spinner_cycle

      

   .. py:method:: start()


   .. py:method:: stop()


   .. py:method:: _start_spinning()


   .. py:method:: __enter__()


   .. py:method:: __exit__(exc_type, exc_val, exc_tb)



.. py:class:: ProgressBar(description, enabled=True, json=False, position=None, leave=True)


   
   :param description: The name of the progress bar, shown on left side of output.
   :type description: str
   :param enabled: If False, usage is a no-op.
   :type enabled: bool
   :param json: If true, outputs json progress to stdout rather than a progress bar.
                Currently, the json format assumes this is only used for "fetch", which
                maintains backward compatibility with conda 4.3 and earlier behavior.
   :type json: bool

   .. py:method:: get_lock()
      :classmethod:


   .. py:method:: update_to(fraction)


   .. py:method:: finish()


   .. py:method:: refresh()

      Force refresh i.e. once 100% has been reached


   .. py:method:: close()


   .. py:method:: _tqdm(*args, **kwargs)
      :staticmethod:

      Deferred import so it doesn't hit the `conda activate` paths.



.. py:class:: DummyExecutor


   Bases: :py:obj:`concurrent.futures.Executor`

   This is an abstract base class for concrete asynchronous executors.

   .. py:method:: submit(fn, *args, **kwargs)

      Submits a callable to be executed with the given arguments.

      Schedules the callable to be executed as fn(*args, **kwargs) and returns
      a Future instance representing the execution of the callable.

      :returns: A Future representing the given call.


   .. py:method:: map(func, *iterables)

      Returns an iterator equivalent to map(fn, iter).

      :param fn: A callable that will take as many arguments as there are
                 passed iterables.
      :param timeout: The maximum number of seconds to wait. If None, then there
                      is no limit on the wait time.
      :param chunksize: The size of the chunks the iterable will be broken into
                        before being passed to a child process. This argument is only
                        used by ProcessPoolExecutor; it is ignored by
                        ThreadPoolExecutor.

      :returns: map(func, *iterables) but the calls may
                be evaluated out-of-order.
      :rtype: An iterator equivalent to

      :raises TimeoutError: If the entire result iterator could not be generated
          before the given timeout.
      :raises Exception: If fn(*args) raises for any values.


   .. py:method:: shutdown(wait=True)

      Clean-up the resources associated with the Executor.

      It is safe to call this method several times. Otherwise, no other
      methods can be called after this one.

      :param wait: If True then shutdown will not return until all running
                   futures have finished executing and the resources used by the
                   executor have been reclaimed.
      :param cancel_futures: If True then shutdown will cancel all pending
                             futures. Futures that are completed or running will not be
                             cancelled.



.. py:class:: ThreadLimitedThreadPoolExecutor(max_workers=10)


   Bases: :py:obj:`concurrent.futures.ThreadPoolExecutor`

   This is an abstract base class for concrete asynchronous executors.

   Initializes a new ThreadPoolExecutor instance.

   :param max_workers: The maximum number of threads that can be used to
                       execute the given calls.
   :param thread_name_prefix: An optional name prefix to give our threads.
   :param initializer: A callable used to initialize worker threads.
   :param initargs: A tuple of arguments to pass to the initializer.

   .. py:method:: submit(fn, *args, **kwargs)

      This is an exact reimplementation of the `submit()` method on the parent class, except
      with an added `try/except` around `self._adjust_thread_count()`.  So long as there is at
      least one living thread, this thread pool will not throw an exception if threads cannot
      be expanded to `max_workers`.

      In the implementation, we use "protected" attributes from concurrent.futures (`_base`
      and `_WorkItem`). Consider vendoring the whole concurrent.futures library
      as an alternative to these protected imports.

      https://github.com/agronholm/pythonfutures/blob/3.2.0/concurrent/futures/thread.py#L121-L131  # NOQA
      https://github.com/python/cpython/blob/v3.6.4/Lib/concurrent/futures/thread.py#L114-L124



.. py:data:: as_completed

   

.. py:function:: get_instrumentation_record_file()


.. py:class:: time_recorder(entry_name=None, module_name=None)


   Bases: :py:obj:`ContextDecorator`

   Base class for a context manager class (implementing __enter__() and __exit__()) that also
   makes it a decorator.

   .. py:attribute:: record_file

      

   .. py:attribute:: start_time

      

   .. py:attribute:: total_call_num

      

   .. py:attribute:: total_run_time

      

   .. py:method:: _set_entry_name(f)


   .. py:method:: __call__(f)


   .. py:method:: __enter__()


   .. py:method:: __exit__(exc_type, exc_val, exc_tb)


   .. py:method:: log_totals()
      :classmethod:


   .. py:method:: _ensure_dir()



.. py:function:: print_instrumentation_data()


