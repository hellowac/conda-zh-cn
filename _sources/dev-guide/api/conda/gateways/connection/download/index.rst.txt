:py:mod:`download`
==================

.. py:module:: conda.gateways.connection.download

.. autoapi-nested-parse::

   Download logic for conda indices and packages.



Classes
-------

.. autoapisummary::

   conda.gateways.connection.download.TmpDownload



Functions
---------

.. autoapisummary::

   conda.gateways.connection.download.disable_ssl_verify_warning
   conda.gateways.connection.download.download
   conda.gateways.connection.download.download_inner
   conda.gateways.connection.download.download_partial_file
   conda.gateways.connection.download.download_http_errors
   conda.gateways.connection.download.download_text



Attributes
----------

.. autoapisummary::

   conda.gateways.connection.download.CHUNK_SIZE


.. py:data:: CHUNK_SIZE

   

.. py:function:: disable_ssl_verify_warning()


.. py:function:: download(url, target_full_path, md5=None, sha256=None, size=None, progress_update_callback=None)


.. py:function:: download_inner(url, target_full_path, md5, sha256, size, progress_update_callback)


.. py:function:: download_partial_file(target_full_path: str | pathlib.Path, *, url: str, sha256: str, md5: str, size: int)

   Create or open locked partial download file, moving onto target_full_path
   when finished. Preserve partial file on exception.


.. py:function:: download_http_errors(url: str)

   Exception translator used inside download()


.. py:function:: download_text(url)


.. py:class:: TmpDownload(url, verbose=True)


   Context manager to handle downloads to a tempfile.

   .. py:method:: __enter__()


   .. py:method:: __exit__(exc_type, exc_value, traceback)



