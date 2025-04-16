:py:mod:`signature_verification`
================================

.. py:module:: conda.trust.signature_verification

.. autoapi-nested-parse::

   Interface between conda-content-trust and conda.



Classes
-------

.. autoapisummary::

   conda.trust.signature_verification._SignatureVerification




Attributes
----------

.. autoapisummary::

   conda.trust.signature_verification.RE_ROOT_METADATA
   conda.trust.signature_verification.signature_verification


.. py:exception:: SignatureError


   Bases: :py:obj:`Exception`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:data:: RE_ROOT_METADATA

   

.. py:class:: _SignatureVerification


   .. py:property:: enabled
      :type: bool


   .. py:property:: trusted_root
      :type: dict


   .. py:property:: key_mgr
      :type: dict | None


   .. py:method:: _fetch_channel_signing_data(signing_data_url: str, filename: str, etag=None, mod_stamp=None) -> dict


   .. py:method:: verify(repodata_fn: str, record: conda.models.records.PackageRecord)


   .. py:method:: __call__(repodata_fn: str, unlink_precs: tuple[conda.models.records.PackageRecord, Ellipsis], link_precs: tuple[conda.models.records.PackageRecord, Ellipsis]) -> None


   .. py:method:: cache_clear() -> None
      :classmethod:



.. py:data:: signature_verification

   

