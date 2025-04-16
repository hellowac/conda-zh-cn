:py:mod:`index`
===============

.. py:module:: conda.core.index

.. autoapi-nested-parse::

   Tools for fetching the current index.



Classes
-------

.. autoapisummary::

   conda.core.index.Index
   conda.core.index.ReducedIndex



Functions
---------

.. autoapisummary::

   conda.core.index.check_allowlist
   conda.core.index.get_index
   conda.core.index.fetch_index
   conda.core.index.dist_str_in_index
   conda.core.index._supplement_index_with_prefix
   conda.core.index._supplement_index_with_cache
   conda.core.index._make_virtual_package
   conda.core.index._supplement_index_with_features
   conda.core.index._supplement_index_with_system
   conda.core.index.get_archspec_name
   conda.core.index.calculate_channel_urls
   conda.core.index.get_reduced_index



Attributes
----------

.. autoapisummary::

   conda.core.index.LAST_CHANNEL_URLS


.. py:data:: LAST_CHANNEL_URLS
   :value: []

   

.. py:function:: check_allowlist(channel_urls: list[str]) -> None

   Check if the given channel URLs are allowed by the context's allowlist.
   :param channel_urls: A list of channel URLs to check against the allowlist.
   :raises ChannelNotAllowed: If any URL is not in the allowlist.
   :raises ChannelDenied: If any URL is in the denylist.


.. py:class:: Index(channels: collections.abc.Iterable[str | conda.models.channel.Channel] = (), prepend: bool = True, platform: str | None = None, subdirs: tuple[str, Ellipsis] | None = None, use_local: bool = False, use_cache: bool | None = None, prefix: str | os.PathLike[str] | pathlib.Path | conda.core.prefix_data.PrefixData | None = None, repodata_fn: str | None = context.repodata_fns[-1], use_system: bool = False)


   Bases: :py:obj:`collections.UserDict`

   The ``Index`` provides information about available packages from all relevant sources.

   There are four types of sources for package information, namely

   Channels
       represent packages available from standard sources identified with a url, mostly online,
       but can also be on a local filesystem using the ``file://`` scheme.
       Programatically, channels are represented by :class:`conda.models.channel.Channel`, their data
       is fetched using :class:`conda.core.subdir_data.SubdirData`.

       For more information see :ref:`concepts-channels`.

       Individual packages from channels are usually represented by :class:`conda.models.records.PackageRecord`.

   Prefix
       represents packages that are already installed. Every :class:`Index` can be associated
       with exactly one Prefix, which is the location of one of the conda :ref:`concepts-conda-environments`.
       The package information about the installed packages is represented by :class:`conda.core.prefix_data.PrefixData`.

       Individual packages from prefixes are usually represented by :class:`conda.models.records.PrefixRecord`.

   Package Cache
       represents packages that are locally unpacked, but may not be installed in the environment
       associated with this index. These are usually packages that have been installed in any environment
       of the local conda installation, but may have been removed from all environments by now.

       Individual packages from the package are usually represented by :class:`conda.models.records.PackageCacheRecord`.

   Virtual Packages
       represent properties of the system, not actual conda packages in the normal sense. These are,
       for example, system packages that inform the solver about the operating system in use, or
       track features that can be used to steer package priority.

       Individual virtual packages are represented by special :class:`conda.models.records.PackageRecord`,
       see :meth:`conda.models.records.PackageRecord.virtual_package` and
       :meth:`conda.models.records.PackageRecord.feature`.

   Initializes a new index with the desired components.

   :param channels: channels identified by canonical names or URLS or Channel objects;
                    for more details, see :meth:`conda.models.channel.Channel.from_value`
   :param prepend: if ``True`` (default), add configured channel with higher priority than passed channels;
                   if ``False``, do *not* add configured channels.
   :param platform: see ``subdirs``.
   :param subdirs: platform and subdirs determine the selection of subdirs in the channels;
                   if both are ``None``, subdirs is taken from the configuration;
                   if both are given, ``subdirs`` takes precedence and ``platform`` is ignored;
                   if only ``platform`` is given, subdirs will be ``(platform, "noarch")``;
                   if ``subdirs`` is given, subdirs will be ``subdirs``.
   :param use_local: if ``True``, add the special "local" channel for locally built packages with lowest priority.
   :param use_cache: if ``True``, add packages from the package cache.
   :param prefix: associate prefix with this index and add its packages.
   :param repodata_fn: filename of the repodata, default taken from config, almost always "repodata.json".
   :param use_system: if ``True``, add system packages, that is virtual packages defined by plugins, usually used
                      to make intrinsic information about the system, such as cpu architecture or operating system, available
                      to the solver.

   .. py:property:: cache_entries
      :type: tuple[conda.models.records.PackageCacheRecord, Ellipsis]

      Contents of the package cache if active.

      :returns: All packages available from the package cache.

   .. py:property:: system_packages
      :type: dict[conda.models.records.PackageRecord, conda.models.records.PackageRecord]

      System packages provided by plugins.

      :returns: Identity mapping of the available system packages in a ``dict``.

   .. py:property:: features
      :type: dict[conda.models.records.PackageRecord, conda.models.records.PackageRecord]

      Active tracking features.

      :returns: Identity mapping of the local tracking features in a ``dict``.

   .. py:property:: data
      :type: dict[conda.models.records.PackageRecord, conda.models.records.PackageRecord]

      The entire index as a dict; avoid if possible.

      .. warning::

         This returns the entire contents of the index as a single identity mapping in
         a ``dict``. This may be convenient, but it comes at a cost because all sources
         must be fully loaded at significant overhead for :class:`~conda.models.records.PackageRecord`
         construction for **every** package.
         
         Hence, all uses of :attr:`data`, including all iteration over the entire index,
         is strongly discouraged.

   .. py:method:: reload(*, prefix: bool = False, cache: bool = False, features: bool = False, system: bool = False) -> None

      Reload one or more of the index components.

      Can be used to refresh the index with new information, for example after a new
      package has been installed into the index.

      :param prefix: if ``True``, reload the prefix data.
      :param cache: if ``True``, reload the package cache.
      :param features: if ``True``, reload the tracking features.
      :param system: if ``True``, reload the system packages.


   .. py:method:: __repr__() -> str

      Return repr(self).


   .. py:method:: get_reduced_index(specs: collections.abc.Iterable[conda.models.match_spec.MatchSpec]) -> ReducedIndex

      Create a reduced index with a subset of packages.

      Can be used to create a reduced index as a subset from an existing index.

      :param specs: the specs that span the subset.

      :returns: a reduced index with the same sources as this index, but limited to ``specs``
                and their dependency graph.


   .. py:method:: _supplement_index_dict_with_prefix() -> None

      Supplement the index with information from its prefix.


   .. py:method:: _supplement_index_dict_with_cache() -> None


   .. py:method:: _realize() -> None


   .. py:method:: _retrieve_from_channels(key: conda.models.records.PackageRecord) -> conda.models.records.PackageRecord | None


   .. py:method:: _retrieve_all_from_channels(key: conda.models.records.PackageRecord) -> list[conda.models.records.PackageRecord]


   .. py:method:: _update_from_prefix(key: conda.models.records.PackageRecord, prec: conda.models.records.PackageRecord | None) -> conda.models.records.PackageRecord | None


   .. py:method:: _update_from_cache(key: conda.models.records.PackageRecord, prec: conda.models.records.PackageRecord | None) -> conda.models.records.PackageRecord | None


   .. py:method:: __getitem__(key: conda.models.records.PackageRecord) -> conda.models.records.PackageRecord


   .. py:method:: __contains__(key: conda.models.records.PackageRecord) -> bool


   .. py:method:: __copy__() -> Self



.. py:class:: ReducedIndex(specs: collections.abc.Iterable[conda.models.match_spec.MatchSpec], channels: tuple[str, Ellipsis] = (), prepend: bool = True, platform: str | None = None, subdirs: tuple[str, Ellipsis] | None = None, use_local: bool = False, use_cache: bool | None = None, prefix: str | os.PathLike[str] | pathlib.Path | conda.core.prefix_data.PrefixData | None = None, repodata_fn: str | None = context.repodata_fns[-1], use_system: bool = False)


   Bases: :py:obj:`Index`

   Index that contains a subset of available packages.

   Like :class:`Index`, this makes information about packages from the same four
   sources available. However, the contents of the reduced index is limited to
   a subset of packages relevant to a given specification.
   This works by taking into account all packages that match the given specification
   together with their dependencies and their dependencies dependencies, etc.

   .. note:: See :meth:`Index.get_reduced_index` for convenient construction.

   Initialize a new reduced index.

   :param specs: the collection of specifications that span the subset of packages.
   :param all other args: see :class:`Index`.

   .. py:method:: __repr__() -> str

      Return repr(self).


   .. py:method:: _derive_reduced_index() -> None



.. py:function:: get_index(channel_urls: collections.abc.Iterable[str | conda.models.channel.Channel] = (), prepend: bool = True, platform: str | None = None, use_local: bool = False, use_cache: bool = False, unknown: bool | None = None, prefix: str | None = None, repodata_fn: str = context.repodata_fns[-1]) -> Index

   Return the index of packages available on the channels

   If prepend=False, only the channels passed in as arguments are used.
   If platform=None, then the current platform is used.
   If prefix is supplied, then the packages installed in that prefix are added.

   :param channel_urls: Channels to include in the index.
   :param prepend: If False, only the channels passed in are used.
   :param platform: Target platform for the index.
   :param use_local: Whether to use local channels.
   :param use_cache: Whether to use cached index information.
   :param unknown: Include unknown packages.
   :param prefix: Path to environment prefix to include in the index.
   :param repodata_fn: Filename of the repodata file.
   :return: A dictionary representing the package index.


.. py:function:: fetch_index(channel_urls: list[str], use_cache: bool = False, index: dict | None = None, repodata_fn: str = context.repodata_fns[-1]) -> dict

   Fetch the package index from the specified channels.

   :param channel_urls: A list of channel URLs to fetch the index from.
   :param use_cache: Whether to use the cached index data.
   :param index: An optional pre-existing index to update.
   :param repodata_fn: The name of the repodata file.
   :return: A dictionary representing the fetched or updated package index.


.. py:function:: dist_str_in_index(index: dict[Any, Any], dist_str: str) -> bool

   Check if a distribution string matches any package in the index.

   :param index: The package index.
   :param dist_str: The distribution string to match against the index.
   :return: True if there is a match; False otherwise.


.. py:function:: _supplement_index_with_prefix(index: Index | dict[Any, Any], prefix: str | os.PathLike[str] | pathlib.Path | conda.core.prefix_data.PrefixData) -> None

   Supplement the given index with information from the specified environment prefix.

   :param index: The package index to supplement.
   :param prefix: The path to the environment prefix.


.. py:function:: _supplement_index_with_cache(index: dict[Any, Any]) -> None

   Supplement the given index with packages from the cache.

   :param index: The package index to supplement.


.. py:function:: _make_virtual_package(name: str, version: str | None = None, build_string: str | None = None) -> conda.models.records.PackageRecord

   Create a virtual package record.

   :param name: The name of the virtual package.
   :param version: The version of the virtual package, defaults to "0".
   :param build_string: The build string of the virtual package, defaults to "0".
   :return: A PackageRecord representing the virtual package.


.. py:function:: _supplement_index_with_features(index: dict[conda.models.records.PackageRecord, conda.models.records.PackageRecord], features: list[str] = []) -> None

   Supplement the given index with virtual feature records.

   :param index: The package index to supplement.
   :param features: A list of feature names to add to the index.


.. py:function:: _supplement_index_with_system(index: dict[conda.models.records.PackageRecord, conda.models.records.PackageRecord]) -> None

   Loads and populates virtual package records from conda plugins
   and adds them to the provided index, unless there is a naming
   conflict.

   :param index: The package index to supplement.


.. py:function:: get_archspec_name() -> str | None

   Determine the architecture specification name for the current environment.

   :return: The architecture name if available, otherwise None.


.. py:function:: calculate_channel_urls(channel_urls: tuple[str] = (), prepend: bool = True, platform: str | None = None, use_local: bool = False) -> list[str]

   Calculate the full list of channel URLs to use based on the given parameters.

   :param channel_urls: Initial list of channel URLs.
   :param prepend: Whether to prepend default channels to the list.
   :param platform: The target platform for the channels.
   :param use_local: Whether to include the local channel.
   :return: The calculated list of channel URLs.


.. py:function:: get_reduced_index(prefix: str | None, channels: list[str], subdirs: list[str], specs: list[conda.models.match_spec.MatchSpec], repodata_fn: str) -> dict

   Generate a reduced package index based on the given specifications.

   This function is useful for optimizing the solver by reducing the amount
   of data it needs to consider.

   :param prefix: Path to an environment prefix to include installed packages.
   :param channels: A list of channel names to include in the index.
   :param subdirs: A list of subdirectories to consider for each channel.
   :param specs: A list of MatchSpec objects to filter the packages.
   :param repodata_fn: Filename of the repodata file to use.
   :return: A dictionary representing the reduced package index.


