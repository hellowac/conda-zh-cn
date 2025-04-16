:py:mod:`main_package`
======================

.. py:module:: conda.cli.main_package

.. autoapi-nested-parse::

   CLI implementation for `conda package`.

   Provides some low-level tools for creating conda packages.




Functions
---------

.. autoapisummary::

   conda.cli.main_package.configure_parser
   conda.cli.main_package.remove
   conda.cli.main_package.execute
   conda.cli.main_package.get_installed_version
   conda.cli.main_package.create_info
   conda.cli.main_package.fix_shebang
   conda.cli.main_package._add_info_dir
   conda.cli.main_package.create_conda_pkg
   conda.cli.main_package.make_tarbz2
   conda.cli.main_package.which_package
   conda.cli.main_package.which_prefix



Attributes
----------

.. autoapisummary::

   conda.cli.main_package.shebang_pat


.. py:function:: configure_parser(sub_parsers: argparse._SubParsersAction, **kwargs) -> argparse.ArgumentParser


.. py:function:: remove(prefix, files)

   Remove files for a given prefix.


.. py:function:: execute(args: argparse.Namespace, parser: argparse.ArgumentParser) -> int


.. py:function:: get_installed_version(prefix, name)


.. py:function:: create_info(name, version, build_number, requires_py)


.. py:data:: shebang_pat

   

.. py:function:: fix_shebang(tmp_dir, path)


.. py:function:: _add_info_dir(t, tmp_dir, files, has_prefix, info)


.. py:function:: create_conda_pkg(prefix, files, info, tar_path, update_info=None)

   Create a conda package and return a list of warnings.


.. py:function:: make_tarbz2(prefix, name='unknown', version='0.0', build_number=0, files=None)


.. py:function:: which_package(path)

   Return the package containing the path.

   Provided the path of a (presumably) conda installed file, iterate over
   the conda packages the file came from. Usually the iteration yields
   only one package.


.. py:function:: which_prefix(path)

   Return the prefix for the provided path.

   Provided the path of a (presumably) conda installed file, return the
   environment prefix in which the file in located.


