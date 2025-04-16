:py:mod:`s3`
============

.. py:module:: conda.gateways.connection.adapters.s3

.. autoapi-nested-parse::

   Defines S3 transport adapter for CondaSession (requests.Session).



Classes
-------

.. autoapisummary::

   conda.gateways.connection.adapters.s3.S3Adapter




Attributes
----------

.. autoapisummary::

   conda.gateways.connection.adapters.s3.stderrlog


.. py:data:: stderrlog

   

.. py:class:: S3Adapter


   Bases: :py:obj:`conda.gateways.connection.BaseAdapter`

   The Base Transport Adapter

   .. py:method:: send(request: conda.gateways.connection.PreparedRequest, stream: bool = False, timeout: None | float | tuple[float, float] | tuple[float, None] = None, verify: bool | str = True, cert: None | bytes | str | tuple[bytes | str, bytes | str] = None, proxies: dict[str, str] | None = None) -> conda.gateways.connection.Response

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


   .. py:method:: _send_boto3(resp: conda.gateways.connection.Response, request: conda.gateways.connection.PreparedRequest) -> conda.gateways.connection.Response


   .. py:method:: _write_tempfile(writer_callable)



