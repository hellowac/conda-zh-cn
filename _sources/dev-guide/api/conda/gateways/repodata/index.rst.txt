:py:mod:`repodata`
==================

.. py:module:: conda.gateways.repodata

.. autoapi-nested-parse::

   Repodata interface.



.. toctree::
   :hidden:
   :titlesonly:
   :maxdepth: 3

   jlap/index.rst
   lock/index.rst


Classes
-------

.. autoapisummary::

   conda.gateways.repodata.PackageCacheData
   conda.gateways.repodata.Channel
   conda.gateways.repodata.RepoInterface
   conda.gateways.repodata.CondaRepoInterface
   conda.gateways.repodata.RepodataState
   conda.gateways.repodata.RepodataCache
   conda.gateways.repodata.RepodataFetch



Functions
---------

.. autoapisummary::

   conda.gateways.repodata.stringify
   conda.gateways.repodata.maybe_unquote
   conda.gateways.repodata.get_session
   conda.gateways.repodata.mkdir_p_sudo_safe
   conda.gateways.repodata.lock
   conda.gateways.repodata.get_repo_interface
   conda.gateways.repodata._add_http_value_to_dict
   conda.gateways.repodata.conda_http_errors
   conda.gateways.repodata._md5_not_for_security
   conda.gateways.repodata.cache_fn_url
   conda.gateways.repodata.get_cache_control_max_age
   conda.gateways.repodata.create_cache_dir



Attributes
----------

.. autoapisummary::

   conda.gateways.repodata.CONDA_HOMEPAGE_URL
   conda.gateways.repodata.REPODATA_FN
   conda.gateways.repodata.context
   conda.gateways.repodata.join_url
   conda.gateways.repodata.stderrlog
   conda.gateways.repodata.CHECK_ALTERNATE_FORMAT_INTERVAL
   conda.gateways.repodata.LAST_MODIFIED_KEY
   conda.gateways.repodata.ETAG_KEY
   conda.gateways.repodata.CACHE_CONTROL_KEY
   conda.gateways.repodata.URL_KEY
   conda.gateways.repodata.CACHE_STATE_SUFFIX
   conda.gateways.repodata.ERROR_SNIPPET_LENGTH


.. py:exception:: CondaError(message, caused_by=None, **kwargs)


   Bases: :py:obj:`Exception`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.

   .. py:attribute:: return_code
      :value: 1

      

   .. py:attribute:: reportable
      :value: False

      

   .. py:method:: __repr__()

      Return repr(self).


   .. py:method:: __str__()

      Return str(self).


   .. py:method:: dump_map()



.. py:function:: stringify(obj, content_max_len=0)


.. py:data:: CONDA_HOMEPAGE_URL
   :value: 'https://conda.io'

   

.. py:data:: REPODATA_FN
   :value: 'repodata.json'

   

.. py:data:: context

   

.. py:data:: join_url

   

.. py:function:: maybe_unquote(url)


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



.. py:exception:: CondaDependencyError(message)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CondaHTTPError(message, url, status_code, reason, elapsed_time, response=None, caused_by=None)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: CondaSSLError(message, caused_by=None, **kwargs)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: NotWritableError(path, errno, **kwargs)


   Bases: :py:obj:`conda.CondaError`, :py:obj:`OSError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: ProxyError


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: UnavailableInvalidChannel(channel, status_code, response: requests.models.Response | None = None)


   Bases: :py:obj:`ChannelError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.

   .. py:attribute:: status_code
      :type: str | int

      


.. py:class:: Channel(scheme=None, auth=None, location=None, token=None, name=None, platform=None, package_filename=None)


   Channel:
   scheme <> auth <> location <> token <> channel <> subchannel <> platform <> package_filename

   Package Spec:
   channel <> subchannel <> namespace <> package_name


   .. py:property:: channel_location


   .. py:property:: channel_name


   .. py:property:: subdir


   .. py:property:: canonical_name


   .. py:property:: base_url


   .. py:property:: base_urls


   .. py:property:: subdir_url


   .. py:property:: url_channel_wtf


   .. py:attribute:: _cache_

      

   .. py:method:: _reset_state()
      :staticmethod:


   .. py:method:: from_url(url)
      :staticmethod:


   .. py:method:: from_channel_name(channel_name)
      :staticmethod:


   .. py:method:: from_value(value: str | None) -> Self
      :staticmethod:

      Construct a new :class:`Channel` from a single value.

      :param value: Anyone of the following forms:

                    `None`, or one of the special strings "<unknown>", "None:///<unknown>", or "None":
                        represents the unknown channel, used for packages with unknown origin.

                    A URL including a scheme like ``file://`` or ``https://``:
                        represents a channel URL.

                    A local directory path:
                        represents a local channel; relative paths must start with ``./``.

                    A package file (i.e. the path to a file ending in ``.conda`` or ``.tar.bz2``):
                        represents a channel for a single package

                    A known channel name:
                        represents a known channel, e.g. from the users ``.condarc`` file or
                        the global configuration.

      :returns: A channel object.


   .. py:method:: make_simple_channel(channel_alias, channel_url, name=None)
      :staticmethod:


   .. py:method:: urls(with_credentials=False, subdirs=None)


   .. py:method:: url(with_credentials=False)


   .. py:method:: __str__()

      Return str(self).


   .. py:method:: __repr__()

      Return repr(self).


   .. py:method:: __eq__(other)

      Return self==value.


   .. py:method:: __hash__()

      Return hash(self).


   .. py:method:: __nonzero__()


   .. py:method:: __bool__()


   .. py:method:: __json__()


   .. py:method:: dump()



.. py:function:: get_session(url: str)

   Function that determines the correct Session object to be returned
   based on the URL that is passed in.


.. py:function:: mkdir_p_sudo_safe(path)


.. py:function:: lock(fd)


.. py:data:: stderrlog

   

.. py:data:: CHECK_ALTERNATE_FORMAT_INTERVAL

   

.. py:data:: LAST_MODIFIED_KEY
   :value: 'mod'

   

.. py:data:: ETAG_KEY
   :value: 'etag'

   

.. py:data:: CACHE_CONTROL_KEY
   :value: 'cache_control'

   

.. py:data:: URL_KEY
   :value: 'url'

   

.. py:data:: CACHE_STATE_SUFFIX
   :value: '.info.json'

   

.. py:data:: ERROR_SNIPPET_LENGTH
   :value: 32

   

.. py:exception:: RepodataIsEmpty(channel, status_code, response: requests.models.Response | None = None)


   Bases: :py:obj:`conda.exceptions.UnavailableInvalidChannel`

   Subclass used to determine when empty repodata should be cached, e.g. for a
   channel that doesn't provide current_repodata.json

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: RepodataOnDisk


   Bases: :py:obj:`Exception`

   Indicate that RepoInterface.repodata() successfully wrote repodata to disk,
   instead of returning a string.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:class:: RepoInterface


   Bases: :py:obj:`abc.ABC`

   Helper class that provides a standard way to create an ABC using
   inheritance.

   .. py:method:: repodata(state: dict) -> str

      Given a mutable state dictionary with information about the cache,
      return repodata.json (or current_repodata.json) as a str. This function
      also updates state, which is expected to be saved by the caller.



.. py:exception:: Response304ContentUnchanged


   Bases: :py:obj:`Exception`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:function:: get_repo_interface() -> type[RepoInterface]


.. py:class:: CondaRepoInterface(url: str, repodata_fn: str | None, **kwargs)


   Bases: :py:obj:`RepoInterface`

   Provides an interface for retrieving repodata data from channels.

   .. py:attribute:: _url
      :type: str

      

   .. py:attribute:: _repodata_fn
      :type: str

      

   .. py:method:: repodata(state: RepodataState) -> str | None

      Given a mutable state dictionary with information about the cache,
      return repodata.json (or current_repodata.json) as a str. This function
      also updates state, which is expected to be saved by the caller.



.. py:function:: _add_http_value_to_dict(resp, http_key, d, dict_key)


.. py:function:: conda_http_errors(url, repodata_fn)

   Use in a with: statement to translate requests exceptions to conda ones.


.. py:class:: RepodataState(cache_path_json: pathlib.Path | str = '', cache_path_state: pathlib.Path | str = '', repodata_fn='', dict=None)


   Bases: :py:obj:`collections.UserDict`

   Load/save info file that accompanies cached `repodata.json`.

   .. py:property:: mod
      :type: str

      Last-Modified header or ""

   .. py:property:: etag
      :type: str

      Etag header or ""

   .. py:property:: cache_control
      :type: str

      Cache-Control header or ""

   .. py:attribute:: _aliased

      

   .. py:attribute:: _strings

      

   .. py:method:: has_format(format: str) -> tuple[bool, datetime.datetime | None]


   .. py:method:: set_has_format(format: str, value: bool)


   .. py:method:: clear_has_format(format: str)

      Remove 'has_{format}' instead of setting to False.


   .. py:method:: should_check_format(format: str) -> bool

      Return True if named format should be attempted.


   .. py:method:: __contains__(key: str) -> bool


   .. py:method:: __setitem__(key: str, item: Any) -> None


   .. py:method:: __getitem__(key: str) -> Any



.. py:class:: RepodataCache(base, repodata_fn)


   Handle caching for a single repodata.json + repodata.info.json
   (<hex-string>*.json inside `dir`)

   Avoid race conditions while loading, saving repodata.json and cache state.

   base: directory and filename prefix for cache, e.g. /cache/dir/abc123;
   writes /cache/dir/abc123.json

   .. py:property:: cache_path_json


   .. py:property:: cache_path_state

      Out-of-band etag and other state needed by the RepoInterface.

   .. py:method:: load(*, state_only=False) -> str


   .. py:method:: load_state()

      Update self.state without reading repodata.json.

      Return self.state.


   .. py:method:: save(data: str)

      Write data to <repodata>.json cache path, synchronize state.


   .. py:method:: replace(temp_path: pathlib.Path)

      Rename path onto <repodata>.json path, synchronize state.

      Relies on path's mtime not changing on move. `temp_path` should be
      adjacent to `self.cache_path_json` to be on the same filesystem.


   .. py:method:: refresh(refresh_ns=0)

      Update access time in cache info file to indicate a HTTP 304 Not Modified response.


   .. py:method:: lock(mode='a+')

      Lock .info.json file. Hold lock while modifying related files.

      mode: "a+" then seek(0) to write/create; "r+" to read.


   .. py:method:: stale()

      Compare state refresh_ns against cache control header and
      context.local_repodata_ttl.


   .. py:method:: timeout()

      Return number of seconds until cache times out (<= 0 if already timed
      out).



.. py:class:: RepodataFetch(cache_path_base: pathlib.Path, channel: conda.models.channel.Channel, repodata_fn: str, *, repo_interface_cls)


   Combine RepodataCache and RepoInterface to provide subdir_data.SubdirData()
   with what it needs.

   Provide a variety of formats since some ``RepoInterface`` have to
   ``json.loads(...)`` anyway, and some clients don't need the Python data
   structure at all.

   .. py:property:: url_w_repodata_fn


   .. py:property:: cache_path_json


   .. py:property:: cache_path_state

      Out-of-band etag and other state needed by the RepoInterface.

   .. py:property:: repo_cache
      :type: RepodataCache


   .. py:property:: _repo
      :type: RepoInterface

      Changes as we mutate self.repodata_fn.

   .. py:attribute:: cache_path_base
      :type: pathlib.Path

      

   .. py:attribute:: channel
      :type: conda.models.channel.Channel

      

   .. py:attribute:: repodata_fn
      :type: str

      

   .. py:attribute:: url_w_subdir
      :type: str

      

   .. py:attribute:: url_w_credentials
      :type: str

      

   .. py:attribute:: repo_interface_cls
      :type: Any

      

   .. py:method:: fetch_latest_parsed() -> tuple[dict, RepodataState]

      Retrieve parsed latest or latest-cached repodata as a dict; update
      cache.

      :return: (repodata contents, state including cache headers)


   .. py:method:: fetch_latest_path() -> tuple[pathlib.Path, RepodataState]

      Retrieve latest or latest-cached repodata; update cache.

      :return: (pathlib.Path to uncompressed repodata contents, RepodataState)


   .. py:method:: fetch_latest() -> tuple[dict | str, RepodataState]

      Return up-to-date repodata and cache information. Fetch repodata from
      remote if cache has expired; return cached data if cache has not
      expired; return stale cached data or dummy data if in offline mode.


   .. py:method:: read_cache() -> tuple[str, RepodataState]

      Read repodata from disk, without trying to fetch a fresh version.



.. py:function:: _md5_not_for_security(data)


.. py:function:: cache_fn_url(url, repodata_fn=REPODATA_FN)


.. py:function:: get_cache_control_max_age(cache_control_value: str | None)


.. py:function:: create_cache_dir()


