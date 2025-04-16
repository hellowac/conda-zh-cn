:py:mod:`helpers`
=================

.. py:module:: conda.testing.notices.helpers

.. autoapi-nested-parse::

   Collection of helper functions used in conda.notices tests.



Classes
-------

.. autoapisummary::

   conda.testing.notices.helpers.DummyArgs
   conda.testing.notices.helpers.MockResponse



Functions
---------

.. autoapisummary::

   conda.testing.notices.helpers.get_test_notices
   conda.testing.notices.helpers.add_resp_to_mock
   conda.testing.notices.helpers.create_notice_cache_files
   conda.testing.notices.helpers.offset_cache_file_mtime
   conda.testing.notices.helpers.notices_decorator_assert_message_in_stdout
   conda.testing.notices.helpers.get_notice_cache_filenames



Attributes
----------

.. autoapisummary::

   conda.testing.notices.helpers.DEFAULT_NOTICE_MESG


.. py:data:: DEFAULT_NOTICE_MESG
   :value: 'Here is an example message that will be displayed to users'

   

.. py:function:: get_test_notices(messages: collections.abc.Sequence[str], level: str | None = 'info', created_at: datetime.datetime | None = None, expired_at: datetime.datetime | None = None) -> dict


.. py:function:: add_resp_to_mock(mock_session: unittest.mock.MagicMock, status_code: int, messages_json: dict, raise_exc: bool = False) -> None

   Adds any number of MockResponse to MagicMock object as side_effects


.. py:function:: create_notice_cache_files(cache_dir: pathlib.Path, cache_files: collections.abc.Sequence[str], messages_json_seq: collections.abc.Sequence[dict]) -> None

   Creates the cache files that we use in tests


.. py:function:: offset_cache_file_mtime(mtime_offset) -> None

   Allows for offsetting the mtime of the notices cache file. This is often
   used to mock an older creation time the cache file.


.. py:class:: DummyArgs(**kwargs)


   Dummy object that sets all kwargs as object properties.


.. py:function:: notices_decorator_assert_message_in_stdout(captured, messages: collections.abc.Sequence[str], dummy_mesg: str | None = None, not_in: bool = False)

   Tests a run of notices decorator where we expect to see the messages
   print to stdout.


.. py:class:: MockResponse(status_code, json_data, raise_exc=False)


   .. py:method:: json()



.. py:function:: get_notice_cache_filenames(ctx: conda.base.context.Context) -> tuple[str]

   Returns the filenames of the cache files that will be searched for


