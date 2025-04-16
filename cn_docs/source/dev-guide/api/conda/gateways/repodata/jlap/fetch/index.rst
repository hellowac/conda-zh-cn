:py:mod:`fetch`
===============

.. py:module:: conda.gateways.repodata.jlap.fetch

.. autoapi-nested-parse::

   JLAP consumer.



Classes
-------

.. autoapisummary::

   conda.gateways.repodata.jlap.fetch.HashWriter



Functions
---------

.. autoapisummary::

   conda.gateways.repodata.jlap.fetch.hash
   conda.gateways.repodata.jlap.fetch.process_jlap_response
   conda.gateways.repodata.jlap.fetch.fetch_jlap
   conda.gateways.repodata.jlap.fetch.request_jlap
   conda.gateways.repodata.jlap.fetch.format_hash
   conda.gateways.repodata.jlap.fetch.find_patches
   conda.gateways.repodata.jlap.fetch.apply_patches
   conda.gateways.repodata.jlap.fetch.withext
   conda.gateways.repodata.jlap.fetch.timeme
   conda.gateways.repodata.jlap.fetch.build_headers
   conda.gateways.repodata.jlap.fetch.download_and_hash
   conda.gateways.repodata.jlap.fetch._is_http_error_most_400_codes
   conda.gateways.repodata.jlap.fetch.request_url_jlap_state



Attributes
----------

.. autoapisummary::

   conda.gateways.repodata.jlap.fetch.DIGEST_SIZE
   conda.gateways.repodata.jlap.fetch.JLAP_KEY
   conda.gateways.repodata.jlap.fetch.HEADERS
   conda.gateways.repodata.jlap.fetch.NOMINAL_HASH
   conda.gateways.repodata.jlap.fetch.ON_DISK_HASH
   conda.gateways.repodata.jlap.fetch.LATEST
   conda.gateways.repodata.jlap.fetch.STORE_HEADERS


.. py:data:: DIGEST_SIZE
   :value: 32

   

.. py:data:: JLAP_KEY
   :value: 'jlap'

   

.. py:data:: HEADERS
   :value: 'headers'

   

.. py:data:: NOMINAL_HASH
   :value: 'blake2_256_nominal'

   

.. py:data:: ON_DISK_HASH
   :value: 'blake2_256'

   

.. py:data:: LATEST
   :value: 'latest'

   

.. py:data:: STORE_HEADERS

   

.. py:function:: hash()

   Ordinary hash.


.. py:exception:: Jlap304NotModified


   Bases: :py:obj:`Exception`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: JlapSkipZst


   Bases: :py:obj:`Exception`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: JlapPatchNotFound


   Bases: :py:obj:`LookupError`

   Base class for lookup errors.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:function:: process_jlap_response(response: conda.gateways.connection.Response, pos=0, iv=b'')


.. py:function:: fetch_jlap(url, pos=0, etag=None, iv=b'', ignore_etag=True, session=None)


.. py:function:: request_jlap(url, pos=0, etag=None, ignore_etag=True, session: conda.gateways.connection.Session | None = None)

   Return the part of the remote .jlap file we are interested in.


.. py:function:: format_hash(hash)

   Abbreviate hash for formatting.


.. py:function:: find_patches(patches, have, want)


.. py:function:: apply_patches(data, apply)


.. py:function:: withext(url, ext)


.. py:function:: timeme(message)


.. py:function:: build_headers(json_path: pathlib.Path, state: conda.gateways.repodata.RepodataState)

   Caching headers for a path and state.


.. py:class:: HashWriter(backing, hasher)


   Bases: :py:obj:`io.RawIOBase`

   Base class for raw binary I/O.

   Initialize self.  See help(type(self)) for accurate signature.

   .. py:method:: write(b: bytes)


   .. py:method:: close()

      Flush and close the IO object.

      This method has no effect if the file is already closed.



.. py:function:: download_and_hash(hasher, url, json_path: pathlib.Path, session: conda.gateways.connection.Session, state: conda.gateways.repodata.RepodataState | None, is_zst=False, dest_path: pathlib.Path | None = None)

   Download url if it doesn't exist, passing bytes through hasher.update().

   json_path: Path of old cached data (ignore etag if not exists).
   dest_path: Path to write new data.


.. py:function:: _is_http_error_most_400_codes(e: requests.HTTPError) -> bool

   Determine whether the `HTTPError` is an HTTP 400 error code (except for 416).


.. py:function:: request_url_jlap_state(url, state: conda.gateways.repodata.RepodataState, full_download=False, *, session: conda.gateways.connection.Session, cache: conda.gateways.repodata.RepodataCache, temp_path: pathlib.Path) -> dict | None


