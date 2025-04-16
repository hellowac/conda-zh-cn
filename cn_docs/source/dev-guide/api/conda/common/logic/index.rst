:py:mod:`logic`
===============

.. py:module:: conda.common.logic

.. autoapi-nested-parse::

   The basic idea to nest logical expressions is instead of trying to denest
   things via distribution, we add new variables. So if we have some logical
   expression expr, we replace it with x and add expr <-> x to the clauses,
   where x is a new variable, and expr <-> x is recursively evaluated in the
   same way, so that the final clauses are ORs of atoms.

   To use this, create a new Clauses object with the max var, for instance, if you
   already have [[1, 2, -3]], you would use C = Clause(3).  All functions return
   a new literal, which represents that function, or True or False if the expression
   can be resolved fully. They may also add new clauses to C.clauses, which
   will then be delivered to the SAT solver.

   All functions take atoms as arguments (an atom is an integer, representing a
   literal or a negated literal, or boolean constants True or False; that is,
   it is the callers' responsibility to do the conversion of expressions
   recursively. This is done because we do not have data structures
   representing the various logical classes, only atoms.

   The polarity argument can be set to True or False if you know that the literal
   being used will only be used in the positive or the negative, respectively
   (e.g., you will only use x, not -x).  This will generate fewer clauses. It
   is probably best if you do not take advantage of this directly, but rather
   through the Require and Prevent functions.



Classes
-------

.. autoapisummary::

   conda.common.logic.Clauses



Functions
---------

.. autoapisummary::

   conda.common.logic.minimal_unsatisfiable_subset



Attributes
----------

.. autoapisummary::

   conda.common.logic.TRUE
   conda.common.logic.FALSE
   conda.common.logic.PycoSatSolver
   conda.common.logic.PyCryptoSatSolver
   conda.common.logic.PySatSolver


.. py:data:: TRUE

   

.. py:data:: FALSE

   

.. py:data:: PycoSatSolver
   :value: 'pycosat'

   

.. py:data:: PyCryptoSatSolver
   :value: 'pycryptosat'

   

.. py:data:: PySatSolver
   :value: 'pysat'

   

.. py:class:: Clauses(m=0, sat_solver=PycoSatSolver)


   .. py:property:: m


   .. py:property:: unsat


   .. py:method:: get_clause_count()


   .. py:method:: as_list()


   .. py:method:: _check_variable(variable)


   .. py:method:: _check_literal(literal)


   .. py:method:: add_clause(clause)


   .. py:method:: add_clauses(clauses)


   .. py:method:: name_var(m, name)


   .. py:method:: new_var(name=None)


   .. py:method:: from_name(name)


   .. py:method:: from_index(m)


   .. py:method:: _assign(vals, name=None)


   .. py:method:: _convert(x)


   .. py:method:: _eval(func, args, no_literal_args, polarity, name)


   .. py:method:: Prevent(what, *args)


   .. py:method:: Require(what, *args)


   .. py:method:: Not(x, polarity=None, name=None)


   .. py:method:: And(f, g, polarity=None, name=None)


   .. py:method:: Or(f, g, polarity=None, name=None)


   .. py:method:: Xor(f, g, polarity=None, name=None)


   .. py:method:: ITE(c, t, f, polarity=None, name=None)

      If c Then t Else f.

      In this function, if any of c, t, or f are True and False the resulting
      expression is resolved.


   .. py:method:: All(iter, polarity=None, name=None)


   .. py:method:: Any(vals, polarity=None, name=None)


   .. py:method:: AtMostOne_NSQ(vals, polarity=None, name=None)


   .. py:method:: AtMostOne_BDD(vals, polarity=None, name=None)


   .. py:method:: AtMostOne(vals, polarity=None, name=None)


   .. py:method:: ExactlyOne_NSQ(vals, polarity=None, name=None)


   .. py:method:: ExactlyOne_BDD(vals, polarity=None, name=None)


   .. py:method:: ExactlyOne(vals, polarity=None, name=None)


   .. py:method:: LinearBound(equation, lo, hi, preprocess=True, polarity=None, name=None)


   .. py:method:: sat(additional=None, includeIf=False, names=False, limit=0)

      Calculate a SAT solution for the current clause set.

      Returned is the list of those solutions.  When the clauses are
      unsatisfiable, an empty list is returned.



   .. py:method:: itersolve(constraints=None, m=None)


   .. py:method:: minimize(objective, bestsol=None, trymax=False)



.. py:function:: minimal_unsatisfiable_subset(clauses, sat, explicit_specs)

   Given a set of clauses, find a minimal unsatisfiable subset (an
   unsatisfiable core)

   A set is a minimal unsatisfiable subset if no proper subset is
   unsatisfiable.  A set of clauses may have many minimal unsatisfiable
   subsets of different sizes.

   sat should be a function that takes a tuple of clauses and returns True if
   the clauses are satisfiable and False if they are not.  The algorithm will
   work with any order-reversing function (reversing the order of subset and
   the order False < True), that is, any function where (A <= B) iff (sat(B)
   <= sat(A)), where A <= B means A is a subset of B and False < True).



