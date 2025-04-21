:py:mod:`cuda`
==============

.. py:module:: conda.plugins.virtual_packages.cuda

.. autoapi-nested-parse::

   Detect CUDA version.




Functions
---------

.. autoapisummary::

   conda.plugins.virtual_packages.cuda.cuda_version
   conda.plugins.virtual_packages.cuda.cached_cuda_version
   conda.plugins.virtual_packages.cuda.conda_virtual_packages
   conda.plugins.virtual_packages.cuda._cuda_driver_version_detector_target



.. py:function:: cuda_version()

   Attempt to detect the version of CUDA present in the operating system.

   On Windows and Linux, the CUDA library is installed by the NVIDIA
   driver package, and is typically found in the standard library path,
   rather than with the CUDA SDK (which is optional for running CUDA apps).

   On macOS, the CUDA library is only installed with the CUDA SDK, and
   might not be in the library path.

   Returns: version string (e.g., '9.2') or None if CUDA is not found.


.. py:function:: cached_cuda_version()

   A cached version of the cuda detection system.


.. py:function:: conda_virtual_packages()


.. py:function:: _cuda_driver_version_detector_target(queue)

   Attempt to detect the version of CUDA present in the operating system in a
   subprocess.

   On Windows and Linux, the CUDA library is installed by the NVIDIA
   driver package, and is typically found in the standard library path,
   rather than with the CUDA SDK (which is optional for running CUDA apps).

   On macOS, the CUDA library is only installed with the CUDA SDK, and
   might not be in the library path.

   Returns: version string (e.g., '9.2') or None if CUDA is not found.
            The result is put in the queue rather than a return value.


