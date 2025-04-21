:py:mod:`history`
=================

.. py:module:: conda.history

.. autoapi-nested-parse::

   Tools interfacing with conda's history file.



Classes
-------

.. autoapisummary::

   conda.history.History



Functions
---------

.. autoapisummary::

   conda.history.write_head
   conda.history.is_diff
   conda.history.pretty_diff
   conda.history.pretty_content



Attributes
----------

.. autoapisummary::

   conda.history.h


.. py:exception:: CondaHistoryWarning


   Bases: :py:obj:`Warning`

   Base class for warning categories.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:function:: write_head(fo)


.. py:function:: is_diff(content)


.. py:function:: pretty_diff(diff)


.. py:function:: pretty_content(content)


.. py:class:: History(prefix)


   .. py:attribute:: com_pat

      

   .. py:attribute:: spec_pat

      

   .. py:attribute:: conda_v_pat

      

   .. py:method:: __enter__()


   .. py:method:: __exit__(exc_type, exc_value, traceback)


   .. py:method:: init_log_file()


   .. py:method:: file_is_empty()


   .. py:method:: update() -> None

      Update the history file (creating a new one if necessary).


   .. py:method:: parse() -> list[tuple[str, set[str], list[str]]]

      Parse the history file.

      Return a list of tuples(datetime strings, set of distributions/diffs, comments).

      Comments appearing before the first section header (e.g. ``==> 2024-01-01 00:00:00 <==``)
      in the history file will be ignored.


   .. py:method:: _parse_old_format_specs_string(specs_string)
      :staticmethod:

      Parse specifications string that use conda<4.5 syntax.

      .. rubric:: 示例

      - "param >=1.5.1,<2.0'"
      - "python>=3.5.1,jupyter >=1.0.0,<2.0,matplotlib >=1.5.1,<2.0"


   .. py:method:: _parse_comment_line(line)
      :classmethod:

      Parse comment lines in the history file.

      These lines can be of command type or action type.

      .. rubric:: 示例

      - "# cmd: /scratch/mc3/bin/conda install -c conda-forge param>=1.5.1,<2.0"
      - "# install specs: python>=3.5.1,jupyter >=1.0.0,<2.0,matplotlib >=1.5.1,<2.0"


   .. py:method:: get_user_requests()

      Return a list of user requested items.

      Each item is a dict with the following keys:
      'date': the date and time running the command
      'cmd': a list of argv of the actual command which was run
      'action': install/remove/update
      'specs': the specs being used


   .. py:method:: get_requested_specs_map()


   .. py:method:: construct_states()

      Return a list of tuples(datetime strings, set of distributions).


   .. py:method:: get_state(rev=-1)

      Return the state, i.e. the set of distributions, for a given revision.

      Defaults to latest (which is the same as the current state when
      the log file is up-to-date).

      Returns a list of dist_strs.


   .. py:method:: print_log()


   .. py:method:: object_log()


   .. py:method:: write_changes(last_state, current_state)


   .. py:method:: write_specs(remove_specs=(), update_specs=(), neutered_specs=())



.. py:data:: h

   

