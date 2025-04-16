:py:mod:`types`
===============

.. py:module:: conda.notices.types

.. autoapi-nested-parse::

   Implements all conda.notices types.



Classes
-------

.. autoapisummary::

   conda.notices.types.ChannelNotice
   conda.notices.types.ChannelNoticeResultSet
   conda.notices.types.ChannelNoticeResponse




Attributes
----------

.. autoapisummary::

   conda.notices.types.UNDEFINED_MESSAGE_ID


.. py:data:: UNDEFINED_MESSAGE_ID
   :value: 'undefined'

   

.. py:class:: ChannelNotice


   Bases: :py:obj:`NamedTuple`

   Represents an individual channel notice.

   .. py:attribute:: id
      :type: str

      

   .. py:attribute:: channel_name
      :type: str | None

      

   .. py:attribute:: message
      :type: str | None

      

   .. py:attribute:: level
      :type: conda.base.constants.NoticeLevel

      

   .. py:attribute:: created_at
      :type: datetime.datetime | None

      

   .. py:attribute:: expired_at
      :type: datetime.datetime | None

      

   .. py:attribute:: interval
      :type: int | None

      

   .. py:method:: to_dict()



.. py:class:: ChannelNoticeResultSet


   Bases: :py:obj:`NamedTuple`

   Represents a list of a channel notices, plus some accompanying
   metadata such as `viewed_channel_notices`.

   .. py:attribute:: channel_notices
      :type: collections.abc.Sequence[ChannelNotice]

      

   .. py:attribute:: total_number_channel_notices
      :type: int

      

   .. py:attribute:: viewed_channel_notices
      :type: int

      


.. py:class:: ChannelNoticeResponse


   Bases: :py:obj:`NamedTuple`

   .. py:property:: notices
      :type: collections.abc.Sequence[ChannelNotice]


   .. py:attribute:: url
      :type: str

      

   .. py:attribute:: name
      :type: str

      

   .. py:attribute:: json_data
      :type: dict | None

      

   .. py:method:: _parse_notice_level(level: str | None) -> conda.base.constants.NoticeLevel
      :staticmethod:

      We use this to validate notice levels and provide reasonable defaults
      if any are invalid.


   .. py:method:: _parse_iso_timestamp(iso_timestamp: str | None) -> datetime.datetime | None
      :staticmethod:

      Parse ISO timestamp and fail over to a default value of none.


   .. py:method:: get_cache_key(url: str, cache_dir: pathlib.Path) -> pathlib.Path
      :classmethod:

      Returns where this channel response will be cached by hashing the URL.



