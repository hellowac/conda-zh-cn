:py:mod:`env`
=============

.. py:module:: conda.env.env

.. autoapi-nested-parse::

   Environment object describing the conda environment.yaml file.



Classes
-------

.. autoapisummary::

   conda.env.env.Dependencies
   conda.env.env.Environment



Functions
---------

.. autoapisummary::

   conda.env.env.validate_keys
   conda.env.env.from_environment
   conda.env.env.from_yaml
   conda.env.env._expand_channels
   conda.env.env.from_file
   conda.env.env.get_filename
   conda.env.env.print_result



Attributes
----------

.. autoapisummary::

   conda.env.env.VALID_KEYS


.. py:data:: VALID_KEYS
   :value: ('name', 'dependencies', 'prefix', 'channels', 'variables')

   

.. py:function:: validate_keys(data, kwargs)

   Check for unknown keys, remove them and print a warning


.. py:function:: from_environment(name, prefix, no_builds=False, ignore_channels=False, from_history=False)

       Get ``Environment`` object from prefix
   :param name: The name of environment
   :param prefix: The path of prefix
   :param no_builds: Whether has build requirement
   :param ignore_channels: whether ignore_channels
   :param from_history: Whether environment file should be based on explicit specs in history

   Returns:     Environment object


.. py:function:: from_yaml(yamlstr, **kwargs)

   Load and return a ``Environment`` from a given ``yaml`` string


.. py:function:: _expand_channels(data)

   Expands ``Environment`` variables for the channels found in the ``yaml`` data


.. py:function:: from_file(filename)

   Load and return an ``Environment`` from a given file


.. py:class:: Dependencies(raw, *args, **kwargs)


   Bases: :py:obj:`dict`

   A ``dict`` subclass that parses the raw dependencies into a conda and pip list

   Initialize self.  See help(type(self)) for accurate signature.

   .. py:method:: parse()

      Parse the raw dependencies into a conda and pip list


   .. py:method:: add(package_name)

      Add a package to the ``Environment``



.. py:class:: Environment(name=None, filename=None, channels=None, dependencies=None, prefix=None, variables=None)


   A class representing an ``environment.yaml`` file

   .. py:method:: add_channels(channels)

      Add channels to the ``Environment``


   .. py:method:: remove_channels()

      Remove all channels from the ``Environment``


   .. py:method:: to_dict(stream=None)

      Convert information related to the ``Environment`` into a dictionary


   .. py:method:: to_yaml(stream=None)

      Convert information related to the ``Environment`` into a ``yaml`` string


   .. py:method:: save()

      Save the ``Environment`` data to a ``yaml`` file



.. py:function:: get_filename(filename)

   Expand filename if local path or return the ``url``


.. py:function:: print_result(args, prefix, result)

   Print the result of an install operation


