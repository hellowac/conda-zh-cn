:py:mod:`python_api`
====================

.. py:module:: conda.cli.python_api

.. autoapi-nested-parse::

   Wrapper for running conda CLI commands as a Python API.



Classes
-------

.. autoapisummary::

   conda.cli.python_api.Commands



Functions
---------

.. autoapisummary::

   conda.cli.python_api.run_command



Attributes
----------

.. autoapisummary::

   conda.cli.python_api.STRING
   conda.cli.python_api.STDOUT


.. py:class:: Commands


   .. py:attribute:: CLEAN
      :value: 'clean'

      

   .. py:attribute:: CONFIG
      :value: 'config'

      

   .. py:attribute:: CREATE
      :value: 'create'

      

   .. py:attribute:: INFO
      :value: 'info'

      

   .. py:attribute:: INSTALL
      :value: 'install'

      

   .. py:attribute:: LIST
      :value: 'list'

      

   .. py:attribute:: REMOVE
      :value: 'remove'

      

   .. py:attribute:: SEARCH
      :value: 'search'

      

   .. py:attribute:: UPDATE
      :value: 'update'

      

   .. py:attribute:: RUN
      :value: 'run'

      

   .. py:attribute:: NOTICES
      :value: 'notices'

      


.. py:data:: STRING

   

.. py:data:: STDOUT

   

.. py:function:: run_command(command, *arguments, **kwargs)

   Runs a conda command in-process with a given set of command-line interface arguments.

   Differences from the command-line interface:
       Always uses --yes flag, thus does not ask for confirmation.

   :param command: one of the Commands.
   :param \*arguments: instructions you would normally pass to the conda command on the command line
                       see below for examples. Be very careful to delimit arguments exactly as you
                       want them to be delivered. No 'combine then split at spaces' or other
                       information destroying processing gets performed on the arguments.
   :param \*\*kwargs: special instructions for programmatic overrides

   :keyword use_exception_handler: defaults to False. False will let the code calling
                                   `run_command` handle all exceptions.  True won't raise when an exception
                                   has occurred, and instead give a non-zero return code
   :keyword search_path: an optional non-standard search path for configuration information
                         that overrides the default SEARCH_PATH
   :keyword stdout: Define capture behavior for stream sys.stdout. Defaults to STRING.
                    STRING captures as a string.  None leaves stream untouched.
                    Otherwise redirect to file-like object stdout.
   :keyword stderr: Define capture behavior for stream sys.stderr. Defaults to STRING.
                    STRING captures as a string.  None leaves stream untouched.
                    STDOUT redirects to stdout target and returns None as stderr value.
                    Otherwise redirect to file-like object stderr.

   :returns: a tuple of stdout, stderr, and return_code.
             stdout, stderr are either strings, None or the corresponding file-like function argument.

   .. rubric:: 示例

   >>> run_command(Commands.CREATE, "-n", "newenv", "python=3", "flask",                         use_exception_handler=True)
   >>> run_command(Commands.CREATE, "-n", "newenv", "python=3", "flask")
   >>> run_command(Commands.CREATE, ["-n", "newenv", "python=3", "flask"], search_path=())


