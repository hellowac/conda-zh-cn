:py:mod:`version`
=================

.. py:module:: conda.models.version

.. autoapi-nested-parse::

   Implements the version spec with parsing and comparison logic.

   Object inheritance:

   .. autoapi-inheritance-diagram:: BaseSpec VersionSpec BuildNumberMatch
      :top-classes: conda.models.version.BaseSpec
      :parts: 1



Classes
-------

.. autoapisummary::

   conda.models.version.SingleStrArgCachingType
   conda.models.version.VersionOrder
   conda.models.version.BaseSpec
   conda.models.version.VersionSpec
   conda.models.version.BuildNumberMatch



Functions
---------

.. autoapisummary::

   conda.models.version.normalized_version
   conda.models.version.ver_eval
   conda.models.version.treeify
   conda.models.version.untreeify
   conda.models.version.compatible_release_operator



Attributes
----------

.. autoapisummary::

   conda.models.version.version_check_re
   conda.models.version.version_split_re
   conda.models.version.version_cache
   conda.models.version.VSPEC_TOKENS
   conda.models.version.version_relation_re
   conda.models.version.regex_split_re
   conda.models.version.OPERATOR_MAP
   conda.models.version.OPERATOR_START
   conda.models.version.VersionMatch


.. py:function:: normalized_version(version: str) -> VersionOrder

   Parse a version string and return VersionOrder object.


.. py:function:: ver_eval(vtest, spec)


.. py:data:: version_check_re

   

.. py:data:: version_split_re

   

.. py:data:: version_cache

   

.. py:class:: SingleStrArgCachingType


   Bases: :py:obj:`type`

   .. py:method:: __call__(arg)

      Call self as a function.



.. py:class:: VersionOrder(vstr: str)


   Implement an order relation between version strings.

   Version strings can contain the usual alphanumeric characters
   (A-Za-z0-9), separated into components by dots and underscores. Empty
   segments (i.e. two consecutive dots, a leading/trailing underscore)
   are not permitted. An optional epoch number - an integer
   followed by '!' - can proceed the actual version string
   (this is useful to indicate a change in the versioning
   scheme itself). Version comparison is case-insensitive.

   Conda supports six types of version strings:
   * Release versions contain only integers, e.g. '1.0', '2.3.5'.
   * Pre-release versions use additional letters such as 'a' or 'rc',
     for example '1.0a1', '1.2.beta3', '2.3.5rc3'.
   * Development versions are indicated by the string 'dev',
     for example '1.0dev42', '2.3.5.dev12'.
   * Post-release versions are indicated by the string 'post',
     for example '1.0post1', '2.3.5.post2'.
   * Tagged versions have a suffix that specifies a particular
     property of interest, e.g. '1.1.parallel'. Tags can be added
     to any of the preceding four types. As far as sorting is concerned,
     tags are treated like strings in pre-release versions.
   * An optional local version string separated by '+' can be appended
     to the main (upstream) version string. It is only considered
     in comparisons when the main versions are equal, but otherwise
     handled in exactly the same manner.

   To obtain a predictable version ordering, it is crucial to keep the
   version number scheme of a given package consistent over time.
   Specifically,
   * version strings should always have the same number of components
     (except for an optional tag suffix or local version string),
   * letters/strings indicating non-release versions should always
     occur at the same position.

   Before comparison, version strings are parsed as follows:
   * They are first split into epoch, version number, and local version
     number at '!' and '+' respectively. If there is no '!', the epoch is
     set to 0. If there is no '+', the local version is empty.
   * The version part is then split into components at '.' and '_'.
   * Each component is split again into runs of numerals and non-numerals
   * Subcomponents containing only numerals are converted to integers.
   * Strings are converted to lower case, with special treatment for 'dev'
     and 'post'.
   * When a component starts with a letter, the fillvalue 0 is inserted
     to keep numbers and strings in phase, resulting in '1.1.a1' == 1.1.0a1'.
   * The same is repeated for the local version part.

   .. rubric:: Examples

   1.2g.beta15.rc  =>  [[0], [1], [2, 'g'], [0, 'beta', 15], [0, 'rc']]
   1!2.15.1_ALPHA  =>  [[1], [2], [15], [1, '_alpha']]

   The resulting lists are compared lexicographically, where the following
   rules are applied to each pair of corresponding subcomponents:
   * integers are compared numerically
   * strings are compared lexicographically, case-insensitive
   * strings are smaller than integers, except
   * 'dev' versions are smaller than all corresponding versions of other types
   * 'post' versions are greater than all corresponding versions of other types
   * if a subcomponent has no correspondent, the missing correspondent is
     treated as integer 0 to ensure '1.1' == '1.1.0'.

   The resulting order is:
          0.4
        < 0.4.0
        < 0.4.1.rc
       == 0.4.1.RC   # case-insensitive comparison
        < 0.4.1
        < 0.5a1
        < 0.5b3
        < 0.5C1      # case-insensitive comparison
        < 0.5
        < 0.9.6
        < 0.960923
        < 1.0
        < 1.1dev1    # special case 'dev'
        < 1.1_       # appended underscore is special case for openssl-like versions
        < 1.1a1
        < 1.1.0dev1  # special case 'dev'
       == 1.1.dev1   # 0 is inserted before string
        < 1.1.a1
        < 1.1.0rc1
        < 1.1.0
       == 1.1
        < 1.1.0post1 # special case 'post'
       == 1.1.post1  # 0 is inserted before string
        < 1.1post1   # special case 'post'
        < 1996.07.12
        < 1!0.4.1    # epoch increased
        < 1!3.1.1.6
        < 2!0.4.1    # epoch increased again

   Some packages (most notably openssl) have incompatible version conventions.
   In particular, openssl interprets letters as version counters rather than
   pre-release identifiers. For openssl, the relation

     1.0.1 < 1.0.1a  =>  False  # should be true for openssl

   holds, whereas conda packages use the opposite ordering. You can work-around
   this problem by appending an underscore to plain version numbers:

     1.0.1_ < 1.0.1a =>  True   # ensure correct ordering for openssl

   .. py:attribute:: _cache_

      

   .. py:method:: __str__() -> str

      Return str(self).


   .. py:method:: __repr__() -> str

      Return repr(self).


   .. py:method:: _eq(t1: list[str], t2: list[str]) -> bool


   .. py:method:: __eq__(other: object) -> bool

      Return self==value.


   .. py:method:: startswith(other: object) -> bool


   .. py:method:: __ne__(other: object) -> bool

      Return self!=value.


   .. py:method:: __lt__(other: object) -> bool

      Return self<value.


   .. py:method:: __gt__(other: object) -> bool

      Return self>value.


   .. py:method:: __le__(other: object) -> bool

      Return self<=value.


   .. py:method:: __ge__(other: object) -> bool

      Return self>=value.



.. py:data:: VSPEC_TOKENS
   :value: '\\s*\\^[^$]*[$]|\\s*[()|,]|[^()|,]+'

   

.. py:function:: treeify(spec_str)

   .. rubric:: Examples

   >>> treeify("1.2.3")
   '1.2.3'
   >>> treeify("1.2.3,>4.5.6")
   (',', '1.2.3', '>4.5.6')
   >>> treeify("1.2.3,4.5.6|<=7.8.9")
   ('|', (',', '1.2.3', '4.5.6'), '<=7.8.9')
   >>> treeify("(1.2.3|4.5.6),<=7.8.9")
   (',', ('|', '1.2.3', '4.5.6'), '<=7.8.9')
   >>> treeify("((1.5|((1.6|1.7), 1.8), 1.9 |2.0))|2.1")
   ('|', '1.5', (',', ('|', '1.6', '1.7'), '1.8', '1.9'), '2.0', '2.1')
   >>> treeify("1.5|(1.6|1.7),1.8,1.9|2.0|2.1")
   ('|', '1.5', (',', ('|', '1.6', '1.7'), '1.8', '1.9'), '2.0', '2.1')


.. py:function:: untreeify(spec, _inand=False, depth=0)

   .. rubric:: Examples

   >>> untreeify('1.2.3')
   '1.2.3'
   >>> untreeify((',', '1.2.3', '>4.5.6'))
   '1.2.3,>4.5.6'
   >>> untreeify(('|', (',', '1.2.3', '4.5.6'), '<=7.8.9'))
   '(1.2.3,4.5.6)|<=7.8.9'
   >>> untreeify((',', ('|', '1.2.3', '4.5.6'), '<=7.8.9'))
   '(1.2.3|4.5.6),<=7.8.9'
   >>> untreeify(('|', '1.5', (',', ('|', '1.6', '1.7'), '1.8', '1.9'), '2.0', '2.1'))
   '1.5|((1.6|1.7),1.8,1.9)|2.0|2.1'


.. py:function:: compatible_release_operator(x, y)


.. py:data:: version_relation_re

   

.. py:data:: regex_split_re

   

.. py:data:: OPERATOR_MAP

   

.. py:data:: OPERATOR_START

   

.. py:class:: BaseSpec(spec_str, matcher, is_exact)


   .. py:property:: spec


   .. py:property:: raw_value


   .. py:property:: exact_value


   .. py:method:: is_exact()


   .. py:method:: __eq__(other)

      Return self==value.


   .. py:method:: __ne__(other)

      Return self!=value.


   .. py:method:: __hash__()

      Return hash(self).


   .. py:method:: __str__()

      Return str(self).


   .. py:method:: __repr__()

      Return repr(self).


   .. py:method:: merge(other)
      :abstractmethod:


   .. py:method:: regex_match(spec_str)


   .. py:method:: operator_match(spec_str)


   .. py:method:: any_match(spec_str)


   .. py:method:: all_match(spec_str)


   .. py:method:: exact_match(spec_str)


   .. py:method:: always_true_match(spec_str)



.. py:class:: VersionSpec(vspec)


   Bases: :py:obj:`BaseSpec`

   .. py:attribute:: _cache_

      

   .. py:method:: get_matcher(vspec)


   .. py:method:: merge(other)


   .. py:method:: union(other)



.. py:data:: VersionMatch

   

.. py:class:: BuildNumberMatch(vspec)


   Bases: :py:obj:`BaseSpec`

   .. py:property:: exact_value
      :type: int | None


   .. py:attribute:: _cache_

      

   .. py:method:: get_matcher(vspec)


   .. py:method:: merge(other)


   .. py:method:: union(other)


   .. py:method:: __str__()

      Return str(self).


   .. py:method:: __repr__()

      Return repr(self).



