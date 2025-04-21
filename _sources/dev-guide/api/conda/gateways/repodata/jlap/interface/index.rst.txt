:py:mod:`interface`
===================

.. py:module:: conda.gateways.repodata.jlap.interface

.. autoapi-nested-parse::

   JLAP interface for repodata.



Classes
-------

.. autoapisummary::

   conda.gateways.repodata.jlap.interface.JlapRepoInterface
   conda.gateways.repodata.jlap.interface.RepodataStateSkipFormat
   conda.gateways.repodata.jlap.interface.ZstdRepoInterface




.. py:class:: JlapRepoInterface(url: str, repodata_fn: str | None, *, cache: conda.gateways.repodata.RepodataCache, **kwargs)


   Bases: :py:obj:`conda.gateways.repodata.RepoInterface`

   Helper class that provides a standard way to create an ABC using
   inheritance.

   .. py:method:: repodata(state: dict | conda.gateways.repodata.RepodataState) -> str | None

      Fetch newest repodata if necessary.

      Always writes to ``cache_path_json``.


   .. py:method:: repodata_parsed(state: dict | conda.gateways.repodata.RepodataState) -> dict | None

      JLAP has to parse the JSON anyway.

      Use this to avoid a redundant parse when repodata is updated.

      When repodata is not updated, it doesn't matter whether this function or
      the caller reads from a file.


   .. py:method:: _repodata_state_copy(state: dict | conda.gateways.repodata.RepodataState)



.. py:class:: RepodataStateSkipFormat(*args, skip_formats=set(), **kwargs)


   Bases: :py:obj:`conda.gateways.repodata.RepodataState`

   Load/save info file that accompanies cached `repodata.json`.

   .. py:attribute:: skip_formats
      :type: set[str]

      

   .. py:method:: should_check_format(format)

      Return True if named format should be attempted.



.. py:class:: ZstdRepoInterface(url: str, repodata_fn: str | None, *, cache: conda.gateways.repodata.RepodataCache, **kwargs)


   Bases: :py:obj:`JlapRepoInterface`

   Support repodata.json.zst (if available) without checking .jlap

   .. py:method:: _repodata_state_copy(state: dict | conda.gateways.repodata.RepodataState)



