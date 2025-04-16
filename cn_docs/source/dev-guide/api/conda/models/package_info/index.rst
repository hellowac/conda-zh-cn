:py:mod:`package_info`
======================

.. py:module:: conda.models.package_info

.. autoapi-nested-parse::

   (Legacy) Low-level implementation of a PackageRecord.



Classes
-------

.. autoapisummary::

   conda.models.package_info.NoarchField
   conda.models.package_info.Noarch
   conda.models.package_info.PreferredEnv
   conda.models.package_info.PackageMetadata
   conda.models.package_info.PackageInfo




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



.. py:class:: Noarch(**kwargs)


   Bases: :py:obj:`conda.auxlib.entity.Entity`

   .. py:attribute:: type

      

   .. py:attribute:: entry_points

      


.. py:class:: PreferredEnv(**kwargs)


   Bases: :py:obj:`conda.auxlib.entity.Entity`

   .. py:attribute:: name

      

   .. py:attribute:: executable_paths

      

   .. py:attribute:: softlink_paths

      


.. py:class:: PackageMetadata(**kwargs)


   Bases: :py:obj:`conda.auxlib.entity.Entity`

   .. py:attribute:: package_metadata_version

      

   .. py:attribute:: noarch

      

   .. py:attribute:: preferred_env

      


.. py:class:: PackageInfo(**kwargs)


   Bases: :py:obj:`conda.auxlib.entity.ImmutableEntity`

   .. py:property:: name


   .. py:property:: version


   .. py:property:: build


   .. py:property:: build_number


   .. py:attribute:: extracted_package_dir

      

   .. py:attribute:: package_tarball_full_path

      

   .. py:attribute:: channel

      

   .. py:attribute:: repodata_record

      

   .. py:attribute:: url

      

   .. py:attribute:: icondata

      

   .. py:attribute:: package_metadata

      

   .. py:attribute:: paths_data

      

   .. py:method:: dist_str()



