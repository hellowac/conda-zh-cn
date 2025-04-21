:py:mod:`python`
================

.. py:module:: conda.common.path.python

.. autoapi-nested-parse::

   Common Python specific path utilities.




Functions
---------

.. autoapisummary::

   conda.common.path.python.pyc_path
   conda.common.path.python.missing_pyc_files
   conda.common.path.python.parse_entry_point_def
   conda.common.path.python.get_python_short_path
   conda.common.path.python.get_python_site_packages_short_path
   conda.common.path.python.get_major_minor_version
   conda.common.path.python.get_python_noarch_target_path



Attributes
----------

.. autoapisummary::

   conda.common.path.python._VERSION_REGEX


.. py:function:: pyc_path(py_path, python_major_minor_version)

   This must not return backslashes on Windows as that will break
   tests and leads to an eventual need to make url_to_path return
   backslashes too and that may end up changing files on disc or
   to the result of comparisons with the contents of them.


.. py:function:: missing_pyc_files(python_major_minor_version, files)


.. py:function:: parse_entry_point_def(ep_definition)


.. py:function:: get_python_short_path(python_version=None)


.. py:function:: get_python_site_packages_short_path(python_version)


.. py:data:: _VERSION_REGEX

   

.. py:function:: get_major_minor_version(string, with_dot=True)


.. py:function:: get_python_noarch_target_path(source_short_path, target_site_packages_short_path)


