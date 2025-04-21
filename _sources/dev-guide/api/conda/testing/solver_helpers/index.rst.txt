:py:mod:`solver_helpers`
========================

.. py:module:: conda.testing.solver_helpers

.. autoapi-nested-parse::

   Helpers for testing the solver.



Classes
-------

.. autoapisummary::

   conda.testing.solver_helpers.SimpleEnvironment
   conda.testing.solver_helpers.SolverTests



Functions
---------

.. autoapisummary::

   conda.testing.solver_helpers.index_packages
   conda.testing.solver_helpers.package_string
   conda.testing.solver_helpers.package_string_set
   conda.testing.solver_helpers.package_dict
   conda.testing.solver_helpers.empty_prefix
   conda.testing.solver_helpers.temp_simple_env



.. py:function:: index_packages(num)

   Get the index data of the ``helpers.get_index_r_*`` helpers.


.. py:function:: package_string(record)


.. py:function:: package_string_set(packages)

   Transforms package container in package string set.


.. py:function:: package_dict(packages)

   Transforms package container into a dictionary.


.. py:class:: SimpleEnvironment(path, solver_class, subdirs=context.subdirs)


   Helper environment object.

   .. py:property:: _channel_packages

      Helper that unfolds the ``repo_packages`` into a dictionary.

   .. py:attribute:: REPO_DATA_KEYS
      :value: ('build', 'build_number', 'depends', 'license', 'md5', 'name', 'sha256', 'size', 'subdir',...

      

   .. py:method:: solver(add, remove)

      Writes ``repo_packages`` to the disk and creates a solver instance.


   .. py:method:: solver_transaction(add=(), remove=(), as_specs=False)


   .. py:method:: install(*specs, as_specs=False)


   .. py:method:: remove(*specs, as_specs=False)


   .. py:method:: _package_data(record)

      Turn record into data, to be written in the JSON environment/repo files.


   .. py:method:: _write_installed_packages()


   .. py:method:: _write_repo_packages(channel_name, packages)

      Write packages to the channel path.



.. py:function:: empty_prefix()


.. py:function:: temp_simple_env(solver_class=Solver) -> SimpleEnvironment


.. py:class:: SolverTests


   Tests for :py:class:`conda.core.solve.Solver` implementations.

   .. py:property:: solver_class
      :type: type[conda.core.solve.Solver]
      :abstractmethod:

      Class under test.

   .. py:property:: tests_to_skip


   .. py:method:: skip_tests(request)


   .. py:method:: env()


   .. py:method:: find_package_in_list(packages, **kwargs)


   .. py:method:: find_package(**kwargs)


   .. py:method:: assert_unsatisfiable(exc_info, entries)

      Helper to assert that a :py:class:`conda.exceptions.UnsatisfiableError`
      instance as a the specified set of unsatisfiable specifications.


   .. py:method:: test_empty(env)


   .. py:method:: test_iopro_mkl(env)


   .. py:method:: test_iopro_nomkl(env)


   .. py:method:: test_mkl(env)


   .. py:method:: test_accelerate(env)


   .. py:method:: test_scipy_mkl(env)


   .. py:method:: test_anaconda_nomkl(env)


   .. py:method:: test_pseudo_boolean(env)


   .. py:method:: test_unsat_from_r1(env)


   .. py:method:: test_unsat_simple(env)


   .. py:method:: test_get_dists(env)


   .. py:method:: test_unsat_shortest_chain_1(env)


   .. py:method:: test_unsat_shortest_chain_2(env)


   .. py:method:: test_unsat_shortest_chain_3(env)


   .. py:method:: test_unsat_shortest_chain_4(env)


   .. py:method:: test_unsat_chain(env)


   .. py:method:: test_unsat_any_two_not_three(env)


   .. py:method:: test_unsat_expand_single(env)


   .. py:method:: test_unsat_missing_dep(env)


   .. py:method:: test_nonexistent(env)


   .. py:method:: test_timestamps_and_deps(env)


   .. py:method:: test_nonexistent_deps(env)


   .. py:method:: test_install_package_with_feature(env)


   .. py:method:: test_unintentional_feature_downgrade(env)


   .. py:method:: test_circular_dependencies(env)


   .. py:method:: test_irrational_version(env)


   .. py:method:: test_no_features(env)


   .. py:method:: test_channel_priority_1(monkeypatch, env)


   .. py:method:: test_unsat_channel_priority(monkeypatch, env)


   .. py:method:: test_remove(env)


   .. py:method:: test_surplus_features_1(env)


   .. py:method:: test_surplus_features_2(env)


   .. py:method:: test_get_reduced_index_broadening_with_unsatisfiable_early_dep(env)


   .. py:method:: test_get_reduced_index_broadening_preferred_solution(env)


   .. py:method:: test_arch_preferred_over_noarch_when_otherwise_equal(env)


   .. py:method:: test_noarch_preferred_over_arch_when_version_greater(env)


   .. py:method:: test_noarch_preferred_over_arch_when_version_greater_dep(env)


   .. py:method:: test_noarch_preferred_over_arch_when_build_greater(env)


   .. py:method:: test_noarch_preferred_over_arch_when_build_greater_dep(env)



