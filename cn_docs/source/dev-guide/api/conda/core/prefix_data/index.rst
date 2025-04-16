:py:mod:`prefix_data`
=====================

.. py:module:: conda.core.prefix_data

.. autoapi-nested-parse::

   Tools for managing the packages installed within an environment.



Classes
-------

.. autoapisummary::

   conda.core.prefix_data.PrefixDataType
   conda.core.prefix_data.PrefixData



Functions
---------

.. autoapisummary::

   conda.core.prefix_data.get_conda_anchor_files_and_records
   conda.core.prefix_data.python_record_for_prefix
   conda.core.prefix_data.get_python_version_for_prefix
   conda.core.prefix_data.delete_prefix_from_linked_data



.. py:class:: PrefixDataType


   Bases: :py:obj:`type`

   Basic caching of PrefixData instance objects.

   .. py:method:: __call__(prefix_path: str | os.PathLike | pathlib.Path, pip_interop_enabled: bool | None = None)

      Call self as a function.



.. py:class:: PrefixData(prefix_path: str | os.PathLike[str] | pathlib.Path, pip_interop_enabled: bool | None = None)


   .. py:property:: _prefix_records


   .. py:property:: is_writable


   .. py:property:: _python_pkg_record

      Return the prefix record for the package python.

   .. py:attribute:: _cache_
      :type: dict[pathlib.Path, PrefixData]

      

   .. py:method:: __eq__(other: Any) -> bool

      Return self==value.


   .. py:method:: load()


   .. py:method:: reload()


   .. py:method:: _get_json_fn(prefix_record)


   .. py:method:: insert(prefix_record, remove_auth=True)


   .. py:method:: remove(package_name)


   .. py:method:: get(package_name, default=NULL)


   .. py:method:: iter_records()


   .. py:method:: iter_records_sorted()


   .. py:method:: all_subdir_urls()


   .. py:method:: query(package_ref_or_match_spec)


   .. py:method:: _load_single_record(prefix_record_json_path)


   .. py:method:: _load_site_packages()

      Load non-conda-installed python packages in the site-packages of the prefix.

      Python packages not handled by conda are installed via other means,
      like using pip or using python setup.py develop for local development.

      Packages found that are not handled by conda are converted into a
      prefix record and handled in memory.

      Packages clobbering conda packages (i.e. the conda-meta record) are
      removed from the in memory representation.


   .. py:method:: _get_environment_state_file()


   .. py:method:: _write_environment_state_file(state)


   .. py:method:: get_environment_env_vars()


   .. py:method:: set_environment_env_vars(env_vars)


   .. py:method:: unset_environment_env_vars(env_vars)



.. py:function:: get_conda_anchor_files_and_records(site_packages_short_path, python_records)

   Return the anchor files for the conda records of python packages.


.. py:function:: python_record_for_prefix(prefix) -> conda.models.records.PrefixRecord | None

   For the given conda prefix, return the PrefixRecord of the Python installed
   in that prefix.


.. py:function:: get_python_version_for_prefix(prefix) -> str | None

   For the given conda prefix, return the version of the Python installation
   in that prefix.


.. py:function:: delete_prefix_from_linked_data(path: str | os.PathLike | pathlib.Path) -> bool

   Here, path may be a complete prefix or a dist inside a prefix


