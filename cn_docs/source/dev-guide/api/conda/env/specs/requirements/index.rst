:py:mod:`requirements`
======================

.. py:module:: conda.env.specs.requirements

.. autoapi-nested-parse::

   Define requirements.txt spec.



Classes
-------

.. autoapisummary::

   conda.env.specs.requirements.RequirementsSpec




.. py:class:: RequirementsSpec(filename=None, name=None, **kwargs)


   Reads dependencies from a requirements.txt file
   and returns an Environment object from it.

   .. py:property:: environment


   .. py:attribute:: msg

      

   .. py:attribute:: extensions

      

   .. py:method:: _valid_file()


   .. py:method:: _valid_name()


   .. py:method:: can_handle()



