:py:mod:`fixtures`
==================

.. py:module:: conda.testing.gateways.fixtures

.. autoapi-nested-parse::

   Collection of pytest fixtures used in conda.gateways tests.




Functions
---------

.. autoapisummary::

   conda.testing.gateways.fixtures.minio_s3_server



Attributes
----------

.. autoapisummary::

   conda.testing.gateways.fixtures.MINIO_EXE


.. py:data:: MINIO_EXE

   

.. py:function:: minio_s3_server(xprocess, tmp_path)

   Mock a local S3 server using `minio`

   This requires:
   - pytest-xprocess: runs the background process
   - minio: the executable must be in PATH

   Note, the given S3 server will be EMPTY! The test function needs
   to populate it. You can use
   `conda.testing.helpers.populate_s3_server` for that.


