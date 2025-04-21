:py:mod:`resolve`
=================

.. py:module:: conda.resolve

.. autoapi-nested-parse::

   Low-level SAT solver wrapper/interface for the classic solver.

   See conda.core.solver.Solver for the high-level API.



Classes
-------

.. autoapisummary::

   conda.resolve.Resolve



Functions
---------

.. autoapisummary::

   conda.resolve._get_sat_solver_cls
   conda.resolve.exactness_and_number_of_deps



Attributes
----------

.. autoapisummary::

   conda.resolve.stdoutlog
   conda.resolve.Unsatisfiable
   conda.resolve.ResolvePackageNotFound
   conda.resolve._sat_solvers


.. py:data:: stdoutlog

   

.. py:data:: Unsatisfiable

   

.. py:data:: ResolvePackageNotFound

   

.. py:data:: _sat_solvers

   

.. py:function:: _get_sat_solver_cls(sat_solver_choice=SatSolverChoice.PYCOSAT)


.. py:function:: exactness_and_number_of_deps(resolve_obj, ms)

   Sorting key to emphasize packages that have more strict
   requirements. More strict means the reduced index can be reduced
   more, so we want to consider these more constrained deps earlier in
   reducing the index.


.. py:class:: Resolve(index, processed=False, channels=())


   .. py:method:: __hash__()

      Return hash(self).


   .. py:method:: default_filter(features=None, filter=None)


   .. py:method:: valid(spec_or_prec, filter, optional=True)

      Tests if a package, MatchSpec, or a list of both has satisfiable
      dependencies, assuming cyclic dependencies are always valid.

      :param spec_or_prec: a package record, a MatchSpec, or an iterable of these.
      :param filter: a dictionary of (fkey,valid) pairs, used to consider a subset
                     of dependencies, and to eliminate repeated searches.
      :param optional: if True (default), do not enforce optional specifications
                       when considering validity. If False, enforce them.

      :returns: True if the full set of dependencies can be satisfied; False otherwise.
                If filter is supplied and update is True, it will be updated with the
                search results.


   .. py:method:: valid2(spec_or_prec, filter_out, optional=True)


   .. py:method:: invalid_chains(spec, filter, optional=True)

      Constructs a set of 'dependency chains' for invalid specs.

      A dependency chain is a tuple of MatchSpec objects, starting with
      the requested spec, proceeding down the dependency tree, ending at
      a specification that cannot be satisfied.

      :param spec: a package key or MatchSpec
      :param filter: a dictionary of (prec, valid) pairs to be used when
                     testing for package validity.

      :returns: A tuple of tuples, empty if the MatchSpec is valid.


   .. py:method:: verify_specs(specs)

      Perform a quick verification that specs and dependencies are reasonable.

      :param specs: An iterable of strings or MatchSpec objects to be tested.

      :returns: Nothing, but if there is a conflict, an error is thrown.

      Note that this does not attempt to resolve circular dependencies.


   .. py:method:: _classify_bad_deps(bad_deps, specs_to_add, history_specs, strict_channel_priority)


   .. py:method:: find_matches_with_strict(ms, strict_channel_priority)


   .. py:method:: find_conflicts(specs, specs_to_add=None, history_specs=None)


   .. py:method:: breadth_first_search_for_dep_graph(root_spec, target_name, dep_graph, num_targets=1)

      Return shorted path from root_spec to target_name


   .. py:method:: build_graph_of_deps(spec)


   .. py:method:: build_conflict_map(specs, specs_to_add=None, history_specs=None)

      Perform a deeper analysis on conflicting specifications, by attempting
      to find the common dependencies that might be the cause of conflicts.

      :param specs: An iterable of strings or MatchSpec objects to be tested.
      :param It is assumed that the specs conflict.:

      :returns: A list of lists of bad deps
      :rtype: bad_deps

      Strategy:
          If we're here, we know that the specs conflict. This could be because:
          - One spec conflicts with another; e.g.
                ['numpy 1.5*', 'numpy >=1.6']
          - One spec conflicts with a dependency of another; e.g.
                ['numpy 1.5*', 'scipy 0.12.0b1']
          - Each spec depends on *the same package* but in a different way; e.g.,
                ['A', 'B'] where A depends on numpy 1.5, and B on numpy 1.6.
          Technically, all three of these cases can be boiled down to the last
          one if we treat the spec itself as one of the "dependencies". There
          might be more complex reasons for a conflict, but this code only
          considers the ones above.

          The purpose of this code, then, is to identify packages (like numpy
          above) that all of the specs depend on *but in different ways*. We
          then identify the dependency chains that lead to those packages.


   .. py:method:: _get_strict_channel(package_name)


   .. py:method:: _broader(ms, specs_by_name)

      Prevent introduction of matchspecs that broaden our selection of choices.


   .. py:method:: _get_package_pool(specs)


   .. py:method:: get_reduced_index(explicit_specs, sort_by_exactness=True, exit_on_conflict=False)


   .. py:method:: match_any(mss, prec)


   .. py:method:: find_matches(spec: conda.models.match_spec.MatchSpec) -> tuple[conda.models.records.PackageRecord]


   .. py:method:: ms_depends(prec: conda.models.records.PackageRecord) -> list[conda.models.match_spec.MatchSpec]


   .. py:method:: version_key(prec, vtype=None)


   .. py:method:: _make_channel_priorities(channels)
      :staticmethod:


   .. py:method:: get_pkgs(ms, emptyok=False)


   .. py:method:: to_sat_name(val)
      :staticmethod:


   .. py:method:: to_feature_metric_id(prec_dist_str, feat)
      :staticmethod:


   .. py:method:: push_MatchSpec(C, spec)


   .. py:method:: gen_clauses()


   .. py:method:: generate_spec_constraints(C, specs)


   .. py:method:: generate_feature_count(C)


   .. py:method:: generate_update_count(C, specs)


   .. py:method:: generate_feature_metric(C)


   .. py:method:: generate_removal_count(C, specs)


   .. py:method:: generate_install_count(C, specs)


   .. py:method:: generate_package_count(C, missing)


   .. py:method:: generate_version_metrics(C, specs, include0=False)


   .. py:method:: dependency_sort(must_have: dict[str, conda.models.records.PackageRecord]) -> list[conda.models.records.PackageRecord]


   .. py:method:: environment_is_consistent(installed)


   .. py:method:: get_conflicting_specs(specs, explicit_specs)


   .. py:method:: bad_installed(installed, new_specs)


   .. py:method:: restore_bad(pkgs, preserve)


   .. py:method:: install_specs(specs, installed, update_deps=True)


   .. py:method:: install(specs, installed=None, update_deps=True, returnall=False)


   .. py:method:: remove_specs(specs, installed)


   .. py:method:: remove(specs, installed)


   .. py:method:: solve(specs: list, returnall: bool = False, _remove=False, specs_to_add=None, history_specs=None, should_retry_solve=False) -> list[conda.models.records.PackageRecord]



