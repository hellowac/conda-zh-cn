:py:mod:`match_spec`
====================

.. py:module:: conda.models.match_spec

.. autoapi-nested-parse::

   Implements the query language for conda packages (a.k.a, MatchSpec).

   The MatchSpec is the conda package specification (e.g. `conda==23.3`, `python<3.7`,
   `cryptography * *_0`) and is used to communicate the desired packages to install.



Classes
-------

.. autoapisummary::

   conda.models.match_spec.MatchSpecType
   conda.models.match_spec.MatchSpec
   conda.models.match_spec.MatchInterface
   conda.models.match_spec._StrMatchMixin
   conda.models.match_spec.ExactStrMatch
   conda.models.match_spec.ExactLowerStrMatch
   conda.models.match_spec.GlobStrMatch
   conda.models.match_spec.GlobLowerStrMatch
   conda.models.match_spec.SplitStrMatch
   conda.models.match_spec.FeatureMatch
   conda.models.match_spec.ChannelMatch
   conda.models.match_spec.CaseInsensitiveStrMatch



Functions
---------

.. autoapisummary::

   conda.models.match_spec._parse_version_plus_build
   conda.models.match_spec._parse_legacy_dist
   conda.models.match_spec._parse_channel
   conda.models.match_spec._parse_spec_str



Attributes
----------

.. autoapisummary::

   conda.models.match_spec._PARSE_CACHE
   conda.models.match_spec._implementors


.. py:class:: MatchSpecType


   Bases: :py:obj:`type`

   .. py:method:: __call__(spec_arg=None, **kwargs)

      Call self as a function.



.. py:class:: MatchSpec(optional=False, target=None, **kwargs)


   The query language for conda packages.

   Any of the fields that comprise a :class:`PackageRecord` can be used to compose a
   :class:`MatchSpec`.

   :class:`MatchSpec` can be composed with keyword arguments, where keys are any of the
   attributes of :class:`PackageRecord`.  Values for keyword arguments are the exact values the
   attribute should match against.  Many fields can also be matched against non-exact values--by
   including wildcard `*` and `>`/`<` ranges--where supported.  Any non-specified field is
   the equivalent of a full wildcard match.

   :class:`MatchSpec` can also be composed using a single positional argument, with optional
   keyword arguments.  Keyword arguments also override any conflicting information provided in
   the positional argument.  The positional argument can be either an existing :class:`MatchSpec`
   instance or a string.  Conda has historically supported more than one string representation
   for equivalent :class:`MatchSpec` queries.  This :class:`MatchSpec` should accept any existing
   valid spec string, and correctly compose a :class:`MatchSpec` instance.

   A series of rules are now followed for creating the canonical string representation of a
   :class:`MatchSpec` instance.  The canonical string representation can generically be
   represented by

       (channel(/subdir):(namespace):)name(version(build))[key1=value1,key2=value2]

   where `()` indicate optional fields.  The rules for constructing a canonical string
   representation are:

   1. `name` (i.e. "package name") is required, but its value can be '*'.  Its position is always
      outside the key-value brackets.
   2. If `version` is an exact version, it goes outside the key-value brackets and is prepended
      by `==`. If `version` is a "fuzzy" value (e.g. `1.11.*`), it goes outside the key-value
      brackets with the `.*` left off and is prepended by `=`.  Otherwise `version` is included
      inside key-value brackets.
   3. If `version` is an exact version, and `build` is an exact value, `build` goes outside
      key-value brackets prepended by a `=`.  Otherwise, `build` goes inside key-value brackets.
      `build_string` is an alias for `build`.
   4. The `namespace` position is being held for a future conda feature.
   5. If `channel` is included and is an exact value, a `::` separator is ued between `channel`
      and `name`.  `channel` can either be a canonical channel name or a channel url.  In the
      canonical string representation, the canonical channel name will always be used.
   6. If `channel` is an exact value and `subdir` is an exact value, `subdir` is appended to
      `channel` with a `/` separator.  Otherwise, `subdir` is included in the key-value brackets.
   7. Key-value brackets can be delimited by comma, space, or comma+space.  Value can optionally
      be wrapped in single or double quotes, but must be wrapped if `value` contains a comma,
      space, or equal sign.  The canonical format uses comma delimiters and single quotes.
   8. When constructing a :class:`MatchSpec` instance from a string, any key-value pair given
      inside the key-value brackets overrides any matching parameter given outside the brackets.

   When :class:`MatchSpec` attribute values are simple strings, the are interpreted using the
   following conventions:

     - If the string begins with `^` and ends with `$`, it is converted to a regex.
     - If the string contains an asterisk (`*`), it is transformed from a glob to a regex.
     - Otherwise, an exact match to the string is sought.


   .. rubric:: Examples

   >>> str(MatchSpec(name='foo', build='py2*', channel='conda-forge'))
   'conda-forge::foo[build=py2*]'
   >>> str(MatchSpec('foo 1.0 py27_0'))
   'foo==1.0=py27_0'
   >>> str(MatchSpec('foo=1.0=py27_0'))
   'foo==1.0=py27_0'
   >>> str(MatchSpec('conda-forge::foo[version=1.0.*]'))
   'conda-forge::foo=1.0'
   >>> str(MatchSpec('conda-forge/linux-64::foo>=1.0'))
   "conda-forge/linux-64::foo[version='>=1.0']"
   >>> str(MatchSpec('*/linux-64::foo>=1.0'))
   "foo[subdir=linux-64,version='>=1.0']"

   To fully-specify a package with a full, exact spec, the fields
     - channel
     - subdir
     - name
     - version
     - build
   must be given as exact values.  In the future, the namespace field will be added to this list.
   Alternatively, an exact spec is given by '*[md5=12345678901234567890123456789012]'
   or '*[sha256=f453db4ffe2271ec492a2913af4e61d4a6c118201f07de757df0eff769b65d2e]'.

   .. py:property:: is_name_only_spec


   .. py:property:: optional


   .. py:property:: target


   .. py:property:: original_spec_str


   .. py:property:: name


   .. py:property:: strictness


   .. py:property:: spec


   .. py:property:: version


   .. py:property:: fn


   .. py:attribute:: FIELD_NAMES
      :value: ('channel', 'subdir', 'name', 'version', 'build', 'build_number', 'track_features', 'features',...

      

   .. py:attribute:: FIELD_NAMES_SET

      

   .. py:attribute:: _MATCHER_CACHE

      

   .. py:method:: from_dist_str(dist_str)
      :classmethod:


   .. py:method:: get_exact_value(field_name)


   .. py:method:: get_raw_value(field_name)


   .. py:method:: get(field_name, default=None)


   .. py:method:: dist_str()


   .. py:method:: match(rec)

      Accepts a `PackageRecord` or a dict, and matches can pull from any field
      in that record.  Returns True for a match, and False for no match.


   .. py:method:: _match_individual(record, field_name, match_component)


   .. py:method:: _is_simple()


   .. py:method:: _is_single()


   .. py:method:: _to_filename_do_not_use()


   .. py:method:: __repr__()

      Return repr(self).


   .. py:method:: __str__()

      Return str(self).


   .. py:method:: __json__()


   .. py:method:: conda_build_form()


   .. py:method:: __eq__(other)

      Return self==value.


   .. py:method:: __hash__()

      Return hash(self).


   .. py:method:: _hash_key()


   .. py:method:: __contains__(field)


   .. py:method:: _build_components(**kwargs)


   .. py:method:: _make_component(field_name, value)
      :staticmethod:


   .. py:method:: merge(match_specs, union=False)
      :classmethod:


   .. py:method:: union(match_specs)
      :classmethod:


   .. py:method:: _merge(other, union=False)



.. py:function:: _parse_version_plus_build(v_plus_b)

   This should reliably pull the build string out of a version + build string combo.
   .. rubric:: Examples

   >>> _parse_version_plus_build("=1.2.3 0")
   ('=1.2.3', '0')
   >>> _parse_version_plus_build("1.2.3=0")
   ('1.2.3', '0')
   >>> _parse_version_plus_build(">=1.0 , < 2.0 py34_0")
   ('>=1.0,<2.0', 'py34_0')
   >>> _parse_version_plus_build(">=1.0 , < 2.0 =py34_0")
   ('>=1.0,<2.0', 'py34_0')
   >>> _parse_version_plus_build("=1.2.3 ")
   ('=1.2.3', None)
   >>> _parse_version_plus_build(">1.8,<2|==1.7")
   ('>1.8,<2|==1.7', None)
   >>> _parse_version_plus_build("* openblas_0")
   ('*', 'openblas_0')
   >>> _parse_version_plus_build("* *")
   ('*', '*')


.. py:function:: _parse_legacy_dist(dist_str)

   .. rubric:: Examples

   >>> _parse_legacy_dist("_license-1.1-py27_1.tar.bz2")
   ('_license', '1.1', 'py27_1')
   >>> _parse_legacy_dist("_license-1.1-py27_1")
   ('_license', '1.1', 'py27_1')


.. py:function:: _parse_channel(channel_val)


.. py:data:: _PARSE_CACHE

   

.. py:function:: _parse_spec_str(spec_str)


.. py:class:: MatchInterface(value)


   .. py:property:: raw_value


   .. py:property:: exact_value
      :abstractmethod:

      If the match value is an exact specification, returns the value.
      Otherwise returns None.

   .. py:method:: match(other)
      :abstractmethod:


   .. py:method:: matches(value)


   .. py:method:: merge(other)


   .. py:method:: union(other)



.. py:class:: _StrMatchMixin


   .. py:property:: exact_value


   .. py:method:: __str__()

      Return str(self).


   .. py:method:: __repr__()

      Return repr(self).


   .. py:method:: __eq__(other)

      Return self==value.


   .. py:method:: __hash__()

      Return hash(self).



.. py:class:: ExactStrMatch(value)


   Bases: :py:obj:`_StrMatchMixin`, :py:obj:`MatchInterface`

   .. py:attribute:: __slots__
      :value: ('_raw_value',)

      

   .. py:method:: match(other)



.. py:class:: ExactLowerStrMatch(value)


   Bases: :py:obj:`ExactStrMatch`

   .. py:method:: match(other)



.. py:class:: GlobStrMatch(value)


   Bases: :py:obj:`_StrMatchMixin`, :py:obj:`MatchInterface`

   .. py:property:: exact_value

      If the match value is an exact specification, returns the value.
      Otherwise returns None.

   .. py:property:: matches_all


   .. py:attribute:: __slots__
      :value: ('_raw_value', '_re_match')

      

   .. py:method:: match(other)


   .. py:method:: merge(other)



.. py:class:: GlobLowerStrMatch(value)


   Bases: :py:obj:`GlobStrMatch`


.. py:class:: SplitStrMatch(value)


   Bases: :py:obj:`MatchInterface`

   .. py:property:: exact_value

      If the match value is an exact specification, returns the value.
      Otherwise returns None.

   .. py:attribute:: __slots__
      :value: ('_raw_value',)

      

   .. py:method:: _convert(value)


   .. py:method:: match(other)


   .. py:method:: __repr__()

      Return repr(self).


   .. py:method:: __str__()

      Return str(self).


   .. py:method:: __eq__(other)

      Return self==value.


   .. py:method:: __hash__()

      Return hash(self).



.. py:class:: FeatureMatch(value)


   Bases: :py:obj:`MatchInterface`

   .. py:property:: exact_value

      If the match value is an exact specification, returns the value.
      Otherwise returns None.

   .. py:attribute:: __slots__
      :value: ('_raw_value',)

      

   .. py:method:: _convert(value)


   .. py:method:: match(other)


   .. py:method:: __repr__()

      Return repr(self).


   .. py:method:: __str__()

      Return str(self).


   .. py:method:: __eq__(other)

      Return self==value.


   .. py:method:: __hash__()

      Return hash(self).



.. py:class:: ChannelMatch(value)


   Bases: :py:obj:`GlobStrMatch`

   .. py:method:: match(other)


   .. py:method:: __str__()

      Return str(self).


   .. py:method:: __repr__()

      Return repr(self).



.. py:class:: CaseInsensitiveStrMatch(value)


   Bases: :py:obj:`GlobLowerStrMatch`

   .. py:method:: match(other)



.. py:data:: _implementors

   

