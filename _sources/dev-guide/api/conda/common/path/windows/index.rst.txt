:py:mod:`windows`
=================

.. py:module:: conda.common.path.windows

.. autoapi-nested-parse::

   Common Windows path utilities.




Functions
---------

.. autoapisummary::

   conda.common.path.windows.win_path_ok
   conda.common.path.windows.win_path_double_escape
   conda.common.path.windows.win_path_backout
   conda.common.path.windows._path_to
   conda.common.path.windows.win_path_to_unix
   conda.common.path.windows.unix_path_to_win



.. py:function:: win_path_ok(path)


.. py:function:: win_path_double_escape(path)


.. py:function:: win_path_backout(path)


.. py:function:: _path_to(paths: conda.common.path.PathType | conda.common.path.PathsType | None, prefix: conda.common.path.PathType | None = None, *, cygdrive: bool, to_unix: bool) -> str | tuple[str, Ellipsis] | None


.. py:function:: win_path_to_unix(paths: conda.common.path.PathType | conda.common.path.PathsType | None, prefix: conda.common.path.PathType | None = None, *, cygdrive: bool = False) -> str | tuple[str, Ellipsis] | None

   Convert Windows paths to Unix paths.

   .. note::
       Produces unexpected results when run on Unix.

   :param paths: The path(s) to convert.
   :param prefix: The (Windows path-style) prefix directory to use for the conversion.
                  If not provided, no checks for prefix paths will be made.
   :param cygdrive: Whether to use the Cygwin-style drive prefix.


.. py:function:: unix_path_to_win(paths: conda.common.path.PathType | conda.common.path.PathsType | None, prefix: conda.common.path.PathType | None = None, *, cygdrive: bool = False) -> str | tuple[str, Ellipsis] | None

   Convert Unix paths to Windows paths.

   .. note::
       Produces unexpected results when run on Unix.

   :param paths: The path(s) to convert.
   :param prefix: The (Windows path-style) prefix directory to use for the conversion.
                  If not provided, no checks for prefix paths will be made.
   :param cygdrive: Unused. Present to keep the signature consistent with `win_path_to_unix`.


