:py:mod:`serialize`
===================

.. py:module:: conda.common.serialize

.. autoapi-nested-parse::

   YAML and JSON serialization and deserialization functions.




Functions
---------

.. autoapisummary::

   conda.common.serialize._yaml_round_trip
   conda.common.serialize._yaml_safe
   conda.common.serialize.yaml_round_trip_load
   conda.common.serialize.yaml_safe_load
   conda.common.serialize.yaml_round_trip_dump
   conda.common.serialize.yaml_safe_dump
   conda.common.serialize.json_load
   conda.common.serialize.json_dump



.. py:function:: _yaml_round_trip()


.. py:function:: _yaml_safe()


.. py:function:: yaml_round_trip_load(string)


.. py:function:: yaml_safe_load(string)

   .. rubric:: Examples

   >>> yaml_safe_load("key: value")
   {'key': 'value'}


.. py:function:: yaml_round_trip_dump(object, stream=None)

   Dump object to string or stream.


.. py:function:: yaml_safe_dump(object, stream=None)

   Dump object to string or stream.


.. py:function:: json_load(string)


.. py:function:: json_dump(object)


