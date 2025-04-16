:py:mod:`conda_argparse`
========================

.. py:module:: conda.cli.conda_argparse

.. autoapi-nested-parse::

   Conda command line interface parsers.



Classes
-------

.. autoapisummary::

   conda.cli.conda_argparse.ArgumentParser
   conda.cli.conda_argparse._GreedySubParsersAction



Functions
---------

.. autoapisummary::

   conda.cli.conda_argparse.generate_pre_parser
   conda.cli.conda_argparse.generate_parser
   conda.cli.conda_argparse.do_call
   conda.cli.conda_argparse.find_builtin_commands
   conda.cli.conda_argparse._exec
   conda.cli.conda_argparse._exec_win
   conda.cli.conda_argparse._exec_unix
   conda.cli.conda_argparse.configure_parser_plugins



Attributes
----------

.. autoapisummary::

   conda.cli.conda_argparse.escaped_user_rc_path
   conda.cli.conda_argparse.escaped_sys_rc_path
   conda.cli.conda_argparse.BUILTIN_COMMANDS


.. py:data:: escaped_user_rc_path

   

.. py:data:: escaped_sys_rc_path

   

.. py:data:: BUILTIN_COMMANDS

   

.. py:function:: generate_pre_parser(**kwargs) -> ArgumentParser


.. py:function:: generate_parser(**kwargs) -> ArgumentParser


.. py:function:: do_call(args: argparse.Namespace, parser: ArgumentParser)

   Serves as the primary entry point for commands referred to in this file and for
   all registered plugin subcommands.


.. py:function:: find_builtin_commands(parser)


.. py:class:: ArgumentParser(*args, add_help=True, **kwargs)


   Bases: :py:obj:`argparse.ArgumentParser`

   Object for parsing command line strings into Python objects.

   :keyword - prog -- The name of the program (default: ``os.path.basename(sys.argv[0])``)
   :keyword - usage -- A usage message (default: auto-generated from arguments)
   :keyword - description -- A description of what the program does:
   :keyword - epilog -- Text following the argument descriptions:
   :keyword - parents -- Parsers whose arguments should be copied into this one:
   :keyword - formatter_class -- HelpFormatter class for printing help messages:
   :keyword - prefix_chars -- Characters that prefix optional arguments:
   :keyword - fromfile_prefix_chars -- Characters that prefix files containing: additional arguments
   :keyword - argument_default -- The default value for all arguments:
   :keyword - conflict_handler -- String indicating how to handle conflicts:
   :keyword - add_help -- Add a -h/-help option:
   :keyword - allow_abbrev -- Allow long options to be abbreviated unambiguously:
   :keyword - exit_on_error -- Determines whether or not ArgumentParser exits with: error info when an error occurs

   .. py:method:: _check_value(action, value)


   .. py:method:: parse_args(*args, override_args=None, **kwargs)



.. py:class:: _GreedySubParsersAction(option_strings, prog, parser_class, dest=SUPPRESS, required=False, help=None, metavar=None)


   Bases: :py:obj:`argparse._SubParsersAction`

   A custom subparser action to conditionally act as a greedy consumer.

   This is a workaround since argparse.REMAINDER does not work as expected,
   see https://github.com/python/cpython/issues/61252.

   .. py:method:: __call__(parser, namespace, values, option_string=None)


   .. py:method:: _get_subactions()

      Sort actions for subcommands to appear alphabetically in help blurb.



.. py:function:: _exec(executable_args, env_vars)


.. py:function:: _exec_win(executable_args, env_vars)


.. py:function:: _exec_unix(executable_args, env_vars)


.. py:function:: configure_parser_plugins(sub_parsers) -> None

   For each of the provided plugin-based subcommands, we'll create
   a new subparser for an improved help printout and calling the
   :meth:`~conda.plugins.types.CondaSubcommand.configure_parser`
   with the newly created subcommand specific argument parser.


