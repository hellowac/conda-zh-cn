:py:mod:`actions`
=================

.. py:module:: conda.cli.actions

.. autoapi-nested-parse::

   Collection of custom argparse actions.



Classes
-------

.. autoapisummary::

   conda.cli.actions.NullCountAction
   conda.cli.actions.ExtendConstAction




.. py:class:: NullCountAction(option_strings, dest, default=None, required=False, help=None)


   Bases: :py:obj:`argparse._CountAction`

   Information about how to convert command line strings to Python objects.

   Action objects are used by an ArgumentParser to represent the information
   needed to parse a single argument from one or more strings from the
   command line. The keyword arguments to the Action constructor are also
   all attributes of Action instances.

   :keyword - option_strings -- A list of command-line option strings which: should be associated with this action.
   :keyword - dest -- The name of the attribute to hold the created object:
   :kwtype - dest -- The name of the attribute to hold the created object: s
   :keyword - nargs -- The number of command-line arguments that should be: consumed. By default, one argument will be consumed and a single
                                                                            value will be produced.  Other values include:
                                                                                - N (an integer) consumes N arguments (and produces a list)
                                                                                - '?' consumes zero or one arguments
                                                                                - '*' consumes zero or more arguments (and produces a list)
                                                                                - '+' consumes one or more arguments (and produces a list)
                                                                            Note that the difference between the default and nargs=1 is that
                                                                            with the default, a single value will be produced, while with
                                                                            nargs=1, a list containing a single value will be produced.
   :keyword - const -- The value to be produced if the option is specified and the: option uses an action that takes no values.
   :keyword - default -- The value to be produced if the option is not specified.:
   :keyword - type -- A callable that accepts a single string argument, and: returns the converted value.  The standard Python types str, int,
                                                                             float, and complex are useful examples of such callables.  If None,
                                                                             str is used.
   :keyword - choices -- A container of values that should be allowed. If not None,: after a command-line argument has been converted to the appropriate
                                                                                     type, an exception will be raised if it is not a member of this
                                                                                     collection.
   :keyword - required -- True if the action must always be specified at the: command line. This is only meaningful for optional command-line
                                                                              arguments.
   :keyword - help -- The help string describing the argument.:
   :keyword - metavar -- The name to be used for the option's argument with the: help string. If None, the 'dest' value will be used as the name.

   .. py:method:: _ensure_value(namespace, name, value)
      :staticmethod:


   .. py:method:: __call__(parser, namespace, values, option_string=None)



.. py:class:: ExtendConstAction(option_strings, dest, const, default=None, type=None, choices=None, required=False, help=None, metavar=None)


   Bases: :py:obj:`argparse.Action`

   A derivative of _AppendConstAction and Python 3.8's _ExtendAction

   .. py:method:: __call__(parser, namespace, values, option_string=None)



