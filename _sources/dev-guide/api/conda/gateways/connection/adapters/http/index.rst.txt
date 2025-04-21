:py:mod:`http`
==============

.. py:module:: conda.gateways.connection.adapters.http

.. autoapi-nested-parse::

   Defines HTTP transport adapter for CondaSession (requests.Session).

   Closely derived from pip:

   https://github.com/pypa/pip/blob/8c24fd2a80bad21aa29aec02fb48bd89a1e8f5e1/src/pip/_internal/network/session.py#L254

   Under the MIT license:

   Copyright (c) 2008-2023 The pip developers (see AUTHORS.txt file on the pip repository)

   Permission is hereby granted, free of charge, to any person obtaining
   a copy of this software and associated documentation files (the
   "Software"), to deal in the Software without restriction, including
   without limitation the rights to use, copy, modify, merge, publish,
   distribute, sublicense, and/or sell copies of the Software, and to
   permit persons to whom the Software is furnished to do so, subject to
   the following conditions:

   The above copyright notice and this permission notice shall be
   included in all copies or substantial portions of the Software.

   THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
   EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
   MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
   NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
   LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
   OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
   WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.



Classes
-------

.. autoapisummary::

   conda.gateways.connection.adapters.http._SSLContextAdapterMixin
   conda.gateways.connection.adapters.http.HTTPAdapter




.. py:class:: _SSLContextAdapterMixin(*, ssl_context: Optional[ssl.SSLContext] = None, **kwargs: Any)


   Mixin to add the ``ssl_context`` constructor argument to HTTP adapters.

   The additional argument is forwarded directly to the pool manager. This allows us
   to dynamically decide what SSL store to use at runtime, which is used to implement
   the optional ``truststore`` backend.

   .. py:method:: init_poolmanager(connections: int, maxsize: int, block: bool = DEFAULT_POOLBLOCK, **pool_kwargs: Any) -> urllib3.PoolManager



.. py:class:: HTTPAdapter(*, ssl_context: Optional[ssl.SSLContext] = None, **kwargs: Any)


   Bases: :py:obj:`_SSLContextAdapterMixin`, :py:obj:`conda.gateways.connection.HTTPAdapter`

   Mixin to add the ``ssl_context`` constructor argument to HTTP adapters.

   The additional argument is forwarded directly to the pool manager. This allows us
   to dynamically decide what SSL store to use at runtime, which is used to implement
   the optional ``truststore`` backend.


