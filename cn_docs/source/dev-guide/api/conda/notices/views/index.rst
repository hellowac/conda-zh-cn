:py:mod:`views`
===============

.. py:module:: conda.notices.views

.. autoapi-nested-parse::

   Handles all display/view logic.




Functions
---------

.. autoapisummary::

   conda.notices.views.print_notices
   conda.notices.views.print_notice_message
   conda.notices.views.print_more_notices_message



.. py:function:: print_notices(channel_notices: collections.abc.Sequence[conda.notices.types.ChannelNotice])

   Accepts a list of channel notice responses and prints a display.

   :param channel_notices: A sequence of ChannelNotice objects.


.. py:function:: print_notice_message(notice: conda.notices.types.ChannelNotice, indent: str = '  ') -> None

   Prints a single channel notice.


.. py:function:: print_more_notices_message(total_notices: int, displayed_notices: int, viewed_notices: int) -> None

   Conditionally shows a message informing users how many more message there are.


