:py:mod:`channel`
=================

.. py:module:: conda.models.channel

.. autoapi-nested-parse::

   Defines Channel and MultiChannel objects and other channel-related functions.

   Object inheritance:

   .. autoapi-inheritance-diagram:: Channel MultiChannel
      :top-classes: conda.models.channel.Channel
      :parts: 1



Classes
-------

.. autoapisummary::

   conda.models.channel.ChannelType
   conda.models.channel.Channel
   conda.models.channel.MultiChannel



Functions
---------

.. autoapisummary::

   conda.models.channel.tokenized_startswith
   conda.models.channel.tokenized_conda_url_startswith
   conda.models.channel._get_channel_for_name
   conda.models.channel._read_channel_configuration
   conda.models.channel.parse_conda_channel_url
   conda.models.channel.get_conda_build_local_url
   conda.models.channel.prioritize_channels
   conda.models.channel.all_channel_urls
   conda.models.channel.offline_keep
   conda.models.channel.get_channel_objs



.. py:class:: ChannelType


   Bases: :py:obj:`type`

   This metaclass does basic caching and enables static constructor method usage with a
   single arg.

   .. py:method:: __call__(*args, **kwargs)

      Call self as a function.



.. py:class:: Channel(scheme=None, auth=None, location=None, token=None, name=None, platform=None, package_filename=None)


   Channel:
   scheme <> auth <> location <> token <> channel <> subchannel <> platform <> package_filename

   Package Spec:
   channel <> subchannel <> namespace <> package_name


   .. py:property:: channel_location


   .. py:property:: channel_name


   .. py:property:: subdir


   .. py:property:: canonical_name


   .. py:property:: base_url


   .. py:property:: base_urls


   .. py:property:: subdir_url


   .. py:property:: url_channel_wtf


   .. py:attribute:: _cache_

      

   .. py:method:: _reset_state()
      :staticmethod:


   .. py:method:: from_url(url)
      :staticmethod:


   .. py:method:: from_channel_name(channel_name)
      :staticmethod:


   .. py:method:: from_value(value: str | None) -> Self
      :staticmethod:

      Construct a new :class:`Channel` from a single value.

      :param value: Anyone of the following forms:

                    `None`, or one of the special strings "<unknown>", "None:///<unknown>", or "None":
                        represents the unknown channel, used for packages with unknown origin.

                    A URL including a scheme like ``file://`` or ``https://``:
                        represents a channel URL.

                    A local directory path:
                        represents a local channel; relative paths must start with ``./``.

                    A package file (i.e. the path to a file ending in ``.conda`` or ``.tar.bz2``):
                        represents a channel for a single package

                    A known channel name:
                        represents a known channel, e.g. from the users ``.condarc`` file or
                        the global configuration.

      :returns: A channel object.


   .. py:method:: make_simple_channel(channel_alias, channel_url, name=None)
      :staticmethod:


   .. py:method:: urls(with_credentials=False, subdirs=None)


   .. py:method:: url(with_credentials=False)


   .. py:method:: __str__()

      Return str(self).


   .. py:method:: __repr__()

      Return repr(self).


   .. py:method:: __eq__(other)

      Return self==value.


   .. py:method:: __hash__()

      Return hash(self).


   .. py:method:: __nonzero__()


   .. py:method:: __bool__()


   .. py:method:: __json__()


   .. py:method:: dump()



.. py:class:: MultiChannel(name, channels, platform=None)


   Bases: :py:obj:`Channel`

   Channel:
   scheme <> auth <> location <> token <> channel <> subchannel <> platform <> package_filename

   Package Spec:
   channel <> subchannel <> namespace <> package_name


   .. py:property:: channel_location


   .. py:property:: canonical_name


   .. py:property:: base_url


   .. py:property:: base_urls


   .. py:method:: urls(with_credentials=False, subdirs=None)


   .. py:method:: url(with_credentials=False)


   .. py:method:: dump()



.. py:function:: tokenized_startswith(test_iterable, startswith_iterable)


.. py:function:: tokenized_conda_url_startswith(test_url, startswith_url)


.. py:function:: _get_channel_for_name(channel_name)


.. py:function:: _read_channel_configuration(scheme, host, port, path)


.. py:function:: parse_conda_channel_url(url)


.. py:function:: get_conda_build_local_url()


.. py:function:: prioritize_channels(channels, with_credentials=True, subdirs=None)


.. py:function:: all_channel_urls(channels, subdirs=None, with_credentials=True)


.. py:function:: offline_keep(url)


.. py:function:: get_channel_objs(ctx: conda.base.context.Context)

   Return current channels as Channel objects


