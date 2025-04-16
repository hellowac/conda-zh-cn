:py:mod:`python`
================

.. py:module:: conda.common.pkg_formats.python

.. autoapi-nested-parse::

   Common Python package format utilities.



Classes
-------

.. autoapisummary::

   conda.common.pkg_formats.python.PythonDistribution
   conda.common.pkg_formats.python.PythonInstalledDistribution
   conda.common.pkg_formats.python.PythonEggInfoDistribution
   conda.common.pkg_formats.python.PythonEggLinkDistribution
   conda.common.pkg_formats.python.PythonDistributionMetadata
   conda.common.pkg_formats.python.Evaluator



Functions
---------

.. autoapisummary::

   conda.common.pkg_formats.python.norm_package_name
   conda.common.pkg_formats.python.pypi_name_to_conda_name
   conda.common.pkg_formats.python.norm_package_version
   conda.common.pkg_formats.python.split_spec
   conda.common.pkg_formats.python.parse_specification
   conda.common.pkg_formats.python.get_site_packages_anchor_files
   conda.common.pkg_formats.python.get_dist_file_from_egg_link
   conda.common.pkg_formats.python.parse_marker
   conda.common.pkg_formats.python._is_literal
   conda.common.pkg_formats.python.get_default_marker_context
   conda.common.pkg_formats.python.interpret



Attributes
----------

.. autoapisummary::

   conda.common.pkg_formats.python.PYPI_TO_CONDA
   conda.common.pkg_formats.python.PYPI_CONDA_DEPS
   conda.common.pkg_formats.python.PARTIAL_PYPI_SPEC_PATTERN
   conda.common.pkg_formats.python.PY_FILE_RE
   conda.common.pkg_formats.python.PySpec
   conda.common.pkg_formats.python.IDENTIFIER
   conda.common.pkg_formats.python.VERSION_IDENTIFIER
   conda.common.pkg_formats.python.COMPARE_OP
   conda.common.pkg_formats.python.MARKER_OP
   conda.common.pkg_formats.python.OR
   conda.common.pkg_formats.python.AND
   conda.common.pkg_formats.python.NON_SPACE
   conda.common.pkg_formats.python.STRING_CHUNK
   conda.common.pkg_formats.python.DEFAULT_MARKER_CONTEXT
   conda.common.pkg_formats.python.evaluator


.. py:data:: PYPI_TO_CONDA

   

.. py:data:: PYPI_CONDA_DEPS

   

.. py:data:: PARTIAL_PYPI_SPEC_PATTERN

   

.. py:data:: PY_FILE_RE

   

.. py:data:: PySpec

   

.. py:exception:: MetadataWarning


   Bases: :py:obj:`Warning`

   Base class for warning categories.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:class:: PythonDistribution(anchor_full_path, python_version)


   Base object describing a python distribution based on path to anchor file.

   .. py:property:: name


   .. py:property:: norm_name


   .. py:property:: conda_name


   .. py:property:: version


   .. py:attribute:: MANIFEST_FILES
      :value: ()

      

   .. py:attribute:: REQUIRES_FILES
      :value: ()

      

   .. py:attribute:: MANDATORY_FILES
      :value: ()

      

   .. py:attribute:: ENTRY_POINTS_FILES
      :value: ('entry_points.txt',)

      

   .. py:method:: init(prefix_path, anchor_file, python_version)
      :staticmethod:


   .. py:method:: _check_files()

      Check the existence of mandatory files for a given distribution.


   .. py:method:: _check_path_data(path, checksum, size)

      Normalizes record data content and format.


   .. py:method:: _parse_requires_file_data(data, global_section='__global__')
      :staticmethod:


   .. py:method:: _parse_entries_file_data(data)
      :staticmethod:


   .. py:method:: _load_requires_provides_file()


   .. py:method:: manifest_full_path()


   .. py:method:: get_paths()

      Read the list of installed paths from record or source file.

      .. rubric:: 示例

      [(u'skdata/__init__.py', u'sha256=47DEQpj8HBSa-_TImW-5JCeuQeRkm5NMpJWZG3hSuFU', 0),
       (u'skdata/diabetes.py', None, None),
       ...
      ]


   .. py:method:: get_dist_requirements()


   .. py:method:: get_python_requirements()


   .. py:method:: get_external_requirements()


   .. py:method:: get_extra_provides()


   .. py:method:: get_conda_dependencies()

      Process metadata fields providing dependency information.

      This includes normalizing fields, and evaluating environment markers.


   .. py:method:: get_optional_dependencies()
      :abstractmethod:


   .. py:method:: get_entry_points()



.. py:class:: PythonInstalledDistribution(prefix_path, anchor_file, python_version)


   Bases: :py:obj:`PythonDistribution`

   Python distribution installed via distutils.

   .. rubric:: 备注

   - https://www.python.org/dev/peps/pep-0376/

   .. py:attribute:: MANIFEST_FILES
      :value: ('RECORD',)

      

   .. py:attribute:: REQUIRES_FILES
      :value: ()

      

   .. py:attribute:: MANDATORY_FILES
      :value: ('METADATA',)

      

   .. py:attribute:: ENTRY_POINTS_FILES
      :value: ()

      

   .. py:attribute:: is_manageable
      :value: True

      


.. py:class:: PythonEggInfoDistribution(anchor_full_path, python_version, sp_reference)


   Bases: :py:obj:`PythonDistribution`

   Python distribution installed via setuptools.

   .. rubric:: 备注

   - http://peak.telecommunity.com/DevCenter/EggFormats

   .. py:property:: is_manageable


   .. py:attribute:: MANIFEST_FILES
      :value: ('installed-files.txt', 'SOURCES', 'SOURCES.txt')

      

   .. py:attribute:: REQUIRES_FILES
      :value: ('requires.txt', 'depends.txt')

      

   .. py:attribute:: MANDATORY_FILES
      :value: ()

      

   .. py:attribute:: ENTRY_POINTS_FILES
      :value: ('entry_points.txt',)

      


.. py:class:: PythonEggLinkDistribution(prefix_path, anchor_file, python_version)


   Bases: :py:obj:`PythonEggInfoDistribution`

   Python distribution installed via setuptools.

   .. rubric:: 备注

   - http://peak.telecommunity.com/DevCenter/EggFormats

   .. py:attribute:: is_manageable
      :value: False

      


.. py:class:: PythonDistributionMetadata(path)


   Object representing the metada of a Python Distribution given by anchor
   file (or directory) path.

   This metadata is extracted from a single file. Python distributions might
   create additional files that complement this metadata information, but
   that is handled at the python distribution level.

   .. rubric:: 备注

   - https://packaging.python.org/specifications/core-metadata/
   - Metadata 2.1: https://www.python.org/dev/peps/pep-0566/
   - Metadata 2.0: https://www.python.org/dev/peps/pep-0426/ (Withdrawn)
   - Metadata 1.2: https://www.python.org/dev/peps/pep-0345/
   - Metadata 1.1: https://www.python.org/dev/peps/pep-0314/
   - Metadata 1.0: https://www.python.org/dev/peps/pep-0241/

   .. py:property:: name


   .. py:property:: version


   .. py:attribute:: FILE_NAMES
      :value: ('METADATA', 'PKG-INFO')

      

   .. py:attribute:: SINGLE_USE_KEYS

      

   .. py:attribute:: MULTIPLE_USE_KEYS

      

   .. py:method:: _process_path(path, metadata_filenames)
      :staticmethod:

      Find metadata file inside dist-info folder, or check direct file.


   .. py:method:: _message_to_dict(message)
      :classmethod:

      Convert the RFC-822 headers data into a dictionary.

      `message` is an email.parser.Message instance.

      The canonical method to transform metadata fields into such a data
      structure is as follows:
        - The original key-value format should be read with
          email.parser.HeaderParser
        - All transformed keys should be reduced to lower case. Hyphens
          should be replaced with underscores, but otherwise should retain
          all other characters
        - The transformed value for any field marked with "(Multiple-use")
          should be a single list containing all the original values for the
          given key
        - The Keywords field should be converted to a list by splitting the
          original value on whitespace characters
        - The message body, if present, should be set to the value of the
          description key.
        - The result should be stored as a string-keyed dictionary.


   .. py:method:: _read_metadata(fpath)
      :classmethod:

      Read the original format which is stored as RFC-822 headers.


   .. py:method:: _get_multiple_data(keys)

      Helper method to get multiple data values by keys.

      Keys is an iterable including the preferred key in order, to include
      values of key that might have been replaced (deprecated), for example
      keys can be ['requires_dist', 'requires'], where the key 'requires' is
      deprecated and replaced by 'requires_dist'.


   .. py:method:: get_dist_requirements()

      Changed in version 2.1: The field format specification was relaxed to
      accept the syntax used by popular publishing tools.

      Each entry contains a string naming some other distutils project
      required by this distribution.

      The format of a requirement string contains from one to four parts:
        - A project name, in the same format as the Name: field. The only
          mandatory part.
        - A comma-separated list of ‘extra’ names. These are defined by the
          required project, referring to specific features which may need
          extra dependencies.
        - A version specifier. Tools parsing the format should accept
          optional parentheses around this, but tools generating it should
          not use parentheses.
        - An environment marker after a semicolon. This means that the
          requirement is only needed in the specified conditions.

      This field may be followed by an environment marker after a semicolon.

      .. rubric:: 示例

      frozenset(['pkginfo', 'PasteDeploy', 'zope.interface (>3.5.0)',
                 'pywin32 >1.0; sys_platform == "win32"'])

      Return 'Requires' if 'Requires-Dist' is empty.


   .. py:method:: get_python_requirements()

      New in version 1.2.

      This field specifies the Python version(s) that the distribution is
      guaranteed to be compatible with. Installation tools may look at this
      when picking which version of a project to install.

      The value must be in the format specified in Version specifiers.

      This field may be followed by an environment marker after a semicolon.

      .. rubric:: 示例

      frozenset(['>=3', '>2.6,!=3.0.*,!=3.1.*', '~=2.6',
                 '>=3; sys_platform == "win32"'])


   .. py:method:: get_external_requirements()

      Changed in version 2.1: The field format specification was relaxed to
      accept the syntax used by popular publishing tools.

      Each entry contains a string describing some dependency in the system
      that the distribution is to be used. This field is intended to serve
      as a hint to downstream project maintainers, and has no semantics
      which are meaningful to the distutils distribution.

      The format of a requirement string is a name of an external dependency,
      optionally followed by a version declaration within parentheses.

      This field may be followed by an environment marker after a semicolon.

      Because they refer to non-Python software releases, version numbers for
      this field are not required to conform to the format specified in PEP
      440: they should correspond to the version scheme used by the external
      dependency.

      Notice that there’s is no particular rule on the strings to be used!

      .. rubric:: 示例

      frozenset(['C', 'libpng (>=1.5)', 'make; sys_platform != "win32"'])


   .. py:method:: get_extra_provides()

      New in version 2.1.

      A string containing the name of an optional feature. Must be a valid
      Python identifier. May be used to make a dependency conditional on
      hether the optional feature has been requested.

      .. rubric:: 示例

      frozenset(['pdf', 'doc', 'test'])


   .. py:method:: get_dist_provides()

      New in version 1.2.

      Changed in version 2.1: The field format specification was relaxed to
      accept the syntax used by popular publishing tools.

      Each entry contains a string naming a Distutils project which is
      contained within this distribution. This field must include the project
      identified in the Name field, followed by the version : Name (Version).

      A distribution may provide additional names, e.g. to indicate that
      multiple projects have been bundled together. For instance, source
      distributions of the ZODB project have historically included the
      transaction project, which is now available as a separate distribution.
      Installing such a source distribution satisfies requirements for both
      ZODB and transaction.

      A distribution may also provide a “virtual” project name, which does
      not correspond to any separately-distributed project: such a name might
      be used to indicate an abstract capability which could be supplied by
      one of multiple projects. E.g., multiple projects might supply RDBMS
      bindings for use by a given ORM: each project might declare that it
      provides ORM-bindings, allowing other projects to depend only on having
      at most one of them installed.

      A version declaration may be supplied and must follow the rules
      described in Version specifiers. The distribution’s version number
      will be implied if none is specified.

      This field may be followed by an environment marker after a semicolon.

      Return `Provides` in case `Provides-Dist` is empty.


   .. py:method:: get_dist_obsolete()

      New in version 1.2.

      Changed in version 2.1: The field format specification was relaxed to
      accept the syntax used by popular publishing tools.

      Each entry contains a string describing a distutils project’s
      distribution which this distribution renders obsolete, meaning that
      the two projects should not be installed at the same time.

      Version declarations can be supplied. Version numbers must be in the
      format specified in Version specifiers [1].

      The most common use of this field will be in case a project name
      changes, e.g. Gorgon 2.3 gets subsumed into Torqued Python 1.0. When
      you install Torqued Python, the Gorgon distribution should be removed.

      This field may be followed by an environment marker after a semicolon.

      Return `Obsoletes` in case `Obsoletes-Dist` is empty.

      .. rubric:: 示例

      frozenset(['Gorgon', "OtherProject (<3.0) ; python_version == '2.7'"])

      .. rubric:: 备注

      - [1] https://packaging.python.org/specifications/version-specifiers/


   .. py:method:: get_classifiers()

      Classifiers are described in PEP 301, and the Python Package Index
      publishes a dynamic list of currently defined classifiers.

      This field may be followed by an environment marker after a semicolon.

      .. rubric:: 示例

      frozenset(['Development Status :: 4 - Beta',
                 "Environment :: Console (Text Based) ; os_name == "posix"])



.. py:function:: norm_package_name(name)


.. py:function:: pypi_name_to_conda_name(pypi_name)


.. py:function:: norm_package_version(version)

   Normalize a version by removing extra spaces and parentheses.


.. py:function:: split_spec(spec, sep)

   Split a spec by separator and return stripped start and end parts.


.. py:function:: parse_specification(spec)

   Parse a requirement from a python distribution metadata and return a
   namedtuple with name, extras, constraints, marker and url components.

   This method does not enforce strict specifications but extracts the
   information which is assumed to be *correct*. As such no errors are raised.

   .. rubric:: 示例

   PySpec(name='requests', extras=['security'], constraints='>=3.3.0',
          marker='foo >= 2.7 or bar == 1', url=''])


.. py:function:: get_site_packages_anchor_files(site_packages_path, site_packages_dir)

   Get all the anchor files for the site packages directory.


.. py:function:: get_dist_file_from_egg_link(egg_link_file, prefix_path)

   Return the egg info file path following an egg link.


.. py:function:: parse_marker(marker_string)

   Parse marker string and return a dictionary containing a marker expression.

   The dictionary will contain keys "op", "lhs" and "rhs" for non-terminals in
   the expression grammar, or strings. A string contained in quotes is to be
   interpreted as a literal string, and a string not contained in quotes is a
   variable (such as os_name).


.. py:data:: IDENTIFIER

   

.. py:data:: VERSION_IDENTIFIER

   

.. py:data:: COMPARE_OP

   

.. py:data:: MARKER_OP

   

.. py:data:: OR

   

.. py:data:: AND

   

.. py:data:: NON_SPACE

   

.. py:data:: STRING_CHUNK

   

.. py:function:: _is_literal(o)


.. py:class:: Evaluator


   This class is used to evaluate marker expressions.

   .. py:attribute:: operations

      

   .. py:method:: evaluate(expr, context)

      Evaluate a marker expression returned by the :func:`parse_requirement`
      function in the specified context.



.. py:function:: get_default_marker_context()

   Return the default context dictionary to use when parsing markers.


.. py:data:: DEFAULT_MARKER_CONTEXT

   

.. py:data:: evaluator

   

.. py:function:: interpret(marker, execution_context=None)

   Interpret a marker and return a result depending on environment.

   :param marker: The marker to interpret.
   :type marker: str
   :param execution_context: The context used for name lookup.
   :type execution_context: mapping


