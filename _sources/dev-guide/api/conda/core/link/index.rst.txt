:py:mod:`link`
==============

.. py:module:: conda.core.link

.. autoapi-nested-parse::

   Package installation implemented as a series of link/unlink transactions.



Classes
-------

.. autoapisummary::

   conda.core.link.PrefixSetup
   conda.core.link.ActionGroup
   conda.core.link.PrefixActionGroup
   conda.core.link.ChangeReport
   conda.core.link.UnlinkLinkTransaction



Functions
---------

.. autoapisummary::

   conda.core.link.determine_link_type
   conda.core.link.make_unlink_actions
   conda.core.link.match_specs_to_dists
   conda.core.link.run_script
   conda.core.link.messages



.. py:function:: determine_link_type(extracted_package_dir, target_prefix)


.. py:function:: make_unlink_actions(transaction_context, target_prefix, prefix_record)


.. py:function:: match_specs_to_dists(packages_info_to_link, specs)


.. py:class:: PrefixSetup


   Bases: :py:obj:`NamedTuple`

   .. py:attribute:: target_prefix
      :type: str

      

   .. py:attribute:: unlink_precs
      :type: tuple[conda.models.records.PackageRecord, Ellipsis]

      

   .. py:attribute:: link_precs
      :type: tuple[conda.models.records.PackageRecord, Ellipsis]

      

   .. py:attribute:: remove_specs
      :type: tuple[conda.resolve.MatchSpec, Ellipsis]

      

   .. py:attribute:: update_specs
      :type: tuple[conda.resolve.MatchSpec, Ellipsis]

      

   .. py:attribute:: neutered_specs
      :type: tuple[conda.resolve.MatchSpec, Ellipsis]

      


.. py:class:: ActionGroup


   Bases: :py:obj:`NamedTuple`

   .. py:attribute:: type
      :type: str

      

   .. py:attribute:: pkg_data
      :type: conda.models.package_info.PackageInfo | None

      

   .. py:attribute:: actions
      :type: collections.abc.Iterable[conda.core.path_actions._Action]

      

   .. py:attribute:: target_prefix
      :type: str

      


.. py:class:: PrefixActionGroup


   Bases: :py:obj:`NamedTuple`

   .. py:attribute:: remove_menu_action_groups
      :type: collections.abc.Iterable[ActionGroup]

      

   .. py:attribute:: unlink_action_groups
      :type: collections.abc.Iterable[ActionGroup]

      

   .. py:attribute:: unregister_action_groups
      :type: collections.abc.Iterable[ActionGroup]

      

   .. py:attribute:: link_action_groups
      :type: collections.abc.Iterable[ActionGroup]

      

   .. py:attribute:: register_action_groups
      :type: collections.abc.Iterable[ActionGroup]

      

   .. py:attribute:: compile_action_groups
      :type: collections.abc.Iterable[ActionGroup]

      

   .. py:attribute:: make_menu_action_groups
      :type: collections.abc.Iterable[ActionGroup]

      

   .. py:attribute:: entry_point_action_groups
      :type: collections.abc.Iterable[ActionGroup]

      

   .. py:attribute:: prefix_record_groups
      :type: collections.abc.Iterable[ActionGroup]

      


.. py:class:: ChangeReport


   Bases: :py:obj:`NamedTuple`

   .. py:attribute:: prefix
      :type: str

      

   .. py:attribute:: specs_to_remove
      :type: collections.abc.Iterable[conda.resolve.MatchSpec]

      

   .. py:attribute:: specs_to_add
      :type: collections.abc.Iterable[conda.resolve.MatchSpec]

      

   .. py:attribute:: removed_precs
      :type: collections.abc.Iterable[conda.models.records.PackageRecord]

      

   .. py:attribute:: new_precs
      :type: collections.abc.Iterable[conda.models.records.PackageRecord]

      

   .. py:attribute:: updated_precs
      :type: collections.abc.Iterable[conda.models.records.PackageRecord]

      

   .. py:attribute:: downgraded_precs
      :type: collections.abc.Iterable[conda.models.records.PackageRecord]

      

   .. py:attribute:: superseded_precs
      :type: collections.abc.Iterable[conda.models.records.PackageRecord]

      

   .. py:attribute:: fetch_precs
      :type: collections.abc.Iterable[conda.models.records.PackageRecord]

      

   .. py:attribute:: revised_precs
      :type: collections.abc.Iterable[conda.models.records.PackageRecord]

      


.. py:class:: UnlinkLinkTransaction(*setups)


   .. py:property:: nothing_to_do


   .. py:method:: download_and_extract()


   .. py:method:: prepare()


   .. py:method:: verify()


   .. py:method:: _verify_pre_link_message(all_link_groups)


   .. py:method:: execute()


   .. py:method:: _get_pfe()


   .. py:method:: _prepare(transaction_context, target_prefix, unlink_precs, link_precs, remove_specs, update_specs, neutered_specs)
      :classmethod:


   .. py:method:: _verify_individual_level(prefix_action_group)
      :staticmethod:


   .. py:method:: _verify_prefix_level(target_prefix_AND_prefix_action_group_tuple)
      :staticmethod:


   .. py:method:: _verify_transaction_level(prefix_setups)
      :staticmethod:


   .. py:method:: _verify(prefix_setups, prefix_action_groups)


   .. py:method:: _execute(all_action_groups)


   .. py:method:: _execute_actions(axngroup)
      :staticmethod:


   .. py:method:: _execute_post_link_actions(axngroup)
      :staticmethod:


   .. py:method:: _reverse_actions(axngroup, reverse_from_idx=-1)
      :staticmethod:


   .. py:method:: _get_python_info(target_prefix, prefix_recs_to_unlink, packages_info_to_link) -> tuple[str | None, str | None]
      :staticmethod:

      Return the python version and location of the site-packages directory at the end of the transaction


   .. py:method:: _make_link_actions(transaction_context, package_info, target_prefix, requested_link_type, requested_spec)
      :staticmethod:


   .. py:method:: _make_entry_point_actions(transaction_context, package_info, target_prefix, requested_link_type, requested_spec, link_action_groups)
      :staticmethod:


   .. py:method:: _make_compile_actions(transaction_context, package_info, target_prefix, requested_link_type, requested_spec, link_action_groups)
      :staticmethod:


   .. py:method:: _make_legacy_action_groups()


   .. py:method:: print_transaction_summary()


   .. py:method:: _change_report_str(change_report)


   .. py:method:: _calculate_change_report(prefix, unlink_precs, link_precs, download_urls, specs_to_remove, specs_to_add)
      :staticmethod:



.. py:function:: run_script(prefix: str, prec, action: str = 'post-link', env_prefix: str = None, activate: bool = False) -> bool

   Call the post-link (or pre-unlink) script, returning True on success,
   False on failure.


.. py:function:: messages(prefix)


