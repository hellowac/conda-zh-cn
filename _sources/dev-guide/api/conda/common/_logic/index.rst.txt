:py:mod:`_logic`
================

.. py:module:: conda.common._logic


Classes
-------

.. autoapisummary::

   conda.common._logic._ClauseList
   conda.common._logic._ClauseArray
   conda.common._logic._SatSolver
   conda.common._logic._PycoSatSolver
   conda.common._logic._PyCryptoSatSolver
   conda.common._logic._PySatSolver
   conda.common._logic.Clauses




Attributes
----------

.. autoapisummary::

   conda.common._logic.TRUE
   conda.common._logic.FALSE
   conda.common._logic._sat_solver_str_to_cls
   conda.common._logic._sat_solver_cls_to_str


.. py:data:: TRUE

   

.. py:data:: FALSE

   

.. py:class:: _ClauseList


   Storage for the CNF clauses, represented as a list of tuples of ints.

   .. py:method:: get_clause_count()

      Return number of stored clauses.


   .. py:method:: save_state()

      Get state information to be able to revert temporary additions of
      supplementary clauses.  _ClauseList: state is simply the number of clauses.


   .. py:method:: restore_state(saved_state)

      Restore state saved via `save_state`.
      Removes clauses that were added after the state has been saved.


   .. py:method:: as_list()

      Return clauses as a list of tuples of ints.


   .. py:method:: as_array()

      Return clauses as a flat int array, each clause being terminated by 0.



.. py:class:: _ClauseArray


   Storage for the CNF clauses, represented as a flat int array.
   Each clause is terminated by int(0).

   .. py:method:: extend(clauses)


   .. py:method:: append(clause)


   .. py:method:: get_clause_count()

      Return number of stored clauses.
      This is an O(n) operation since we don't store the number of clauses
      explicitly due to performance reasons (Python interpreter overhead in
      self.append).


   .. py:method:: save_state()

      Get state information to be able to revert temporary additions of
      supplementary clauses. _ClauseArray: state is the length of the int
      array, NOT number of clauses.


   .. py:method:: restore_state(saved_state)

      Restore state saved via `save_state`.
      Removes clauses that were added after the state has been saved.


   .. py:method:: as_list()

      Return clauses as a list of tuples of ints.


   .. py:method:: as_array()

      Return clauses as a flat int array, each clause being terminated by 0.



.. py:class:: _SatSolver(**run_kwargs)


   Simple wrapper to call a SAT solver given a _ClauseList/_ClauseArray instance.

   .. py:method:: get_clause_count()


   .. py:method:: as_list()


   .. py:method:: save_state()


   .. py:method:: restore_state(saved_state)


   .. py:method:: run(m, **kwargs)


   .. py:method:: setup(m, **kwargs)
      :abstractmethod:

      Create a solver instance, add the clauses to it, and return it.


   .. py:method:: invoke(solver)
      :abstractmethod:

      Start the actual SAT solving and return the calculated solution.


   .. py:method:: process_solution(sat_solution)
      :abstractmethod:

      Process the solution returned by self.invoke.
      Returns a list of satisfied variables or None if no solution is found.



.. py:class:: _PycoSatSolver(**run_kwargs)


   Bases: :py:obj:`_SatSolver`

   Simple wrapper to call a SAT solver given a _ClauseList/_ClauseArray instance.

   .. py:method:: setup(m, limit=0, **kwargs)

      Create a solver instance, add the clauses to it, and return it.


   .. py:method:: invoke(iter_sol)

      Start the actual SAT solving and return the calculated solution.


   .. py:method:: process_solution(sat_solution)

      Process the solution returned by self.invoke.
      Returns a list of satisfied variables or None if no solution is found.



.. py:class:: _PyCryptoSatSolver(**run_kwargs)


   Bases: :py:obj:`_SatSolver`

   Simple wrapper to call a SAT solver given a _ClauseList/_ClauseArray instance.

   .. py:method:: setup(m, threads=1, **kwargs)

      Create a solver instance, add the clauses to it, and return it.


   .. py:method:: invoke(solver)

      Start the actual SAT solving and return the calculated solution.


   .. py:method:: process_solution(solution)

      Process the solution returned by self.invoke.
      Returns a list of satisfied variables or None if no solution is found.



.. py:class:: _PySatSolver(**run_kwargs)


   Bases: :py:obj:`_SatSolver`

   Simple wrapper to call a SAT solver given a _ClauseList/_ClauseArray instance.

   .. py:method:: setup(m, **kwargs)

      Create a solver instance, add the clauses to it, and return it.


   .. py:method:: invoke(solver)

      Start the actual SAT solving and return the calculated solution.


   .. py:method:: process_solution(sat_solution)

      Process the solution returned by self.invoke.
      Returns a list of satisfied variables or None if no solution is found.



.. py:data:: _sat_solver_str_to_cls

   

.. py:data:: _sat_solver_cls_to_str

   

.. py:class:: Clauses(m=0, sat_solver_str=_sat_solver_cls_to_str[_PycoSatSolver])


   .. py:method:: get_clause_count()


   .. py:method:: as_list()


   .. py:method:: new_var()


   .. py:method:: assign(vals)


   .. py:method:: Combine(args, polarity)


   .. py:method:: Eval(func, args, polarity)


   .. py:method:: Prevent(func, *args)


   .. py:method:: Require(func, *args)


   .. py:method:: Not(x, polarity=None, add_new_clauses=False)


   .. py:method:: And(f, g, polarity, add_new_clauses=False)


   .. py:method:: Or(f, g, polarity, add_new_clauses=False)


   .. py:method:: Xor(f, g, polarity, add_new_clauses=False)


   .. py:method:: ITE(c, t, f, polarity, add_new_clauses=False)


   .. py:method:: All(iter, polarity=None)


   .. py:method:: Any(iter, polarity)


   .. py:method:: AtMostOne_NSQ(vals, polarity)


   .. py:method:: AtMostOne_BDD(vals, polarity=None)


   .. py:method:: ExactlyOne_NSQ(vals, polarity)


   .. py:method:: ExactlyOne_BDD(vals, polarity)


   .. py:method:: LB_Preprocess(lits, coeffs)


   .. py:method:: BDD(lits, coeffs, nterms, lo, hi, polarity)


   .. py:method:: LinearBound(lits, coeffs, lo, hi, preprocess, polarity)


   .. py:method:: _run_sat(m, limit=0)


   .. py:method:: sat(additional=None, includeIf=False, limit=0)

      Calculate a SAT solution for the current clause set.

      Returned is the list of those solutions.  When the clauses are
      unsatisfiable, an empty list is returned.



   .. py:method:: minimize(lits, coeffs, bestsol=None, trymax=False)

      Minimize the objective function given by (coeff, integer) pairs in
      zip(coeffs, lits).
      The actual minimization is multiobjective: first, we minimize the
      largest active coefficient value, then we minimize the sum.



