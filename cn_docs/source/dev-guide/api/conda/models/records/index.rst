:py:mod:`records`
=================

.. py:module:: conda.models.records

.. autoapi-nested-parse::

   Implements the data model for conda packages.

   A PackageRecord is the record of a package present in a channel. A PackageCache is the record of a
   downloaded and cached package. A PrefixRecord is the record of a package installed into a conda
   environment.

   Object inheritance:

   .. autoapi-inheritance-diagram:: PackageRecord PackageCacheRecord PrefixRecord
      :top-classes: conda.models.records.PackageRecord
      :parts: 1



Classes
-------

.. autoapisummary::

   conda.models.records.LinkTypeField
   conda.models.records.NoarchField
   conda.models.records.TimestampField
   conda.models.records.Link
   conda.models.records._FeaturesField
   conda.models.records.ChannelField
   conda.models.records.SubdirField
   conda.models.records.FilenameField
   conda.models.records.PackageTypeField
   conda.models.records.PathData
   conda.models.records.PathDataV1
   conda.models.records.PathsData
   conda.models.records.PackageRecord
   conda.models.records.Md5Field
   conda.models.records.PackageCacheRecord
   conda.models.records.PrefixRecord




Attributes
----------

.. autoapisummary::

   conda.models.records.EMPTY_LINK


.. py:class:: LinkTypeField(enum_class, default=NULL, required=True, validation=None, in_dump=True, default_in_dump=True, nullable=False, immutable=False, aliases=())


   Bases: :py:obj:`conda.auxlib.entity.EnumField`

   Fields are doing something very similar to boxing and unboxing
   of c#/java primitives.  __set__ should take a "primitive" or "raw" value and create a "boxed"
   or "programmatically usable" value of it.  While __get__ should return the boxed value,
   dump in turn should unbox the value into a primitive or raw value.

   :param types_:
   :type types_: primitive literal or type or sequence of types
   :param default: If default is callable, it's guaranteed to return a
                   valid value at the time of Entity creation.
   :type default: any, callable, optional
   :param required:
   :type required: boolean, optional
   :param validation:
   :type validation: callable, optional
   :param dump:
   :type dump: boolean, optional

   .. py:method:: box(instance, instance_type, val)



.. py:class:: NoarchField(enum_class, default=NULL, required=True, validation=None, in_dump=True, default_in_dump=True, nullable=False, immutable=False, aliases=())


   Bases: :py:obj:`conda.auxlib.entity.EnumField`

   Fields are doing something very similar to boxing and unboxing
   of c#/java primitives.  __set__ should take a "primitive" or "raw" value and create a "boxed"
   or "programmatically usable" value of it.  While __get__ should return the boxed value,
   dump in turn should unbox the value into a primitive or raw value.

   :param types_:
   :type types_: primitive literal or type or sequence of types
   :param default: If default is callable, it's guaranteed to return a
                   valid value at the time of Entity creation.
   :type default: any, callable, optional
   :param required:
   :type required: boolean, optional
   :param validation:
   :type validation: callable, optional
   :param dump:
   :type dump: boolean, optional

   .. py:method:: box(instance, instance_type, val)



.. py:class:: TimestampField


   Bases: :py:obj:`conda.auxlib.entity.NumberField`

   Fields are doing something very similar to boxing and unboxing
   of c#/java primitives.  __set__ should take a "primitive" or "raw" value and create a "boxed"
   or "programmatically usable" value of it.  While __get__ should return the boxed value,
   dump in turn should unbox the value into a primitive or raw value.

   :param types_:
   :type types_: primitive literal or type or sequence of types
   :param default: If default is callable, it's guaranteed to return a
                   valid value at the time of Entity creation.
   :type default: any, callable, optional
   :param required:
   :type required: boolean, optional
   :param validation:
   :type validation: callable, optional
   :param dump:
   :type dump: boolean, optional

   .. py:method:: _make_seconds(val)
      :staticmethod:


   .. py:method:: _make_milliseconds(val)
      :staticmethod:


   .. py:method:: box(instance, instance_type, val)


   .. py:method:: dump(instance, instance_type, val)


   .. py:method:: __get__(instance, instance_type)



.. py:class:: Link(**kwargs)


   Bases: :py:obj:`conda.auxlib.entity.DictSafeMixin`, :py:obj:`conda.auxlib.entity.Entity`

   .. py:attribute:: source

      

   .. py:attribute:: type

      


.. py:data:: EMPTY_LINK

   

.. py:class:: _FeaturesField(**kwargs)


   Bases: :py:obj:`conda.auxlib.entity.ListField`

   Fields are doing something very similar to boxing and unboxing
   of c#/java primitives.  __set__ should take a "primitive" or "raw" value and create a "boxed"
   or "programmatically usable" value of it.  While __get__ should return the boxed value,
   dump in turn should unbox the value into a primitive or raw value.

   :param types_:
   :type types_: primitive literal or type or sequence of types
   :param default: If default is callable, it's guaranteed to return a
                   valid value at the time of Entity creation.
   :type default: any, callable, optional
   :param required:
   :type required: boolean, optional
   :param validation:
   :type validation: callable, optional
   :param dump:
   :type dump: boolean, optional

   .. py:method:: box(instance, instance_type, val)


   .. py:method:: dump(instance, instance_type, val)



.. py:class:: ChannelField(aliases=())


   Bases: :py:obj:`conda.auxlib.entity.ComposableField`

   Fields are doing something very similar to boxing and unboxing
   of c#/java primitives.  __set__ should take a "primitive" or "raw" value and create a "boxed"
   or "programmatically usable" value of it.  While __get__ should return the boxed value,
   dump in turn should unbox the value into a primitive or raw value.

   :param types_:
   :type types_: primitive literal or type or sequence of types
   :param default: If default is callable, it's guaranteed to return a
                   valid value at the time of Entity creation.
   :type default: any, callable, optional
   :param required:
   :type required: boolean, optional
   :param validation:
   :type validation: callable, optional
   :param dump:
   :type dump: boolean, optional

   .. py:method:: dump(instance, instance_type, val)


   .. py:method:: __get__(instance, instance_type)



.. py:class:: SubdirField


   Bases: :py:obj:`conda.auxlib.entity.StringField`

   Fields are doing something very similar to boxing and unboxing
   of c#/java primitives.  __set__ should take a "primitive" or "raw" value and create a "boxed"
   or "programmatically usable" value of it.  While __get__ should return the boxed value,
   dump in turn should unbox the value into a primitive or raw value.

   :param types_:
   :type types_: primitive literal or type or sequence of types
   :param default: If default is callable, it's guaranteed to return a
                   valid value at the time of Entity creation.
   :type default: any, callable, optional
   :param required:
   :type required: boolean, optional
   :param validation:
   :type validation: callable, optional
   :param dump:
   :type dump: boolean, optional

   .. py:method:: __get__(instance, instance_type)



.. py:class:: FilenameField(aliases=())


   Bases: :py:obj:`conda.auxlib.entity.StringField`

   Fields are doing something very similar to boxing and unboxing
   of c#/java primitives.  __set__ should take a "primitive" or "raw" value and create a "boxed"
   or "programmatically usable" value of it.  While __get__ should return the boxed value,
   dump in turn should unbox the value into a primitive or raw value.

   :param types_:
   :type types_: primitive literal or type or sequence of types
   :param default: If default is callable, it's guaranteed to return a
                   valid value at the time of Entity creation.
   :type default: any, callable, optional
   :param required:
   :type required: boolean, optional
   :param validation:
   :type validation: callable, optional
   :param dump:
   :type dump: boolean, optional

   .. py:method:: __get__(instance, instance_type)



.. py:class:: PackageTypeField


   Bases: :py:obj:`conda.auxlib.entity.EnumField`

   Fields are doing something very similar to boxing and unboxing
   of c#/java primitives.  __set__ should take a "primitive" or "raw" value and create a "boxed"
   or "programmatically usable" value of it.  While __get__ should return the boxed value,
   dump in turn should unbox the value into a primitive or raw value.

   :param types_:
   :type types_: primitive literal or type or sequence of types
   :param default: If default is callable, it's guaranteed to return a
                   valid value at the time of Entity creation.
   :type default: any, callable, optional
   :param required:
   :type required: boolean, optional
   :param validation:
   :type validation: callable, optional
   :param dump:
   :type dump: boolean, optional

   .. py:method:: __get__(instance, instance_type)



.. py:class:: PathData(**kwargs)


   Bases: :py:obj:`conda.auxlib.entity.Entity`

   .. py:property:: path


   .. py:attribute:: _path

      

   .. py:attribute:: prefix_placeholder

      

   .. py:attribute:: file_mode

      

   .. py:attribute:: no_link

      

   .. py:attribute:: path_type

      


.. py:class:: PathDataV1(**kwargs)


   Bases: :py:obj:`PathData`

   .. py:attribute:: sha256

      

   .. py:attribute:: size_in_bytes

      

   .. py:attribute:: inode_paths

      

   .. py:attribute:: sha256_in_prefix

      


.. py:class:: PathsData(**kwargs)


   Bases: :py:obj:`conda.auxlib.entity.Entity`

   .. py:attribute:: paths_version

      

   .. py:attribute:: paths

      


.. py:class:: PackageRecord(*args, **kwargs)


   Bases: :py:obj:`conda.auxlib.entity.DictSafeMixin`, :py:obj:`conda.auxlib.entity.Entity`

   Representation of a concrete package archive (tarball or .conda file).

   It captures all the relevant information about a given package archive, including its source,
   in the following attributes.

   Note that there are two subclasses, :class:`PrefixRecord` and
   :class:`PackageCacheRecord`. These capture the same information, but are augmented with
   additional information relevant for these two sources of packages.

   Further note that :class:`PackageRecord` makes use of its :attr:`_pkey`
   for comparison and hash generation.
   This means that for common operations, like comparisons between :class:`PackageRecord` s
   and reference of :class:`PackageRecord` s in mappings, _different_ objects appear identical.
   The fields taken into account are marked in the following list of attributes.
   The subclasses do not add further attributes to the :attr:`_pkey`.

   .. py:property:: schannel

      The canonical name of the channel of this package.

      Part of the :attr:`_pkey`.

      :type: str

   .. py:property:: _pkey

      The components of the PackageRecord that are used for comparison and hashing.

      The :attr:`_pkey` is a tuple made up of the following fields of the :class:`PackageRecord`.
      Two :class:`PackageRecord` s test equal if their respective :attr:`_pkey` s are equal.
      The hash of the :class:`PackageRecord` (important for dictionary access) is the hash of the :attr:`_pkey`.

      The included fields are:

      * :attr:`schannel`
      * :attr:`subdir`
      * :attr:`name`
      * :attr:`version`
      * :attr:`build_number`
      * :attr:`build`
      * :attr:`fn` only if :ref:`separate_format_cache <auto-config-reference>` is set to true (default: false)

      :type: tuple

   .. py:property:: is_unmanageable


   .. py:property:: combined_depends


   .. py:property:: namekey


   .. py:attribute:: name

      

   .. py:attribute:: version

      

   .. py:attribute:: build

      

   .. py:attribute:: build_number

      

   .. py:attribute:: channel

      

   .. py:attribute:: subdir

      

   .. py:attribute:: fn

      

   .. py:attribute:: md5

      

   .. py:attribute:: legacy_bz2_md5

      

   .. py:attribute:: legacy_bz2_size

      

   .. py:attribute:: url

      

   .. py:attribute:: sha256

      

   .. py:attribute:: arch

      

   .. py:attribute:: platform

      

   .. py:attribute:: depends

      

   .. py:attribute:: constrains

      

   .. py:attribute:: track_features

      

   .. py:attribute:: features

      

   .. py:attribute:: noarch

      

   .. py:attribute:: preferred_env

      

   .. py:attribute:: python_site_packages_path

      

   .. py:attribute:: license

      

   .. py:attribute:: license_family

      

   .. py:attribute:: package_type

      

   .. py:attribute:: timestamp

      

   .. py:attribute:: date

      

   .. py:attribute:: size

      

   .. py:attribute:: metadata
      :type: set[str]

      

   .. py:method:: __hash__()

      Return hash(self).


   .. py:method:: __eq__(other)

      Return self==value.


   .. py:method:: dist_str(canonical_name: bool = True) -> str


   .. py:method:: dist_fields_dump()


   .. py:method:: __str__()

      Return str(self).


   .. py:method:: to_match_spec()


   .. py:method:: to_simple_match_spec()


   .. py:method:: record_id()


   .. py:method:: feature(feature_name) -> PackageRecord
      :classmethod:


   .. py:method:: virtual_package(name: str, version: str | None = None, build_string: str | None = None) -> PackageRecord
      :classmethod:

      Create a virtual package record.

      :param name: The name of the virtual package.
      :param version: The version of the virtual package, defaults to "0".
      :param build_string: The build string of the virtual package, defaults to "0".
      :return: A PackageRecord representing the virtual package.



.. py:class:: Md5Field


   Bases: :py:obj:`conda.auxlib.entity.StringField`

   Fields are doing something very similar to boxing and unboxing
   of c#/java primitives.  __set__ should take a "primitive" or "raw" value and create a "boxed"
   or "programmatically usable" value of it.  While __get__ should return the boxed value,
   dump in turn should unbox the value into a primitive or raw value.

   :param types_:
   :type types_: primitive literal or type or sequence of types
   :param default: If default is callable, it's guaranteed to return a
                   valid value at the time of Entity creation.
   :type default: any, callable, optional
   :param required:
   :type required: boolean, optional
   :param validation:
   :type validation: callable, optional
   :param dump:
   :type dump: boolean, optional

   .. py:method:: __get__(instance, instance_type)



.. py:class:: PackageCacheRecord(*args, **kwargs)


   Bases: :py:obj:`PackageRecord`

   Representation of a package that has been downloaded or unpacked in the local package cache.

   Specialization of :class:`PackageRecord` that adds information for packages that exist in the
   local package cache, either as the downloaded package file, or unpacked in its own package dir,
   or both.

   Note that this class does not add new fields to the :attr:`PackageRecord._pkey` so that a pure
   :class:`PackageRecord` object that has the same ``_pkey`` fields as a different
   :class:`PackageCacheRecord` object (or, indeed, a :class:`PrefixRecord` object) will be considered
   equal and will produce the same hash.

   .. py:property:: is_fetched

      Whether the package file exists locally.

      :type: bool

   .. py:property:: is_extracted

      Whether the package has been extracted locally.

      :type: bool

   .. py:property:: tarball_basename

      The basename of the local package file.

      :type: str

   .. py:attribute:: package_tarball_full_path

      

   .. py:attribute:: extracted_package_dir

      

   .. py:attribute:: md5

      

   .. py:method:: _calculate_md5sum()



.. py:class:: PrefixRecord(*args, **kwargs)


   Bases: :py:obj:`PackageRecord`

   Representation of a package that is installed in a local conda environmnet.

   Specialization of :class:`PackageRecord` that adds information for packages that are installed
   in a local conda environment or prefix.

   Note that this class does not add new fields to the :attr:`PackageRecord._pkey` so that a pure
   :class:`PackageRecord` object that has the same ``_pkey`` fields as a different
   :class:`PrefixRecord` object (or, indeed, a :class:`PackageCacheRecord` object) will be considered
   equal and will produce the same hash.

   Objects of this class are generally constructed from metadata in json files inside `$prefix/conda-meta`.

   .. py:attribute:: package_tarball_full_path

      

   .. py:attribute:: extracted_package_dir

      

   .. py:attribute:: files

      

   .. py:attribute:: paths_data

      

   .. py:attribute:: link

      

   .. py:attribute:: requested_spec

      

   .. py:attribute:: auth

      


