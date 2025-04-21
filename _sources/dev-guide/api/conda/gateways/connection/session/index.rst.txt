:py:mod:`session`
=================

.. py:module:: conda.gateways.connection.session

.. autoapi-nested-parse::

   Requests session configured with all accepted scheme adapters.



Classes
-------

.. autoapisummary::

   conda.gateways.connection.session.EnforceUnusedAdapter
   conda.gateways.connection.session.CondaSessionType
   conda.gateways.connection.session.CondaSession
   conda.gateways.connection.session.CondaHttpAuth



Functions
---------

.. autoapisummary::

   conda.gateways.connection.session.get_channel_name_from_url
   conda.gateways.connection.session.get_session
   conda.gateways.connection.session.get_session_storage_key



Attributes
----------

.. autoapisummary::

   conda.gateways.connection.session.RETRIES
   conda.gateways.connection.session.CONDA_SESSION_SCHEMES


.. py:data:: RETRIES
   :value: 3

   

.. py:data:: CONDA_SESSION_SCHEMES

   

.. py:class:: EnforceUnusedAdapter


   Bases: :py:obj:`conda.gateways.connection.BaseAdapter`

   The Base Transport Adapter

   .. py:method:: send(request, *args, **kwargs)

      Sends PreparedRequest object. Returns Response object.

      :param request: The :class:`PreparedRequest <PreparedRequest>` being sent.
      :param stream: (optional) Whether to stream the request content.
      :param timeout: (optional) How long to wait for the server to send
          data before giving up, as a float, or a :ref:`(connect timeout,
          read timeout) <timeouts>` tuple.
      :type timeout: float or tuple
      :param verify: (optional) Either a boolean, in which case it controls whether we verify
          the server's TLS certificate, or a string, in which case it must be a path
          to a CA bundle to use
      :param cert: (optional) Any user-provided SSL certificate to be trusted.
      :param proxies: (optional) The proxies dictionary to apply to the request.


   .. py:method:: close()
      :abstractmethod:

      Cleans up adapter specific items.



.. py:function:: get_channel_name_from_url(url: str) -> str | None

   Given a URL, determine the channel it belongs to and return its name.


.. py:function:: get_session(url: str)

   Function that determines the correct Session object to be returned
   based on the URL that is passed in.


.. py:function:: get_session_storage_key(auth) -> str

   Function that determines which storage key to use for our CondaSession object caching


.. py:class:: CondaSessionType


   Bases: :py:obj:`type`

   Takes advice from https://github.com/requests/requests/issues/1871#issuecomment-33327847
   and creates one Session instance per thread.

   .. py:method:: __call__(**kwargs)

      Call self as a function.



.. py:class:: CondaSession(auth: conda.gateways.connection.AuthBase | tuple[str, str] | None = None)


   Bases: :py:obj:`conda.gateways.connection.Session`

   A Requests session.

   Provides cookie persistence, connection-pooling, and configuration.

   Basic Usage::

     >>> import requests
     >>> s = requests.Session()
     >>> s.get('https://httpbin.org/get')
     <Response [200]>

   Or as a context manager::

     >>> with requests.Session() as s:
     ...     s.get('https://httpbin.org/get')
     <Response [200]>

   :param auth: Optionally provide ``requests.AuthBase`` compliant objects

   .. py:method:: prepare_request(request: requests.models.Request) -> requests.models.PreparedRequest

      Constructs a :class:`PreparedRequest <PreparedRequest>` for
      transmission and returns it. The :class:`PreparedRequest` has settings
      merged from the :class:`Request <Request>` instance and those of the
      :class:`Session`.

      :param request: :class:`Request` instance to prepare with this
          session's settings.
      :rtype: requests.PreparedRequest


   .. py:method:: cache_clear()
      :classmethod:



.. py:class:: CondaHttpAuth


   Bases: :py:obj:`conda.gateways.connection.AuthBase`

   Base class that all auth implementations derive from

   .. py:method:: __call__(request)


   .. py:method:: _apply_basic_auth(request)
      :staticmethod:


   .. py:method:: add_binstar_token(url)
      :staticmethod:


   .. py:method:: handle_407(response, **kwargs)
      :staticmethod:

      Prompts the user for the proxy username and password and modifies the
      proxy in the session object to include it.

      This method is modeled after
        * requests.auth.HTTPDigestAuth.handle_401()
        * requests.auth.HTTPProxyAuth
        * the previous conda.fetch.handle_proxy_407()

      It both adds 'username:password' to the proxy URL, as well as adding a
      'Proxy-Authorization' header.  If any of this is incorrect, please file an issue.




