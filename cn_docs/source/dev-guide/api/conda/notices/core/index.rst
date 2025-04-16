:py:mod:`core`
==============

.. py:module:: conda.notices.core

.. autoapi-nested-parse::

   Core conda notices logic.




Functions
---------

.. autoapisummary::

   conda.notices.core.retrieve_notices
   conda.notices.core.display_notices
   conda.notices.core.notices
   conda.notices.core.get_channel_name_and_urls
   conda.notices.core.flatten_notice_responses
   conda.notices.core.filter_notices
   conda.notices.core.is_channel_notices_enabled
   conda.notices.core.is_channel_notices_cache_expired



Attributes
----------

.. autoapisummary::

   conda.notices.core.ChannelName
   conda.notices.core.ChannelUrl
   conda.notices.core.logger


.. py:data:: ChannelName

   

.. py:data:: ChannelUrl

   

.. py:data:: logger

   

.. py:function:: retrieve_notices(limit: int | None = None, always_show_viewed: bool = True, silent: bool = False) -> conda.notices.types.ChannelNoticeResultSet

   Function used for retrieving notices. This is called by the "notices" decorator as well
   as the sub-command "notices"

   :param limit: Limit the number of notices to show (defaults to None).
   :param always_show_viewed: Whether all notices should be shown, not only the unread ones
                              (defaults to True).
   :param silent: Whether to use a spinner when fetching and caching notices.


.. py:function:: display_notices(channel_notice_set: conda.notices.types.ChannelNoticeResultSet) -> None

   Prints the channel notices to std out.


.. py:function:: notices(func)

   Wrapper for "execute" entry points for subcommands.

   If channel notices need to be fetched, we do that first and then
   run the command normally. We then display these notices at the very
   end of the command output so that the user is more likely to see them.

   This ordering was specifically done to address the following bug report:
       - https://github.com/conda/conda/issues/11847

   :param func: Function to be decorated


.. py:function:: get_channel_name_and_urls(channels: collections.abc.Sequence[conda.models.channel.Channel | conda.models.channel.MultiChannel]) -> list[tuple[ChannelUrl, ChannelName]]

   Return a sequence of Channel URL and name tuples.

   This function handles both Channel and MultiChannel object types.


.. py:function:: flatten_notice_responses(channel_notice_responses: collections.abc.Sequence[conda.notices.types.ChannelNoticeResponse]) -> collections.abc.Sequence[conda.notices.types.ChannelNotice]


.. py:function:: filter_notices(channel_notices: collections.abc.Sequence[conda.notices.types.ChannelNotice], limit: int | None = None, exclude: set[str] | None = None) -> collections.abc.Sequence[conda.notices.types.ChannelNotice]

   Perform filtering actions for the provided sequence of ChannelNotice objects.


.. py:function:: is_channel_notices_enabled(ctx: conda.base.context.Context) -> bool

   Determines whether channel notices are enabled and therefore displayed when
   invoking the `notices` command decorator.

   This only happens when:
    - offline is False
    - number_channel_notices is greater than 0

   :param ctx: The conda context object


.. py:function:: is_channel_notices_cache_expired() -> bool

   Checks to see if the notices cache file we use to keep track of
   displayed notices is expired. This involves checking the mtime
   attribute of the file. Anything older than what is specified as
   the NOTICES_DECORATOR_DISPLAY_INTERVAL is considered expired.


