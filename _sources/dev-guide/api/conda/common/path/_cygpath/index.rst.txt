:py:mod:`_cygpath`
==================

.. py:module:: conda.common.path._cygpath



Functions
---------

.. autoapisummary::

   conda.common.path._cygpath.nt_to_posix
   conda.common.path._cygpath._get_root
   conda.common.path._cygpath._get_RE_WIN_ROOT
   conda.common.path._cygpath._to_unix_root
   conda.common.path._cygpath._to_unix_mount
   conda.common.path._cygpath._to_unix_drive
   conda.common.path._cygpath.translate_unix
   conda.common.path._cygpath.posix_to_nt
   conda.common.path._cygpath._to_win_drive
   conda.common.path._cygpath._to_win_mount
   conda.common.path._cygpath._to_win_root
   conda.common.path._cygpath._resolve_path
   conda.common.path._cygpath.resolve_paths



Attributes
----------

.. autoapisummary::

   conda.common.path._cygpath.RE_WIN_MOUNT
   conda.common.path._cygpath.RE_WIN_DRIVE
   conda.common.path._cygpath.RE_UNIX_DRIVE
   conda.common.path._cygpath.RE_UNIX_MOUNT
   conda.common.path._cygpath.RE_UNIX_ROOT


.. py:function:: nt_to_posix(path: conda.common.path.PathType, prefix: conda.common.path.PathType | None, cygdrive: bool = False) -> str

   A fallback implementation of `cygpath --unix`.

   :param path: The path to convert.
   :param prefix: The Windows style prefix directory to use for the conversion.
                  If not provided, no checks for root paths will be made.
   :param cygdrive: Whether to use the Cygwin-style drive prefix.


.. py:function:: _get_root(prefix: str) -> str


.. py:function:: _get_RE_WIN_ROOT(prefix: str) -> re.Pattern


.. py:function:: _to_unix_root(match: re.Match) -> str


.. py:data:: RE_WIN_MOUNT

   

.. py:function:: _to_unix_mount(match: re.Match) -> str


.. py:data:: RE_WIN_DRIVE

   

.. py:function:: _to_unix_drive(match: re.Match, cygdrive: bool) -> str


.. py:function:: translate_unix(match: re.Match) -> str


.. py:function:: posix_to_nt(path: conda.common.path.PathType, prefix: conda.common.path.PathType | None, cygdrive: bool = False) -> str

   A fallback implementation of `cygpath --windows`.

   :param path: The path to convert.
   :param prefix: The Windows style prefix directory to use for the conversion.
                  If not provided, no checks for root paths will be made.
   :param cygdrive: Unused. Present to keep the signature consistent with `nt_to_posix`.


.. py:data:: RE_UNIX_DRIVE

   

.. py:function:: _to_win_drive(match: re.Match) -> str


.. py:data:: RE_UNIX_MOUNT

   

.. py:function:: _to_win_mount(match: re.Match) -> str


.. py:data:: RE_UNIX_ROOT

   

.. py:function:: _to_win_root(match: re.Match, root: str) -> str


.. py:function:: _resolve_path(path: str, sep: str) -> str


.. py:function:: resolve_paths(paths: str, pathsep: str, sep: str) -> str


