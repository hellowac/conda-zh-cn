:py:mod:`fetch`
===============

.. py:module:: conda.notices.fetch

.. autoapi-nested-parse::

   Notices network fetch logic.




Functions
---------

.. autoapisummary::

   conda.notices.fetch.get_notice_responses
   conda.notices.fetch.get_channel_notice_response



Attributes
----------

.. autoapisummary::

   conda.notices.fetch.logger


.. py:data:: logger

   

.. py:function:: get_notice_responses(url_and_names: collections.abc.Sequence[tuple[str, str]], silent: bool = False, max_workers: int = 10) -> collections.abc.Sequence[conda.notices.types.ChannelNoticeResponse]

   Provided a list of channel notification url/name tuples, return a sequence of
   ChannelNoticeResponse objects.

   :param url_and_names: channel url and the channel name
   :param silent: turn off "loading animation" (defaults to False)
   :param max_workers: increase worker number in thread executor (defaults to 10)

   :returns: Sequence[ChannelNoticeResponse]


.. py:function:: get_channel_notice_response(url: str, name: str) -> conda.notices.types.ChannelNoticeResponse | None

   Return a channel response object. We use this to wrap the response with
   additional channel information to use. If the response was invalid we suppress/log
   and error message.


