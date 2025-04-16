:py:mod:`compat`
================

.. py:module:: conda.common.compat

.. autoapi-nested-parse::

   Common compatibility code.




Functions
---------

.. autoapisummary::

   conda.common.compat.encode_for_env_var
   conda.common.compat.encode_environment
   conda.common.compat.isiterable
   conda.common.compat.open_utf8
   conda.common.compat.open
   conda.common.compat.six_with_metaclass
   conda.common.compat.ensure_binary
   conda.common.compat.ensure_text_type
   conda.common.compat.ensure_unicode
   conda.common.compat.ensure_fs_path_encoding
   conda.common.compat.ensure_utf8_encoding



Attributes
----------

.. autoapisummary::

   conda.common.compat.on_win
   conda.common.compat.on_mac
   conda.common.compat.on_linux
   conda.common.compat.ENCODE_ENVIRONMENT
   conda.common.compat.NoneType
   conda.common.compat.primitive_types


.. py:data:: on_win

   

.. py:data:: on_mac

   

.. py:data:: on_linux

   

.. py:data:: ENCODE_ENVIRONMENT
   :value: True

   

.. py:function:: encode_for_env_var(value) -> str

   Environment names and values need to be string.


.. py:function:: encode_environment(env)


.. py:function:: isiterable(obj)


.. py:function:: open_utf8(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True)


.. py:function:: open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True)


.. py:function:: six_with_metaclass(meta, *bases)

   Create a base class with a metaclass.


.. py:data:: NoneType

   

.. py:data:: primitive_types
   :value: ()

   

.. py:function:: ensure_binary(value)


.. py:function:: ensure_text_type(value) -> str


.. py:function:: ensure_unicode(value)


.. py:function:: ensure_fs_path_encoding(value)


.. py:function:: ensure_utf8_encoding(value)


