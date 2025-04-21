:py:mod:`api`
=============

.. py:module:: conda.api

.. autoapi-nested-parse::

   Collection of conda's high-level APIs.



Classes
-------

.. autoapisummary::

   conda.api.Solver
   conda.api.SubdirData
   conda.api.PackageCacheData
   conda.api.PrefixData




Attributes
----------

.. autoapisummary::

   conda.api.DepsModifier
   conda.api.UpdateModifier


.. py:data:: DepsModifier

   

.. py:data:: UpdateModifier

   

.. py:class:: Solver(prefix, channels, subdirs=(), specs_to_add=(), specs_to_remove=())


   **Beta** While in beta, expect both major and minor changes across minor releases.

   A high-level API to conda's solving logic. Three public methods are provided to access a
   solution in various forms.

     * :meth:`solve_final_state`
     * :meth:`solve_for_diff`
     * :meth:`solve_for_transaction`


   **Beta**

   :param prefix: The conda prefix / environment location for which the :class:`Solver`
                  is being instantiated.
   :type prefix: str
   :param channels: A prioritized list of channels to use for the solution.
   :type channels: Sequence[:class:`Channel`]
   :param subdirs: A prioritized list of subdirs to use for the solution.
   :type subdirs: Sequence[str]
   :param specs_to_add: The set of package specs to add to the prefix.
   :type specs_to_add: set[:class:`MatchSpec`]
   :param specs_to_remove: The set of package specs to remove from the prefix.
   :type specs_to_remove: set[:class:`MatchSpec`]

   .. py:method:: solve_final_state(update_modifier=NULL, deps_modifier=NULL, prune=NULL, ignore_pinned=NULL, force_remove=NULL)

      **Beta** While in beta, expect both major and minor changes across minor releases.

      Gives the final, solved state of the environment.

      :param deps_modifier: An optional flag indicating special solver handling for dependencies. The
                            default solver behavior is to be as conservative as possible with dependency
                            updates (in the case the dependency already exists in the environment), while
                            still ensuring all dependencies are satisfied.  Options include
                            * NO_DEPS
                            * ONLY_DEPS
                            * UPDATE_DEPS
                            * UPDATE_DEPS_ONLY_DEPS
                            * FREEZE_INSTALLED
      :type deps_modifier: DepsModifier
      :param prune: If ``True``, the solution will not contain packages that were
                    previously brought into the environment as dependencies but are no longer
                    required as dependencies and are not user-requested.
      :type prune: bool
      :param ignore_pinned: If ``True``, the solution will ignore pinned package configuration
                            for the prefix.
      :type ignore_pinned: bool
      :param force_remove: Forces removal of a package without removing packages that depend on it.
      :type force_remove: bool

      :returns:     In sorted dependency order from roots to leaves, the package references for
                    the solved state of the environment.
      :rtype: tuple[PackageRef]


   .. py:method:: solve_for_diff(update_modifier=NULL, deps_modifier=NULL, prune=NULL, ignore_pinned=NULL, force_remove=NULL, force_reinstall=False)

      **Beta** While in beta, expect both major and minor changes across minor releases.

      Gives the package references to remove from an environment, followed by
      the package references to add to an environment.

      :param deps_modifier: See :meth:`solve_final_state`.
      :type deps_modifier: DepsModifier
      :param prune: See :meth:`solve_final_state`.
      :type prune: bool
      :param ignore_pinned: See :meth:`solve_final_state`.
      :type ignore_pinned: bool
      :param force_remove: See :meth:`solve_final_state`.
      :type force_remove: bool
      :param force_reinstall: For requested specs_to_add that are already satisfied in the environment,
                              instructs the solver to remove the package and spec from the environment,
                              and then add it back--possibly with the exact package instance modified,
                              depending on the spec exactness.
      :type force_reinstall: bool

      :returns:     A two-tuple of PackageRef sequences.  The first is the group of packages to
                    remove from the environment, in sorted dependency order from leaves to roots.
                    The second is the group of packages to add to the environment, in sorted
                    dependency order from roots to leaves.
      :rtype: tuple[PackageRef], tuple[PackageRef]


   .. py:method:: solve_for_transaction(update_modifier=NULL, deps_modifier=NULL, prune=NULL, ignore_pinned=NULL, force_remove=NULL, force_reinstall=False)

      **Beta** While in beta, expect both major and minor changes across minor releases.

      Gives an UnlinkLinkTransaction instance that can be used to execute the solution
      on an environment.

      :param deps_modifier: See :meth:`solve_final_state`.
      :type deps_modifier: DepsModifier
      :param prune: See :meth:`solve_final_state`.
      :type prune: bool
      :param ignore_pinned: See :meth:`solve_final_state`.
      :type ignore_pinned: bool
      :param force_remove: See :meth:`solve_final_state`.
      :type force_remove: bool
      :param force_reinstall: See :meth:`solve_for_diff`.
      :type force_reinstall: bool

      :rtype: UnlinkLinkTransaction



.. py:class:: SubdirData(channel)


   **Beta** While in beta, expect both major and minor changes across minor releases.

   High-level management and usage of repodata.json for subdirs.

   **Beta** While in beta, expect both major and minor changes across minor releases.

   :param channel: The target subdir for the instance. Must either be a url that includes a subdir
                   or a :obj:`Channel` that includes a subdir. e.g.:
                       * 'https://repo.anaconda.com/pkgs/main/linux-64'
                       * Channel('https://repo.anaconda.com/pkgs/main/linux-64')
                       * Channel('conda-forge/osx-64')
   :type channel: str or Channel

   .. py:method:: query(package_ref_or_match_spec)

      **Beta** While in beta, expect both major and minor changes across minor releases.

      Run a query against this specific instance of repodata.

      :param package_ref_or_match_spec: Either an exact :obj:`PackageRef` to match against, or a :obj:`MatchSpec`
                                        query object.  A :obj:`str` will be turned into a :obj:`MatchSpec` automatically.
      :type package_ref_or_match_spec: PackageRef or MatchSpec or str

      :returns: tuple[PackageRecord]


   .. py:method:: query_all(package_ref_or_match_spec, channels=None, subdirs=None)
      :staticmethod:

      **Beta** While in beta, expect both major and minor changes across minor releases.

      Run a query against all repodata instances in channel/subdir matrix.

      :param package_ref_or_match_spec: Either an exact :obj:`PackageRef` to match against, or a :obj:`MatchSpec`
                                        query object.  A :obj:`str` will be turned into a :obj:`MatchSpec` automatically.
      :type package_ref_or_match_spec: PackageRef or MatchSpec or str
      :param channels: An iterable of urls for channels or :obj:`Channel` objects. If None, will fall
                       back to context.channels.
      :type channels: Iterable[Channel or str] or None
      :param subdirs: If None, will fall back to context.subdirs.
      :type subdirs: Iterable[str] or None

      :returns: tuple[PackageRecord]


   .. py:method:: iter_records()

      **Beta** While in beta, expect both major and minor changes across minor releases.

      :returns:

                A generator over all records contained in the repodata.json
                    instance.  Warning: this is a generator that is exhausted on first use.
      :rtype: Iterable[PackageRecord]


   .. py:method:: reload()

      **Beta** While in beta, expect both major and minor changes across minor releases.

      Update the instance with new information. Backing information (i.e. repodata.json)
      is lazily downloaded/loaded on first use by the other methods of this class. You
      should only use this method if you are *sure* you have outdated data.

      :returns: SubdirData



.. py:class:: PackageCacheData(pkgs_dir)


   **Beta** While in beta, expect both major and minor changes across minor releases.

   High-level management and usage of package caches.

   **Beta** While in beta, expect both major and minor changes across minor releases.

   :param pkgs_dir:
   :type pkgs_dir: str

   .. py:property:: is_writable

      **Beta** While in beta, expect both major and minor changes across minor releases.

      Indicates if the package cache location is writable or read-only.

      :returns: bool

   .. py:method:: get(package_ref, default=NULL)

      **Beta** While in beta, expect both major and minor changes across minor releases.

      :param package_ref: A :obj:`PackageRef` instance representing the key for the
                          :obj:`PackageCacheRecord` being sought.
      :type package_ref: PackageRef
      :param default: The default value to return if the record does not exist. If not
                      specified and no record exists, :exc:`KeyError` is raised.

      :returns: PackageCacheRecord


   .. py:method:: query(package_ref_or_match_spec)

      **Beta** While in beta, expect both major and minor changes across minor releases.

      Run a query against this specific package cache instance.

      :param package_ref_or_match_spec: Either an exact :obj:`PackageRef` to match against, or a :obj:`MatchSpec`
                                        query object.  A :obj:`str` will be turned into a :obj:`MatchSpec` automatically.
      :type package_ref_or_match_spec: PackageRef or MatchSpec or str

      :returns: tuple[PackageCacheRecord]


   .. py:method:: query_all(package_ref_or_match_spec, pkgs_dirs=None)
      :staticmethod:

      **Beta** While in beta, expect both major and minor changes across minor releases.

      Run a query against all package caches.

      :param package_ref_or_match_spec: Either an exact :obj:`PackageRef` to match against, or a :obj:`MatchSpec`
                                        query object.  A :obj:`str` will be turned into a :obj:`MatchSpec` automatically.
      :type package_ref_or_match_spec: PackageRef or MatchSpec or str
      :param pkgs_dirs: If None, will fall back to context.pkgs_dirs.
      :type pkgs_dirs: Iterable[str] or None

      :returns: tuple[PackageCacheRecord]


   .. py:method:: iter_records()

      **Beta** While in beta, expect both major and minor changes across minor releases.

      :returns:

                A generator over all records contained in the package
                    cache instance.  Warning: this is a generator that is exhausted on first use.
      :rtype: Iterable[PackageCacheRecord]


   .. py:method:: first_writable(pkgs_dirs=None)
      :staticmethod:

      **Beta** While in beta, expect both major and minor changes across minor releases.

      Get an instance object for the first writable package cache.

      :param pkgs_dirs: If None, will fall back to context.pkgs_dirs.
      :type pkgs_dirs: Iterable[str]

      :returns:     An instance for the first writable package cache.
      :rtype: PackageCacheData


   .. py:method:: reload()

      **Beta** While in beta, expect both major and minor changes across minor releases.

      Update the instance with new information. Backing information (i.e. contents of
      the pkgs_dir) is lazily loaded on first use by the other methods of this class. You
      should only use this method if you are *sure* you have outdated data.

      :returns: PackageCacheData



.. py:class:: PrefixData(prefix_path)


   **Beta** While in beta, expect both major and minor changes across minor releases.

   High-level management and usage of conda environment prefixes.

   **Beta** While in beta, expect both major and minor changes across minor releases.

   :param prefix_path:
   :type prefix_path: str

   .. py:property:: is_writable

      **Beta** While in beta, expect both major and minor changes across minor releases.

      Indicates if the prefix is writable or read-only.

      :returns:     True if the prefix is writable.  False if read-only.  None if the prefix
                    does not exist as a conda environment.
      :rtype: bool or None

   .. py:method:: get(package_ref, default=NULL)

      **Beta** While in beta, expect both major and minor changes across minor releases.

      :param package_ref: A :obj:`PackageRef` instance representing the key for the
                          :obj:`PrefixRecord` being sought.
      :type package_ref: PackageRef
      :param default: The default value to return if the record does not exist. If not
                      specified and no record exists, :exc:`KeyError` is raised.

      :returns: PrefixRecord


   .. py:method:: query(package_ref_or_match_spec)

      **Beta** While in beta, expect both major and minor changes across minor releases.

      Run a query against this specific prefix instance.

      :param package_ref_or_match_spec: Either an exact :obj:`PackageRef` to match against, or a :obj:`MatchSpec`
                                        query object.  A :obj:`str` will be turned into a :obj:`MatchSpec` automatically.
      :type package_ref_or_match_spec: PackageRef or MatchSpec or str

      :returns: tuple[PrefixRecord]


   .. py:method:: iter_records()

      **Beta** While in beta, expect both major and minor changes across minor releases.

      :returns:

                A generator over all records contained in the prefix.
                    Warning: this is a generator that is exhausted on first use.
      :rtype: Iterable[PrefixRecord]


   .. py:method:: reload()

      **Beta** While in beta, expect both major and minor changes across minor releases.

      Update the instance with new information. Backing information (i.e. contents of
      the conda-meta directory) is lazily loaded on first use by the other methods of this
      class. You should only use this method if you are *sure* you have outdated data.

      :returns: PrefixData



