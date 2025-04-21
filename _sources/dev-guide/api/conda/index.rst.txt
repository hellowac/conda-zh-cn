:py:mod:`conda`
===============

.. py:module:: conda

.. autoapi-nested-parse::

   OS-agnostic, system-level binary package manager.



.. toctree::
   :hidden:
   :titlesonly:
   :maxdepth: 3

   __main__/index.rst
   _vendor/index.rst
   activate/index.rst
   api/index.rst
   auxlib/index.rst
   base/index.rst
   cli/index.rst
   common/index.rst
   core/index.rst
   deprecations/index.rst
   env/index.rst
   exception_handler/index.rst
   exceptions/index.rst
   exports/index.rst
   gateways/index.rst
   history/index.rst
   instructions/index.rst
   misc/index.rst
   models/index.rst
   notices/index.rst
   plan/index.rst
   plugins/index.rst
   reporters/index.rst
   resolve/index.rst
   testing/index.rst
   trust/index.rst
   utils/index.rst



Functions
---------

.. autoapisummary::

   conda.conda_signal_handler



Attributes
----------

.. autoapisummary::

   conda.__version__
   conda.__name__
   conda.__author__
   conda.__email__
   conda.__license__
   conda.__copyright__
   conda.__summary__
   conda.__url__
   conda.CONDA_PACKAGE_ROOT


.. py:data:: __version__

   

.. py:data:: __name__
   :value: 'conda'

   

.. py:data:: __author__
   :value: 'Anaconda, Inc.'

   

.. py:data:: __email__
   :value: 'conda@continuum.io'

   

.. py:data:: __license__
   :value: 'BSD-3-Clause'

   

.. py:data:: __copyright__
   :value: 'Copyright (c) 2012, Anaconda, Inc.'

   

.. py:data:: __summary__

   

.. py:data:: __url__
   :value: 'https://github.com/conda/conda'

   

.. py:data:: CONDA_PACKAGE_ROOT

   

.. py:exception:: CondaError(message, caused_by=None, **kwargs)


   Bases: :py:obj:`Exception`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.

   .. py:attribute:: return_code
      :value: 1

      

   .. py:attribute:: reportable
      :value: False

      

   .. py:method:: __repr__()

      Return repr(self).


   .. py:method:: __str__()

      Return str(self).


   .. py:method:: dump_map()



.. py:exception:: CondaMultiError(errors)


   Bases: :py:obj:`CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.

   .. py:method:: __repr__()

      Return repr(self).


   .. py:method:: __str__()

      Return str(self).


   .. py:method:: dump_map()


   .. py:method:: contains(exception_class)



.. py:exception:: CondaExitZero(message, caused_by=None, **kwargs)


   Bases: :py:obj:`CondaError`

   Common base class for all non-exit exceptions.

   Initialize self.  See help(type(self)) for accurate signature.

   .. py:attribute:: return_code
      :value: 0

      


.. py:function:: conda_signal_handler(signum, frame)


