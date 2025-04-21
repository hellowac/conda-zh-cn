:py:mod:`path_actions`
======================

.. py:module:: conda.core.path_actions

.. autoapi-nested-parse::

   Atomic actions that make up a package installation or removal transaction.



Classes
-------

.. autoapisummary::

   conda.core.path_actions._Action
   conda.core.path_actions.PathAction
   conda.core.path_actions.MultiPathAction
   conda.core.path_actions.PrefixPathAction
   conda.core.path_actions.CreateInPrefixPathAction
   conda.core.path_actions.LinkPathAction
   conda.core.path_actions.PrefixReplaceLinkAction
   conda.core.path_actions.MakeMenuAction
   conda.core.path_actions.CompileMultiPycAction
   conda.core.path_actions.AggregateCompileMultiPycAction
   conda.core.path_actions.CreatePythonEntryPointAction
   conda.core.path_actions.CreatePrefixRecordAction
   conda.core.path_actions.UpdateHistoryAction
   conda.core.path_actions.RegisterEnvironmentLocationAction
   conda.core.path_actions.RemoveFromPrefixPathAction
   conda.core.path_actions.UnlinkPathAction
   conda.core.path_actions.RemoveMenuAction
   conda.core.path_actions.RemoveLinkedPackageRecordAction
   conda.core.path_actions.UnregisterEnvironmentLocationAction
   conda.core.path_actions.CacheUrlAction
   conda.core.path_actions.ExtractPackageAction




Attributes
----------

.. autoapisummary::

   conda.core.path_actions.FileNotFoundError
   conda.core.path_actions._MENU_RE
   conda.core.path_actions.REPR_IGNORE_KWARGS


.. py:data:: FileNotFoundError

   

.. py:data:: _MENU_RE

   

.. py:data:: REPR_IGNORE_KWARGS
   :value: ('transaction_context', 'package_info', 'hold_path')

   

.. py:class:: _Action


   .. py:property:: verified


   .. py:attribute:: _verified
      :value: False

      

   .. py:method:: verify()
      :abstractmethod:


   .. py:method:: execute()
      :abstractmethod:


   .. py:method:: reverse()
      :abstractmethod:


   .. py:method:: cleanup()
      :abstractmethod:


   .. py:method:: __repr__()

      Return repr(self).



.. py:class:: PathAction


   Bases: :py:obj:`_Action`

   .. py:property:: target_full_path
      :abstractmethod:



.. py:class:: MultiPathAction


   Bases: :py:obj:`_Action`

   .. py:property:: target_full_paths
      :abstractmethod:



.. py:class:: PrefixPathAction(transaction_context, target_prefix, target_short_path)


   Bases: :py:obj:`PathAction`

   .. py:property:: target_short_paths


   .. py:property:: target_full_path



.. py:class:: CreateInPrefixPathAction(transaction_context, package_info, source_prefix, source_short_path, target_prefix, target_short_path)


   Bases: :py:obj:`PrefixPathAction`

   .. py:property:: source_full_path


   .. py:method:: verify()


   .. py:method:: cleanup()



.. py:class:: LinkPathAction(transaction_context, package_info, extracted_package_dir, source_short_path, target_prefix, target_short_path, link_type, source_path_data)


   Bases: :py:obj:`CreateInPrefixPathAction`

   .. py:method:: create_file_link_actions(transaction_context, package_info, target_prefix, requested_link_type)
      :classmethod:


   .. py:method:: create_directory_actions(transaction_context, package_info, target_prefix, requested_link_type, file_link_actions)
      :classmethod:


   .. py:method:: create_python_entry_point_windows_exe_action(transaction_context, package_info, target_prefix, requested_link_type, entry_point_def)
      :classmethod:


   .. py:method:: verify()


   .. py:method:: execute()


   .. py:method:: reverse()



.. py:class:: PrefixReplaceLinkAction(transaction_context, package_info, extracted_package_dir, source_short_path, target_prefix, target_short_path, link_type, prefix_placeholder, file_mode, source_path_data)


   Bases: :py:obj:`LinkPathAction`

   .. py:method:: verify()


   .. py:method:: execute()



.. py:class:: MakeMenuAction(transaction_context, package_info, target_prefix, target_short_path)


   Bases: :py:obj:`CreateInPrefixPathAction`

   .. py:method:: create_actions(transaction_context, package_info, target_prefix, requested_link_type)
      :classmethod:


   .. py:method:: execute()


   .. py:method:: reverse()



.. py:class:: CompileMultiPycAction(transaction_context, package_info, target_prefix, source_short_paths, target_short_paths)


   Bases: :py:obj:`MultiPathAction`

   .. py:property:: target_full_paths


   .. py:property:: source_full_paths


   .. py:method:: create_actions(transaction_context, package_info, target_prefix, requested_link_type, file_link_actions)
      :classmethod:


   .. py:method:: verify()


   .. py:method:: cleanup()


   .. py:method:: execute()


   .. py:method:: reverse()



.. py:class:: AggregateCompileMultiPycAction(*individuals, **kw)


   Bases: :py:obj:`CompileMultiPycAction`

   Bunch up all of our compile actions, so that they all get carried out at once.
   This avoids clobbering and is faster when we have several individual packages requiring
   compilation.


.. py:class:: CreatePythonEntryPointAction(transaction_context, package_info, target_prefix, target_short_path, module, func)


   Bases: :py:obj:`CreateInPrefixPathAction`

   .. py:method:: create_actions(transaction_context, package_info, target_prefix, requested_link_type)
      :classmethod:


   .. py:method:: execute()


   .. py:method:: reverse()



.. py:class:: CreatePrefixRecordAction(transaction_context, package_info, target_prefix, target_short_path, requested_link_type, requested_spec, all_link_path_actions)


   Bases: :py:obj:`CreateInPrefixPathAction`

   .. py:method:: create_actions(transaction_context, package_info, target_prefix, requested_link_type, requested_spec, all_link_path_actions)
      :classmethod:


   .. py:method:: execute()


   .. py:method:: reverse()



.. py:class:: UpdateHistoryAction(transaction_context, target_prefix, target_short_path, remove_specs, update_specs, neutered_specs)


   Bases: :py:obj:`CreateInPrefixPathAction`

   .. py:method:: create_actions(transaction_context, target_prefix, remove_specs, update_specs, neutered_specs)
      :classmethod:


   .. py:method:: execute()


   .. py:method:: reverse()


   .. py:method:: cleanup()



.. py:class:: RegisterEnvironmentLocationAction(transaction_context, target_prefix)


   Bases: :py:obj:`PathAction`

   .. py:property:: target_full_path
      :abstractmethod:


   .. py:method:: verify()


   .. py:method:: execute()


   .. py:method:: reverse()


   .. py:method:: cleanup()



.. py:class:: RemoveFromPrefixPathAction(transaction_context, linked_package_data, target_prefix, target_short_path)


   Bases: :py:obj:`PrefixPathAction`

   .. py:method:: verify()



.. py:class:: UnlinkPathAction(transaction_context, linked_package_data, target_prefix, target_short_path, link_type=LinkType.hardlink)


   Bases: :py:obj:`RemoveFromPrefixPathAction`

   .. py:method:: execute()


   .. py:method:: reverse()


   .. py:method:: cleanup()



.. py:class:: RemoveMenuAction(transaction_context, linked_package_data, target_prefix, target_short_path)


   Bases: :py:obj:`RemoveFromPrefixPathAction`

   .. py:method:: create_actions(transaction_context, linked_package_data, target_prefix)
      :classmethod:


   .. py:method:: execute()


   .. py:method:: reverse()


   .. py:method:: cleanup()



.. py:class:: RemoveLinkedPackageRecordAction(transaction_context, linked_package_data, target_prefix, target_short_path)


   Bases: :py:obj:`UnlinkPathAction`

   .. py:method:: execute()


   .. py:method:: reverse()



.. py:class:: UnregisterEnvironmentLocationAction(transaction_context, target_prefix)


   Bases: :py:obj:`PathAction`

   .. py:property:: target_full_path
      :abstractmethod:


   .. py:method:: verify()


   .. py:method:: execute()


   .. py:method:: reverse()


   .. py:method:: cleanup()



.. py:class:: CacheUrlAction(url, target_pkgs_dir, target_package_basename, sha256=None, size=None, md5=None)


   Bases: :py:obj:`PathAction`

   .. py:property:: target_full_path


   .. py:method:: verify()


   .. py:method:: execute(progress_update_callback=None)


   .. py:method:: _execute_local(source_path, target_package_cache, progress_update_callback=None)


   .. py:method:: _execute_channel(target_package_cache, progress_update_callback=None)


   .. py:method:: reverse()


   .. py:method:: cleanup()


   .. py:method:: __str__()

      Return str(self).



.. py:class:: ExtractPackageAction(source_full_path, target_pkgs_dir, target_extracted_dirname, record_or_spec, sha256, size, md5)


   Bases: :py:obj:`PathAction`

   .. py:property:: target_full_path


   .. py:method:: verify()


   .. py:method:: execute(progress_update_callback=None)


   .. py:method:: reverse()


   .. py:method:: cleanup()


   .. py:method:: __str__()

      Return str(self).



