:py:mod:`fixtures`
==================

.. py:module:: conda.testing.notices.fixtures

.. autoapi-nested-parse::

   Collection of pytest fixtures used in conda.notices tests.




Functions
---------

.. autoapisummary::

   conda.testing.notices.fixtures.notices_cache_dir
   conda.testing.notices.fixtures.notices_mock_fetch_get_session
   conda.testing.notices.fixtures.conda_notices_args_n_parser



.. py:function:: notices_cache_dir(tmpdir)

   Fixture that creates the notices cache dir while also mocking
   out a call to user_cache_dir.


.. py:function:: notices_mock_fetch_get_session()


.. py:function:: conda_notices_args_n_parser()


