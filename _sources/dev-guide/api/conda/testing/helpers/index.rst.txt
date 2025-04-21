:py:mod:`helpers`
=================

.. py:module:: conda.testing.helpers

.. autoapi-nested-parse::

   Collection of helper functions used in conda tests.




Functions
---------

.. autoapisummary::

   conda.testing.helpers.strip_expected
   conda.testing.helpers.raises
   conda.testing.helpers.captured
   conda.testing.helpers.assert_equals
   conda.testing.helpers.assert_not_in
   conda.testing.helpers.assert_in
   conda.testing.helpers.add_subdir
   conda.testing.helpers.add_subdir_to_iter
   conda.testing.helpers.tempdir
   conda.testing.helpers.supplement_index_with_repodata
   conda.testing.helpers.add_feature_records_legacy
   conda.testing.helpers._export_subdir_data_to_repodata
   conda.testing.helpers._sync_channel_to_disk
   conda.testing.helpers._alias_canonical_channel_name_cache_to_file_prefixed
   conda.testing.helpers._patch_for_local_exports
   conda.testing.helpers._get_index_r_base
   conda.testing.helpers.get_index_r_1
   conda.testing.helpers.get_index_r_2
   conda.testing.helpers.get_index_r_4
   conda.testing.helpers.get_index_r_5
   conda.testing.helpers.get_index_must_unfreeze
   conda.testing.helpers.get_index_cuda
   conda.testing.helpers.record
   conda.testing.helpers._get_solver_base
   conda.testing.helpers.get_solver
   conda.testing.helpers.get_solver_2
   conda.testing.helpers.get_solver_4
   conda.testing.helpers.get_solver_5
   conda.testing.helpers.get_solver_aggregate_1
   conda.testing.helpers.get_solver_aggregate_2
   conda.testing.helpers.get_solver_must_unfreeze
   conda.testing.helpers.get_solver_cuda
   conda.testing.helpers.convert_to_dist_str
   conda.testing.helpers.solver_class



Attributes
----------

.. autoapisummary::

   conda.testing.helpers.TEST_DATA_DIR
   conda.testing.helpers.CHANNEL_DIR_V2
   conda.testing.helpers.EXPORTED_CHANNELS_DIR
   conda.testing.helpers.expected_error_prefix


.. py:data:: TEST_DATA_DIR

   

.. py:data:: CHANNEL_DIR_V2

   

.. py:data:: EXPORTED_CHANNELS_DIR

   

.. py:data:: expected_error_prefix
   :value: 'Using Anaconda Cloud api site https://api.anaconda.org'

   

.. py:function:: strip_expected(stderr)


.. py:function:: raises(exception, func, string=None)


.. py:function:: captured(disallow_stderr=True)


.. py:function:: assert_equals(a, b, output='')


.. py:function:: assert_not_in(a, b, output='')


.. py:function:: assert_in(a, b, output='')


.. py:function:: add_subdir(dist_string)


.. py:function:: add_subdir_to_iter(iterable)


.. py:function:: tempdir()


.. py:function:: supplement_index_with_repodata(index, repodata, channel, priority)


.. py:function:: add_feature_records_legacy(index)


.. py:function:: _export_subdir_data_to_repodata(subdir_data: conda.core.subdir_data.SubdirData)

   This function is only temporary and meant to patch wrong / undesirable
   testing behaviour. It should end up being replaced with the new class-based,
   backend-agnostic solver tests.


.. py:function:: _sync_channel_to_disk(subdir_data: conda.core.subdir_data.SubdirData)

   This function is only temporary and meant to patch wrong / undesirable
   testing behaviour. It should end up being replaced with the new class-based,
   backend-agnostic solver tests.


.. py:function:: _alias_canonical_channel_name_cache_to_file_prefixed(name, subdir_data=None)

   This function is only temporary and meant to patch wrong / undesirable
   testing behaviour. It should end up being replaced with the new class-based,
   backend-agnostic solver tests.


.. py:function:: _patch_for_local_exports(name, subdir_data)

   This function is only temporary and meant to patch wrong / undesirable
   testing behaviour. It should end up being replaced with the new class-based,
   backend-agnostic solver tests.


.. py:function:: _get_index_r_base(json_filename_or_packages, channel_name, subdir=context.subdir, add_pip=False, merge_noarch=False)


.. py:function:: get_index_r_1(subdir=context.subdir, add_pip=True, merge_noarch=False)


.. py:function:: get_index_r_2(subdir=context.subdir, add_pip=True, merge_noarch=False)


.. py:function:: get_index_r_4(subdir=context.subdir, add_pip=True, merge_noarch=False)


.. py:function:: get_index_r_5(subdir=context.subdir, add_pip=False, merge_noarch=False)


.. py:function:: get_index_must_unfreeze(subdir=context.subdir, add_pip=True, merge_noarch=False)


.. py:function:: get_index_cuda(subdir=context.subdir, add_pip=True, merge_noarch=False)


.. py:function:: record(name='a', version='1.0', depends=None, build='0', build_number=0, timestamp=0, channel=None, **kwargs)


.. py:function:: _get_solver_base(channel_id, tmpdir, specs_to_add=(), specs_to_remove=(), prefix_records=(), history_specs=(), add_pip=False, merge_noarch=False)


.. py:function:: get_solver(tmpdir, specs_to_add=(), specs_to_remove=(), prefix_records=(), history_specs=(), add_pip=False, merge_noarch=False)


.. py:function:: get_solver_2(tmpdir, specs_to_add=(), specs_to_remove=(), prefix_records=(), history_specs=(), add_pip=False, merge_noarch=False)


.. py:function:: get_solver_4(tmpdir, specs_to_add=(), specs_to_remove=(), prefix_records=(), history_specs=(), add_pip=False, merge_noarch=False)


.. py:function:: get_solver_5(tmpdir, specs_to_add=(), specs_to_remove=(), prefix_records=(), history_specs=(), add_pip=False, merge_noarch=False)


.. py:function:: get_solver_aggregate_1(tmpdir, specs_to_add=(), specs_to_remove=(), prefix_records=(), history_specs=(), add_pip=False, merge_noarch=False)


.. py:function:: get_solver_aggregate_2(tmpdir, specs_to_add=(), specs_to_remove=(), prefix_records=(), history_specs=(), add_pip=False, merge_noarch=False)


.. py:function:: get_solver_must_unfreeze(tmpdir, specs_to_add=(), specs_to_remove=(), prefix_records=(), history_specs=(), add_pip=False, merge_noarch=False)


.. py:function:: get_solver_cuda(tmpdir, specs_to_add=(), specs_to_remove=(), prefix_records=(), history_specs=(), add_pip=False, merge_noarch=False)


.. py:function:: convert_to_dist_str(solution)


.. py:function:: solver_class()


