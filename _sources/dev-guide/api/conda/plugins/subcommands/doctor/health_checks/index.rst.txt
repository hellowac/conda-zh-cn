:py:mod:`health_checks`
=======================

.. py:module:: conda.plugins.subcommands.doctor.health_checks

.. autoapi-nested-parse::

   Backend logic implementation for `conda doctor`.




Functions
---------

.. autoapisummary::

   conda.plugins.subcommands.doctor.health_checks.check_envs_txt_file
   conda.plugins.subcommands.doctor.health_checks.excluded_files_check
   conda.plugins.subcommands.doctor.health_checks.find_packages_with_missing_files
   conda.plugins.subcommands.doctor.health_checks.find_altered_packages
   conda.plugins.subcommands.doctor.health_checks.missing_files
   conda.plugins.subcommands.doctor.health_checks.altered_files
   conda.plugins.subcommands.doctor.health_checks.env_txt_check
   conda.plugins.subcommands.doctor.health_checks.requests_ca_bundle_check
   conda.plugins.subcommands.doctor.health_checks.conda_health_checks



Attributes
----------

.. autoapisummary::

   conda.plugins.subcommands.doctor.health_checks.logger
   conda.plugins.subcommands.doctor.health_checks.OK_MARK
   conda.plugins.subcommands.doctor.health_checks.X_MARK


.. py:data:: logger

   

.. py:data:: OK_MARK
   :value: '✅'

   

.. py:data:: X_MARK
   :value: '❌'

   

.. py:function:: check_envs_txt_file(prefix: str | os.PathLike | pathlib.Path) -> bool

   Checks whether the environment is listed in the environments.txt file


.. py:function:: excluded_files_check(filename: str) -> bool


.. py:function:: find_packages_with_missing_files(prefix: str | pathlib.Path) -> dict[str, list[str]]

   Finds packages listed in conda-meta which have missing files.


.. py:function:: find_altered_packages(prefix: str | pathlib.Path) -> dict[str, list[str]]

   Finds altered packages


.. py:function:: missing_files(prefix: str, verbose: bool) -> None


.. py:function:: altered_files(prefix: str, verbose: bool) -> None


.. py:function:: env_txt_check(prefix: str, verbose: bool) -> None


.. py:function:: requests_ca_bundle_check(prefix: str, verbose: bool) -> None


.. py:function:: conda_health_checks()


