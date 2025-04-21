:py:mod:`solve`
===============

.. py:module:: conda.core.solve

.. autoapi-nested-parse::

   The classic solver implementation.



Classes
-------

.. autoapisummary::

   conda.core.solve.Solver
   conda.core.solve.SolverStateContainer



Functions
---------

.. autoapisummary::

   conda.core.solve.get_pinned_specs
   conda.core.solve.diff_for_unlink_link_precs



.. py:class:: Solver(prefix: str, channels: collections.abc.Iterable[conda.models.channel.Channel], subdirs: collections.abc.Iterable[str] = (), specs_to_add: collections.abc.Iterable[conda.models.match_spec.MatchSpec] = (), specs_to_remove: collections.abc.Iterable[conda.models.match_spec.MatchSpec] = (), repodata_fn: str = REPODATA_FN, command=NULL)


   A high-level API to conda's solving logic. Three public methods are provided to access a
   solution in various forms.

     * :meth:`solve_final_state`
     * :meth:`solve_for_diff`
     * :meth:`solve_for_transaction`

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

   .. py:method:: solve_for_transaction(update_modifier=NULL, deps_modifier=NULL, prune=NULL, ignore_pinned=NULL, force_remove=NULL, force_reinstall=NULL, should_retry_solve=False)

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
      :param should_retry_solve: See :meth:`solve_final_state`.
      :type should_retry_solve: bool

      :rtype: UnlinkLinkTransaction


   .. py:method:: solve_for_diff(update_modifier=NULL, deps_modifier=NULL, prune=NULL, ignore_pinned=NULL, force_remove=NULL, force_reinstall=NULL, should_retry_solve=False) -> tuple[tuple[conda.models.records.PackageRecord, Ellipsis], tuple[conda.models.records.PackageRecord, Ellipsis]]

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
      :param force_reinstall:
                              For requested specs_to_add that are already satisfied in the environment,
                                  instructs the solver to remove the package and spec from the environment,
                                  and then add it back--possibly with the exact package instance modified,
                                  depending on the spec exactness.
      :type force_reinstall: bool
      :param should_retry_solve: See :meth:`solve_final_state`.
      :type should_retry_solve: bool

      :returns:     A two-tuple of PackageRef sequences.  The first is the group of packages to
                    remove from the environment, in sorted dependency order from leaves to roots.
                    The second is the group of packages to add to the environment, in sorted
                    dependency order from roots to leaves.
      :rtype: tuple[PackageRef], tuple[PackageRef]


   .. py:method:: solve_final_state(update_modifier=NULL, deps_modifier=NULL, prune=NULL, ignore_pinned=NULL, force_remove=NULL, should_retry_solve=False)

      Gives the final, solved state of the environment.

      :param update_modifier: An optional flag directing how updates are handled regarding packages already
                              existing in the environment.
      :type update_modifier: UpdateModifier
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
      :param should_retry_solve: Indicates whether this solve will be retried. This allows us to control
                                 whether to call find_conflicts (slow) in ssc.r.solve
      :type should_retry_solve: bool

      :returns:     In sorted dependency order from roots to leaves, the package references for
                    the solved state of the environment.
      :rtype: tuple[PackageRef]


   .. py:method:: determine_constricting_specs(spec, solution_precs)


   .. py:method:: get_request_package_in_solution(solution_precs, specs_map)


   .. py:method:: get_constrained_packages(pre_packages, post_packages, index_keys)


   .. py:method:: _collect_all_metadata(ssc)


   .. py:method:: _remove_specs(ssc)


   .. py:method:: _find_inconsistent_packages(ssc)


   .. py:method:: _package_has_updates(ssc, spec, installed_pool)


   .. py:method:: _should_freeze(ssc, target_prec, conflict_specs, explicit_pool, installed_pool)


   .. py:method:: _add_specs(ssc)


   .. py:method:: _run_sat(ssc)


   .. py:method:: _post_sat_handling(ssc)


   .. py:method:: _notify_conda_outdated(link_precs)


   .. py:method:: _prepare(prepared_specs)



.. py:class:: SolverStateContainer(prefix, update_modifier, deps_modifier, prune, ignore_pinned, force_remove, should_retry_solve)


   .. py:method:: prefix_data()


   .. py:method:: specs_from_history_map()


   .. py:method:: track_features_specs()


   .. py:method:: pinned_specs()


   .. py:method:: set_repository_metadata(index, r)


   .. py:method:: _init_solution_precs()


   .. py:method:: working_state_reset()



.. py:function:: get_pinned_specs(prefix)

   Find pinned specs from file and return a tuple of MatchSpec.


.. py:function:: diff_for_unlink_link_precs(prefix, final_precs, specs_to_add=(), force_reinstall=NULL) -> tuple[tuple[conda.models.records.PackageRecord, Ellipsis], tuple[conda.models.records.PackageRecord, Ellipsis]]


