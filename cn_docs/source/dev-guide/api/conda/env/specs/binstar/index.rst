:py:mod:`binstar`
=================

.. py:module:: conda.env.specs.binstar

.. autoapi-nested-parse::

   Define binstar spec.



Classes
-------

.. autoapisummary::

   conda.env.specs.binstar.BinstarSpec




.. py:class:: BinstarSpec(name=None)


   spec = BinstarSpec('darth/deathstar')
   spec.can_handle() # => True / False
   spec.environment # => YAML string
   spec.msg # => Error messages
   :raises: EnvironmentFileNotDownloaded

   .. py:attribute:: msg

      

   .. py:method:: can_handle() -> bool

      Validates loader can process environment definition.
      :return: True or False


   .. py:method:: valid_name() -> bool

      Validates name
      :return: True or False


   .. py:method:: valid_package() -> bool

      Returns True if package has an environment file
      :return: True or False


   .. py:method:: binstar() -> types.ModuleType | None


   .. py:method:: file_data() -> list[dict[str, str]]


   .. py:method:: environment() -> conda.env.env.Environment


   .. py:method:: package()


   .. py:method:: username() -> str


   .. py:method:: packagename() -> str



