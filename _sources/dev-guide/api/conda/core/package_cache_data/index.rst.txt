:py:mod:`package_cache_data`
============================

.. py:module:: conda.core.package_cache_data

.. autoapi-nested-parse::

   Tools for managing the package cache (previously downloaded packages).



Classes
-------

.. autoapisummary::

   conda.core.package_cache_data.PackageCacheType
   conda.core.package_cache_data.PackageCacheData
   conda.core.package_cache_data.UrlsData
   conda.core.package_cache_data.ProgressiveFetchExtract



Functions
---------

.. autoapisummary::

   conda.core.package_cache_data.do_cache_action
   conda.core.package_cache_data.do_extract_action
   conda.core.package_cache_data.do_cleanup
   conda.core.package_cache_data.do_reverse
   conda.core.package_cache_data.done_callback



Attributes
----------

.. autoapisummary::

   conda.core.package_cache_data.FileNotFoundError
   conda.core.package_cache_data.THREADSAFE_EXTRACT
   conda.core.package_cache_data.EXTRACT_THREADS


.. py:data:: FileNotFoundError

   

.. py:data:: THREADSAFE_EXTRACT
   :value: False

   

.. py:data:: EXTRACT_THREADS

   

.. py:class:: PackageCacheType


   Bases: :py:obj:`type`

   This metaclass does basic caching of PackageCache instance objects.

   .. py:method:: __call__(pkgs_dir: str | os.PathLike | pathlib.Path)

      Call self as a function.



.. py:class:: PackageCacheData(pkgs_dir)


   .. py:property:: _package_cache_records


   .. py:property:: is_writable


   .. py:attribute:: _cache_
      :type: dict[str, PackageCacheData]

      

   .. py:method:: insert(package_cache_record)


   .. py:method:: load()


   .. py:method:: reload()


   .. py:method:: get(package_ref, default=NULL)


   .. py:method:: remove(package_ref, default=NULL)


   .. py:method:: query(package_ref_or_match_spec)


   .. py:method:: iter_records()


   .. py:method:: query_all(package_ref_or_match_spec, pkgs_dirs=None)
      :classmethod:


   .. py:method:: first_writable(pkgs_dirs=None)
      :classmethod:


   .. py:method:: writable_caches(pkgs_dirs=None)
      :classmethod:


   .. py:method:: read_only_caches(pkgs_dirs=None)
      :classmethod:


   .. py:method:: all_caches_writable_first(pkgs_dirs=None)
      :classmethod:


   .. py:method:: get_all_extracted_entries()
      :classmethod:


   .. py:method:: get_entry_to_link(package_ref)
      :classmethod:


   .. py:method:: tarball_file_in_cache(tarball_path, md5sum=None, exclude_caches=())
      :classmethod:


   .. py:method:: clear()
      :classmethod:


   .. py:method:: tarball_file_in_this_cache(tarball_path, md5sum=None)


   .. py:method:: _check_writable()


   .. py:method:: _clean_tarball_path_and_get_md5sum(tarball_path, md5sum=None)
      :staticmethod:


   .. py:method:: _scan_for_dist_no_channel(dist_str)


   .. py:method:: itervalues()


   .. py:method:: values()


   .. py:method:: __repr__()

      Return repr(self).


   .. py:method:: _make_single_record(package_filename)


   .. py:method:: _dedupe_pkgs_dir_contents(pkgs_dir_contents)
      :staticmethod:



.. py:class:: UrlsData(pkgs_dir)


   .. py:method:: __contains__(url)


   .. py:method:: __iter__()


   .. py:method:: add_url(url)


   .. py:method:: get_url(package_path)



.. py:class:: ProgressiveFetchExtract(link_prefs)


   
   :param link_prefs: A sequence of :class:`PackageRecord`s to ensure available in a known
                      package cache, typically for a follow-on :class:`UnlinkLinkTransaction`.
                      Here, "available" means the package tarball is both downloaded and extracted
                      to a package directory.
   :type link_prefs: tuple[PackageRecord]

   .. py:property:: cache_actions


   .. py:property:: extract_actions


   .. py:method:: make_actions_for_record(pref_or_spec)
      :staticmethod:


   .. py:method:: prepare()


   .. py:method:: execute()

      Run each action in self.paired_actions. Each action in cache_actions
      runs before its corresponding extract_actions.


   .. py:method:: _progress_bar(prec_or_spec, position=None, leave=False, context_manager=None) -> conda.plugins.types.ProgressBarBase
      :staticmethod:


   .. py:method:: __hash__()

      Return hash(self).


   .. py:method:: __eq__(other)

      Return self==value.



.. py:function:: do_cache_action(prec, cache_action, progress_bar, download_total=1.0, *, cancelled)

   This function gets called from `ProgressiveFetchExtract.execute`.


.. py:function:: do_extract_action(prec, extract_action, progress_bar)

   This function gets called after do_cache_action completes.


.. py:function:: do_cleanup(actions)


.. py:function:: do_reverse(actions)


.. py:function:: done_callback(future: concurrent.futures.Future, actions: tuple[conda.core.path_actions.CacheUrlAction | conda.core.path_actions.ExtractPackageAction, Ellipsis], progress_bar: conda.plugins.types.ProgressBarBase, exceptions: list[Exception], finish: bool = False)


