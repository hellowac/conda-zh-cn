:py:mod:`integration`
=====================

.. py:module:: conda.testing.integration

.. autoapi-nested-parse::

   These helpers were originally defined in tests/test_create.py,
   but were refactored here so downstream projects can benefit from
   them too.



Classes
-------

.. autoapisummary::

   conda.testing.integration.Commands



Functions
---------

.. autoapisummary::

   conda.testing.integration.escape_for_winpath
   conda.testing.integration.package_is_installed
   conda.testing.integration.get_shortcut_dir



Attributes
----------

.. autoapisummary::

   conda.testing.integration.TEST_LOG_LEVEL
   conda.testing.integration.PYTHON_BINARY
   conda.testing.integration.UNICODE_CHARACTERS
   conda.testing.integration.UNICODE_CHARACTERS_RESTRICTED
   conda.testing.integration.which_or_where
   conda.testing.integration.cp_or_copy
   conda.testing.integration.env_or_set
   conda.testing.integration.SPACER_CHARACTER


.. py:data:: TEST_LOG_LEVEL

   

.. py:data:: PYTHON_BINARY

   

.. py:data:: UNICODE_CHARACTERS
   :value: 'ōγђ家固한áêñßôç'

   

.. py:data:: UNICODE_CHARACTERS_RESTRICTED
   :value: 'abcdef'

   

.. py:data:: which_or_where

   

.. py:data:: cp_or_copy

   

.. py:data:: env_or_set

   

.. py:data:: SPACER_CHARACTER
   :value: ' '

   

.. py:function:: escape_for_winpath(p)


.. py:class:: Commands


   .. py:attribute:: COMPARE
      :value: 'compare'

      

   .. py:attribute:: CONFIG
      :value: 'config'

      

   .. py:attribute:: CLEAN
      :value: 'clean'

      

   .. py:attribute:: CREATE
      :value: 'create'

      

   .. py:attribute:: INFO
      :value: 'info'

      

   .. py:attribute:: INSTALL
      :value: 'install'

      

   .. py:attribute:: LIST
      :value: 'list'

      

   .. py:attribute:: REMOVE
      :value: 'remove'

      

   .. py:attribute:: SEARCH
      :value: 'search'

      

   .. py:attribute:: UPDATE
      :value: 'update'

      

   .. py:attribute:: RUN
      :value: 'run'

      


.. py:function:: package_is_installed(prefix: str | os.PathLike | pathlib.Path, spec: str | conda.models.match_spec.MatchSpec) -> conda.models.records.PrefixRecord | None


.. py:function:: get_shortcut_dir(prefix_for_unix=sys.prefix)


