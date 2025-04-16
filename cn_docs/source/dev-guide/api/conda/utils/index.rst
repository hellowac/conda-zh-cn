:py:mod:`utils`
===============

.. py:module:: conda.utils

.. autoapi-nested-parse::

   Utility functions.




Functions
---------

.. autoapisummary::

   conda.utils.unix_path_to_win
   conda.utils.win_path_to_cygwin
   conda.utils.cygwin_path_to_win
   conda.utils.translate_stream
   conda.utils.human_bytes
   conda.utils.sys_prefix_unfollowed
   conda.utils.quote_for_shell
   conda.utils.massage_arguments
   conda.utils.wrap_subprocess_call
   conda.utils.get_comspec
   conda.utils.ensure_dir_exists



Attributes
----------

.. autoapisummary::

   conda.utils._UNIX_SHELL_BASE
   conda.utils._MSYS2_SHELL_BASE
   conda.utils._SHELLS
   conda.utils._RE_UNSAFE


.. py:function:: unix_path_to_win(path, root_prefix='')

   Convert a path or :-separated string of paths into a Windows representation

   Does not add cygdrive.  If you need that, set root_prefix to "/cygdrive"


.. py:function:: win_path_to_cygwin(path)


.. py:function:: cygwin_path_to_win(path)


.. py:function:: translate_stream(stream, translator)


.. py:function:: human_bytes(n)

   Return the number of bytes n in more human readable form.

   .. rubric:: Examples

   >>> human_bytes(42)
   '42 B'
   >>> human_bytes(1042)
   '1 KB'
   >>> human_bytes(10004242)
   '9.5 MB'
   >>> human_bytes(100000004242)
   '93.13 GB'


.. py:data:: _UNIX_SHELL_BASE

   

.. py:data:: _MSYS2_SHELL_BASE

   

.. py:data:: _SHELLS

   

.. py:function:: sys_prefix_unfollowed()

   Since conda is installed into non-root environments as a symlink only
   and because sys.prefix follows symlinks, this function can be used to
   get the 'unfollowed' sys.prefix.

   This value is usually the same as the prefix of the environment into
   which conda has been symlinked. An example of when this is necessary
   is when conda looks for external sub-commands in find_commands.py


.. py:function:: quote_for_shell(*arguments)

   Properly quote arguments for command line passing.

   For POSIX uses `shlex.join`, for Windows uses a custom implementation to properly escape
   metacharacters.

   :param arguments: Arguments to quote.
   :type arguments: list of str
   :return: Quoted arguments.
   :rtype: str


.. py:data:: _RE_UNSAFE

   

.. py:function:: massage_arguments(arguments, errors='assert')


.. py:function:: wrap_subprocess_call(root_prefix, prefix, dev_mode, debug_wrapper_scripts, arguments, use_system_tmp_path=False)


.. py:function:: get_comspec()

   Returns COMSPEC from envvars.

   Ensures COMSPEC envvar is set to cmd.exe, if not attempt to find it.

   :raises KeyError: COMSPEC is undefined and cannot be found.
   :returns: COMSPEC value.
   :rtype: str


.. py:function:: ensure_dir_exists(func)

   Ensures that the directory exists for functions returning
   a Path object containing a directory


