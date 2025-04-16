:py:mod:`entity`
================

.. py:module:: conda.auxlib.entity

.. autoapi-nested-parse::

   This module provides serializable, validatable, type-enforcing domain objects and data
   transfer objects. It has many of the same motivations as the python
   `Marshmallow <http://marshmallow.readthedocs.org/en/latest/why.html>`_ package. It is most
   similar to `Schematics <http://schematics.readthedocs.io/>`_.

   ========
   Tutorial
   ========

   Chapter 1: Entity and Field Basics
   ----------------------------------

       >>> class Color(Enum):
       ...     blue = 0
       ...     black = 1
       ...     red = 2
       >>> class Car(Entity):
       ...     weight = NumberField(required=False)
       ...     wheels = IntField(default=4, validation=lambda x: 3 <= x <= 4)
       ...     color = EnumField(Color)

       >>> # create a new car object
       >>> car = Car(color=Color.blue, weight=4242.46)
       >>> car
       Car(weight=4242.46, color=0)

       >>> # it has 4 wheels, all by default
       >>> car.wheels
       4

       >>> # but a car can't have 5 wheels!
       >>> #  the `validation=` field is a simple callable that returns a
       >>> #  boolean based on validity
       >>> car.wheels = 5
       Traceback (most recent call last):
       ValidationError: Invalid value 5 for wheels

       >>> # we can call .dump() on car, and just get back a standard
       >>> #  python dict actually, it's an ordereddict to match attribute
       >>> #  declaration order
       >>> type(car.dump())
       <class '...OrderedDict'>
       >>> car.dump()
       OrderedDict([('weight', 4242.46), ('wheels', 4), ('color', 0)])

       >>> # and json too (note the order!)
       >>> car.json()
       '{"weight": 4242.46, "wheels": 4, "color": 0}'

       >>> # green cars aren't allowed
       >>> car.color = "green"
       Traceback (most recent call last):
       ValidationError: 'green' is not a valid Color

       >>> # but black cars are!
       >>> car.color = "black"
       >>> car.color
       <Color.black: 1>

       >>> # car.color really is an enum, promise
       >>> type(car.color)
       <enum 'Color'>

       >>> # enum assignment can be with any of (and preferentially)
       >>> #   (1) an enum literal,
       >>> #   (2) a valid enum value, or
       >>> #   (3) a valid enum name
       >>> car.color = Color.blue; car.color.value
       0
       >>> car.color = 1; car.color.name
       'black'

       >>> # let's do a round-trip marshalling of this thing
       >>> same_car = Car.from_json(car.json())  # or equally Car.from_json(json.dumps(car.dump()))
       >>> same_car == car
       True

       >>> # actually, they're two different instances
       >>> same_car is not car
       True

       >>> # this works too
       >>> cloned_car = Car(**car.dump())
       >>> cloned_car == car
       True

       >>> # while we're at it, these are all equivalent too
       >>> car == Car.from_objects(car)
       True
       >>> car == Car.from_objects({"weight": 4242.46, "wheels": 4, "color": 1})
       True
       >>> car == Car.from_json('{"weight": 4242.46, "color": 1}')
       True

       >>> # .from_objects() even lets you stack and combine objects
       >>> class DumbClass:
       ...     color = 0
       ...     wheels = 3
       >>> Car.from_objects(DumbClass(), dict(weight=2222, color=1))
       Car(weight=2222, wheels=3, color=0)
       >>> # and also pass kwargs that override properties pulled
       >>> #  off any objects
       >>> Car.from_objects(DumbClass(), {'weight': 2222, 'color': 1}, color=2, weight=33)
       Car(weight=33, wheels=3, color=2)


   Chapter 2: Entity and Field Composition
   ---------------------------------------

       >>> # now let's get fancy
       >>> # a ComposableField "nests" another valid Entity
       >>> # a ListField's first argument is a "generic" type,
       >>> #   which can be a valid Entity, any python primitive
       >>> #   type, or a list of Entities/types
       >>> class Fleet(Entity):
       ...     boss_car = ComposableField(Car)
       ...     cars = ListField(Car)

       >>> # here's our fleet of company cars
       >>> company_fleet = Fleet(boss_car=Car(color='red'), cars=[car, same_car, cloned_car])
       >>> company_fleet.pretty_json()  #doctest: +SKIP
       {
         "boss_car": {
           "wheels": 4
           "color": 2,
         },
         "cars": [
           {
             "weight": 4242.46,
             "wheels": 4
             "color": 1,
           },
           {
             "weight": 4242.46,
             "wheels": 4
             "color": 1,
           },
           {
             "weight": 4242.46,
             "wheels": 4
             "color": 1,
           }
         ]
       }

       >>> # the boss' car is red of course (and it's still an Enum)
       >>> company_fleet.boss_car.color.name
       'red'

       >>> # and there are three cars left for the employees
       >>> len(company_fleet.cars)
       3


   Chapter 3: Immutability
   -----------------------

       >>> class ImmutableCar(ImmutableEntity):
       ...     wheels = IntField(default=4, validation=lambda x: 3 <= x <= 4)
       ...     color = EnumField(Color)
       >>> icar = ImmutableCar.from_objects({'wheels': 3, 'color': 'blue'})
       >>> icar
       ImmutableCar(wheels=3, color=0)

       >>> icar.wheels = 4
       Traceback (most recent call last):
       AttributeError: Assignment not allowed. ImmutableCar is immutable.

       >>> class FixedWheelCar(Entity):
       ...     wheels = IntField(default=4, immutable=True)
       ...     color = EnumField(Color)
       >>> fwcar = FixedWheelCar.from_objects(icar)
       >>> fwcar.json()
       '{"wheels": 3, "color": 0}'

       >>> # repainting the car is easy
       >>> fwcar.color = Color.red
       >>> fwcar.color.name
       'red'

       >>> # can't really change the number of wheels though
       >>> fwcar.wheels = 18
       Traceback (most recent call last):
       AttributeError: The wheels field is immutable.


   Chapter X: The del and null Weeds
   ---------------------------------

       >>> old_date = lambda: isoparse('1982-02-17')
       >>> class CarBattery(Entity):
       ...     # NOTE: default value can be a callable!
       ...     first_charge = DateField(required=False)  # default=None, nullable=False
       ...     latest_charge = DateField(default=old_date, nullable=True)  # required=True
       ...     expiration = DateField(default=old_date, required=False, nullable=False)

       >>> # starting point
       >>> battery = CarBattery()
       >>> battery
       CarBattery()
       >>> battery.json()
       '{"latest_charge": "1982-02-17T00:00:00", "expiration": "1982-02-17T00:00:00"}'

       >>> # first_charge is not assigned a default value. Once one is assigned, it can be deleted,
       >>> #   but it can't be made null.
       >>> battery.first_charge = isoparse('2016-03-23')
       >>> battery
       CarBattery(first_charge=datetime.datetime(2016, 3, 23, 0, 0))
       >>> battery.first_charge = None
       Traceback (most recent call last):
       ValidationError: Value for first_charge not given or invalid.
       >>> del battery.first_charge
       >>> battery
       CarBattery()

       >>> # latest_charge can be null, but it can't be deleted. The default value is a callable.
       >>> del battery.latest_charge
       Traceback (most recent call last):
       AttributeError: The latest_charge field is required and cannot be deleted.
       >>> battery.latest_charge = None
       >>> battery.json()
       '{"latest_charge": null, "expiration": "1982-02-17T00:00:00"}'

       >>> # expiration is assigned by default, can't be made null, but can be deleted.
       >>> battery.expiration
       datetime.datetime(1982, 2, 17, 0, 0)
       >>> battery.expiration = None
       Traceback (most recent call last):
       ValidationError: Value for expiration not given or invalid.
       >>> del battery.expiration
       >>> battery.json()
       '{"latest_charge": null}'




Classes
-------

.. autoapisummary::

   conda.auxlib.entity.Field
   conda.auxlib.entity.BooleanField
   conda.auxlib.entity.IntegerField
   conda.auxlib.entity.NumberField
   conda.auxlib.entity.StringField
   conda.auxlib.entity.DateField
   conda.auxlib.entity.EnumField
   conda.auxlib.entity.ListField
   conda.auxlib.entity.MapField
   conda.auxlib.entity.ComposableField
   conda.auxlib.entity.Entity
   conda.auxlib.entity.ImmutableEntity




Attributes
----------

.. autoapisummary::

   conda.auxlib.entity.BoolField
   conda.auxlib.entity.IntField


.. py:class:: Field(default=NULL, required=True, validation=None, in_dump=True, default_in_dump=True, nullable=False, immutable=False, aliases=())


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

   .. py:property:: name


   .. py:property:: required


   .. py:property:: type


   .. py:property:: default


   .. py:property:: in_dump


   .. py:property:: default_in_dump


   .. py:property:: nullable


   .. py:property:: is_nullable


   .. py:property:: immutable


   .. py:attribute:: _order_helper
      :value: 0

      

   .. py:method:: set_name(name)


   .. py:method:: __get__(instance, instance_type)


   .. py:method:: __set__(instance, val)


   .. py:method:: __delete__(instance)


   .. py:method:: box(instance, instance_type, val)


   .. py:method:: unbox(instance, instance_type, val)


   .. py:method:: dump(instance, instance_type, val)


   .. py:method:: validate(instance, val)

      :returns: if val is valid
      :rtype: True

      :raises ValidationError:



.. py:class:: BooleanField(default=NULL, required=True, validation=None, in_dump=True, default_in_dump=True, nullable=False, immutable=False, aliases=())


   Bases: :py:obj:`Field`

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

   .. py:attribute:: _type

      

   .. py:method:: box(instance, instance_type, val)



.. py:data:: BoolField

   

.. py:class:: IntegerField(default=NULL, required=True, validation=None, in_dump=True, default_in_dump=True, nullable=False, immutable=False, aliases=())


   Bases: :py:obj:`Field`

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

   .. py:attribute:: _type

      


.. py:data:: IntField

   

.. py:class:: NumberField(default=NULL, required=True, validation=None, in_dump=True, default_in_dump=True, nullable=False, immutable=False, aliases=())


   Bases: :py:obj:`Field`

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

   .. py:attribute:: _type
      :value: ()

      


.. py:class:: StringField(default=NULL, required=True, validation=None, in_dump=True, default_in_dump=True, nullable=False, immutable=False, aliases=())


   Bases: :py:obj:`Field`

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

   .. py:attribute:: _type

      

   .. py:method:: box(instance, instance_type, val)



.. py:class:: DateField(default=NULL, required=True, validation=None, in_dump=True, default_in_dump=True, nullable=False, immutable=False, aliases=())


   Bases: :py:obj:`Field`

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

   .. py:attribute:: _type

      

   .. py:method:: box(instance, instance_type, val)


   .. py:method:: dump(instance, instance_type, val)



.. py:class:: EnumField(enum_class, default=NULL, required=True, validation=None, in_dump=True, default_in_dump=True, nullable=False, immutable=False, aliases=())


   Bases: :py:obj:`Field`

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



.. py:class:: ListField(element_type, default=NULL, required=True, validation=None, in_dump=True, default_in_dump=True, nullable=False, immutable=False, aliases=())


   Bases: :py:obj:`Field`

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

   .. py:attribute:: _type

      

   .. py:method:: box(instance, instance_type, val)


   .. py:method:: unbox(instance, instance_type, val)


   .. py:method:: dump(instance, instance_type, val)


   .. py:method:: validate(instance, val)

      :returns: if val is valid
      :rtype: True

      :raises ValidationError:



.. py:class:: MapField(default=NULL, required=True, validation=None, in_dump=True, default_in_dump=True, nullable=False, immutable=True, aliases=())


   Bases: :py:obj:`Field`

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

   .. py:attribute:: _type

      

   .. py:method:: box(instance, instance_type, val)



.. py:class:: ComposableField(field_class, default=NULL, required=True, validation=None, in_dump=True, default_in_dump=True, nullable=False, immutable=False, aliases=())


   Bases: :py:obj:`Field`

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



.. py:class:: Entity(**kwargs)


   .. py:property:: _initd


   .. py:attribute:: __fields__

      

   .. py:attribute:: _lazy_validate
      :value: False

      

   .. py:method:: from_objects(*objects, **override_fields)
      :classmethod:

      Construct a new object of type ``cls`` from existing objects or dicts.

      Allows the creation of new objects of concrete :class:`Entity` subclasses by
      combining information from several sources. This can be any combination of
      objects and dictionaries passed in as positional arguments. When looking for
      the value of the fields of the :class:`Entity` subclass, the first object
      that provides an attribute (or, in the case of a dict an entry) that has the
      name of the field or one of its aliases will take precedence. Any keyword
      arguments passed in will override this and take precedence.

      :param cls: The class to create, usually determined by call, e.g. ``PrefixRecord.from_objects(...)``.
      :type cls: :class:`Entity` subclass
      :param \*objects: Any combination of objects and dicts in order of decending precedence.
      :type \*objects: tuple(object or dict)
      :param \*\*override_fields: Any individual fields overriding possible contents from ``*objects``.
      :type \*\*override_fields: dict(str, object)


   .. py:method:: from_json(json_str)
      :classmethod:


   .. py:method:: load(data_dict)
      :classmethod:


   .. py:method:: validate()


   .. py:method:: __repr__()

      Return repr(self).


   .. py:method:: __register__()
      :classmethod:


   .. py:method:: json(indent=None, separators=None, **kwargs)


   .. py:method:: pretty_json(indent=2, separators=(',', ': '), **kwargs)


   .. py:method:: dump()


   .. py:method:: __dump_fields()
      :classmethod:


   .. py:method:: __eq__(other)

      Return self==value.


   .. py:method:: __hash__()

      Return hash(self).



.. py:class:: ImmutableEntity(**kwargs)


   Bases: :py:obj:`Entity`

   .. py:method:: __setattr__(attribute, value)

      Implement setattr(self, name, value).


   .. py:method:: __delattr__(item)

      Implement delattr(self, name).



