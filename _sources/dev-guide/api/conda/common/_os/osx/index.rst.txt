:py:mod:`osx`
=============

.. py:module:: conda.common._os.osx



Functions
---------

.. autoapisummary::

   conda.common._os.osx.mac_ver



.. py:function:: mac_ver() -> str

   Returns macOS version, without compatibility modes for 11.x.
   https://github.com/conda/conda/issues/13832
   If Python was compiled against macOS <=10.15, we might get 10.16 instead of 11.0.
   For these cases, we must set SYSTEM_VERSION_COMPAT=0 and call sw_vers directly.


