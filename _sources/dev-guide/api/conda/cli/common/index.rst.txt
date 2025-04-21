:py:mod:`common`
================

.. py:module:: conda.cli.common

.. autoapi-nested-parse::

   Common utilities for conda command line tools.




Functions
---------

.. autoapisummary::

   conda.cli.common.confirm
   conda.cli.common.confirm_yn
   conda.cli.common.is_active_prefix
   conda.cli.common.arg2spec
   conda.cli.common.specs_from_args
   conda.cli.common.strip_comment
   conda.cli.common.spec_from_line
   conda.cli.common.specs_from_url
   conda.cli.common.names_in_specs
   conda.cli.common.disp_features
   conda.cli.common.stdout_json
   conda.cli.common.stdout_json_success
   conda.cli.common.print_envs_list
   conda.cli.common.check_non_admin
   conda.cli.common.validate_prefix
   conda.cli.common.validate_prefix_is_writable



Attributes
----------

.. autoapisummary::

   conda.cli.common.spec_pat


.. py:function:: confirm(message='Proceed', choices=('yes', 'no'), default='yes', dry_run=NULL)


.. py:function:: confirm_yn(message='Proceed', default='yes', dry_run=NULL)


.. py:function:: is_active_prefix(prefix: str) -> bool

   Determines whether the args we pass in are pointing to the active prefix.
   Can be used a validation step to make sure operations are not being
   performed on the active prefix.


.. py:function:: arg2spec(arg, json=False, update=False)


.. py:function:: specs_from_args(args, json=False)


.. py:data:: spec_pat

   

.. py:function:: strip_comment(line)


.. py:function:: spec_from_line(line)


.. py:function:: specs_from_url(url, json=False)


.. py:function:: names_in_specs(names, specs)


.. py:function:: disp_features(features)


.. py:function:: stdout_json(d)


.. py:function:: stdout_json_success(success=True, **kwargs)


.. py:function:: print_envs_list(known_conda_prefixes, output=True)


.. py:function:: check_non_admin()


.. py:function:: validate_prefix(prefix)

   Verifies the prefix is a valid conda environment.

   :raises EnvironmentLocationNotFound: Non-existent path or not a directory.
   :raises DirectoryNotACondaEnvironmentError: Directory is not a conda environment.
   :returns: Valid prefix.
   :rtype: str


.. py:function:: validate_prefix_is_writable(prefix: str) -> str

   Verifies the environment directory is writable by trying to access
   the conda-meta/history file. If this file is not writable then we assume
   the whole prefix is not writable and raise an exception.

   :raises EnvironmentNotWritableError: Conda does not have permission to write to the prefix
   :returns: Valid prefix.
   :rtype: str


