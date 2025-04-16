:py:mod:`exports`
=================

.. py:module:: conda.exports

.. autoapi-nested-parse::

   Backported exports for conda-build.



Classes
-------

.. autoapisummary::

   conda.exports.Completer
   conda.exports.InstalledPackages



Functions
---------

.. autoapisummary::

   conda.exports.__getattr__
   conda.exports.iteritems
   conda.exports.rm_rf
   conda.exports.hash_file
   conda.exports.verify
   conda.exports.get_index
   conda.exports.package_cache
   conda.exports.symlink_conda
   conda.exports._symlink_conda_hlp
   conda.exports.win_conda_bat_redirect
   conda.exports.linked_data
   conda.exports.linked
   conda.exports.is_linked
   conda.exports.download



Attributes
----------

.. autoapisummary::

   conda.exports.non_x86_linux_machines
   conda.exports.get_default_urls
   conda.exports.arch_name
   conda.exports.binstar_upload
   conda.exports.bits
   conda.exports.default_prefix
   conda.exports.default_python
   conda.exports.envs_dirs
   conda.exports.pkgs_dirs
   conda.exports.platform
   conda.exports.root_dir
   conda.exports.root_writable
   conda.exports.subdir
   conda.exports.conda_build
   conda.exports.get_rc_urls
   conda.exports.get_local_urls
   conda.exports.load_condarc
   conda.exports.PaddingError
   conda.exports.LinkError
   conda.exports.CondaOSError
   conda.exports.CondaFileNotFoundError
   conda.exports.PY3
   conda.exports.string_types
   conda.exports.text_type


.. py:data:: non_x86_linux_machines

   

.. py:data:: get_default_urls

   

.. py:data:: arch_name

   

.. py:data:: binstar_upload

   

.. py:data:: bits

   

.. py:data:: default_prefix

   

.. py:data:: default_python

   

.. py:data:: envs_dirs

   

.. py:data:: pkgs_dirs

   

.. py:data:: platform

   

.. py:data:: root_dir

   

.. py:data:: root_writable

   

.. py:data:: subdir

   

.. py:data:: conda_build

   

.. py:data:: get_rc_urls

   

.. py:data:: get_local_urls

   

.. py:data:: load_condarc

   

.. py:data:: PaddingError

   

.. py:data:: LinkError

   

.. py:data:: CondaOSError

   

.. py:data:: CondaFileNotFoundError

   

.. py:data:: PY3
   :value: True

   

.. py:data:: string_types

   

.. py:data:: text_type

   

.. py:function:: __getattr__(name: str) -> Any


.. py:function:: iteritems(d, **kw)


.. py:class:: Completer


   .. py:method:: get_items()


   .. py:method:: __contains__(item)


   .. py:method:: __iter__()



.. py:class:: InstalledPackages



.. py:function:: rm_rf(path, max_retries=5, trash=True)


.. py:function:: hash_file(_)


.. py:function:: verify(_)


.. py:function:: get_index(channel_urls=(), prepend=True, platform=None, use_local=False, use_cache=False, unknown=None, prefix=None)


.. py:function:: package_cache()


.. py:function:: symlink_conda(prefix, root_dir, shell=None)


.. py:function:: _symlink_conda_hlp(prefix, root_dir, where, symlink_fn)


.. py:function:: win_conda_bat_redirect(src, dst, shell)

   Special function for Windows XP where the `CreateSymbolicLink`
   function is not available.

   Simply creates a `.bat` file at `dst` which calls `src` together with
   all command line arguments.

   Works of course only with callable files, e.g. `.bat` or `.exe` files.


.. py:function:: linked_data(prefix, ignore_channels=False)

   Return a dictionary of the linked packages in prefix.


.. py:function:: linked(prefix, ignore_channels=False)

   Return the Dists of linked packages in prefix.


.. py:function:: is_linked(prefix, dist)

   Return the install metadata for a linked package in a prefix, or None
   if the package is not linked in the prefix.


.. py:function:: download(url, dst_path, session=None, md5sum=None, urlstxt=False, retries=3, sha256=None, size=None)


