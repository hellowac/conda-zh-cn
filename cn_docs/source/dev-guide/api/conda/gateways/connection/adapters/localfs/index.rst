:py:mod:`localfs`
=================

.. py:module:: conda.gateways.connection.adapters.localfs

.. autoapi-nested-parse::

   Defines local filesystem transport adapter for CondaSession (requests.Session).



Classes
-------

.. autoapisummary::

   conda.gateways.connection.adapters.localfs.LocalFSAdapter




.. py:class:: LocalFSAdapter


   Bases: :py:obj:`conda.gateways.connection.BaseAdapter`

   The Base Transport Adapter

   .. py:method:: send(request, stream=None, timeout=None, verify=None, cert=None, proxies=None)

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

      Cleans up adapter specific items.



