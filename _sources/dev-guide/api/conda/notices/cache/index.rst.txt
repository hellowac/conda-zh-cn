:py:mod:`cache`
===============

.. py:module:: conda.notices.cache

.. autoapi-nested-parse::

   Handles all caching logic including:
     - Retrieving from cache
     - Saving to cache
     - Determining whether not certain items have expired and need to be refreshed




Functions
---------

.. autoapisummary::

   conda.notices.cache.cached_response
   conda.notices.cache.is_notice_response_cache_expired
   conda.notices.cache.get_notices_cache_dir
   conda.notices.cache.get_notices_cache_file
   conda.notices.cache.get_notice_response_from_cache
   conda.notices.cache.write_notice_response_to_cache
   conda.notices.cache.mark_channel_notices_as_viewed
   conda.notices.cache.get_viewed_channel_notice_ids



Attributes
----------

.. autoapisummary::

   conda.notices.cache.logger


.. py:data:: logger

   

.. py:function:: cached_response(func)


.. py:function:: is_notice_response_cache_expired(channel_notice_response: conda.notices.types.ChannelNoticeResponse) -> bool

   This checks the contents of the cache response to see if it is expired.

   If for whatever reason we encounter an exception while parsing the individual
   messages, we assume an invalid cache and return true.


.. py:function:: get_notices_cache_dir() -> pathlib.Path

   Returns the location of the notices cache directory as a Path object


.. py:function:: get_notices_cache_file() -> pathlib.Path

   Returns the location of the notices cache file as a Path object


.. py:function:: get_notice_response_from_cache(url: str, name: str, cache_dir: pathlib.Path) -> conda.notices.types.ChannelNoticeResponse | None

   Retrieves a notice response object from cache if it exists.


.. py:function:: write_notice_response_to_cache(channel_notice_response: conda.notices.types.ChannelNoticeResponse, cache_dir: pathlib.Path) -> None

   Writes our notice data to our local cache location.


.. py:function:: mark_channel_notices_as_viewed(cache_file: pathlib.Path, channel_notices: collections.abc.Sequence[conda.notices.types.ChannelNotice]) -> None

   Insert channel notice into our database marking it as read.


.. py:function:: get_viewed_channel_notice_ids(cache_file: pathlib.Path, channel_notices: collections.abc.Sequence[conda.notices.types.ChannelNotice]) -> set[str]

   Return the ids of the channel notices which have already been seen.


