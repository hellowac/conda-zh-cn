:py:mod:`read`
==============

.. py:module:: conda.gateways.disk.read

.. autoapi-nested-parse::

   Disk utility functions for reading and processing file contents.




Functions
---------

.. autoapisummary::

   conda.gateways.disk.read.yield_lines
   conda.gateways.disk.read.compute_sum
   conda.gateways.disk.read.read_package_info
   conda.gateways.disk.read.read_index_json
   conda.gateways.disk.read.read_index_json_from_tarball
   conda.gateways.disk.read.read_repodata_json
   conda.gateways.disk.read.read_icondata
   conda.gateways.disk.read.read_package_metadata
   conda.gateways.disk.read.read_paths_json
   conda.gateways.disk.read.read_has_prefix
   conda.gateways.disk.read.read_no_link
   conda.gateways.disk.read.read_soft_links
   conda.gateways.disk.read.read_python_record



Attributes
----------

.. autoapisummary::

   conda.gateways.disk.read.listdir


.. py:data:: listdir

   

.. py:function:: yield_lines(path)

   Generator function for lines in file.  Empty generator if path does not exist.

   :param path: path to file
   :type path: str

   :returns: each line in file, not starting with '#'
   :rtype: iterator


.. py:function:: compute_sum(path: str | os.PathLike, algo: Literal[md5, sha256]) -> str


.. py:function:: read_package_info(record, package_cache_record)


.. py:function:: read_index_json(extracted_package_directory)


.. py:function:: read_index_json_from_tarball(package_tarball_full_path)


.. py:function:: read_repodata_json(extracted_package_directory)


.. py:function:: read_icondata(extracted_package_directory)


.. py:function:: read_package_metadata(extracted_package_directory)


.. py:function:: read_paths_json(extracted_package_directory)


.. py:function:: read_has_prefix(path)

   Reads `has_prefix` file and return dict mapping filepaths to tuples(placeholder, FileMode).

   A line in `has_prefix` contains one of:
     * filepath
     * placeholder mode filepath

   Mode values are one of:
     * text
     * binary


.. py:function:: read_no_link(info_dir)


.. py:function:: read_soft_links(extracted_package_directory, files)


.. py:function:: read_python_record(prefix_path, anchor_file, python_version)

   Convert a python package defined by an anchor file (Metadata information)
   into a conda prefix record object.


