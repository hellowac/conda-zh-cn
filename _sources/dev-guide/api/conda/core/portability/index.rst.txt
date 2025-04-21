:py:mod:`portability`
=====================

.. py:module:: conda.core.portability

.. autoapi-nested-parse::

   Tools for cross-OS portability.




Functions
---------

.. autoapisummary::

   conda.core.portability._subdir_is_win
   conda.core.portability.update_prefix
   conda.core.portability.replace_prefix
   conda.core.portability.binary_replace
   conda.core.portability.has_pyzzer_entry_point
   conda.core.portability.replace_pyzzer_entry_point_shebang
   conda.core.portability.replace_long_shebang
   conda.core.portability.generate_shebang_for_entry_point



Attributes
----------

.. autoapisummary::

   conda.core.portability.SHEBANG_REGEX
   conda.core.portability.MAX_SHEBANG_LENGTH
   conda.core.portability.POPULAR_ENCODINGS


.. py:data:: SHEBANG_REGEX
   :value: b'^(#!(?:[ ]*)(/(?:\\\\ |[^ \\n\\r\\t])*)(.*))$'

   

.. py:data:: MAX_SHEBANG_LENGTH

   

.. py:data:: POPULAR_ENCODINGS
   :value: ('utf-8', 'utf-16-le', 'utf-16-be', 'utf-32-le', 'utf-32-be')

   

.. py:exception:: _PaddingError


   Bases: :py:obj:`Exception`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:function:: _subdir_is_win(subdir: str) -> bool


.. py:function:: update_prefix(path, new_prefix, placeholder=PREFIX_PLACEHOLDER, mode=FileMode.text, subdir=context.subdir)


.. py:function:: replace_prefix(mode: conda.models.enums.FileMode, data: bytes, placeholder: str, new_prefix: str, subdir: str = 'noarch') -> bytes

   Replaces `placeholder` text with the `new_prefix` provided. The `mode` provided can
   either be text or binary.

   We use the `POPULAR_ENCODINGS` module level constant defined above to make several
   passes at replacing the placeholder. We do this to account for as many encodings as
   possible. If this causes any performance problems in the future, it could potentially
   be removed (i.e. just using the most popular "utf-8" encoding").

   More information/discussion available here: https://github.com/conda/conda/pull/9946


.. py:function:: binary_replace(data: bytes, search: bytes, replacement: bytes, encoding: str = 'utf-8', subdir: str = 'noarch') -> bytes

   Perform a binary replacement of `data`, where the placeholder `search` is
   replaced with `replacement` and the remaining string is padded with null characters.
   All input arguments are expected to be bytes objects.

   :param data: The bytes object that will be searched and replaced
   :param search: The bytes object to find
   :param replacement: The bytes object that will replace `search`
   :param encoding: The encoding of the expected string in the binary.
   :type encoding: str


.. py:function:: has_pyzzer_entry_point(data)


.. py:function:: replace_pyzzer_entry_point_shebang(all_data, placeholder, new_prefix)

   Code adapted from pyzzer.  This is meant to deal with entry point exe's created by distlib,
   which consist of a launcher, then a shebang, then a zip archive of the entry point code to run.
   We need to change the shebang.
   https://bitbucket.org/vinay.sajip/pyzzer/src/5d5740cb04308f067d5844a56fbe91e7a27efccc/pyzzer/__init__.py?at=default&fileviewer=file-view-default#__init__.py-112  # NOQA


.. py:function:: replace_long_shebang(mode, data)


.. py:function:: generate_shebang_for_entry_point(executable, with_usr_bin_env=False)

   This function can be used to generate a shebang line for Python entry points.

   Use cases:
   - At install/link time, to generate the `noarch: python` entry points.
   - conda init uses it to create its own entry point during conda-build


