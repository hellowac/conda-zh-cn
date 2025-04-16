:py:mod:`subdir_data`
=====================

.. py:module:: conda.core.subdir_data

.. autoapi-nested-parse::

   Tools for managing a subdir's repodata.json.



Classes
-------

.. autoapisummary::

   conda.core.subdir_data.SubdirDataType
   conda.core.subdir_data.PackageRecordList
   conda.core.subdir_data.SubdirData



Functions
---------

.. autoapisummary::

   conda.core.subdir_data.make_feature_record



Attributes
----------

.. autoapisummary::

   conda.core.subdir_data.REPODATA_PICKLE_VERSION
   conda.core.subdir_data.MAX_REPODATA_VERSION
   conda.core.subdir_data.REPODATA_HEADER_RE


.. py:data:: REPODATA_PICKLE_VERSION
   :value: 30

   

.. py:data:: MAX_REPODATA_VERSION
   :value: 2

   

.. py:data:: REPODATA_HEADER_RE
   :value: b'"(_etag|_mod|_cache_control)":[ ]?"(.*?[^\\\\])"[,}\\s]'

   

.. py:class:: SubdirDataType


   Bases: :py:obj:`type`

   .. py:method:: __call__(channel, repodata_fn=REPODATA_FN)

      Call self as a function.



.. py:class:: PackageRecordList(initlist=None)


   Bases: :py:obj:`collections.UserList`

   Lazily convert dicts to PackageRecord.

   .. py:method:: __getitem__(i)



.. py:class:: SubdirData(channel, repodata_fn=REPODATA_FN, RepoInterface=CondaRepoInterface)


   .. py:property:: _repo
      :type: conda.gateways.repodata.RepoInterface

      Changes as we mutate self.repodata_fn.

   .. py:property:: repo_cache
      :type: conda.gateways.repodata.RepodataCache


   .. py:property:: repo_fetch
      :type: conda.gateways.repodata.RepodataFetch

      Object to get repodata. Not cached since self.repodata_fn is mutable.

      Replaces self._repo & self.repo_cache.

   .. py:property:: cache_path_base


   .. py:property:: url_w_repodata_fn


   .. py:property:: cache_path_json


   .. py:property:: cache_path_state

      Out-of-band etag and other state needed by the RepoInterface.

   .. py:property:: cache_path_pickle


   .. py:attribute:: _cache_

      

   .. py:method:: clear_cached_local_channel_data(exclude_file=True)
      :classmethod:


   .. py:method:: query_all(package_ref_or_match_spec, channels=None, subdirs=None, repodata_fn=REPODATA_FN)
      :staticmethod:


   .. py:method:: query(package_ref_or_match_spec)


   .. py:method:: reload()


   .. py:method:: load()


   .. py:method:: iter_records()


   .. py:method:: _iter_records_by_name(name)


   .. py:method:: _load()

      Try to load repodata. If e.g. we are downloading
      `current_repodata.json`, fall back to `repodata.json` when the former is
      unavailable.


   .. py:method:: _pickle_me()


   .. py:method:: _read_local_repodata(state: conda.gateways.repodata.RepodataState)


   .. py:method:: _pickle_valid_checks(pickled_state, mod, etag)

      Throw away the pickle if these don't all match.


   .. py:method:: _read_pickled(state: conda.gateways.repodata.RepodataState)


   .. py:method:: _process_raw_repodata_str(raw_repodata_str, state: conda.gateways.repodata.RepodataState | None = None)

      State contains information that was previously in-band in raw_repodata_str.


   .. py:method:: _process_raw_repodata(repodata: dict, state: conda.gateways.repodata.RepodataState | None = None)


   .. py:method:: _get_base_url(repodata: dict, with_credentials: bool = True) -> str

      In repodata_version=1, .tar.bz2 and .conda artifacts are assumed to
      be colocated next to repodata.json, in the same server and directory.

      In repodata_version=2, repodata.json files can define a 'base_url' field
      to override that default assumption. See CEP-15 for more details.

      This method deals with both cases and returns the appropriate value.



.. py:function:: make_feature_record(feature_name)


