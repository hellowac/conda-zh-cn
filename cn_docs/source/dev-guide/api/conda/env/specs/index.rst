:py:mod:`specs`
===============

.. py:module:: conda.env.specs


.. toctree::
   :hidden:
   :titlesonly:
   :maxdepth: 3

   binstar/index.rst
   requirements/index.rst
   yaml_file/index.rst


Classes
-------

.. autoapisummary::

   conda.env.specs.RequirementsSpec
   conda.env.specs.YamlFileSpec



Functions
---------

.. autoapisummary::

   conda.env.specs.get_spec_class_from_file
   conda.env.specs.detect



Attributes
----------

.. autoapisummary::

   conda.env.specs.CONDA_SESSION_SCHEMES
   conda.env.specs.FileSpecTypes


.. py:exception:: EnvironmentFileExtensionNotValid(filename, *args, **kwargs)


   Bases: :py:obj:`CondaEnvException`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: EnvironmentFileNotFound(filename, *args, **kwargs)


   Bases: :py:obj:`CondaEnvException`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:exception:: SpecNotFound(msg, *args, **kwargs)


   Bases: :py:obj:`conda.CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.


.. py:data:: CONDA_SESSION_SCHEMES

   

.. py:class:: RequirementsSpec(filename=None, name=None, **kwargs)


   Reads dependencies from a requirements.txt file
   and returns an Environment object from it.

   .. py:property:: environment


   .. py:attribute:: msg

      

   .. py:attribute:: extensions

      

   .. py:method:: _valid_file()


   .. py:method:: _valid_name()


   .. py:method:: can_handle()



.. py:class:: YamlFileSpec(filename=None, **kwargs)


   .. py:property:: environment


   .. py:attribute:: _environment

      

   .. py:attribute:: extensions

      

   .. py:method:: can_handle()



.. py:data:: FileSpecTypes

   

.. py:function:: get_spec_class_from_file(filename: str) -> FileSpecTypes

   Determine spec class to use from the provided ``filename``

   :raises EnvironmentFileExtensionNotValid | EnvironmentFileNotFound:


.. py:function:: detect(name: str | None = None, filename: str | None = None, directory: str | None = None) -> SpecTypes

   Return the appropriate spec type to use.

   :raises SpecNotFound: Raised if no suitable spec class could be found given the input
   :raises EnvironmentFileExtensionNotValid | EnvironmentFileNotFound:


