:py:mod:`install`
=================

.. py:module:: conda.cli.install

.. autoapi-nested-parse::

   Conda package installation logic.

   Core logic for `conda [create|install|update|remove]` commands.

   See conda.cli.main_create, conda.cli.main_install, conda.cli.main_update, and
   conda.cli.main_remove for the entry points into this module.




Functions
---------

.. autoapisummary::

   conda.cli.install.validate_prefix_exists
   conda.cli.install.validate_new_prefix
   conda.cli.install.check_prefix
   conda.cli.install.clone
   conda.cli.install.print_activate
   conda.cli.install.get_revision
   conda.cli.install.install
   conda.cli.install.revert_actions
   conda.cli.install.handle_txn



Attributes
----------

.. autoapisummary::

   conda.cli.install.stderrlog


.. py:data:: stderrlog

   

.. py:function:: validate_prefix_exists(prefix: str | pathlib.Path) -> None

   Validate that we are receiving at least one valid value for --name or --prefix.


.. py:function:: validate_new_prefix(dest: str, force: bool = False) -> str

   Ensure that the new prefix does not exist.


.. py:function:: check_prefix(prefix: str, json=False)


.. py:function:: clone(src_arg, dst_prefix, json=False, quiet=False, index_args=None)


.. py:function:: print_activate(env_name_or_prefix)


.. py:function:: get_revision(arg, json=False)


.. py:function:: install(args, parser, command='install')

   Logic for `conda install`, `conda update`, and `conda create`.


.. py:function:: revert_actions(prefix, revision=-1, index=None)


.. py:function:: handle_txn(unlink_link_transaction, prefix, args, newenv, remove_op=False)


