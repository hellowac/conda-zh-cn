:py:mod:`core`
==============

.. py:module:: conda.gateways.repodata.jlap.core

.. autoapi-nested-parse::

   JLAP reader.



Classes
-------

.. autoapisummary::

   conda.gateways.repodata.jlap.core.JLAP



Functions
---------

.. autoapisummary::

   conda.gateways.repodata.jlap.core.keyed_hash
   conda.gateways.repodata.jlap.core.line_and_pos



Attributes
----------

.. autoapisummary::

   conda.gateways.repodata.jlap.core.DIGEST_SIZE
   conda.gateways.repodata.jlap.core.DEFAULT_IV


.. py:data:: DIGEST_SIZE
   :value: 32

   

.. py:data:: DEFAULT_IV

   

.. py:function:: keyed_hash(data: bytes, key: bytes)

   Keyed hash.


.. py:function:: line_and_pos(lines: collections.abc.Iterable[bytes], pos=0) -> collections.abc.Iterator[tuple[int, bytes]]

   :param lines: iterator over input split by '\n', with '\n' removed.
   :param pos: initial position


.. py:class:: JLAP(initlist=None)


   Bases: :py:obj:`collections.UserList`

   A more or less complete user-defined wrapper around list objects.

   .. py:property:: body

      All lines except the first, and last two.

   .. py:property:: penultimate

      Next-to-last line. Should contain the footer.

   .. py:property:: last

      Last line. Should contain the trailing checksum.

   .. py:method:: from_lines(lines: collections.abc.Iterable[bytes], iv: bytes, pos=0, verify=True)
      :classmethod:

      :param lines: iterator over input split by b'\n', with b'\n' removed
      :param pos: initial position
      :param iv: initialization vector (first line of .jlap stream, hex
          decoded). Ignored if pos==0.
      :param verify: assert last line equals computed checksum of previous
          line. Useful for writing new .jlap files if False.

      :raises ValueError: if trailing and computed checksums do not match

      :return: list of (offset, line, checksum)


   .. py:method:: from_path(path: pathlib.Path | str, verify=True)
      :classmethod:


   .. py:method:: add(line: str)

      Add line to buffer, following checksum rules.

      Buffer must not be empty.

      (Remember to pop trailing checksum and possibly trailing metadata line, if
      appending to a complete jlap file)

      Less efficient than creating a new buffer from many lines and our last iv,
      and extending.

      :return: self


   .. py:method:: terminate()

      Add trailing checksum to buffer.

      :return: self


   .. py:method:: write(path: pathlib.Path)

      Write buffer to path.



