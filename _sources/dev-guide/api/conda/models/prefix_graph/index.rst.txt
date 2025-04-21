:py:mod:`prefix_graph`
======================

.. py:module:: conda.models.prefix_graph

.. autoapi-nested-parse::

   Implements directed graphs to sort and manipulate packages within a prefix.

   Object inheritance:

   .. autoapi-inheritance-diagram:: PrefixGraph GeneralGraph
      :top-classes: conda.models.prefix_graph.PrefixGraph
      :parts: 1



Classes
-------

.. autoapisummary::

   conda.models.prefix_graph.PrefixGraph
   conda.models.prefix_graph.GeneralGraph




.. py:class:: PrefixGraph(records, specs=())


   A directed graph structure used for sorting packages (prefix_records) in prefixes and
   manipulating packages within prefixes (e.g. removing and pruning).

   The terminology used for edge direction is "parents" and "children" rather than "successors"
   and "predecessors". The parent nodes of a record are those records in the graph that
   match the record's "depends" field.  E.g. NodeA depends on NodeB, then NodeA is a child
   of NodeB, and NodeB is a parent of NodeA.  Nodes can have zero parents, or more than two
   parents.

   Most public methods mutate the graph.

   .. py:property:: records


   .. py:method:: remove_spec(spec)

      Remove all matching nodes, and any associated child nodes.

      :param spec:
      :type spec: MatchSpec

      :returns: The removed nodes.
      :rtype: tuple[PrefixRecord]


   .. py:method:: remove_youngest_descendant_nodes_with_specs()

      A specialized method used to determine only dependencies of requested specs.

      :returns: The removed nodes.
      :rtype: tuple[PrefixRecord]


   .. py:method:: prune()

      Prune back all packages until all child nodes are anchored by a spec.

      :returns: The pruned nodes.
      :rtype: tuple[PrefixRecord]


   .. py:method:: get_node_by_name(name)


   .. py:method:: all_descendants(node)


   .. py:method:: all_ancestors(node)


   .. py:method:: _remove_node(node)

      Removes this node and all edges referencing it.


   .. py:method:: _toposort()


   .. py:method:: _toposort_raise_on_cycles(graph)
      :classmethod:


   .. py:method:: _topo_sort_handle_cycles(graph)
      :classmethod:


   .. py:method:: _toposort_pop_key(graph)
      :staticmethod:

      Pop an item from the graph that has the fewest parents.
      In the case of a tie, use the node with the alphabetically-first package name.


   .. py:method:: _toposort_prepare_graph(graph)
      :staticmethod:



.. py:class:: GeneralGraph(records, specs=())


   Bases: :py:obj:`PrefixGraph`

   Compared with PrefixGraph, this class takes in more than one record of a given name,
   and operates on that graph from the higher view across any matching dependencies.  It is
   not a Prefix thing, but more like a "graph of all possible candidates" thing, and is used
   for unsatisfiability analysis

   .. py:method:: breadth_first_search_by_name(root_spec, target_spec)

      Return shorted path from root_spec to spec_name



