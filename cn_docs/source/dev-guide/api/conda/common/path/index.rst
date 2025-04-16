:py:mod:`path`
==============

.. py:module:: conda.common.path

.. autoapi-nested-parse::

   Common path utilities.



.. toctree::
   :hidden:
   :titlesonly:
   :maxdepth: 3

   _cygpath/index.rst
   directories/index.rst
   python/index.rst
   windows/index.rst



Functions
---------

.. autoapisummary::

   conda.common.path.explode_directories
   conda.common.path.get_all_directories
   conda.common.path.get_leaf_directories
   conda.common.path.tokenized_startswith
   conda.common.path.get_major_minor_version
   conda.common.path.get_python_noarch_target_path
   conda.common.path.get_python_short_path
   conda.common.path.get_python_site_packages_short_path
   conda.common.path.missing_pyc_files
   conda.common.path.parse_entry_point_def
   conda.common.path.pyc_path
   conda.common.path.unix_path_to_win
   conda.common.path.win_path_backout
   conda.common.path.win_path_double_escape
   conda.common.path.win_path_ok
   conda.common.path.win_path_to_unix



.. py:function:: explode_directories(child_directories: collections.abc.Iterable[tuple[str, Ellipsis]]) -> set[str]


.. py:function:: get_all_directories(files: collections.abc.Iterable[str]) -> list[tuple[str, Ellipsis]]


.. py:function:: get_leaf_directories(files: collections.abc.Iterable[str]) -> collections.abc.Sequence[str]


.. py:function:: tokenized_startswith(test_iterable, startswith_iterable)


.. py:function:: get_major_minor_version(string, with_dot=True)


.. py:function:: get_python_noarch_target_path(source_short_path, target_site_packages_short_path)


.. py:function:: get_python_short_path(python_version=None)


.. py:function:: get_python_site_packages_short_path(python_version)


.. py:function:: missing_pyc_files(python_major_minor_version, files)


.. py:function:: parse_entry_point_def(ep_definition)


.. py:function:: pyc_path(py_path, python_major_minor_version)

   This must not return backslashes on Windows as that will break
   tests and leads to an eventual need to make url_to_path return
   backslashes too and that may end up changing files on disc or
   to the result of comparisons with the contents of them.


.. py:function:: unix_path_to_win(paths: conda.common.path.PathType | conda.common.path.PathsType | None, prefix: conda.common.path.PathType | None = None, *, cygdrive: bool = False) -> str | tuple[str, Ellipsis] | None

   Convert Unix paths to Windows paths.

   .. note::
       Produces unexpected results when run on Unix.

   :param paths: The path(s) to convert.
   :param prefix: The (Windows path-style) prefix directory to use for the conversion.
                  If not provided, no checks for prefix paths will be made.
   :param cygdrive: Unused. Present to keep the signature consistent with `win_path_to_unix`.


.. py:function:: win_path_backout(path)


.. py:function:: win_path_double_escape(path)


.. py:function:: win_path_ok(path)


.. py:function:: win_path_to_unix(paths: conda.common.path.PathType | conda.common.path.PathsType | None, prefix: conda.common.path.PathType | None = None, *, cygdrive: bool = False) -> str | tuple[str, Ellipsis] | None

   Convert Windows paths to Unix paths.

   .. note::
       Produces unexpected results when run on Unix.

   :param paths: The path(s) to convert.
   :param prefix: The (Windows path-style) prefix directory to use for the conversion.
                  If not provided, no checks for prefix paths will be made.
   :param cygdrive: Whether to use the Cygwin-style drive prefix.


