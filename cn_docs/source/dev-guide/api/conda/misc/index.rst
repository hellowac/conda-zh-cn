:py:mod:`misc`
==============

.. py:module:: conda.misc

.. autoapi-nested-parse::

   Miscellaneous utility functions.




Functions
---------

.. autoapisummary::

   conda.misc.conda_installed_files
   conda.misc._match_specs_from_explicit
   conda.misc.explicit
   conda.misc.rel_path
   conda.misc.walk_prefix
   conda.misc.untracked
   conda.misc.touch_nonadmin
   conda.misc.clone_env
   conda.misc._get_best_prec_match



Attributes
----------

.. autoapisummary::

   conda.misc.url_pat


.. py:function:: conda_installed_files(prefix, exclude_self_build=False)

   Return the set of files which have been installed (using conda) into
   a given prefix.


.. py:data:: url_pat

   

.. py:function:: _match_specs_from_explicit(specs: collections.abc.Iterable[str]) -> collections.abc.Iterable[conda.models.match_spec.MatchSpec]


.. py:function:: explicit(specs, prefix, verbose=False, force_extract=True, index=None)


.. py:function:: rel_path(prefix, path, windows_forward_slashes=True)


.. py:function:: walk_prefix(prefix, ignore_predefined_files=True, windows_forward_slashes=True)

   Return the set of all files in a given prefix directory.


.. py:function:: untracked(prefix, exclude_self_build=False)

   Return (the set) of all untracked files for a given prefix.


.. py:function:: touch_nonadmin(prefix)

   Creates $PREFIX/.nonadmin if sys.prefix/.nonadmin exists (on Windows).


.. py:function:: clone_env(prefix1, prefix2, verbose=True, quiet=False, index_args=None)

   Clone existing prefix1 into new prefix2.


.. py:function:: _get_best_prec_match(precs)


