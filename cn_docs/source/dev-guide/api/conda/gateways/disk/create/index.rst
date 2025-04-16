:py:mod:`create`
================

.. py:module:: conda.gateways.disk.create

.. autoapi-nested-parse::

   Disk utility functions for creating new files or directories.



Classes
-------

.. autoapisummary::

   conda.gateways.disk.create.TemporaryDirectory
   conda.gateways.disk.create.ProgressFileWrapper



Functions
---------

.. autoapisummary::

   conda.gateways.disk.create.write_as_json_to_file
   conda.gateways.disk.create.create_python_entry_point
   conda.gateways.disk.create.create_application_entry_point
   conda.gateways.disk.create.extract_tarball
   conda.gateways.disk.create.make_menu
   conda.gateways.disk.create.create_hard_link_or_copy
   conda.gateways.disk.create._is_unix_executable_using_ORIGIN
   conda.gateways.disk.create._do_softlink
   conda.gateways.disk.create.create_fake_executable_softlink
   conda.gateways.disk.create.copy
   conda.gateways.disk.create._do_copy
   conda.gateways.disk.create.create_link
   conda.gateways.disk.create.compile_multiple_pyc
   conda.gateways.disk.create.create_package_cache_directory
   conda.gateways.disk.create.create_envs_directory



Attributes
----------

.. autoapisummary::

   conda.gateways.disk.create.stdoutlog
   conda.gateways.disk.create.mkdir_p
   conda.gateways.disk.create.python_entry_point_template
   conda.gateways.disk.create.application_entry_point_template


.. py:class:: TemporaryDirectory(suffix='', prefix='tmp', dir=None)


   Create and return a temporary directory.  This has the same
   behavior as mkdtemp but can be used as a context manager.  For
   .. rubric:: Example

   with TemporaryDirectory() as tmpdir:
       ...

   Upon exiting the context, the directory and everything contained
   in it are removed.

   .. py:attribute:: name

      

   .. py:attribute:: _closed
      :value: False

      

   .. py:method:: __repr__()

      Return repr(self).


   .. py:method:: __enter__()


   .. py:method:: cleanup(_warn=False, _warnings=_warnings)


   .. py:method:: __exit__(exc, value, tb)


   .. py:method:: __del__()



.. py:data:: stdoutlog

   

.. py:data:: mkdir_p

   

.. py:data:: python_entry_point_template

   

.. py:data:: application_entry_point_template

   

.. py:function:: write_as_json_to_file(file_path, obj)


.. py:function:: create_python_entry_point(target_full_path, python_full_path, module, func)


.. py:function:: create_application_entry_point(source_full_path, target_full_path, python_full_path)


.. py:class:: ProgressFileWrapper(fileobj, progress_update_callback)


   .. py:method:: __getattr__(name)


   .. py:method:: __setattr__(name, value)

      Implement setattr(self, name, value).


   .. py:method:: read(size=-1)


   .. py:method:: progress_update()



.. py:function:: extract_tarball(tarball_full_path, destination_directory=None, progress_update_callback=None)


.. py:function:: make_menu(prefix, file_path, remove=False)

   Create cross-platform menu items (e.g. Windows Start Menu)

   Passes all menu config files %PREFIX%/Menu/*.json to ``menuinst.install``.
   ``remove=True`` will remove the menu items.


.. py:function:: create_hard_link_or_copy(src, dst)


.. py:function:: _is_unix_executable_using_ORIGIN(path)


.. py:function:: _do_softlink(src, dst)


.. py:function:: create_fake_executable_softlink(src, dst)


.. py:function:: copy(src, dst)


.. py:function:: _do_copy(src, dst)


.. py:function:: create_link(src, dst, link_type=LinkType.hardlink, force=False)


.. py:function:: compile_multiple_pyc(python_exe_full_path, py_full_paths, pyc_full_paths, prefix, py_ver)


.. py:function:: create_package_cache_directory(pkgs_dir)


.. py:function:: create_envs_directory(envs_dir)


