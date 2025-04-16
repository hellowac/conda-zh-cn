:py:mod:`envs_manager`
======================

.. py:module:: conda.core.envs_manager

.. autoapi-nested-parse::

   Tools for managing conda environments.




Functions
---------

.. autoapisummary::

   conda.core.envs_manager.get_user_environments_txt_file
   conda.core.envs_manager.register_env
   conda.core.envs_manager.unregister_env
   conda.core.envs_manager.list_all_known_prefixes
   conda.core.envs_manager.query_all_prefixes
   conda.core.envs_manager._clean_environments_txt
   conda.core.envs_manager._rewrite_environments_txt



.. py:function:: get_user_environments_txt_file(userhome: str = '~') -> str

   Gets the path to the user's environments.txt file.

   :param userhome: The home directory of the user.
   :type userhome: str
   :return: Path to the environments.txt file.
   :rtype: str


.. py:function:: register_env(location: str) -> None

   Registers an environment by adding it to environments.txt file.

   :param location: The file path of the environment to register.
   :type location: str
   :return: None


.. py:function:: unregister_env(location: str) -> None

   Unregisters an environment by removing its entry from the environments.txt file if certain conditions are met.

   The environment is only unregistered if its associated 'conda-meta' directory exists and contains no significant files other than 'history'. If these conditions are met, the environment's path is removed from environments.txt.

   :param location: The file path of the environment to unregister.
   :type location: str
   :return: None


.. py:function:: list_all_known_prefixes() -> list[str]

   Lists all known conda environment prefixes.

   :return: A list of all known conda environment prefixes.
   :rtype: List[str]


.. py:function:: query_all_prefixes(spec: str) -> collections.abc.Iterator[tuple[str, tuple]]

   Queries all known prefixes for a given specification.

   :param spec: The specification to query for.
   :type spec: str
   :return: An iterator of tuples containing the prefix and the query results.
   :rtype: Iterator[Tuple[str, Tuple]]


.. py:function:: _clean_environments_txt(environments_txt_file: str, remove_location: str | None = None) -> tuple[str, Ellipsis]

   Cleans the environments.txt file by removing specified locations.

   :param environments_txt_file: The file path of environments.txt.
   :param remove_location: Optional location to remove from the file.
   :type environments_txt_file: str
   :type remove_location: Optional[str]
   :return: A tuple of the cleaned lines.
   :rtype: Tuple[str, ...]


.. py:function:: _rewrite_environments_txt(environments_txt_file: str, prefixes: list[str]) -> None

   Rewrites the environments.txt file with the specified prefixes.

   :param environments_txt_file: The file path of environments.txt.
   :param prefixes: List of prefixes to write into the file.
   :type environments_txt_file: str
   :type prefixes: List[str]
   :return: None


